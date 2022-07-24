# Mariadb 授权与回收



1. 创建用户

   ```sql
   CREATE USER "username"@"host" IDENTIFIED BY 'password';
   ```

<!-- more -->

1. 授权
   
   ```sql
   GRANT ALL PRIVILEGES ON dbname.* TO "username"@"host";
   ```

1. 回收

   ```sql
   REVOKE ALL PRIVILEGES ON dbname.* FROM "username"@"host";
   ```


