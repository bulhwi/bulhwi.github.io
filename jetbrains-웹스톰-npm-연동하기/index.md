# Jetbrains 웹스톰 NPM 연동하기


# 웹스톰에서 NPM 연동하기.
프론트엔드 개발 툴로 사용중인 웹스톰에서 NPM을 연동하여 'ctrl + shift + f10' 단축기로 간단하게 실행 할수있다.

## 1. package.json 설정.
```json
 "scripts": {
    "build": "hexo generate --deploy",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
```
'npm run ***'으로 위에서 정의된 명령어를 사용할 수 있다. hexo에서 사용가능한 명령어를 설정하였다.

## 2. Add Configuration 클릭.
 ![Example image](/images/addConf.PNG)
 ![Example image](/images/addConf2.PNG)
 
 
 이미지에서 처럼 'package.json'파일의 경로를 잡아주고 Scripts항목에 'package.json'파일에서 설정한 명령어들을 넣어주면 
 'ctrl + shift + f10'단축키로 편하게 작업이 가능해진다. 
