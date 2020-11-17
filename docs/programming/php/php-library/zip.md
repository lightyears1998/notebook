# 压缩文件Zip

- `zip_open()`, `zip_close()`

`zip_read()`, `zip_entry_name()`

```php
$zip = zip_open('filename.zip');
if ($zip) {
    while ($zip_entry = zip_read($zip)) {
        echo '文件名'.zip_entry_name($zip_entry)."\n";
    }
    zip_close($zip);
}
```

ZipArchive类 强大的工具类
