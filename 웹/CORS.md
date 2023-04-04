# CORS
## 웹 개발시 발생하는 CORS 에러
[CORS 에러발생 이미지]

## CORS란?
 - Cross-Origin Resource Sharing
 - 웹 브라우저에서 실행되는 스크립트에서 다른 출처(origin)로부터 리소스를 요청할 때 발생하는 보안 상의 이슈를 해결하기 위한 메커니즘
 - 기본적으로 웹 브라우저는 보안상의 이유(CSRF, XSS 등의 공격)로 같은 출처에서만 리소스를 공유할 수 있음 (SOP)
 - 과거에는 웹 페이지의 리소스가 항상 동일한 출처내에 존재했지만, 최근 웹 애플리케이션은 다른 출처에서 리소스를 가져와 조합하는 것이 국룰
 - 따라서 2010년 즈음에 몇가지 예외 사항에 대해서는 CORS를 허용하기로 했는데 이것을 CORS 정책이라고 부름

## CORS 체크 로직
1. 브라우저가 서버에 스크립트로 리소스를 요청한다.
2. 서버가 해당 리소스를 응답한다.
3. 브라우저가 리소스의 출처가 기존 도메인과 같은지 비교한다.
    - 스킴, 호스트, 포트가 동일하면 뒤의 URI가 달라도 같은 출처
    - 셋 중 하나라도 다르면 다른 출처
[IE 출처 판단 이미지]

4. 출처가 다르면 설정된 CORS 설정에 따라 브라우저가 응답의 파기 여부를 결정한다.

## CORS 설정 방법
1. 리소스 서버의 응답 헤더에 Access-Control-Allow-Origin 추가
   - `Access-Control-Allow-Origin: *` 헤더를 추가하면 모든 도메인에서의 요청을 허용할 수 있지만, 권장되지 않는다.
   - `Access-Control-Allow-Origin: http://stupids.shop`과 같이 허용할 요청 Origin을 명시하는 것이 권장된다.
```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
            .allowedOrigins("*")
            .allowedMethods("GET", "POST", "PUT", "DELETE")
            .allowedHeaders("*");
    }
}
```
2. 리소스 서버의 응답 헤더에 Access-Control-Allow-Headers 추가
   - 
3. Webpack Dev Server로 리버스 프록싱
   - CORS를 가장 많이 마주하는 환경은 로컬에서 프론트엔드 어플리케이션을 개발하는 경우임
   - 백엔드 프레임워크가 `Access-Control-Allow-Origin` 헤더에 `localhost:3000` 같은 범용 출처를 넣어주는 경우는 없기 때문
   - 로컬에서만 개발하는 환경이라면 요청URI를 프록시로 변경하여 출처를 변경하는 방법을 사용할 수 있음
```javascript
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'https://api.evan.com',
        changeOrigin: true,
        pathRewrite: { '^/api': '' },
      },
    }
  }
}
```
3. 