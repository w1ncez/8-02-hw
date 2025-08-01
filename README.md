# Домашнее задание к занятию «Что такое DevOps. СI/СD». Винцентини Сергей

### Задание 1

```
root@vbox:/home/w1nce/8-02-hw# jenkins --version
2.504.3
root@vbox:/home/w1nce/8-02-hw# go version
go version go1.19.8 linux/amd64
```
## Вывод Пайплайна

```
Started by user test
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/test_pipe
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/test_pipe/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/w1ncez/8-02-hw.git # timeout=10
Fetching upstream changes from https://github.com/w1ncez/8-02-hw.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.5'
 > git fetch --tags --force --progress -- https://github.com/w1ncez/8-02-hw.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 223dbc3f489784448004e020f2ef224f17a7b06d (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
Commit message: "Update README.md"
 > git rev-list --no-walk 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
[test_pipe] $ /bin/sh -xe /tmp/jenkins17595120686963481831.sh
+ /usr/local/go/bin/go test .
ok  	github.com/netology-code/sdvps-materials	(cached)
+ docker build . -t ubuntu-bionic:8082/hello-world:v12
Sending build context to Docker daemon  250.9kB

Step 1/8 : FROM golang:1.16 AS builder
 ---> 972d8c0bc0fc
Step 2/8 : WORKDIR $GOPATH/src/github.com/netology-code/sdvps-materials
 ---> Using cache
 ---> 48fce210187f
Step 3/8 : COPY . ./
 ---> Using cache
 ---> edafea3dfa55
Step 4/8 : RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /app .
 ---> Using cache
 ---> 8a0d9965fbd4
Step 5/8 : FROM alpine:latest
 ---> 9234e8fb04c4
Step 6/8 : RUN apk -U add ca-certificates
 ---> Using cache
 ---> 93460b5314b6
Step 7/8 : COPY --from=builder /app /app
 ---> Using cache
 ---> d904abd93ee5
Step 8/8 : CMD ["/app"]
 ---> Using cache
 ---> 69a0a9c088d1
Successfully built 69a0a9c088d1
Successfully tagged ubuntu-bionic:8082/hello-world:v12
+ docker login ubuntu-bionic:8082 -u admin -p admin
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
+ docker push ubuntu-bionic:8082/hello-world:v12
The push refers to repository [ubuntu-bionic:8082/hello-world]
c2a070244d8e: Preparing
22a58f92bd65: Preparing
418dccb7d85a: Preparing
22a58f92bd65: Pushed
c2a070244d8e: Pushed
418dccb7d85a: Pushed
v12: digest: sha256:a2c8410f57bdc94289f1a7a59953b8f24f598e910be9092edf2c3b5fee5cab35 size: 950
+ docker logout
Removing login credentials for https://index.docker.io/v1/
Finished: SUCCESS
```

### Задание 2

## Вывод пайплайна

```
Started by user test
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/pipetest
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Git)
[Pipeline] git
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
Cloning repository https://github.com/netology-code/sdvps-materials.git
 > git init /var/lib/jenkins/workspace/pipetest # timeout=10
Fetching upstream changes from https://github.com/netology-code/sdvps-materials.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.5'
 > git fetch --tags --force --progress -- https://github.com/netology-code/sdvps-materials.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/netology-code/sdvps-materials.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision da5acf7bcb7f437637adf06fbd03a24dc2c8f13e (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f da5acf7bcb7f437637adf06fbd03a24dc2c8f13e # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git checkout -b master da5acf7bcb7f437637adf06fbd03a24dc2c8f13e # timeout=10
Commit message: "branch main, add creds for vagrant box"
First time build. Skipping changelog.
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Test)
[Pipeline] sh
+ go test .
ok  	github.com/netology-code/sdvps-materials	0.003s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build)
[Pipeline] sh
+ docker build . -t ubuntu-bionic:8082/hello-world:v1
Sending build context to Docker daemon  242.2kB

Step 1/8 : FROM golang:1.16 AS builder
 ---> 972d8c0bc0fc
Step 2/8 : WORKDIR $GOPATH/src/github.com/netology-code/sdvps-materials
 ---> Using cache
 ---> 48fce210187f
Step 3/8 : COPY . ./
 ---> fa6d3d7e954b
Step 4/8 : RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /app .
 ---> Running in bf78479a8837
Removing intermediate container bf78479a8837
 ---> 1b1a2a95cd66
Step 5/8 : FROM alpine:latest
 ---> 9234e8fb04c4
Step 6/8 : RUN apk -U add ca-certificates
 ---> Using cache
 ---> 93460b5314b6
Step 7/8 : COPY --from=builder /app /app
 ---> Using cache
 ---> d904abd93ee5
Step 8/8 : CMD ["/app"]
 ---> Using cache
 ---> 69a0a9c088d1
Successfully built 69a0a9c088d1
Successfully tagged ubuntu-bionic:8082/hello-world:v1
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Push)
[Pipeline] sh
+ docker login ubuntu-bionic:8082 -u admin -p admin
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
+ docker push ubuntu-bionic:8082/hello-world:v1
The push refers to repository [ubuntu-bionic:8082/hello-world]
c2a070244d8e: Preparing
22a58f92bd65: Preparing
418dccb7d85a: Preparing
c2a070244d8e: Layer already exists
418dccb7d85a: Layer already exists
22a58f92bd65: Layer already exists
v1: digest: sha256:a2c8410f57bdc94289f1a7a59953b8f24f598e910be9092edf2c3b5fee5cab35 size: 950
+ docker logout
Removing login credentials for https://index.docker.io/v1/
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```

