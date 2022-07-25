## Git 설치 
```
$ sudo apt install git
$ git --version // 버전확인
```

## Git 다운로드 
```
$ git clone [url 주소]
```

## Git 세로 업로드 
* push했을때 올라갈 내 정보를 입력
```
$ git config --global user.name [이름]

$ git config --global user.mail [메일 주소]
```
* config 확인 
```
$ git config --list
```
* Git 레파지토리 가져오기 
```
$ git clone [url 주소] 
```
* 파일 추가 
```
$ git add [파일명]
$ git commit -m "message...(변경 사항 또는 버전)" 
$ git push -u origin [브랜치명] // 보통은 master
```

## 기존 디렉토리를 Git으로 업로드 
* local Git 저장소 등록 
```
$ git init 
```
* remote 저장소 등록 후 push 
```
$ git remote add origin [url 주소]

$ git add .

$ git commit -m "forder"

$ git push -u origin master
```

## 당겨오기 
* 다른 누군가가 추가 파일을 업로드해 둔게 있다면 pull 로 당겨 온다
```
$ git pull
```
* git pull origin 브랜치명’ 으로 특정 브랜치의 pull 도 가능 하다
