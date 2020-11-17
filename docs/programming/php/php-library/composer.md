# Composer 项目依赖项管理

使用 Packagist 作为主源的依赖项管理工具。

## 镜像设置

<https://developer.aliyun.com/composer>

- `composer self-update`
- `composer diagnose`
- `composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/`, `composer config -g --unset repos.packagist`

## 使用

- `composer show --platform`
- `composer update [vendor/packagename]`
- `composer install`
