# SpringBoot VueJS 연동


# Spring Boot + VueJS 연동하기.
Spring boot와 VueJS를 사용하여 프로젝트를 진행할때 기본 구성방법을 정리한다.

## Spring boot 프로젝트 생성 
IDE를 이용하여 springBoot 프로젝트를 생성하여 준다.
기본값인 Maven + SpringBoot로 생성하였다.

## VueJS 프로젝트 구성하기.
* 프로젝트 루트경로에 'frontend' 폴더를 생성하고 그하위에  vueJS 프로젝트를 구성할것이다.
  vue-cli3, vuex, vue-router까지 진행.

```bash
    $ mkdir frontend
    $ cd forntend
    $ npm install -g @vue/cli
    $ vue create ui --no-git
```
springBoot 프로젝트의 루트경로에서 frontend 디렉토리를 만들고, frontend 디렉토리에서 vue-cli를 install 받은 후
vue 프로젝트를 생성한다. 처음엔 그냥 기본값으로 install을 진행한다.
frontend 디렉토리 하위에 ui폴더가 생성되면서 vue 프로젝트가 생성된다.

 ![Example image](/images/createVue.PNG)
 
 정상적으로 생성되었을때의 프로젝트 구조이다. ui하위에 vue.config.js파일을 생성하여 npm build시에 결과파일들의 경로 설정을 해주어야 한다.
 ```javascript
    module.exports = {
        outputDir: "../../src/main/resources/static",
        indexPath: "../static/index.html",
        devServer: {
            proxy: "http://localhost:8080"
        }
    }; 
```
 js, css, html 등 build이후에 결과파일들은 스프링부트 'src/main/resources/static' 하위로 생성되게 하기위한 설정이다.
 ui 폴더 루트경로에서 'npm run build' 명령어를 실행하여 'src/main/resources/static'하위에 forntend 소스들이 정상적으로 빌드되어 생성는지 확인할 수 있다.
 
 ![Example image](/images/npmbuild.PNG)
 
 spring boot 를 실행하여 브라우저에서도 확인한다. 
 
 ![Example image](/images/browser.PNG)
 
 
 ## vue-router, vuex 추가
 브라우저에서 정상적으로 동작하는것을 확인했으니 vue-router와 vuex를 추가한다.
 ```bash
    $ vue add router 
```
```
    $ vue add vuex
```
ui 루트경로에서 'vue add ***' 명령으로 vur-router와 vuex를 추가연동한다.
정상적으로 추가가 되었다면 ui디렉토리에 'router'폴더와 'store'폴더를 확인할 수 있다.
브라우저에서도 'npm run build'를 다시 실행하여, 'vue-router'플러그인이 반영된 샘플 화면으로 바뀐것을 확인할 수 있다.

 ![Example image](/images/addRouterVuex.PNG)
 
 ![Example image](/images/browser2.PNG)

war로 spring boot프로젝트를 빌드한 후 배포하였을때도 정상적으로 동작하는것을 확인할 수 있다.
 
