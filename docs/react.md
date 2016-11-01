# React MobX React-Router 4 Boilerplate

이게 제일 나은것 같음!
https://github.com/mhaagens/react-mobx-react-router4-boilerplate

# requirement

1. install yarn (npm alternative)

    <https://github.com/yarnpkg/yarn>

    > brew install yarn

1. download `jetbrains-react` plugin

    <https://github.com/minwe/jetbrains-react>

    shift double tab ➜ `Importing Settings...` ➜ `~/Downloads/settings.jar`

1. redux-cli 설치 (generator)

    > npm i redux-cli -g  

    `.reduxrc` 파일

        {
        "sourceBase": "src",
        "testBase": "test",
        "smartPath": "smart",
        "dumbPath": "dumb",
        "fileCasing": "default"
        }

    예)

        // generates a dumb component 
        redux g dumb SimpleButton 

        // generates a smart component 
        redux g smart CommentContainer 

        // generate a redux-form with <form> tags in render statement
        redux g form ContactForm

        // generate a Redux 'duck' (reducer, constants, action creators)
        redux g duck todos

1. react chrome extension

    search @ Google

        React Developer Tools - Chrome Web Store - Google
        Redux DevTools - Chrome Web Store - Google


# yarn

`npm install` 사용안하고, `yarn` 사용한다. (겁나 빠름)

# 코드 연습

codepen을 이용한다. 

예) 
<https://codepen.io/search/pens?q=mobx&limit=all&type=type-pens>

# 스타터 프로젝트

여기서 찾는다. 별점, feature로 검색 가능.
일단은 redux-cli 를 이용한다. (react-redux-starterkit)

<http://andrewhfarmer.com/starter-project/>

# 좋은 예제

- dwatch
    
    react + mobx + ajax + electron 

    <https://github.com/Mercateo/dwatch>

- [mobx]Simple app with Ajax, authentication, context, routing: 

    <http://stackoverflow.com/a/36164488/1983583>

-  mobx examples
    https://mobxjs.github.io/mobx/faq/examples.html        