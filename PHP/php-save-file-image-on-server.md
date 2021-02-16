- 참고 URL
    - [[stackoverflow] php-image-upload](https://stackoverflow.com/questions/18801056/php-image-upload-function-save-in-a-dir-and-then-return-save-image-url/18801110)
    

## HTML에서 파일 업로드 하는 코드

```html
<form enctype="multipart/form-data" action="upload.php" method="POST">
    <input type="hidden" name="MAX_FILE_SIZE" value="512000" />
	    Send this file: <input name="userfile" type="file" />
    <input type="submit"/>
</form>
```

- **enctype="multipart/form-data"**
    - POST 시, 파일의 data를 encode 해야 하는데 encode 방식 중 하나
    - Input이 "file" type일 때 쓴다.

## 파일을 서버에 저장하는 PHP 코드 (upload.php)

```php
<?php
	
$uploaddir = '/var/www/uploads/';
$uploadfile = $_SERVER['DOCUMENT_ROOT'] . $uploaddir . basename($_FILES['userfile']['name']);
	
	
if (move_uploaded_file($_FILES['userfile']['tmp_name'], $uploadfile))
	  echo "File is valid, and was successfully uploaded.\n";
else 
	  echo "Upload failed";

?>
```

- **$_FILES['userfile']['tmp_name']**
    - 사용자가 type이 file 인 input에 파일을 업로드하면, 서버에 임시적으로 $_FILES['userfile']['tmp_name'] 에 파일이 저장되고, 페이지가 작업 완료시 사라진다.
    - 따라서 해당 업로드된 파일을 서버에다가 따로 저장하려면

        move_uploaded_file($from, $to) 를 사용해야 한다.

- **$_FILES['userfile']['name']**
    - 클라이언트 상 실제 파일을 가리킨다.
    - 실제 파일의 이름 + 확장자를 가지고 오는데는 basename() 함수와 같이 쓴다.