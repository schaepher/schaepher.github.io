upstream cppver {
        consistent_hash $remote_addr;
        server 127.0.0.1:8090;
}

upstream gover {
        consistent_hash $remote_addr;
        server 127.0.0.1:8091;
}

upstream gover2 {
        consistent_hash $remote_addr;
        server 127.0.0.1:8092;
}

server {
        listen       8088;
        server_name  test.com;

        location / {
                mirror /mirror;
                mirror /mirror2;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_pass http://cppver$request_uri;
        }

        location /mirror {
                internal;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_pass http://gover$request_uri;
        }

        location /mirror2 {
                internal;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_pass http://gover2$request_uri;
        }
}
