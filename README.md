# Realworld Example App

## 1. 컨테이너 이미지 빌드

> *구버전 Git 클라이언트가 설치된 환경에서는 docker build {git repository url} 실행 시 unable to prepare context 에러가 발생할 수 있습니다.*  
> *해결방법은 Git 클라이언트를 최신 버전으로 업데이트 후 docker build를 실행하거나, backend 및 frontend 소스코드를 각각 clone 하여 docker build를 실행하면 됩니다.*  

**Backend**
```
docker build -t gwantaek/realworld-backend https://github.com/gwantaek/spring-boot-realworld-example-app.git

or

git clone https://github.com/gwantaek/spring-boot-realworld-example-app.git
docker build -t gwantaek/realworld-backend spring-boot-realworld-example-app/.
```

**Frontend**
```
docker build -t gwantaek/realworld-frontend https://github.com/gwantaek/react-redux-realworld-example-app.git

or

git clone https://github.com/gwantaek/react-redux-realworld-example-app.git
docker build -t gwantaek/realworld-frontend react-redux-realworld-example-app/.
```


## 2. docker-compose 실행 및 종료
**Dev profile**
```
docker-compose --env-file=.env.dev up -d
```

**Prod profile**
```
docker-compose --env-file=.env.prod up -d
```

**실행 종료**
```
docker-compose down
```

## 3. Article Revision History API
**Path**
```
/articles/{slug}/revisions
```

Article의 **제목과 본문**을 `'test1'`으로 포스팅한 후 **본문**을 `'test1 revision'` 으로 수정하고 revision api를 호출하면 아래 결과를 확인할 수 있습니다.  

**Request**
```
http://localhost/articles/test1/revisions
```

**Response**
```json
{
    "revisions": [
        {
            "id": "adbc2130-769b-4293-9e99-0e322185c4e0",
            "articleId": "0cea4b0a-f62a-4471-b486-475f33b4621d",
            "slug": "test1",
            "title": "test1",
            "description": "test1",
            "body": "test1 revision",
            "type": "UPDATE",
            "revisedAt": "2021-04-25T00:52:59.000Z",
            "cursor": {
                "data": "2021-04-25T00:52:59.000Z"
            }
        },
        {
            "id": "9cbc04e4-f9a1-4155-b4e8-95668d747956",
            "articleId": "0cea4b0a-f62a-4471-b486-475f33b4621d",
            "slug": "test1",
            "title": "test1",
            "description": "test1",
            "body": "test1",
            "type": "INSERT",
            "revisedAt": "2021-04-25T00:52:32.000Z",
            "cursor": {
                "data": "2021-04-25T00:52:32.000Z"
            }
        }
    ],
    "revisionsCount": 2
}
```

## 4. 작업 내역
**Backend**
- Article revision history 기능 & API
- dev & prod properties 추가
- Article revision history 테스트 코드

**Frontend**
- Dockerfile 추가
- Local 개발 환경을 위한 webpack devServer proxy config override
- Nginx server configuration

**Docker-compose** 
- dev & prod 실행 환경 적용
- db_net & app_net 네트워크 분리

## 5. Files
- **.env.dev, .env.prod** : docker-compose profile 환경 변수
- **default.conf** : nginx server configuration
- **docker-compose.yml**
- **README.md**

## 6. 소스코드 Github urls
- https://github.com/gwantaek/docker-compose-realworld-example-app
- https://github.com/gwantaek/spring-boot-realworld-example-app
- https://github.com/gwantaek/react-redux-realworld-example-app
