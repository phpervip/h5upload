# H5直传阿里云oss扩展

### 1.使用composer安装monsteryuan/h5upload扩展

````
composer require monsteryuan/h5upload 1.0.7.x-dev -vvvv
````

### 2.迁移数据库文件

````
使用命令行php artisan admin:install 迁移数据库文件
````

### 3.导出资源文件

`windows`:`php artisan vendor:publish --provider=Encore\h5upload\h5uploadServiceProvider`

`mac|linux`:`php artisan vendor:publish --provider=Encore\\h5upload\\h5uploadServiceProvider`

### 4.在`app/Admin/bootstrap.php`添加代码

```
Encore\Admin\Form::extend('h5upload', \Encore\h5upload\h5uploadFiled::class);
```

### 5.在form方法里面使用

``
$form->h5upload('url','视频');
``

### 设置允许上传扩展的文件

```
可选扩展:video视频类型文件 file所有类型的文件 mp3音频文件 image图片文件
$form->h5upload('url','视频')->setExpansion('video');
```

### 设置多文件上传
```
$form->h5upload('url','h5upload')->setMultiple();
```

### 关于.env配置文件
```
请打开网站https://help.aliyun.com/document_detail/100624.html?spm=a2c4g.11186623.2.10.316879b0jDJxFq#concept-xzh-nzk-2gb根据提升一步一步添加配置
```

### 设置阿里云oss的跨域


### 文件管理页面
```
访问页面 admin/manage 查看已经上传的文件
```

### 需要在其他地方获取详细的资源链接
```
请添加服务提供者
$this->app->bind(ThirdPartyUpload::class, function (Application $application) {
    $type_dev = config('h5upload.type_dev');
    $dev_map = [
        'ali' => Aliyun::class
    ];
    return new $dev_map[$type_dev]($type_dev);
});
然后在其他地方使用获取
app(ThirdPartyUpload::class)->getResourceUri([1,2,3]);
```

### tips
```
如果有什么问题可以联系email:643145444@qq.com,作者会在时间充足的情况下更新扩展
```

### 资源管理页面

![avatar](mange.png)


#有更好的点子
### 1.复制文件
``
app/Admin/Extensions/laravel-admin-ext/h5upload
``

### 2.修改项目composer.json文件的repositories 加入

````
 "h5upload": {
   "type": "path",
   "url": "app/Admin/Extensions/laravel-admin-ext/h5upload"
 }
````

### 3.安装本地

```
composer require monsteryuan/h5upload -vvvv
```
