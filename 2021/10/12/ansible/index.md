# Ansible 使用


/etc/ansible/hosts

命令行工具：https://docs.ansible.com/ansible/latest/cli/ansible.html

```bash
ansible -i hosts -u root -m command -a "/bin/echo hello"
```

m 表示模块。a 表示 args，是模块的参数。

command 模块是默认的，可省略。

```bash
ansible -i hosts myall -u root -a "/bin/echo hello"
```

```bash
ansible-playbook -i hosts deploy.yml
```

```yml
    - name: 0. BUILD
      ansible.builtin.shell:
        cmd: "/bin/bash control.sh build"
        chdir: "{{ local_dir }}"
      delegate_to: 127.0.0.1
      run_once: True
```

在本地执行，在原来的基础上加 `delegate_to` 就行。如果只需执行一次，则加上 `run_once`。

#### 脚本

```bash
#!/bin/bash
# filename: run.sh

cmd=$1
ansible -i hosts target_group -u root -a "$cmd"
```

bash run.sh 'echo "test"'


#### 构建和获取

```yaml
---
- name: "build and fetch"
  hosts: "build-host"
  remote_user: root
  become: True
  gather_facts: False
  tasks:
    - name: 1. PULL AND BUILD
      ansible.builtin.shell:
        cmd: git pull; source ~/.profile; bash control build
        chdir: "/usr/local/app-local-dir"
    - name: 2. SLEEP
     wait_for:
       delay: 10
       timeout: 0
    - name: 3. FETCH
      fetch: src={{ item.src }} dest={{ item.dest }} mode=0775 flat=true
      with_items:
        - {src: "/usr/local/app-remote-dir", dest: "deploy/local-dir"}
```

#### 部署

```yaml
- name: "deploy"
  hosts: "deploy-hosts"
  remote_user: root
  become: False
  gather_facts: False
  vars:
    remote_dir: /usr/local/app-remote-dir
  tasks:
    - name: 1. UPLOAD
      copy: src={{ item.src }} dest={{ item.dest }} mode=0775
      with_items:
        - {src: "deploy/app", dest: "{{ remote_dir }}"}
    - name: 2. RESTART
      shell: "cd {{ remote_dir }}; ./control restart"
    - name: 3. SLEEP
      wait_for:
        delay: 3
        timeout: 0
    - name: 4. STATUS
      ansible.builtin.shell:
        cmd: ps aux | grep app | grep -v grep
      register: out
    - debug: var=out
```

### 部署

```yaml
---

- name: "deploy"
  hosts: "app"
  remote_user: root 
  become: False
  gather_facts: False
  vars:
    src_dir: /usr/local/app-remote-dir
    remote_dir: /usr/local/app-remote-dir
    remote_log_dir: /usr/local/app-remote-dir/log
    backup_dir: files/backup
  tasks:
    - name: 0. BACKUP BIN
      fetch:
        src: "{{ remote_dir }}/app"
        dest: "{{ backup_dir }}/app"
        mode: 0775
        flat: True
      run_once: True

    - name: 1. BACKUP CONFIG
      fetch:
        src: "{{ remote_dir }}/config.json"
        dest: "{{ backup_dir }}/config.json.{{ inventory_hostname }}"
        mode: 0775
        flat: True

    - name: 2. PULL AND BUILD
      ansible.builtin.shell:
        cmd: "git pull; /bin/bash scripts/control build" 
        chdir: "{{ src_dir }}"
      delegate_to: 127.0.0.1
      run_once: True
      register: build_result
    - debug:
        var: build_result
      run_once: True

    - name: 3. ENSURE_REMOTE_DIR
      file:
        path: "{{ item }}"
        state: directory
        mode: 0740
      loop:
        - "{{ remote_dir }}"
        - "{{ remote_log_dir }}"

    - name: 4. UPLOAD
      copy: src={{ item.src }} dest={{ item.dest }} mode=0775
      with_items: 
        - {src: "{{ src_dir }}/app", dest: "{{ remote_dir }}"}
        - {src: "{{ src_dir }}/scripts/control", dest: "{{ remote_dir }}"}
        - {src: "config.json", dest: "{{ remote_dir }}"}

    - name: 5. CONFIG
      replace:
        path: "{{ remote_dir }}/config.json"
        regexp: "ADDR:8087"
        replace: "{{ inventory_hostname }}:8087"

    - name: 6. RESTART
      ansible.builtin.shell: 
        cmd: ./control upgrade
        chdir: "{{ remote_dir }}" 
      register: upgrade_status
    - debug: var=upgrade_status

    - name: 7. SLEEP
      wait_for:
        delay: 3
        timeout: 0

    - name: 8. STATUS
      ansible.builtin.shell:
        cmd: ./control status
        chdir: "{{ remote_dir }}" 
      register: out
    - debug: var=out
```



