# JSON Web Token
## Cookie
- 클라이언트의 브라우저에 Key-Value 형식의 문자열을 기록해두고 사용한다.
- 동작 방식
  1. 클라이언트가 서버에 요청을 보낸다.
  2. 서버는 클라이언트의 요청에 대한 응답을 작성할 때, 클라이언트 측에 저장하고 싶은 정보를 응답 헤더의 Set-Cookie에 담는다.
  3. 이후 해당 클라이언트는 요청을 보낼 때마다, 매번 저장된 쿠키를 요청 헤더의 Cookie에 담아 보낸다. 서버는 이를 이용해 클라이언트를 식벼라하거나 추천 광고를 띄우는 등의 행위를 한다.

-> 용량 제한이 있으며, 보안에 취약하다

## Session
- 서버의 메모리나 로컬 파일, 데이터베이스에 정보를 저장하고 Id로 통신하며 접근한다.
- 동작 방식
  1. 클라이언트가 서버에 요청을 보낸다.
  2. 서버의 브라우저 쿠키에 Session Id를 저장하고, 이를 이용해 정보를 저장한다.
  3. 이후 클라이언트는 요청을 보낼때마다, 발급받은 Session Id를 쿠키에 담아 전송한다.
  4. 서버는 이를 확인하고 인증을 수행한다.

-> 요청이 많아지면 서버에 부하가 심해지고, 서버가 여러대인 경우 세션 정보 동기화가 힘들어진다. (Stateful)

![세션 인증](https://user-images.githubusercontent.com/50614241/226605331-b129bf79-db84-4ed1-88bd-1f31bf55cfa1.png)

## Token
- 서버가 인증되었다는 의미와 사용자 정보를 담고 있는 토큰을 부여하고, 이를 이용하여 사용자의 정보를 확인한다.
- 동작 방식
  1. 클라이언트가 서버에 요청을 보낸다.
  2. 서버가 데이터와 개인키를 이용하여 이를 암호화한 전자서명을 함께 보낸다.
  3. 클라이언트는 이를 저장해두고, 요청마다 헤더에 포함시켜 보낸다.
  4. 서버는 이를 검증하고, 응답한다.

-> 토큰 자체의 데이터 길이가 길어지므로 네트워크 부하가 심해지며, 서버가 Stateless하기 때문에 토큰을 임의로 삭제할 수 없다.

![토큰 인증](https://user-images.githubusercontent.com/50614241/226605321-b089dad8-71e4-4216-9e47-381ae1f7fd45.png)

## JWT
- 인증에 필요한 정보들을 암호화시킨 JSON 토큰
- Claim 토큰 인증 방식 (<-> OAuth 토큰 인증 방식)
- Header, Payload, Signature로 이루어진 JSON 데이터를 Base64로 인코딩한 토큰
- 단점이 꽤나 크리티컬해서 100%로 JWT를 사용하는 곳은 많지 않음
- 요즘에는 단점을 보완하기 위해 데이터 접근에 사용되는 access 토큰과 이를 갱신하기 위해 사용하는 refresh 토큰으로 분리하는 방법을 주로 사용

![JWT 예시](https://user-images.githubusercontent.com/50614241/226605328-3b343b7d-ba45-41bd-afd7-ab4f278a91e5.png)

```java
public class JwtTokenProvider {
    private static final String JWT_SECRET = "secretKey";       // 개인 키

    // 토큰 유효시간
    private static final int JWT_EXPIRATION_MS = 604800000;         // 7일

    // jwt 토큰 생성
    public static String generateToken(Authentication authentication) {
        Date now = new Date();
        Date expireDate = new Date(now.getTime() + JWT_EXPIRATION_MS);

        return Jwts.builder()
            .setSubject((String) authentication.getPrincipal()) // 사용자
            .setIssuedAt(new Date()) // 현재 시간 기반으로 생성
            .setExpiration(expireDate) // 만료 시간 세팅
            .signWith(SignatureAlgorithm.HS512, JWT_SECRET) // 사용할 암호화 알고리즘, signature에 들어갈 secret 값 세팅
            .compact();
    }

    // Jwt 토큰에서 아이디 추출
    public static String getUserIdFromJWT(String token) {
        Claims claims = Jwts.parser()
            .setSigningKey(JWT_SECRET)
            .parseClaimsJws(token)
            .getBody();

        return claims.getSubject();
    }

    // Jwt 토큰 유효성 검사
    public static boolean validateToken(String token) {
        try {
            Jwts.parser().setSigningKey(JWT_SECRET).parseClaimsJws(token);
            return true;
        } catch (SignatureException ex) {
            log.error("Invalid JWT signature");
        } catch (MalformedJwtException ex) {
            log.error("Invalid JWT token");
        } catch (ExpiredJwtException ex) {
            log.error("Expired JWT token");
        } catch (UnsupportedJwtException ex) {
            log.error("Unsupported JWT token");
        } catch (IllegalArgumentException ex) {
            log.error("JWT claims string is empty.");
        }
        return false;
    }
}
```