### Задание 3

## Вывод пайплайна

```
Started by user test
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/pipetest
[Pipeline] {
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Checkout)
[Pipeline] git
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/pipetest/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/hovhannisyan-code/8-2-fork.git # timeout=10
Fetching upstream changes from https://github.com/hovhannisyan-code/8-2-fork.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.5'
 > git fetch --tags --force --progress -- https://github.com/hovhannisyan-code/8-2-fork.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 223dbc3f489784448004e020f2ef224f17a7b06d (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git checkout -b main 223dbc3f489784448004e020f2ef224f17a7b06d # timeout=10
Commit message: "Update README.md"
First time build. Skipping changelog.
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build Binary)
[Pipeline] sh
+ /usr/local/go/bin/go env
GO111MODULE=""
GOARCH="amd64"
GOBIN=""
GOCACHE="/var/lib/jenkins/.cache/go-build"
GOENV="/var/lib/jenkins/.config/go/env"
GOEXE=""
GOEXPERIMENT=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOINSECURE=""
GOMODCACHE="/var/lib/jenkins/go/pkg/mod"
GONOPROXY=""
GONOSUMDB=""
GOOS="linux"
GOPATH="/var/lib/jenkins/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/local/go"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/usr/local/go/pkg/tool/linux_amd64"
GOVCS=""
GOVERSION="go1.17.5"
GCCGO="gccgo"
AR="ar"
CC="gcc"
CXX="g++"
CGO_ENABLED="1"
GOMOD="/var/lib/jenkins/workspace/pipetest/go.mod"
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build1265363395=/tmp/go-build -gno-record-gcc-switches"
[Pipeline] sh
+ CGO_ENABLED=0 GOOS=linux /usr/local/go/bin/go build -a -installsuffix nocgo -o app .
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Archive Binary)
[Pipeline] archiveArtifacts
Archiving artifacts
Recording fingerprints
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Upload to Nexus)
[Pipeline] script
[Pipeline] {
[Pipeline] sh
+ curl -v -u admin:admin --upload-file app http://192.168.1.11:8081/repository/testraw/app
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed

  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 192.168.1.11:8081...
* Connected to 192.168.1.11 (192.168.1.11) port 8081 (#0)
* Server auth using Basic with user 'admin'
> PUT /repository/testraw/app HTTP/1.1
> Host: 192.168.1.11:8081
> Authorization: Basic YWRtaW46YWRtaW4=
> User-Agent: curl/7.88.1
> Accept: */*
> Content-Length: 1864864
> Expect: 100-continue
> 
< HTTP/1.1 100 Continue
} [65536 bytes data]
* We are completely uploaded and fine
< HTTP/1.1 201 Created
< Server: Nexus/3.82.0-08 (COMMUNITY)
< X-Content-Type-Options: nosniff
< Content-Security-Policy: sandbox allow-forms allow-modals allow-popups allow-presentation allow-scripts allow-top-navigation
< X-XSS-Protection: 1; mode=block
< Content-Length: 0
< 

100 1821k    0     0  100 1821k      0  12.5M --:--:-- --:--:-- --:--:-- 12.6M
* Connection #0 to host 192.168.1.11 left intact
[Pipeline] }
[Pipeline] // script
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Declarative: Post Actions)
[Pipeline] echo
Build and upload successful!
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```

