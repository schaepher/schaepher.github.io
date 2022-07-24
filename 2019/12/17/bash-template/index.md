# Bash 脚本模板


这是一个较为通用的脚本模板。

<!-- more -->

```bash
#!/bin/bash
##############################################################
# Filename    : template.sh
# Author      : xxx(xxx@outlook.com)
# Date        : xxxx-xx-xx
# Function    :
#   Bash Template
# Changes     :
# - 20191217 by xxx
#   Create Template
##############################################################

readonly _filename=$(basename $0)

function usage()
{
	cat <<EOF
Description:
  Echo var0 and var1
Usage:
  template.sh --var0=<value> [--var1=<value>]
Options:
  -h --help       Show this help.
  --var0=<value>  Assign <value> to var0
  --var1=<value>  Assign <value> to var1
EOF
    exit 0
}

if [[ "$#" -eq 0 ]]; then usage; fi

# Usage: log <log-level> <log-text>...
# log-level: DEBUG INFO ERROR
function log() { local prefix="[$(date +%Y-%m-%d\ %H:%M:%S)]: "; echo "${prefix} $@" >> /tmp/${_filename}.log; }

# Exit if value is empty
# Usage: required "--var1" "${var1}"
function required() { if [[ ! -n "${2}" ]]; then echo "${1} is required!"; exit 1; fi }

# Usage: output "${key}" "${value}"
# Double Quote is required to preserve new line character.
function output() { local k=$1; shift; local v=$(echo -n "$@" | base64 -w 0); [[ "$debug" -eq 1 ]] && v="$@"; echo ${k}=${v}; }

set -e
_args=$(getopt --option h --long "help",debug,var0:,var1: -- "$@")
eval set -- "${_args}"

# common the next line to avoid exit immediately if a simple command exits with a non-zero status
set +e

while true
do
    case "$1" in
        -h|--help)
            usage
            break
            ;;
        --var0)
            var0=$2
            shift 2
            ;;
        --var1)
            var1=$2
            shift 2
            ;;
        --)
            shift
            break
            ;;
    esac
done

restParams="$@"

required "--var0" "${var0}"

function main()
{
    output var0 "${var0}"
    output var1 "${var1}"
}

log 'INFO' 'script start'
main
log 'INFO' 'script end'
```


## 执行脚本

```php
$commands = [
    ['echo', '"-----script-start-----"'],
    ['mkdir', '-p', '/usr/local/src/scripts'],
    ['cd', '/usr/local/src/scripts'],
    [sprintf('echo "%s" | base64 -di > %s.env', base64_encode(implode("\n", $envArr)), $scriptName)],
    [sprintf('echo "%s" | base64 -di > %s', base64_encode($scriptContent), $scriptName)],
    ['chmod', '+x', $scriptName],
    array_merge(['bash', $scriptName], array_map(CommandEscapeTool::class, 'escape'], $params), ['2>&1']),
    ['echo', 'script_exit_code=$?'],
    ['echo', '-----script-end-----'],
];

$commandStr = sprintf('echo "%s" | base64 -di | bash', base64_encode($commandStr));
```

