### 修改nginx.conf

```js
user tking; // 配置用户

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

### 配置js/css/img相关的文件

```js
#配置当前的图片

location ~ \.(gif|jpg|jpeg)$ {

root /Users/tking/2021work/eyjsc;

}

#配置当前所有以js和css结尾的数据都调用neginx的static文件夹中的内容

location ~ \.(js|css)$ {

root /Users/tking/2021work/eyjsc;

}
```