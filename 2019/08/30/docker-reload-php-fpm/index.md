# Docker 在不重启容器的情况下重新加载 PHP-FPM 配置



执行：`pkill -o -USR2 php-fpm`

> https://stackoverflow.com/questions/37806188/how-to-restart-php-fpm-inside-a-docker-container  
> For me PID 1 is not always correct (especially after killing it once). What helps is `pkill -o -USR2 php-fpm`, because the option -o searches for the oldest process (the master) and kills it.
