# PHP Routing

## 참고
- [[1] With PHP frameworks, why is the “route” concept used?](https://softwareengineering.stackexchange.com/questions/122190/with-php-frameworks-why-is-the-route-concept-used#:~:text=Routing%20is%20the%20process%20of%20taking%20a%20URI%20endpoint%20)
- [[2] How to build a basic server side routing system in PHP](https://medium.com/the-andela-way/how-to-build-a-basic-server-side-routing-system-in-php-e52e613cf241)


## [참고 - [1]](https://softwareengineering.stackexchange.com/questions/122190/with-php-frameworks-why-is-the-route-concept-used#:~:text=Routing%20is%20the%20process%20of%20taking%20a%20URI%20endpoint%20) 정리
- [사전 지식] Rewrite Engine
    - URL의 형태를 수정해주는 엔진을 'Rewrite Engine'이라고 한다 (SEF, Search Engine Friendly).
    - 실제 웹페이지를 보이는 파일과 웹상 검색되는 URL을  분류하는 기법이다.
    - PHP는 주로 아파치 서버랑 같이 쓰이기에 가장 흔히 쓰이는 rewrite engine은 'Apache's **mod_rewrite 모듈**'이다.
        - [참고자료](http://httpd.apache.org/docs/current/mod/mod_rewrite.html)
        - PCRE(Perl Compatible Regular Expressions) regex parser을 이용하여 요청한 URL 을 바로 재작성한다.
        - 기본적으로, URL을 파일시스템의 경로로 매핑하는데, URL을 다른 URL로 redirect 하는 것도 가능하다. 
        - 서버의 변수, 환경 변수, HTTP 헤더 등에 근거하여 URL을 재작성 할 수 있게 하며, 무한개의 rule을 적용할 수 있다.
        - full URL path에 작동하며(path info section도 포함됨), 해당 rewrite rule은 'httpd.conf' 나 '.htaccess' 파일에다가 적을 수 있다.
            - Rewrite rule에 따라 만든 경로(path)는 쿼리문이나 내부 하위 처리(internal sub-processing), 외부요청 리디렉션(external redirection), 내부 프록시 처리량(internal proxy throughput)을 포함할 수 있다. 

- Rewritten URL을 사용하기 위해서는 **routing** 이 필요하다.
    - Routing: URI의 앤드포인트를 가지고 parmaeter로 분해하여 어떤 Module, Controller, Action of controller가 request를 받아야할지 결정하는 것이다.
- 대부분 PHP framewroks는 [MVC pattern]()을 따르고 있다.
- Parameter를 가지고 Controller나 method에 매칭할때는 주로 정규식(regex)을 사용한다.
    - (예시) CodeIgniter URI Routing 
        - 여기서 $route는 패턴화된 Key를 가지고 resulting action을 Value로 가져오는 형태이다. 
        - Resulting Action의 형태: controller/action_method/dynamic_parameter
        > $route['blog/joe'] = "blogs/users/34";<br>
          $route['product/(:any)'] = "catalog/product_lookup";

## [참고 - [2]]((https://medium.com/the-andela-way/how-to-build-a-basic-server-side-routing-system-in-php-e52e613cf241)) 정리


### [추가] ".htaccess" 파일을 통해 URL redirecting
- [참고한 사이트](https://ithemes.com/what-is-the-htaccess-file/)
- ".htaccess" 파일: 웹사이트의 high-level configuration 파일이라고 보면 된다. <br>
단, 이 파일은 Apache를 쓰는 서버에서 쓰인다.
    - 기능
    - **특정 URL로의 redirection이 가능하다**
        - 정규식을 이용하여, 이 기능을 사용할 수 있다.
        - [[Youtube] 참고영상](https://www.youtube.com/watch?v=lRmlDeB7Ovs)
    - 404 page 같은 자신이 만든 커스텀 에러 페이지로의 로드가 가능하다.
    - 우리가 만드는 사이트가 HTTP 대신 HTTPS를 강제로(force) 사용하게 한다.
    - 우리 서버에서 특정 디렉토리들을 Password-protect 할 수 있다. 
    - Hotlinking 을 방지할 수 있다. (Hotlinking이란, 서버 호스트의 대역폭(bandwidth)를 훔쳐쓰고, 해당 호스트가 그 사용 대가를 치루게 하는 것이다.)
