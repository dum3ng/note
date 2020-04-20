## connect from remote

By default the `mysqld` is running on the host `127.0.0.1`

edit /etc/mysql/mysql.conf.d/mysqld.cnf:

```toml
[mysqld]
bind-address = 0.0.0.0
```

Then restart the mysql server: `sudo systemctl restart mysql`

### references

- [option-files](https://dev.mysql.com/doc/refman/5.5/en/option-files.html)
- [bind-address](https://dev.mysql.com/doc/refman/5.5/en/server-options.html#option_mysqld_bind-address)
