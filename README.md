## nginx-applications

Nginxの設定や動作を検証するためのリポジトリ。バックエンドで動作するサンプルコードが付いています。
 
### Installation
#### clone
```bash
$ git clone https://github.com/tksh0113/nginx-applications.git
$ cd nginx-applications
```

#### build
```bash
$ docker-compose up --build
```

### Usage
|  Application  |  EndPoint  |
| ---- | ---- |
| Nginx | http://localhost:8080 |
| PHP (PHP-FPM)| http://localhost:8081 |
| Python (uWSGI)| http://localhost:8082 |
| Python without Nginx | http://localhost:9090 |

### Note
- UNIX ドメインソケットを用いて動作するようにしています。
  - ソケットのパーミッションは666ではなく660にしています。 
  - GroupのPermissionを利用して動くようにしています。
- Dockerはrootユーザーで実行しないよう(non-root)にしています。
 

