# handy_note

## DB

Use navicat11 client to connect localhost mysql database and get 'Client does not support authentication protocol requested by server; consider upgrading MySQL client'

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'newpass';
