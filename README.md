# Drogon Test

Drogon is a C++14/17-based HTTP application framework. Drogon can be used to easily build various types of web application server programs using C++.

- Performance 참고
<https://www.techempower.com/benchmarks/#section=data-r21>

## Pros

- Linux, MacOS, Windows 모두 제공
- Framework 이 설치된 Docker Image 제공

### View 개발

Drogon 에 특화된 CSP (C++ Server Pages) 제공

### CLI 제공

- Project 생성 및 기본 template 제공

```sh
drogon_ctl create project your_project_name
```

- Project directory structure

```sh
controllers
├── TestCtrl.cc
├── TestCtrl.h
├── demo_v1_User.cc
└── demo_v1_User.h
filtermodels
└── model.json
pluginstest
├── CMakeLists.txt
└── test_main.cc
views
CMakeLists.txt
config.json
main.cc
```

## Cons

- Swagger 등 API documentation 공식 지원 없음
- Official Document 미흡

## Sample app. build 및 실행

Local 환경에서 build 및 실행도 가능하나, 아래는 docker 기반 build 및 app 실행으로 구성하였음.

1. Drogon framework docker image 기반 cmake / make build

```sh
docker run --rm --volume="$PWD:/drogon-project" -w="/drogon-project" drogonframework/drogon sh -c "cd build && cmake .. && make"
```

2. drogon-test containerize

- Ubuntu 20.04 base image 기반 실행
  - [Dockerfile](./Dockerfile)

```sh
docker build -t <image_name> .
```

1. drogon-test image run

```sh
docker run --name drogon-test -it -p 8080:80 kloudbank/drogon-test:0.0.1 sh -c "/app/drogon-test"
```

4. API test

```sh
$ curl http://localhost:8080
Hello World!

$ curl http://localhost:8080/demo/v1/user/testuser/info?token=1234
{"gender":1,"result":"ok","user_id":"testuser","user_name":"Jack"}

$ curl -X POST http://localhost:8080/demo/v1/user/token\?userId\=test\&passwd\=1234
{"result":"ok","token":"C8358D7D4FCE40E8A00E47BDE4BF6272"}
```
