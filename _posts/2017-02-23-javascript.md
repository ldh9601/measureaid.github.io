---
layout: post
title: Javascript 정리.
author: 이대한
author-email: ldh9601@measureaid.com
description: LDH - Javascript를 처음 접했을 때 정리한 부분입니다.
image: 

--- 
 
 이전까지 javascript라는 것의 존재유무만을 알았을 뿐 실제로 사용해 본 적이 없었습니다. 이전까지 c계열의 언어만을 사용하다가 처음 javascript를 접했을 때 
 느꼈던 어려움과 의문점들 위주로 작성하였습니다. 아직 완전히 해결되지 못한 의문점들과 잘못된 지식을 가지고 있는 것이 많습니다. 만약 그런 것들을 보신다면 가감없이
 알려주시면 서로 공부하고 나아가는데 도움이 될 것 같습니다.
 
### *1. javascript*

---

* 기본적으로 javascript는 *Object(객체)*로 이루어져 있습니다. 
  * 객체는 객체지향 프로그래밍에서 말하는 객체를 말합니다. 절차지향은 프로세스가 코드의 순세대로 진행되어 데이터를 가공하는데 비해 객체지향은 데이터에 Method(메서드)
  가 접근해 데이터를 가공하는 방식입니다. 때문에 순서와 관계없이 적절하게 선언된 Method를 필요할 때 불러와 데이터를 가공할 수 있게 됩니다. 이를 이용해 비동기 방식의
  실시간 데이터를 가공할 때에도 유용하게 사용할 수 있습니다.

  * javascript의 모든 객체는 *Object*를 상속 받습니다. 때문에 그렇게 만들어진 객체 역시 Object의 속성값을 가지고 있습니다.

* require : 기본적으로 C의 include와 유사합니다. 사용하면서 재미있었던 부분은 하나의 Directory에 여러 Module을 생성하고 이 Directory를 통째로 require
시키면 그 안의 모든 Module이 require되어 사용할 수 있다는 것 이었습니다. 즉, 필요한 Module을 하나의 Directory에 모아두고 필요한 경우 그 Directory만 require
시켜 사용할 수 있는 것 입니다.

   *(Module에 대한 설명은 차후에 하겠습니다.)
 
   **(물론 C계열에서도 하나의 파일에 필요한 header를 모두 include시켜 놓고 그 header만 다시 필요한 곳에서 include하여 사용할 수 있습니다. 단지 이것을 좀 더 간결하고 명확하게 구분하여 사용할 수 있다는 점이 인상적이었습니다.)


* for('key' in '{} || []') : 정말 많이 사용되는 반복문, for문 입니다. 일반적으로 C에서 사용하는 for문의 형식으로도 사용할 수 있지만, 앞의 형태와 같이 
for ... in의 형태로 사용했을 때 매우 편리하게 사용할 수 있는 구문입니다. Object나 Array에서 key값을 자동으로 연산하여 반복문을 동작시키는 형태입니다.
이 구문의 장점은 따로 index값을 설정하여 연산할 필요가 없으며, key값이 형태에 따라 어떠한 값 자체를 가질 수 있다는 것입니다. 예를 들어 Object의 모든 속성값에
대해 반복하고자 하였을 때 key값이 그 반복하는 Attribute, 즉 속성값 그 자체를 가지고 있을 수 있습니다.

##### __*코드 예시*__
~~~
  var testObject = {name : 'tester', value : 3}
  
  for(var key in testObject){
    console.log(key);
  }
  // name 과 value가 log로 찍힘
~~~

* scope : 변수의 범위라 할 수 있습니다. 지역과 전역, 함수와 함수 사이 등 변수가 존재할 수 있는 Context를 뜻 합니다.

* Hoisting : 호이스팅이라는 javascript의 특색(또는 문법적 오류라하는 경우도 있다고 합니다.)입니다. 매우 특이한 특성인데 이것 때문에 많은 프로그램 상에서 많은 
오류가 발생하기도 합니다.

  * 의미 : <함수의 선언과 함수 할당의 구분>이라고 정의할 수 있겠습니다. 변수를 선언할 시, 변수는 그 변수가 호출되는 시점이나 초기화 시에 정의되는 것이 아니라
  코드가 동작하는 최초에 무조건 그 scope의 최상위로 변경되어 정의됩니다. 즉, 함수를 선언하는 시점과 함수가 할당되는 시점이 같지 않다는 것 입니다.
    * 만약 절차상으로 아직 정의되지 않은 변수가 존재하더라도, 접근할 수 있는 Scope내에 존재한다면 선언된 함수나 변수를 먼저 읽어 올 수 있습니다.
    * 단, 그 변수에 값을 할당하는 것은 해당 변수가 호출되어야 합니다. (초기화 값은 호이스팅 되지 않습니다.) / 이 부분에서 선언과 할당이 구분된다는 것을 알 수 있습니다.
    글로 설명을 보았을 때 명확하게 이해되지 않는 부분이 있을 수 있습니다. 때문에 코드로 예시를 보겠습니다.
    
##### __*코드 예시*__
~~~
 var a = 0;
 
 for(var i = 0 ; i < 10 ; i++){
  a += i;
  }
  // a = 45가 됨

  console.log(i);
  // 정상적이라면 for문 내에서만 사용되야 하는 변수이지만 호이스팅의 특성때문에 scope 최상위에 위치하게 되어 호출이 된다. 때문에 10의 값이 출력된다.
  // 호이스팅의 가장 간단한 특성이다
  
~~~
