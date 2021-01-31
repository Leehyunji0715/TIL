### [참고  영상, 보고 연습한 것!]([https://www.youtube.com/watch?v=kEW6f7Pilc4&t=1s](https://www.youtube.com/watch?v=kEW6f7Pilc4&t=1s));

# PDO 기본 구조

## 1) DSN 생성

```php
$host = 'localhost';
$user = 'root';
$password = '0000';
$dbname = 'pdoposts';

// Set DSN (mysqli에서는 $connection 역할인듯)
$dsn = 'mysql:host='. $host . '; dbname=' . $dbname;
```

## 2) PDO instance 생성

```php
//Create a PDO instance
$pdo = new PDO($dsn, $user, $password);

/* 아래 setAttribute 시 fetch() 시 mode를 지정할 필요가 없다.
$pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO:: FETCH_OBJ);
*/

```

## 3) PDO 쿼리 작성 및 fetch()

```php
//PDO QUERY
$stmt = $pdo->query('SELECT * FROM posts');

while($row = $stmt->fetch(PDO::FETCH_ASSOC)){
	echo $row['title'] . '<br>';
}
```

 참고로 fetchAll() 이라는 것도 있는데 여러개의 record를 가져올 때 사용한다.

# Prepared statements

** Unsafe : sql query에다가 직접 유저 input 를 넣는것은 보안상 좋지 않다.

## Positionall Parameters (?)

```php
$author = 'Brian';

$sql = 'SELECT * FROM posts WHERE author = ?';
$stmt = $pdo->prepare($sql); 
$stmt->execute([$author]);
$posts  = $stmt->fetchAll(옵션은 OBJ 위에 선언함);
```

## Named Parameters (:)

```php
$sql = 'SELECT * FROM posts 
				WHERE author = :author && is_published = :ispublished';
$stmt = $pdo->prepare($sql);
$stmt->execute(['author' => $author, 'is_published' => $is_published]);
$posts = $stmt-> fetchAll(); // 요소가 하나일때는 fetch() 쓰면 된다.

foreach($posts as $post){
	echo $post;
}
```

## Row Count

```php
$stmt = $pdo->prepare('SELECT * FROM WHERE author=?');
$stmt->execute([$author]);

$postCount = $stmt->rowCount();
echo $postCount;
```
