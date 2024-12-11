### [Config](https://github.com/prgrms-web-devcourse-final-project/WEB1_2_FlowDay_BE/tree/develop/src/main/java/org/example/flowday/global/security/config)

- SecurityConfig
    - SecurityFilterChain을 이용하여 커스텀 필터를 등록
    - UsernamePasswordAuthenticationFilter를 상속하는 LoginFilter의 불필요한 인증 요청 방지를 위한 formLogin disable
    - 회원가입, 아이디/비밀번호 찾기 등의 기능에 인증을 요청하지 않도록 등록
    - JwtFilter, LoginFilter, LogoutFilter 등록
    - authorizationRequestRepository Custom
    - userInfoEndpoint Custom
    - success/failure Handler 등록

### [Filter](https://github.com/prgrms-web-devcourse-final-project/WEB1_2_FlowDay_BE/tree/develop/src/main/java/org/example/flowday/global/security/filter)

- JwtFilter
    - 헤더에 Jwt 토큰이 존재하는 경우 동작
    - 토큰을 파싱하여 회원 정보 객체 생성 및 등록
- LoginFilter
    - /api/v1/members/login 경로의 POST 요청에 대해 동작
    - 로그인ID, PW를 DB와 대조 후 인증 결과를 바탕으로 Handler 호출
- LogoutFilter
    - /api/v1/members/logout 경로의 POST 요청에 대해 동작
    - 토큰을 파싱하여 해당하는 유저의 RefreshToken 삭제로 보안 강화

### [Handler](https://github.com/prgrms-web-devcourse-final-project/WEB1_2_FlowDay_BE/tree/develop/src/main/java/org/example/flowday/global/security/handler)

- CustomAuthenticationSuccessHandler
    - 인증이 성공한 요청에 대해 JWT 토큰과 ID 반환
- CustomAuthenticationFailureHandler
    - 인증이 실패한 요청에 대해 에러 코드와 메세지 반환

### [Util](https://github.com/prgrms-web-devcourse-final-project/WEB1_2_FlowDay_BE/tree/develop/src/main/java/org/example/flowday/global/security/util)

- [oauth2](https://github.com/prgrms-web-devcourse-final-project/WEB1_2_FlowDay_BE/tree/develop/src/main/java/org/example/flowday/global/security/util/oauth2)
    - dto
        - OAuth2 Recourse Server 간의 Response 구조 차이에 따른 OAuth2Response 인터페이스와 구현체
        - Oauth2 인증에 사용되는 OAuth2User 인터페이스 구현체
    - repository
        - 배포시 게이트웨이 및 블루그린 배포를 위한 다중 서버 환경에서의 세션 불일치로 발생하는 OAuth2 인증 실패 현상을 해결하기 위한 커스텀 AuthorizationRequestRepository 구현체
    - service
        - DefaultOAuth2UserService 를 상속하여 OAuth2 응답 정보를 바탕으로 사용자 정보를 서버 DB에 저장하고 토큰을 발급할 수 있도록 인증 정보를 Handler로 전달하는 클래스
- CookieUtils
    - HttpCookieOAuth2AuthorizationRequestRepository 관련 메서드
- JwtUtil
    - Jwt 토큰 관련 메서드
- SecurityUser
    - SpringSecurity 인증에 사용되는 UserDatails 인터페이스 구현체
- SecurityUserService
    - SpringSecurity 인증에 사용되는 UserDetailsService 인터페이스 구현체
