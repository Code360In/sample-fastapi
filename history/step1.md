# 1. Create directory

```sh
admin@gw-mac sample-fastapi % tree
.
├── README.md
├── backend
│   ├── Dockerfile
│   ├── app
│   │   ├── api
│   │   └── core
│   ├── requirements.txt
│   └── tests
├── docker-compose.yml
└── history.md

5 directories, 5 files
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % touch backend/app/api/__init__.py backend/app/api/server.py
admin@gw-mac sample-fastapi % mkdir backend/app/api/routes
admin@gw-mac sample-fastapi % touch backend/app/api/routes/__init__.py backend/app/api/routes/hedgehogs.py
admin@gw-mac sample-fastapi % tree
.
├── How_to_Install_Python3_on_Mac.md
├── README.md
├── backend
│   ├── Dockerfile
│   ├── app
│   │   ├── api
│   │   │   ├── __init__.py
│   │   │   ├── routes
│   │   │   │   ├── __init__.py
│   │   │   │   └── hedgehogs.py
│   │   │   └── server.py
│   │   └── core
│   ├── requirements.txt
│   └── tests
├── docker-compose.yml
└── history
    └── step1.md

7 directories, 10 files
admin@gw-mac sample-fastapi % 
```

# 2. Install Python module

```sh
admin@gw-mac sample-fastapi % pip3 install -r backend/requirements.txt -t site-packages
Collecting fastapi==0.68.1
  Using cached fastapi-0.68.1-py3-none-any.whl (52 kB)
Collecting uvicorn==0.15.0
  Using cached uvicorn-0.15.0-py3-none-any.whl (54 kB)
Collecting starlette==0.14.2
  Using cached starlette-0.14.2-py3-none-any.whl (60 kB)
Collecting pydantic!=1.7,!=1.7.1,!=1.7.2,!=1.7.3,!=1.8,!=1.8.1,<2.0.0,>=1.6.2
  Using cached pydantic-1.8.2-py3-none-any.whl (126 kB)
Collecting asgiref>=3.4.0
  Using cached asgiref-3.4.1-py3-none-any.whl (25 kB)
Collecting click>=7.0
  Using cached click-8.0.1-py3-none-any.whl (97 kB)
Collecting h11>=0.8
  Using cached h11-0.12.0-py3-none-any.whl (54 kB)
Collecting typing-extensions>=3.7.4.3
  Using cached typing_extensions-3.10.0.2-py3-none-any.whl (26 kB)
Installing collected packages: typing-extensions, starlette, pydantic, h11, click, asgiref, uvicorn, fastapi
Successfully installed asgiref-3.4.1 click-8.0.1 fastapi-0.68.1 h11-0.12.0 pydantic-1.8.2 starlette-0.14.2 typing-extensions-3.10.0.2 uvicorn-0.15.0
WARNING: You are using pip version 21.1.3; however, version 21.2.4 is available.
You should consider upgrading via the '/opt/homebrew/opt/python@3.9/bin/python3.9 -m pip install --upgrade pip' command.
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % cat .vscode/settings.json 
{
    "python.analysis.extraPaths": [
        "./site-packages"
    ],
    "python.autoComplete.extraPaths": [
        "./site-packages"
    ]
}
admin@gw-mac sample-fastapi % 
```


# 3. Build image

