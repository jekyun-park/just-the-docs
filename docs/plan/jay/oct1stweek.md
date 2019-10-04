---
layout: default
title: Jay's Oct 1st Week Plan
parent: Jay's Plan
grand_parent: Plan
nav_order: 1
permalink: /docs/plan/jay/oct1stweek

---

1. TOC
{:toc}







[TOC]



# 나의 웹 계획

------



- 프로젝트 렌더링 ( :star: :star: :star: :star: :star: )

  - 노드 스터디 이후 개발 들어가기 전에 날 잡아서 프로젝트 렌더링 또는 스케치 해서 메인 기능 외에 다른 기능들 구체화

  ------

- 사이드 페이지 컨텐츠 (추후 개발 :star: :star: )

  - 랭킹보드 (요일별, 주별, 월별)
    - 사람들이 좋아요를 많이 누른 게시물 리스트 보여주기
    - 사람들이 스크랩 많이 한 게시물 리스트 보여주기

  ------

- 이미지 합성 중 로딩 (우선 개발 :star: :star: :star: :star: )

  - 이미지 합성 중 로딩할 때는 시간이 오래 걸릴 수 있으므로 이미지 합성 창을 따로 두기 보다는
    이미지 합성 하는 동안 다른 작업을 할 수 있도록 설계 ( 이미지 합성이 완료되면 알림창 )

  ------



# 10월 첫째주 노드 스터디

------

- 1장 노드 JS ?

  - 자바스크립트를 실행할 수 있는 Runtime 환경

  - 이벤트 기반

    1. 이벤트 리스너에 콜백 함수 등록
    2. 이벤트 발생
    3. 등록된 콜백 함수 호출

    

  - 논블로킹 & 싱글 스레드

    - ~= 비동기방식
    - e.g. 식당에서 한 명의 점원이 모든 주문을 받고 주문의 순서와 상과없이 음식이 나오면 바로 서빙

    

  - 노드의 장점과 단점

    | 장점                                            | 단점                                   |
    | ----------------------------------------------- | -------------------------------------- |
    | 멀티 스레드 방식에 비해 컴퓨터 자원을 적게 사용 | 싱글 스레드라서 cpu 코어를 하나만 사용 |
    | I/O 작업이 많은 서버로 적합                     | CPU 작업이 많은 서버로는 부적합        |
    | 멀티 스레드 방식보다 쉬움                       | 싱글 스레드가 멈추지 않도록 주의       |
    | 웹 서버가 내장되어 있음                         | 서버 규모가 커지면 관리하기 어려움     |
    | 자바스크립트 사용                               | 어중간한 성능                          |
    | JSON 형식과 호환하기 쉬움                       |                                        |

    

  - 서버 외 노드 기반 웹 프레임워크(프론트)

    - Angular, React, Vue

  ------

  

- 2장 ES2015+ 문법 

  - 템플릿 문자열

    - ```javascript
      const num1 = 1;
      const num2 = 2;
      const result = 3;
      const string = `${num1} 더하기 ${num2} 는 '${result}'`;
      console.log(string); //1 더하기 2는 '3'
      ```

    - ${변수} 형식을 기존 따옴표 대신 백틱 " ` "  안에 넣어서 사용. 백틱을 사용하기 때문에 작음 따옴표와 큰 따옴표를 백틱 안에 넣어서 사용 가능

    

  - 화살표 함수

    - 기존 함수 function() {} 형식

      - ```javascript
        function add1(x,y) {	
        	return x+y;
        }
        ```

      

      - ```javascript
        const add1 = (x,y) => {
        	return x+y;
        };
        
        const add2 = (x,y) => x+y;
        const add3 = (x,y) => (x+y);
        
        function not1(x) {
            return !x;
        }
        
        const not2 = x => !x;
        ```

        기존에는 함수명을 적고 함수명 옆에 괄호를 적고 파라미터를 입력해주었다면 

        화살표 방식은 함수명을 변수명 처럼 선언하고 파라미터를 입력해준다음 화살표를 

        이용해 함수식을 적어주는 방식		

        

  - 프로미스

    - 중첩되는 콜백함수 ( 코드의 깊이가 깊어짐 ) 을 간결하게 바꿀 수 있음

    - 모든 콜백 함수를 프로미스 방식으로 바꿀 수 있는 것은 아님. 프로미스 방식을 지원해야 함.

      - ```javascript
        const condition = true;
        const promise  = new Promise((resolve, reject) => {
            if (condition) {
                resolve('성공');
            } else {
                reject('실패');
            }
        });
        
        promise
        .then((message) => {
            console.log(message);
        })
        .catch((error) => {
            console.log(error);
        });
        ```

        promise 객체에서 conditon 이 true 이면 promise 에서 resolve 이벤트를 발생시키고 promise.then() 을 통해 '성공' 메세지를 올려준다. 

        반면 condition  이 false 이면 promise 에서 reject 이벤트를 발생시키고 promise.catch() 를 통해 '실패' 메세지를 올려준다.

        

      - ```javascript
        promise
        .then((message) => {
            return new Promise((resolve,reject) => {
                resolve(message);
            });
        })
        .then((message2) => {
            console.log(message2);
            return new Promise((resolve, reject) => {
                resolve(message2);
            });
        })
        .then((message3) => {
            console.log(message3);
        })
        .catch((error) => {
            console.log(error);
        });
        ```

        처음 promise then 에서 message 를 resolve 하고 그 다음 then 에서 message2를 resolve 하고  그 다음 then 에서 message3 를 받아 메세지를 올려줌.

        

      - ```javascript
        const promise1 = Promise.resolve('성공1');
        const promise2 = Promise.resolve('성공2');
        Promise.all([promise1, promise2]);
        .then((result) => {
            console.log(result); //['성공1', '성공2']
        })
        .catch((error) => {
            console.error(error);
        });
        ```

        Promise.all 을 활용하면 여러개의 프로미스를 한번에 실행 가능함.

  - async/await

    - 프로미스보다 코드를 더욱 깔끔하게 줄여줌

    - ```javascript
      function findAndSaveUser(Users) {
          User.findOne({})
          .then((user) => {
              user.name = 'zero';
              return user.save();
          })
          .then((user) => {
              return User.findOne({ gender:'m'});
          })
          .catch(err => {
              console.error(err);
          });
      }
      ```

      ```javascript
      async function findAndSaveUser(Users) {
          try {
         		let user = await Users.findOne({});
          	user.name = 'zero';
          	user = await user.save();
         	 	user = await Users.findOne({gender: 'm'});
          	//생략
          } catch(error) {
              console.error(error);
          }
      }
      ```

      프로미스 앞에 await 을 붙여주면 해당 프로미스가 resolve 될때까지 기다림

      

      ```javascript
      const findAndSaveUser = async(Users) => {
          try {
              let user = await Users.findOne({});
              user.name = 'zero';
              user = await user.save();
              user = await User.findOne({gender: 'm'});
              //생략
          } catch(error) {
              console.error(error);
          }
      };
      
      ```

      화살표 함수를 써서 작성할 수도 있음

      

- 3장 노드 모듈, 내장 객체, 모듈, 이벤트, 파일시스템 접근

# 깃헙 블로그

------

- 'Just-the-docs' 테마 이용
  - https://blog.chulgil.me/how-to-make-blog-using-github-2/ 프로젝트별 페이지 만드는 방법
  - 기존 깃북이랑 비슷한 테마

