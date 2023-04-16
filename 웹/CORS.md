# CORS
## 웹 개발시 발생하는 CORS 에러
![에러 화면](https://user-images.githubusercontent.com/50614241/229783963-6555bcb7-a758-4731-a7fb-959497b83441.png)

## CORS란?
 - Cross-Origin Resource Sharing
 - 웹 브라우저에서 실행되는 스크립트에서 다른 출처(origin)로부터 리소스를 요청할 때 발생하는 보안 상의 이슈를 해결하기 위한 메커니즘
 - 기본적으로 웹 브라우저는 보안상의 이유(CSRF, XSS 등의 공격)로 같은 출처에서만 리소스를 공유할 수 있음 (SOP)
 - 과거에는 웹 페이지의 리소스가 항상 동일한 출처내에 존재했지만, 최근 웹 애플리케이션은 다른 출처에서 리소스를 가져와 조합하는 것이 대부분
 - 따라서 2010년 즈음에 몇가지 예외 사항에 대해서는 CORS를 허용하기로 했는데 이것을 CORS 정책이라고 부름

## CORS 발생 조건
1. 다른 출처(origin)의 리소스에 접근하는 경우
2. HTTP 메서드가 GET, POST, HEAD 이외의 메서드를 사용하는 경우
3. Content-Type 헤더가 application/x-www-form-urlencoded, multipart/form-data, text/plain 이외의 값으로 설정된 경우
4. XMLHttpRequest 객체가 아닌 다른 방식으로 AJAX 요청을 보내는 경우
5. Credentials 플래그가 true로 설정된 경우

## CORS 체크 로직
1. 브라우저가 서버에 스크립트로 리소스를 요청한다.
2. 서버가 해당 리소스를 응답한다.
3. 브라우저가 리소스의 출처가 기존 도메인과 같은지 비교한다.
    - 스킴, 호스트, 포트가 동일하면 뒤의 URI가 달라도 같은 출처
    - 셋 중 하나라도 다르면 다른 출처
   
![IE의 출처비교](https://user-images.githubusercontent.com/50614241/229783955-7dd8986f-f38f-4f25-846c-6a22a5f3f285.png)

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
```java
@CrossOrigin(origin="*", allowedHeaders = "*")
@Controller
public class MainController {
	@GetMapping(path = "/")
	public String main(Model model) {
		return "main";
	}
}
```
```java
@Component
public class SimpleCorsFilter implements Filter {

    @Override
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) req;
        HttpServletResponse response = (HttpServletResponse) res;
        response.setHeader("Access-Control-Allow-Origin", request.getHeader("Origin"));
        response.setHeader("Access-Control-Allow-Credentials", "true");
        response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE, PUT, PATCH");
        response.setHeader("Access-Control-Max-Age", "3600");
        response.setHeader("Access-Control-Allow-Headers", "Content-Type, Accept, X-Requested-With, remember-me");
        chain.doFilter(req, res);
    }
```
2. Webpack Dev Server로 리버스 프록싱
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
3. 브라우저 CORS 플러그인 활성화
   - 기본적으로 브라우저의 기능이기 때문에 Moesif Origin & CORS Changer, Allow CORS 등의 플러그인을 설치하여 기능을 이용하지 않는 방법도 있다.