---
layout : post
author : yl.jung
title : "[jekyll 블로그] Google CSE 적용하기"
pamallink : /jekyll/blog/google/cse
tage : [연구노트, 인턴십]
comments : true
---

# Google CSE

Google CSE는 구글 맞춤검색 엔진의 약자이다. 실제 우리가 사용하고 있는 구글 검색 기능에서 사용자가 원하는 사이트만 검색하도록 지정할 수 있는 기능이다. 이를 우리 블로그에 적용하여 블로그 자료 검색기능을 적용하고자 한다. 설정 방법으로는 웹에서 제공하는 Control Panel과 XML파일을 만드는 두 가지 방법이 있다. 기본적으로 제공하는 설정을 통해 디자인, 부가적인 검색기능(자동 완성, 동의어 등)도 사용이 가능하다. 좀 더 확장된 부가기능은 통계와 로그가 있는데 Google 애널리틱스와 연동해서 사용이 가능하다. Google CSE를 사용하기 위해서는 적용할 사이트 URL과 구글 계정이 필요하다.

<br>

<br>

## Google CSE 만들기

![Screen Shot 2018-01-08 at 11.28.32 AM](http://res.cloudinary.com/degxeqfok/image/upload/v1515378810/hw5z2ltbtu366je0xwvq.png)

1. Google 계정으로 로그인 한 후 [Control Panel](https://cse.google.com/create/new)로 접속한다.
2. 검색할 사이트(Sites to search)에 검색 할 사이트 URL을 입력한다. [URL 패턴 페이지](https://support.google.com/customsearch/answer/71826)를 참고하여 URL을 등록한다.
3. 언어(language)는 검색 엔진에서 사용할 언어를 선택한다. 버튼이나 기타 디자인 요소들이 선택한 언어로 표시된다.
4. 검색 엔진 이름(name)은 Control Panel에서 사용자에게 보이는 검색엔진 이름을 입력한다.
5. 만들기(Ctrate) 버튼을 클릭하면 새 검색엔진이 만들어진다.

<br>

***Google CSE 사용**

![Screen Shot 2018-01-08 at 11.49.49 AM](http://res.cloudinary.com/degxeqfok/image/upload/v1515379960/nuspb13xfnhwfdklwz9d.png)

- URL을 이용하여 사용자와 공유
  - 생성한 검색 엔진의 Control Panel에서 **설정 -> 기본사항 -> 세부정보 -> 공개 URL** 
- 검색 기능을 사용 할 웹사이트에 검색박스를 import 

<br>

<br>

## 검색박스 import

1. Control Panel에서 import할 검색 엔진을 선택한다.
2. **설정 -> 기본사항 -> 코드 가져오기** 에서 코드를 복사한다.
3. 검색박스가 노출되었으면 하는 페이지에(HTML파일) 해당 코드를 붙여넣기 한다. 

<br>

***디자인에 따른 검색박스 코드**

Google CSE는 검색박스와 결과 페이지 디자인을 선택하여 사용할 수 있다. 제일 처음 검색엔진을 생성하면 기본적으로 오버레이 디자인으로 설정되어 있다.

- 오버레이 디자인

  검색박스에 검색어를 입력하면 modal창으로 결과를 보여주는 디자인

```javascript
<script>
  (function() {
    var cx = 'YOUR_ENGINE_ID';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>

<gcse:search></gcse:search>
```

<br>

- 두 페이지 디자인

  검색박스에 검색어를 입력하면 새 창으로 결과를 보여주는 디자인

  ```resultUrl=""```을 이용하여 결과값을 보여줄 URL을 설정 가능

```javascript
<script>
  (function() {
    var cx = 'YOUR_ENGINE_ID';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:searchbox-only resultsUrl="YOUR_RESULTS_PAGE_URL"></gcse:searchbox-only>
```

<br>

위의 두 디자인 외에도 전체 화면, 두 열, 간단히, Google에서 호스팅 등의 다양한 디자인이 존재한다. 사용자가 구축하는 블로그의 특성에 맞게 원하는 디자인을 적용하여 코드를 사용한다.

<br>

<br>

##검색박스 Customising

Google CSE에서 사용하는 검색박스와 결과 페이지에 대한 디자인은 Control Panel을 이용하여 수정이 가능하다. 하지만, 실제 블로그를 운영하다보면 HTML코드를 이용하여 검색박스를 디자인 하고 싶은 경우가 있다. 해당 경우에 '검색 결과만' 디자인을 이용하여 간단하게 구현이 가능하다.

<br>

생성한 검색엔진에서 디자인을 '검색결과 만'으로 설정하면 아래와 같은 부가적인 설정이 가능하다.

![Screen Shot 2018-01-08 at 2.33.55 PM](http://res.cloudinary.com/degxeqfok/image/upload/v1515389717/ojoluzmnhf8zsu25nxqp.png)

검색결과 코드 가져오기 페이지에서 검색결과 세부정보를 클릭하면 검색어 매개변수 이름을 설정 할 수 있다.

기본 값은 q이며 사용자가 원하는 값을 지정 가능하다.

<br>

웹 상에서 설정이 끝난 후 HTML파일을 수정한다. 

이 때 사용자는 

1. 검색박스를 위치 시킬 HTML파일
2. 결과를 출력 할 HTML파일  두 개의 파일에 대해서 코드를 작성 해야 한다.

<br>

***검색박스**

검색박스에 대한 모든 코드는 자유롭다. 하지만  ```action="결과 페이지 URL"```과 ```name="검색어 매개변수 이름"```은 정확하게 입력하여야 한다. ```action```은 결과를 보여줄 페이지의 URL이며 ```name```은 웹 상에서 설정해주었던 검색어 매개변수의 이름을 반드시 입력하여야 한다.  

```html
<form id="searchForm" action="결과 페이지 URL">
	<input id="searchtext" name="검색어 매개변수 이름" type="text" placeholser="Search...">
	<button>search</button>
</form>	
```

<br>

***결과**

결과는 위의 검색박스에서 설정해준 ```action```으로 이동 한 페이지에서 나올 검색결과이다. 

웹에서 가져온 코드는 디자인 설정이 '검색결과 만'이므로 검색박스에서 매개변수로 전달한 검색어의 검색결과를 출력한다.

결과가 나와야 할 페이지에 아래의 코드를 붙여넣기 해준다.

```javascript
<script>
  (function() {
    var cx = 'YOUR_ENGINE_ID';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:searchresults-only></gcse:searchresults-only>
```

<br>

<br>

## Google CSE를 적용한 Blog 예시

![Screen Shot 2018-01-08 at 3.01.39 PM](http://res.cloudinary.com/degxeqfok/image/upload/v1515391380/jnydq8v39zqc7zujyskn.png)

오른쪽 상단에 검색박스 Customising을 이용하여 검색박스를 적용하였다.

<br>

![Screen Shot 2018-01-08 at 3.04.31 PM](http://res.cloudinary.com/degxeqfok/image/upload/v1515391568/dtv0qvfni0wmcf5mspbv.png)

검색결과가 위와 같이 출력된다.

<br>

<br>

# 참고자료

1. https://developers.google.com/custom-search/, google developers, accessed 2017-01-08
2. http://digitaldrummerj.me/blogging-on-github-part-7-adding-a-custom-google-search/, 개인블로그, accessed 2017-01-08

