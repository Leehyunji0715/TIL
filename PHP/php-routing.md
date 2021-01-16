# PHP Routing

## 내용



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
