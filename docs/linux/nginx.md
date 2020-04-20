# nginx

## remove http header

```nginx
location ~ {
  add_header
  proxy_set_header
  proxy_hide_header
}
```

By using `proxy_hide_header KEEP_ALIVE`, nginx will remove the `KEEP_ALIVE`
header of http response
