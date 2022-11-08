### 修改nginx.conf

```js
user tking;

location ~ \.php$ {

   root /Users/tking/2021work/eyjsc;

   fastcgi_pass 127.0.0.1:9000;

   fastcgi_index index.php;

   fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

   include fastcgi_params;

}
```

### 权限

简介给权限读写