# 七牛云存储PHP SDK（非官方，更好用）

## 初始化

```text
$client = new QiniuClient($accessKey,$secretKey);
```

## 上传

### 上传文件

```text
$client->uploadFile('/local/files/file.txt','test_bucket_name','test/file.txt');
```

### 上传内容作为文件存储

```text
$client->upload('我是文件内容','test_bucket_name','test/file2.txt');
```

### 存储远程文件

```text
$client->uploadRemote('http://www.baidu.com/img/bdlogo.gif','test_bucket_name','test/file3.gif');
```

### 上传凭证 - uploadToken （自制表单上传时需要）

```text
$flag = array('scope'=>'test_bucket_name');
$client->uploadToken($flags);
```

$flags更多选项参加[文档](http://docs.qiniu.com/api/v6/put.html#uploadToken)

## 文件管理 - 单文件操作

### 查看

```text
$client->stat('test_bucket_name','test/file3.gif');
```

### 复制

复制到原bucket

```text
$client->copy('test_bucket_name','test/file3.gif','test/file4.gif');
```

复制到其它bucket

```text
$client->copy('test_bucket_name','test/file3.gif','another_bucket_name','test/file4.gif');
```

### 移动

在原bucket中移动

```text
$client->move('test_bucket_name','test/file4.gif','test/file5.gif');
```

移动到其它bucket

```text
$client->move('test_bucket_name','test/file3.gif','another_bucket_name','test/file5.gif');
```

### 删除

```text
$client->delete('test_bucket_name','test/file.txt');
```

## 文件管理 - 批量操作

```text
$client->batch($operator,$files);
```

### 批量查看文件

```text
$client->batch('stat',array('bucket_name:test/test5.txt','bucket_name:test/test6.png'));
```

### 批量复制文件

test/test5.txt复制到bucket\_name:test/test6.txt

test/test6.txt复制到bucket\_name:test/test7.txt

```text
$client->batch('copy',array(
    array('bucket_name:test/test5.txt','bucket_name:test/test6.txt'),
    array('bucket_name:test/test7.txt','bucket_name:test/test8.txt')
));
```

### 批量移动文件

同复制

```text
$client->batch('move',array(
    array('bucket_name:test/test5.txt','bucket_name:test/test6.txt'),
    array('bucket_name:test/test7.txt','bucket_name:test/test8.txt')
));
```

### 批量删除文件

```text
$client->batch('delete',array('bucket_name:test/test5.txt','bucket_name:test/test6.png'));
```

## 列出文件

详见[官方文档](http://docs.qiniu.com/api/v6/file-handle.html#list)

```text
$client->listFiles($bucket,$limit=10,$prefix='test',$marker='');
```

