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
#### EndPoints
|  Application  |  EndPoint  |
| ---- | ---- |
| Nginx | http://localhost:8080 |
| PHP (PHP-FPM)| http://localhost:8081 |
| Python (uWSGI)| http://localhost:8082 |
| Python without Nginx | http://localhost:9090 |

#### stats
##### PHP-FPM
```bash
$ curl localhost:8081/status
pool:                 www
process manager:      dynamic
start time:           10/Mar/2022:21:24:58 +0000
start since:          1520
accepted conn:        3
listen queue:         0
max listen queue:     0
listen queue len:     0
idle processes:       1
active processes:     1
total processes:      2
max active processes: 1
max children reached: 0
slow requests:        0
```

##### uWSGI
```bash
$ curl localhost:9091
uwsgi@ca94de69ba9e:~$ curl localhost:9091
{
	"version":"2.0.19.1",
	"listen_queue":0,
	"listen_queue_errors":0,
	"signal_queue":0,
	"load":0,
	"pid":8,
	"uid":1002,
# TODO (コンテナ内)
....
curl: (56) Recv failure: Connection reset by peer

# TODO (コンテナ外)
$ curl localhost:9091
curl: (1) Received HTTP/0.9 when not allowed
```

### Note
- UNIX ドメインソケットを用いて動作するようにしています。
  - ソケットのパーミッションは666ではなく660にしています。 
  - GroupのPermissionを利用して動くようにしています。
- Dockerはrootユーザーで実行しないよう(non-root)にしています。
 

