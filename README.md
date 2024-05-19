# springboot 복습

### 환경설정
```
3.xx 버전부터 자바 17 사용.

- 자바17 환경변수 설정 후 file -> project structure에서 sdk java 17로 설정 
- file -> settings에서 자바 컴파일러인 javac을 17버전으로 설정.
- file -> settings에서 gradle 설정 run,test using 
  둘 다 인텔리 제이로 설정하고 jvm sdk와 버전 일치시킴 
```

### 기본 라이브러리
```
우측 상단에 gradle을 클릭하면 해당 프로젝트에서 실행되는 라이브러리를 확인할 수 있다.

스프링 부트 라이브러리
-spring-boot-starter-web
    - spring-boot-starter-tomcat : 톰캣 (웹서버)
    - spring-webmvc : 스프링 웹 MVC
-spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진(view)
-spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
    -spring-boot
        -spring-core
    -spring-boot-starter-logging
        - logback, slf4j

테스트 라이브러리
-spring-boot-starter-test
    -junit:테스트 프레임워크
    -mockito:목 라이브러리
    -assertj:테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    -spring-test:스프링 통합 테스트 지원  
```

### Welcome Page 생성

- resource/statice/index.html
```html
<!doctype html>
<html lang="en">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
Hello
<a href = "/hello">hello</a>
</body>
</html>
```
- static/index.html을 올려두면 Welcome Page 기능을 제공.

### spring 동작환경

- 1.웹브라우저 -> localhost:8080/hello 
- 2.내장 톰켓 서버(was) -> 스프링 컨테이너 컨트롤러를 통해 데이터 return
- 3.viewresolver 스프링부트 템플릿엔진 기본 viewName 매핑 (ex:resource:/templates/ + {viewName}+.html {}:return 문자열)

### gradlew build 관련
- build 실행 시 
```cmd
./gradlew build
cd build/libs
java -jar hello-spring-0.0.1-SNAPSHOT.jar
```
- build 제거 (gradelw있는 폴더로 이동)
```cmd
./gradelw clean
```

### 정적 컨텐츠 이미지
- resource/static 아래의 파일들은 정적 컨텐츠 제공

### MVC와 템플릿 엔진
- MVC : Model, view, Controller
![img.png](src%2Fmain%2Fresources%2Fimages%2Fimg.png)

### @ResponseBody 사용원리
- @ResponseBody를 사용시 HTTP의 Body에 문자 내용을 직접 반환
- viewResolver 대신에 HttpMessageConverter가 동작
- 기본 문자처리 : 'StringHttpMessageConverter'
- 기본 객체처리 : 'MappingJackson2HttpMessageConverter'
- byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음

