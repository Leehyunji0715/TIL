## 오늘 한 일 (2021-01-12)
- [Youtube - 게시판 만들 때 대부분 참조한 영상](https://www.youtube.com/watch?v=ctpNfiLSrhM&list=PLRheCL1cXHrvTkUenAc5GdEvqIpVX-2JJ&index=2)
- 기존에 html로 만든 웹페이지를 .php로 바꾸고, 기본적으로 대부분 웹 페이지에 들어가는 공통된 .php 파일들(header, footer, navbar, section, scripts)을 "/includes" 폴더명 안에다가 넣었다.<br> 확실히 구분을 해놓으니까 코드 찾기도 쉬워지고, 전체적으로 워크스페이스가 깔끔해졌다.
- 마찬가지로 css파일들도 "/css"에 js 파일들도 "/js"에 두었다.
- php를 이용하여 DB(mysql)에 접근할 수 있는데, "mysqli"를 이용하여 접근하였다.<br/>
이는 mysql에만 사용이 가능한 함수들만 있고, 좀 더 좀더 다양한 DB 함수를 사용하려면 "PDO(Php Data Object)"를 사용하면 된다.
    - 연결할 때: $connection = mysqli_connect("localhost", "id", "password", "테이블이름");
    - 데이터를 쿼리할 때: $query_run = mysqli_query($connection, $query);
    - 연결 종료할 때: mysqli_close($connection);
    - 그 외:
        - query 후 row 개수 (=record 수) 세는 함수: mysqli_num_rows($query_run)
        - 여러개의 record를 fetch 했을 때, 각 record를 하나씩 읽어들이는 것: $row = mysqli_fetch_assoc($query_run)<br>
        반복문이랑 같이 쓰이고, 예를 들어, $row['id'] 같이  column 명이랑 쓰이면, 테이블에 저장되어 있는 해당 값을 가져올 수 있다.
- mysql DB에 연결을 할 때, 실제 서비스를 제공할 떄는 공개적으로 connection을 하면 안된다. 따라서 조심해야 하는 정보를 다루는 파일들은 "private"라는 디렉토리를 따로 만들고 난 후, 해당 디렉토리에 저장할 예정이다.<br>
그리고 Apache에서 외부 접속 권한을 다루는 ".htaccess" 파일을 만들어볼 예정이다.<br>
[Stackoverflow-참조링크](https://stackoverflow.com/questions/31683201/safe-to-store-private-php-files-above-public-directory-and-load-them-using-requi)
- 그리고 <table\> 태그를 이용하여 일반적으로 알려진 게시판 페이지를 만들어 보았다. 