```sh
admin@gw-mac sample-fastapi % docker images                                                                             

REPOSITORY              TAG       IMAGE ID       CREATED        SIZE
sample-fastapi_server   latest    3cb8f5e28b79   20 hours ago   47.7MB
<none>                  <none>    bb3f4754c97a   26 hours ago   47.7MB
admin@gw-mac sample-fastapi % docker images rmi 3cb8f5e28b79 bb3f4754c97a
bb3f4754c97a
"docker images" requires at most 1 argument.
See 'docker images --help'.

Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images
admin@gw-mac sample-fastapi % docker rmi 3cb8f5e28b79 bb3f4754c97a 

Untagged: sample-fastapi_server:latest
Deleted: sha256:3cb8f5e28b79d78b2e6079c52d33cdaf1b6b80b753bd68cbf6257b9b42d46676
Deleted: sha256:bb3f4754c97a30fc916087c231c17f5479dc7c74d66f9596c0838464f4af504e
admin@gw-mac sample-fastapi % docker images                              

REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
admin@gw-mac sample-fastapi % docker ps -a

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
admin@gw-mac sample-fastapi % docker-compose build                                                                      

[+] Building 2.3s (11/11) FINISHED                                                                                                                     
 => [internal] load build definition from Dockerfile                                                                                              0.0s
 => => transferring dockerfile: 529B                                                                                                              0.0s
 => [internal] load .dockerignore                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/python:3.9-alpine                                                                              2.2s
 => [auth] library/python:pull token for registry-1.docker.io                                                                                     0.0s
 => [internal] load build context                                                                                                                 0.0s
 => => transferring context: 2.38kB                                                                                                               0.0s
 => [1/5] FROM docker.io/library/python:3.9-alpine@sha256:fc7de772c6b2ab4b60ed4923f71926abcedc2ccac8007d09a616982ee431d17a                        0.0s
 => CACHED [2/5] WORKDIR /backend                                                                                                                 0.0s
 => CACHED [3/5] COPY ./requirements.txt /backend/requirements.txt                                                                                0.0s
 => CACHED [4/5] RUN set -eux  && apk add --no-cache build-base  && pip install --upgrade pip setuptools wheel  && pip install --no-cache-dir --  0.0s
 => CACHED [5/5] COPY . /backend                                                                                                                  0.0s
 => exporting to image                                                                                                                            0.0s
 => => exporting layers                                                                                                                           0.0s
 => => writing image sha256:3cb8f5e28b79d78b2e6079c52d33cdaf1b6b80b753bd68cbf6257b9b42d46676                                                      0.0s
 => => naming to docker.io/library/sample-fastapi_server                                                                                          0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % docker images       

REPOSITORY              TAG       IMAGE ID       CREATED        SIZE
sample-fastapi_server   latest    3cb8f5e28b79   20 hours ago   47.7MB
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % docker run -it --rm 3cb8f5e28b79 /bin/ash

/backend # ls -la
total 24
drwxr-xr-x    1 root     root          4096 Sep  4 04:28 .
drwxr-xr-x    1 root     root          4096 Sep  5 00:47 ..
-rw-rw-r--    1 root     root           407 Sep  3 22:50 Dockerfile
drwxrwxr-x    4 root     root          4096 Sep  4 04:28 app
-rw-rw-r--    1 root     root            31 Sep  3 22:10 requirements.txt
drwxrwxr-x    2 root     root          4096 Sep  3 22:09 tests
/backend #
/backend # python3 -m pip show fastapi
Name: fastapi
Version: 0.68.1
Summary: FastAPI framework, high performance, easy to learn, fast to code, ready for production
Home-page: https://github.com/tiangolo/fastapi
Author: Sebastián Ramírez
Author-email: tiangolo@gmail.com
License: 
Location: /usr/local/lib/python3.9/site-packages
Requires: starlette, pydantic
Required-by: 
/backend # python3 -m pip show uvicorn
Name: uvicorn
Version: 0.15.0
Summary: The lightning-fast ASGI server.
Home-page: https://www.uvicorn.org/
Author: Tom Christie
Author-email: tom@tomchristie.com
License: BSD
Location: /usr/local/lib/python3.9/site-packages
Requires: h11, asgiref, click
Required-by: 
/backend # ls -la /usr/local/lib/python3.9/site-packages
total 224
drwxr-xr-x    1 root     root          4096 Sep  3 22:25 .
drwxr-xr-x    1 root     root          4096 Aug 31 23:59 ..
-rw-r--r--    1 root     root           119 Aug 31 23:58 README.txt
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 __pycache__
drwxr-xr-x    3 root     root          4096 Aug 31 23:59 _distutils_hack
drwxr-xr-x    3 root     root          4096 Sep  3 22:25 asgiref
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 asgiref-3.4.1.dist-info
drwxr-xr-x    3 root     root          4096 Sep  3 22:25 click
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 click-8.0.1.dist-info
-rw-r--r--    1 root     root           152 Aug 31 23:59 distutils-precedence.pth
drwxr-xr-x    7 root     root          4096 Sep  3 22:25 fastapi
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 fastapi-0.68.1.dist-info
drwxr-xr-x    4 root     root          4096 Sep  3 22:25 h11
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 h11-0.12.0.dist-info
drwxr-xr-x    5 root     root          4096 Aug 31 23:59 pip
drwxr-xr-x    2 root     root          4096 Aug 31 23:59 pip-21.2.4.dist-info
drwxr-xr-x    5 root     root          4096 Aug 31 23:59 pkg_resources
drwxr-xr-x    3 root     root          4096 Sep  3 22:25 pydantic
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 pydantic-1.8.2.dist-info
drwxr-xr-x    7 root     root          4096 Aug 31 23:59 setuptools
drwxr-xr-x    2 root     root          4096 Aug 31 23:59 setuptools-57.4.0.dist-info
drwxr-xr-x    4 root     root          4096 Sep  3 22:25 starlette
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 starlette-0.14.2.dist-info
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 typing_extensions-3.10.0.2.dist-info
-rw-r--r--    1 root     root        109284 Sep  3 22:25 typing_extensions.py
drwxr-xr-x    9 root     root          4096 Sep  3 22:25 uvicorn
drwxr-xr-x    2 root     root          4096 Sep  3 22:25 uvicorn-0.15.0.dist-info
drwxr-xr-x    5 root     root          4096 Aug 31 23:59 wheel
drwxr-xr-x    2 root     root          4096 Aug 31 23:59 wheel-0.37.0.dist-info
/backend # 
/backend # exit
admin@gw-mac sample-fastapi % 
```


# 4. Start container

```sh
admin@gw-mac sample-fastapi % docker-compose up  

[+] Running 2/0
 ⠿ Network sample-fastapi_default     Created                                       0.0s
 ⠿ Container sample-fastapi_server_1  Create...                                     0.0s
Attaching to server_1
server_1  | INFO:     Will watch for changes in these directories: ['/backend']
server_1  | INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
server_1  | INFO:     Started reloader process [1] using statreload
server_1  | INFO:     Started server process [8]
server_1  | INFO:     Waiting for application startup.
server_1  | INFO:     Application startup complete.
server_1  | INFO:     172.21.0.1:57134 - "GET /api/hedgehogs/ HTTP/1.1" 200 OK
^CGracefully stopping... (press Ctrl+C again to force)
[+] Running 1/1
 ⠿ Container sample-fastapi_server_1  Stoppe...                                     0.4s
canceled
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % curl http://localhost:8000/api/hedgehogs/ | jq -r '.'

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:-100   109  100   109    0     0   9909      0 --:--:-- --:--:-- --:--:--  9909
[
  {
    "id": 1,
    "name": "momo",
    "color": "SALT & PEPPER",
    "age": 2
  },
  {
    "id": 2,
    "name": "coco",
    "color": "DARK GREY",
    "age": 1.5
  }
]
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % docker-compose down

[+] Running 2/2
 ⠿ Container sample-fastapi_server_1  Remove...                                     0.1s
 ⠿ Network sample-fastapi_default     Removed                                       0.0s
admin@gw-mac sample-fastapi % 
```