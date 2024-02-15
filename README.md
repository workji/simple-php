# simple-php-xdebug

## 環境構築方法
ビルド 

```
docker-compose build
```

起動

```
docker-compose up -d
```

## 動作確認
1. WEBページを確認
```
http://localhost:8180/
```
phpinfo()が表示されていること<br><br>

2. phpmyadminの確認
```
http://localhost:8280/
```
ログイン済みの状態で画面表示されていること<br><br>

3. メール送信テストと確認
<br>appコンテナにアクセスした後、mail送信のスクリプトを実行する
```
$ docker-compose exec app bash

root@f761b2f53458:/var/www# php -r "mail('aaa@local', 'テストタイトル', 'テスト本文', 'From: bbb@local');";
```
メール確認
```
http://localhost:8025/
```
inboxに、テストメールが表示されていること<br>

### Xdebug設定と確認（VSCodeの例）
1. VSCodeの拡張Install
```
Dev Containers
PHP Debug
```

2. VSCodeのlaunch.json設定
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9004
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9004
        }
    ]
}
```

3. 動作確認
```php
<?php
$now = date('Y-m-d H:i:s');
phpinfo();
```

```html
http://localhost をアクセス
```

### Xdebug設定と確認（PHPStormの例）
CLI Interpreterを追加するのみ