---
layout: post
title:  "[Jekyll Blog] Tipue Search를 이용하여 블로그 검색 기능 만들기"
subtitle:   "Tipue Search 플러그인"
categories: etc
tags: etc
comments: true
---


## 개요
> `Tipue Search`를 활용하여, 블로그 검색 기능을 구축한 과정에 대한 기록입니다.  
  
- 목차
	- [Tipue Search란?](#tipue-search란) 
	- [Tipue Search 설치](#tipue-search-설치)
	- [Tipue Search 환경설정](#tipue-search-환경설정)
	- [최적화 적용을 위한 디테일 마무리](#최적화-적용을-위한-디테일-마무리)
  
  
## Tipue Search란?
---
블로그를 운영하다보니 검색 기능이 필요해졌다. 시간이 지날수록 포스트 개수가 늘어나게 되는 것은 당연한 일이기 때문이다. 기술 블로그는 다른 이들과 기술을 공유하는 목적도 있지만 개인적으로 효율적인 기억 관리를 위해 활용하기도 하는데, 정작 본인이 필요한 포스트의 위치가 기억나지 않아 한참 해맨다면 블로그 운영이 무슨 의미가 있을까? 그래서 검색기능을 만들어보기로 결심하였다!
  
* __검색 기능을 뭘로 만들지?__  
우리나라 개발 환경의 고질적인 병폐일까? 검색 기능을 구현하기 위해 가장 먼저 떠오른 것이 슬프게도 DB였다. Oracle, Mysql, Pgsql,... 어떤것을 운영할까? 클라우드를 이용해야 하나?

* __아! 맞다. 이 블로그는 Jekyll로 만들었지!__  
당연히 데이터가 DB에 있어야 DB 검색을 활용할 수 있다. 정적 컴파일러 Jekyll로 제작된 블로그에 DB는 당연 고려대상이 아니다. 그렇다면 Front-End 기술을 이용해야 한다는 의미니깐.. JavaScript를 이용해서 만들어야 하나? 고민하던 중 sitemap.xml, feed.xml이 생각났다. XML 기반의 Data가 구조적으로 모여있으니 XML 파싱을 이용하여 검색 기능을 구현해야겠다 마음먹던 중 귀차니즘이 밀려왔다. ~~난 Front-End 기술을 공유하기 위해 블로그를 만든것이 아닌데.. 데이터 사이언스 기술 공유가 목적인데..~~ 이걸 굳이 만들어야 하나?^^;   

* __Jekyll도 있는데 Front-End 검색 기능이 없겠어?__  
위대한 구글신께 물어보니 역시나 훌륭한 site search plugin을 발견하게 되었다. 그 이름하여 [`Tipue Search`](http://www.tipue.com/search/)! 메인 페이지를 들어가보니 대문에 `제이쿼리를 활용하여 만들었고 무료이며 빠르다`라고 자랑하고 있다. (실제로 자랑 할 만 하다.) 쓸만한지 테스트가 필요하시면 본 블로그 좌측메뉴 About 밑에 붙어있는 검색창을 사용해보시기 바란다.   
  

## Tipue Search 설치(Window PC 버전)
---
필자의 블로그에 구현된 기능이 맘에 드셨다면 바로 설치를 시작해보자.  

1. Github Repository 접속 : [`https://github.com/jekylltools/jekyll-tipue-search`](https://github.com/jekylltools/jekyll-tipue-search)  
![그림1](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-1.jpg)  
2. `Clone or download` 를 클릭하여, `jekyll-tipue-search-master.zip` 파일을 다운받아 압축을 푼다.    
3. 압축을 풀면 나오는 `search.html`파일을 본인의 깃헙 블로그 최상위 디렉토리(예: C:\githubPages\theorydb.github.io)에 복사한다.
![그림2](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-2.jpg)    
![그림3](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-3.jpg)    
4. `압축을 푼 폴더/assets/`안에 있는 `tipuesearch` 폴더를 본인의 깃헙 블로그 `최상위 디렉토리/assets/`(예: C:\githubPages\theorydb.github.io\assets\tipuesearch)아래에 복사한다.
![그림4](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-4.jpg)    

이것으로 설치는 끝났다. 참 쉽죠~?  
이제 환경설정을 통해 블로그에 적용해 보자.
   

## Tipue Search 환경설정  
---
Jekyll 테마에 따라 설정이 약간 다를 수 있다. 본 블로그의 테마는 `Clean Blog`로, 동일한 테마를 사용하시는 경우 그대로 적용하면 된다. (운영중인 테마가 달라 적용에 어려움이 있는 경우 맨 하단의 Disqus에 댓글을 남겨주시면 아는 범위내에서 최대한 설명해 드리겠습니다.)   

1. `본인의 깃헙 블로그 최상위 디렉토리/_config.yml` (예:C:\githubPages\theorydb.github.io\_config.yml) 파일을 열어 맨 아래에 다음의 코드를 추가한다.
	```yml
	tipue_search:
		include:
			pages: false
			collections: []
		exclude:
			files: [search.html, index.html, tags.html]
			categories: []
			tags: []
	```
![그림5](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-5.jpg)     
>* include 부분의 `pages: false`의 설정은 pages 레이아웃에 해당하는 일반 html페이지는 검색하지 않겠다는 것을 의미한다.(포스트 내용 검색에 집중하기 위함) 
>* exclude 부분의 `search.html, index.html, tags.html` 페이지는 검색에서 제외하겠다는 것을 의미한다.  

1. `본인의 깃헙 블로그 최상위 디렉토리/_includes/head.html` (예: C:\githubPages\theorydb.github.io\_includes\head.html) 파일을 열어 `META`영역 제일하단, `LINKS`영역 바로 위의 위치에 다음의 코드를 추가한다.  
	```javascript
	<!-- tipuesearch -->
	<link rel="stylesheet" href="/assets/tipuesearch/css/tipuesearch.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
	<script src="/assets/tipuesearch/tipuesearch_content.js"></script>
	<script src="/assets/tipuesearch/tipuesearch_set.js"></script>
	<script src="/assets/tipuesearch/tipuesearch.min.js"></script>
	```
![그림6](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-6.jpg)  
  
1. `본인의 깃헙 블로그 최상위 디렉토리/search.html` (예: C:\githubPages\theorydb.github.io\search.html) 파일을 열어 아래 그림과 같이 설정한다.  
![그림7](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-7.jpg)  
> * `layout : page` 부분은 포스팅이 담기는 레이아웃 명칭이다.(테마에 따라 다를 수 있음) 
> * `permalink: /search/` 부분은 다음 단계에서 설정할 검색어 및 버튼 Element의 form 태그 내 action 속성과 일치시켜야 한다.
> * `'wholeWords' : false` 속성은 한글 검색을 가능하게 하는 옵션이다.
> * `'showTime' : false` 속성은 검색이 완료되기 까지 소요된 시간을 표시하는 옵션이다.
> * `'minimumLength' : 1` 속성은 최소 검색 글자수에 대한 설정으로 필자는 한단어 이상이면 검색가능하게 설정하였다.  
> * 그 외의 옵션은 Tipue 메인홈페이지 [`Tipue Search`](http://www.tipue.com/search/)에 접속하여 `Options in the .tipuesearch() method`에서 상세하게 확인할 수 있다. 
  
1. 마지막으로 `본인의 깃헙 블로그 최상위 디렉토리/_includes/sidebar.html` (예: C:\githubPages\theorydb.github.io\_includes\sidebar.html) 파일을 열어 아래 그림과 같이 설정한다.  
> [주의사항]
> `sidebar.html` 페이지를 수정하는 이유는 필자가 검색창을 붙이길 원하는 위치의 페이지가 sidebar.html이기 때문입니다. 
> 본인의 블로그에 검색창을 붙일 위치를 정한 후 해당 파일 및 파일 내 위치를 정한 후 해당 부분을 수정해야합니다.  

	```html
    <form action="/search">
      <div class="tipue_search_left">
        <img src="{{ "/assets/tipuesearch/search.png" | relative_url }}" class="tipue_search_icon">
      </div>
      <div class="tipue_search_right">
        <input type="text" name="q" id="tipue_search_input" pattern=".{1,}" title="At least 1 characters" required></div>
      <div style="clear: both;"></div>
    </form>
	```  
![그림8](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-8.jpg)  
> * `action="/search"` 설정은 위의 search.html 파일의 permalink 속성과 일치시킨것이다.
> * `pattern=".{1,}"` 속성은 검색어가 1글자 이상이면 검색을 허용한다는 의미로 활용하는 정규표현식 설정이다. 
> * `title="At least 1 characters"` 설정은 위의 pattern을 지키지 않은 채 검색을 시도할 경우 나타나는 알림메시지 문구이다.
  
1. 설치가 마무리 되었으므로 아래 그림과 같이 검색이 잘 동작하는지 확인한다.
![그림9](https://theorydb.github.io/assets/img/envops/2019-07-03-envops-site-search-9.jpg)   
   
## 최적화 적용을 위한 디테일 마무리  
---
Tipue Search의 디폴트 기능만 설치된 상태이므로 필자는 블로그에 보다 친화적으로 어울릴 수 있도록 기능을 수정해보았다. 이번 단계는 귀차니즘 가동 시 건너뛰셔도 무방하다. 

1. `검색 입력창` 사이즈 조정을 위해 `C:\githubPages\theorydb.github.io\assets\tipuesearch\css\tipuesearch.css`의 CSS 속성을 변경하였다.  
	```css
	#tipue_search_input
	{
	     color: #333;
	     max-width: 150px;
	     max-height: 20px;
		padding: 17px;
		border: 2px solid #626591;
		border-radius: 0;
		-moz-appearance: none;
		-webkit-appearance: none;
	     box-shadow: none; 
		outline: 0;
		margin: 0;
	}
	```

1. `검색버튼(돋보기모양)`이 좌측 메뉴의 배경색에 가려져 잘 보이지 않아 색상을 조절하였고, 본 테마의 img 태그 CSS 속성이 검색창 모양을 삐뚫어져 보이게 만들어 해당 태그의 CSS속성을 상속받아 사이즈를 수정하였다. 마찬가지로 `C:\githubPages\theorydb.github.io\assets\tipuesearch\css\tipuesearch.css` 파일에서 아래와 같이 CSS 속성을 변경하였다.  
	```css
	.tipue_search_icon
	{
	     width: 19px;
	     height: 19px;
	     margin-bottom: 0rem;
	     background-color: #626591;
	}
	.tipue_search_left
	{
	     float: left;
	     padding: 10px 5px 0 0;
	     color: #e3e3e3;
	     max-height: 20px;
	}
	```

이로써 Tipue Search 오픈소스를 활용하여 블로그에 멋진 검색 기능을 구축하였다. 다음 기능으로는 Jekyll 기반 블로그의 `Disqus` 댓글 기능 추가에 대하여 포스팅 할 예정임을 미리알려드린다.  


> Jekyll 기반의 깃헙 페이지 블로그 구축 포스팅은 계속될 예정입니다. 처음 구축하는 방법부터 올리려고 했는데 시간 부족으로 계속 미루고 있네요^^; 포스팅 순서가 어긋나더라도 차후 개인적으로 구현하려는 목표가 모두 완성되는대로 `구축을 위한 설계도` 개념의 포스팅에서 통합 정리 및 링크부여를 통해 가급적 편하게 보시며 구축하실 수 있도록 노력하겠습니다. 읽어주셔서 감사합니다. 






## Jekyll Themes 고르기   
---
이전글 [(개요) 블로그를 만들어 봅시다!](https://theorydb.github.io/envops/2019/05/01/envops-blog-intro/)에서 Jekyll 블로그를 선택한 이유를 말씀드렸다. 여기까지 읽고 계시다면 이미 Jekyll 블로그를 구축하는데 관심이 있는 독자일 것이다. 그렇다면 Jekyll 테마에는 어떤 것들이 있으며 선정하는 기준에 대해서 언급해 보겠다.

* __Jekyll Themes 제공 사이트__  
  대부분의 오픈소스 개발자들이 그러하듯 지킬 역시 많은 양의 테마를 오픈 소스로 제공하고 있다. 아래 사이트에 접속하시면 무료로 제공되는 테마를 원없이 구경하고 선택하실 수 있다. 오히려 많아서 선택하기 어려울 지경이다. 
  + <http://jekyllthemes.org/>  
  + <https://jekyllthemes.io/free>
  + <http://themes.jekyllrc.org/>
  + <https://github.com/topics/jekyll-theme>
![그림1](https://theorydb.github.io/assets/img/envops/2019-05-02-envops-blog-theme-1.jpg)
  
* __Jekyll Themes의 선정기준__  
  아래 기준에서 반드시 포함시킬 요소를 미리 염두에 둔다면 위 사이트에서 테마를 고르기 더 쉬워질 것이다.
  + 모바일에서도 보기 편한 `반응형`인가?
  + `한글 폰트` 가독성이 좋은가?
  + `커스터마이징`하기 쉬운 구조인가?
  + 레이아웃, 줄간격 등 `디자인` 요소가 마음에 드는가?
  + 검색, 태그, 댓글, syntax highlighting, Summary, Google Analytics, 수식입력 등 `기능` 지원 여부
  

## `Clean Blog` 테마를 선택한 이유  
---
필자가 선정한 테마는 [`Clean Blog`](https://blackrockdigital.github.io/startbootstrap-clean-blog/)이다. 이유는 다음과 같다.

* 깔끔한 디자인으로 `Simple is best` 철학이 돋보임
* 반응형 지원으로 모바일 가독성에도 손색이 없음
* 한글 폰트가 다른테마 대비 마음에 듬
* 커스터마이징이 편리함
  
혹시 필자가 선정한 블로그가 크게 마음에 들지 않으신다면 아래 후보군을 참고하시기 바란다. 필자도 아래 후보군들이 꽤 마음에 들어서 많은 고민을 했다. 필자에게는 낙점되지 못 했지만 독자분들께는 더 마음에 드실지도 모른다. 

* __후보군__ 
  + Clean Blog : <https://blackrockdigital.github.io/startbootstrap-clean-blog/>  
  + folio : <http://bogoli.github.io/-folio/>
  + Hydejack : <https://hydejack.com/blog/>
  + EXAMPLE POST : <http://the-development.github.io/flex/>
  + Read Only : <https://html5up.net/read-only>
  + Mediator : <https://blog.base68.com/>
  + Skinny Bones : <https://mmistakes.github.io/skinny-bones-jekyll/>
  + lanyon : <https://github.com/poole/lanyon>

맘에드는 테마를 선택하셨다면 다음글[GitHub 연동 및 Jekyll 설치](https://theorydb.github.io/envops/2019/05/03/envops-blog-github-pages-jekyll/)에서 GitHub 연동 및 Jekyll 설치를 통해 웹서버에서 실행하는 방법을 배워보겠다. 

## GitHub 회원가입 및 Fork
이전글 [블로그 테마(Themes) 고르기 및 환경설정](https://theorydb.github.io/envops/2019/05/02/envops-blog-theme/)에서 멋진 Jekyll 테마를 골랐다는 가정하에 GitHub으로 연동하는 과정을 설명하겠다.

* GitHub 회원가입
  먼저 GitHub <https://github.com/>에 접속 후 아래 그림과 같이 `Sign Up` 버튼을 클릭하여 회원가입을 진행한다.  
  ![그림1](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-1.jpg)
  Username, E-mail, Password 등 간단한 정보를 입력하면 계정이 생성된다.
  
> __사전체크__  
  다음으로 선택한 테마의 소스를 보관할 저장소를 GitHub에 만들어야 한다. 만드는 방법은 크게 2가지가 있다. 하나는 Fork 버튼을 클릭하는 방법이고, 다른 하나는 로그인 후 [Start a Project] 버튼을 클릭하여 직접 Repository를 생성하는 방법이 있다.   
  후자의 경우 _config.yml을 복사한 후 여러 단계를 거쳐야하므로 초보자에게는 복잡하고 어렵다. 따라서 여기서는 전자의 방법을 택한다. 더불어 각자 선택한 테마가 상이할 것이므로 공통으로 필자의 블로그를 Fork하는 방법으로 실습하겠다.  
  만약 초보자라면 필자가 운영중인 테마를 실습삼아 Fork 후 전 과정을 구축하며 미리 시뮬레이션 학습한 후에 선정한 테마를 동일한 방식으로 진행하시며 설치하시는 것을 권장한다.(이런 과정없이 처음부터 한번에 구축하기는 결코 쉽지않다.)
 
* Fork(Clone)을 통한 저장소(Repository) 생성
  필자의 테마 저장소<https://github.com/theorydb/theorydb.github.io>에 접속 후, 아래 그림과 같이 우측 상단의 `Fork` 버튼을 클릭한다.(또는 Clone을 통해 PC에 다운로드 후 Git 설치를 통해 Commit, Push로 올리는 방법도 있는데 여기서는 생략한다. 추후 별도의 포스팅을 통해 Git을 설치하고 사용하는 방법에 대해 설명하겠다. 현 시점에서 소개하기엔 분량이 과하여 집중력을 잃고 자칫 포스팅 전체의 큰 흐름을 잃을까 우려되기 때문이다.) 
  ![그림2](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-2.jpg)
  잠시 기다리면 여러분의 계정에 저장소가 생성되어 필자 블로그의 모든 파일들이 저장소 내에 Copy된 것을 확인할 수 있다.
> __(참고)Reporitory 직접 생성하는 방법__  
> https://github.com/theorydb > repository > new > repository name에 username.github.io 입력 > create repository 버튼을 클릭하면 생성된다.

* Repository name 변경 및 기타설정
  Fork가 완료된 저장소에서 아래 그림과 같이 `Settings`를 클릭하면 최상단에 `Repository name`이 나온다.
  ![그림3](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-3.jpg) 
  가급적 회원가입 시 사용했던 `username`을 이용하여 `username.github.io` 형식으로 저장할 것을 추천한다. 다른 명칭으로 저장할 경우 서브디텍토리가 포함된 보다 복잡한 URL로 접속해야하는 번거로움이 따른다.  

  그 외 동일페이지 하단으로 스크롤하여 내려가면서 Issues 체크, 브랜치는 Master로 설정할것을 권장한다.

* (Tip-생략가능) Fork한 저장소를 초기화(삭제)하고 싶은 경우 
  처음 저장소를 만든다면 실수 및 마음에 드는 형태로 전부 삭제 후 다시 만들고 싶은 경우가 종종 발생한다. 이럴땐 위 3번 과정과 동일한 페이지 맨 밑에 그림과 같은 `Danger Zone`이라는 빨간색으로 둘러쌓인 영역으로 이동한다. `Delete this repository`를 클릭 후 패스워드를 한번 더 입력하게 되면 지금까지 만든 저장소가 전부 삭제된다.
  ![그림4](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-4.jpg)  

* (Tip-생략가능) username이 마음에 안드는 경우
  위 3번 과정에서 URL이 마음에 들지 않아 username을 바꾸고 싶은 경우가 있다. 아래 그림과 같이 `우측상단 프로필 아이콘 클릭 > Settings > Account > Change username 버튼`을 클릭하면 변경 가능하다.
  ![그림5](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-5.jpg)

* 최초의 블로그를 웹브라우저로 접속
  Fork를 통해 아주쉽게 블로그를 완성하였다. 크롬, IE 등 웹브라우저 열어 위에서 설정한 본인의 URL주소 `username.github.io`에 접속하여 페이지가 잘 뜨는지 확인해보자.   

## Git 설치 및 Clone 
---
위 과정을 통해 비록 알맹이는 남의 블로그지만 껍데기만큼은 내 URL로 접속가능한 반쪽자리 블로그가 완성되었다. 당연히 누구도 이 상태로 블로그를 운영하고 싶진 않을 것이다. 다운받아 수정 후 업로드 하는 과정이 필요한데, 이를 위해서 먼저 PC에 Git을 설치해야 한다.

* Git설치
  Git 다운로드 링크 <https://git-scm.com/>에 접속하여 Download 메뉴를 클릭한다. 아래 그림과 같이 본인의 운영체제(OS)와 일치하는 아이콘을 클릭한 후, OS버전에 맞는 Git 설치파일을 다운로드 받아 설치한다.(필자의 경우는 Windows이다.) 
  ![그림6](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-6.jpg)
  설치과정은 별 어려움 없이 디폴트 환경 그대로 `Next` 버튼을 클릭하여 진행해준다.
  
* 위에서 Fork 한 저장소를 PC 내 다운로드 할 폴더를 만든다. 탐색기로 해당 폴더에 들어가 우클릭하면 `Git Bash Here`라는 추가된 메뉴가 보일것이다. 클릭하여 Git Bash창을 실행시킨다.

* Git 사용자 등록을 진행한다.  
```git
	git config --global user.name "사용자"
	git config --global user.email "사용자 이메일"
```  

* 저장소 PC에 Clone 
  위 과정에서 생성한 본인의 블로그 저장소에 접속하여 아래 그림과 같이 `Clone` 명령어를 복사한다.
  ![그림7](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-7.jpg)
  위에서 실행한 Git Bash 실행창에서 아래 그림과 같이 `git clone + [복사한 Clone 명령어]` 형태로 다음과 같이 붙여넣기한다.(우클릭만 하면 붙여넣기 효과)
```git
$ git clone https://github.com/theorydb/theorydb.github.io.git
```
  ![그림8](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-8.jpg)  
  엔터키를 입력하면 위에서 만든 PC내 폴더에 파일이 복사될 것이다. 
  이제 복사한 파일들을 여러분의 환경에 맞게 수정하는 작업을 진행하겠다.  
   
## Ruby & Jekyll 설치
---
파일을 수정하기 전에 먼저 Jekyll을 설치해보자. 우리가 Fork한 테마는 Jekyll 기반으로 개발이 되어있기 때문에 Jekyll을 설치하지 않을 경우 우리가 원하는 방식으로 테마를 수정할 수가 없다. 이전글에서 설명했던 것을 복습하자면 Jekyll은 정적 컴파일러이다. Text로 우리가 작성한 Markdown, _config.yml 등의 파일들은 Jekyll을 통해서 _site폴더내의 산출물로 변환되고 해당 산출물이 WEB에서 실행되는 형태라고 할 수 있다.

* Ruby 설치   
  Ruby는 또 왜 설치해야 하냐고? Jekyll이 Ruby로 만들어져서 그렇다. Ruby를 몰라도 걱정하실 것 없다. 필자도 Ruby를 쓴 경험이 전무하지만 설치과정이 매우 간단하여 어려움 없이 설치 완료하였다. 
  윈도우 OS의 경우 `Ruby와 개발툴킷`을 별도로 설치해줘야 하므로 루비 인스톨러 공식페이지 <https://rubyinstaller.org/downloads/>에 접속하자. 아래 그림과 같이 `=>`로 표시된 Ruby+Devkit 2.5.5-1 (x64)을 클릭하여 다운로드 한 후 Next만 누르며 디폴트로 설치하면 된다.
  ![그림9](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-9.jpg)  

* 아래 그림과 같이 윈도우 검색창에서 `Start Command Prompt with Ruby`를 실행한다.
  ![그림10](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-10.jpg)

* 아래 그림과 같이 프롬프트 상에서 `chcp 65001`를 실행한다. 인코딩을 부여하기 위한 명령어인데 실행하지 않을 경우 이후 진행하게 될 온갖 명령어에서 오류가 발생하므로 꼭 진행하여야 한다.
```ruby
> chcp 65001
```
  ![그림11](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-11.jpg)

* PC내 저장소를 Clone했던 위치로 이동한다. (아래 명령어는 필자의 예시로, 여러분이 지정한 경로로 이동하여야 한다.)
```ruby
C:\>cd "C:\githubPages\theorydb.github.io"
```

* 이제 Ruby에서 지원하는 gem 명령어를 통해 Jekyll은 물론 종속된 필요한 라이브러리를 설치하자. 아래 코드와 그림을 참고하면 된다. 참고로, gem이란 루비에서 제공하는 라이브러를 편리하게 설치할 수 있도록 지원되는 도구다.
```ruby
C:\githubPages\theorydb.github.io>gem install bundler jekyll minima jekyll-feed tzinfo-data rdiscount
```
  ![그림12](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-12.jpg)

* 초기화 설정
  Clone을 끝낸 Repository에 아래 코드와 같이 초기화 설정을 진행한다.
```ruby
C:\githubPages\theorydb.github.io>jekyll new theorydb.github.io
```

* 설치 및 초기화가 완료되면 아래 코드와 그림과 같이 지킬 서버를 구동해보자.
```ruby
C:\githubPages\theorydb.github.io>bundle exec jekyll serve
```
  ![그림13](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-13.jpg)

* 이제 로컬에서 웹브라우저를 실행하여 `http://127.0.0.1:4000/`주소로 접속해보자. Apache 등을 설치하지 않았지만 블로그가 로컬에서 아래 그림과 같이 잘 실행되고 있음을 확인할 수 있다.  
  ![그림14](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-14.jpg)

* 설치는 1회에 걸쳐 끝나기 때문에 앞으로는 위의 복잡한 과정을 전부 숙지할 필요는 없다. 평소 포스팅 작성 시 루비에 접속하여 지킬을 실행하는 정도의 명령어만 알면 되기 때문에 편의상 요약 명령어를 알려드리니 숙지하시기 바란다.
  > `시작` -> start command prompt with ruby -> C:\githubPages\theorydb.github.io -> jekyll serve

* 마무리  
  사실 단순하고 쉬운 과정이었지만 세상 만사가 어디 그렇게 쉬운가.. 분명 위 과정을 따라하시다가 오류가 나신 분도 계실 것이기에 `트러블 슈팅`에 관한 포스팅을 따로 정리할 예정이다. 그때까지는 번거로우시더라도 하단에 댓글을 남겨주시면 대답해 드릴 예정이다. 



## Jekyll 디렉토리 구조  
---
자. 드디어 수정을 위한 모든 과정이 갖추어졌다. 그렇지만 저장소 내 수많은 파일 중 어떤 파일을 어떻게 고쳐야 하는걸까? 필자 역시 처음 Jekyll 블로그를 Clone 후 어떤걸 고쳐야 하는지 막막했던 기억이 있다.  
 
하지만 다행인 것은 많은 폴더와 파일들 중 반드시 고쳐야 하는 것들은 사실 많지 않다는 것이다. 이에 도움이 될 수 있도록 디렉토리 구조를 한 눈에 파악할 수 있도록 하단에 디렉토리 구조에 대한 설명을 추가한다. 
  
특히, `반드시 변경해야 하는 사항을 1번에 명시`하였으니 도움이 되었으면 좋겠다. 참고로 2번 사항은 주로 디자인, 기능을 커스터마이징하는 경우 참조하게 되고 3번 사항은 거의 건드릴 일이 없는 파일들인데 지금은 건너 뛰셨다가 나중에 필요할 때 다시 돌아와 참고하시면 도움이 될 것이다.  

+ __1. 반드시 변경__
  * _featured_tags/             : 카테고리 대분류 폴더
  * _featured_categories/       : 카테고리 소분류(태그) 폴더
  * _data/                      : 개발자 및 운영자, 기타 정보 폴더 (author.yml 수정이 필요)
  * _config.yml                 : 가장 중요한 환경변수 설정 파일
  * README.md                   : GitHub 프로젝트 애서 소개하게 될 글
  * favicon.ico                 : 블로그 접속 시 브라우저 주소창에 표시되는 대표 아이콘
  * about.md                    : About 메뉴 클릭 시 나타나는 블로그에 대한 소개글
  
+ __2. 필요시 변경__  
  * assets/                     : 이미지, CSS 등을 저장 폴더
  * _layouts/                   : 포스트를 감싸기 위한 레이아웃 정의 폴더(페이지, 구성요소 등 UI변경 시 수정)
  * _includes/                  : 재사용을 위한 기본 페이지 폴더
  * Gemfile.lock                : Gemfile에 기록한 레일 기반 라이브러리를 설치 후 기록하는 파일(중복설치 방지)
  * Gemfile                     : 필요한 레일 기반 라이브러리를 자동으로 설치하고 싶을 때 명시하는 설정 파일
  * .gitignore                  : GitHub에 올리고 싶지 않은 파일들은 이 파일에 경로지정 가능(예: _site 산출물, 환경설정, 개인정보, 작성중인 글 등)
  * sitemap.xml                 : 테마의 사이트맵
  * search.html                 : Tipue Search 설치 시, 검색결과를 출력하는 페이지로 활용
  * robots.xml                  : 구글 웹로봇 등 검색엔진 수집 등에 대한 정책을 명시하는 설정파일
  * posts.md                    : 포스트 작성 관련 설정파일
  
+ __3. 변경 필요없음(참고)__  
  * _posts/                     : 포스트를 저장하는 폴더
  * .git/                       : GitHub 연동을 위한 상태정보가 담긴 폴더
  * _site/                      : Jekyll 빌드 생성 결과물 폴더(실제 GitPages에서 WEB으로 보여지는 산출물)
  * .sass-cache/                : 레일 엔진에서 사용하는 캐시 저장폴더(변하지 않는 산출물들에 대한 파싱을 하지 않아 속도보장)
  * _sass/                      : 일종의 CSS 조각파일 저장 폴더
  * _js/                        : JavaScript 저장 폴더 
  * _plugins/                   : 플로그인 저장 폴더(크롬 정책상 어차피 사용안함)
  * LICENSE.md                  : 테마 개발자의 라이센스 설명
  * index.html                  : 블로그 최초 접속 페이지
  * googlea0d1f22cc8208170.html : 구글 검색엔진에 블로그를 등록하는 과정의 소유권 확인 파일
  * feed.xml                    : RSS Feed 활용을 위한 XML
  * browserconfig.xml           : 윈도우8 이상 IE11 접속 시 클라이언트가 요청하는 환경설정 파일(윈도우의 표준 파괴 본능은 여기에도 숨어있다. ㅡ,.ㅡ)
  * 404.md                      : 404 Not Found Page(블로그에 없는 페이지 요청 시 등장하는 페이지)
  * .eslintrc                   : EcmaScript Lint(자바스크립트 협업 개발을 위한 규칙 정의) 환경설정 파일
  * .eslintignore               : EcmaScript Lint 무시할 규칙 지정(전역변수 에러표시 예외처리 등)
  * .babelrc                    : Babel(자바스크립트 컴파일러) 설정파일
  
보다 자세한 사항은 [지킬 한글화 공식 홈페이지](http://jekyllrb-ko.github.io/docs/structure/)를 참고하시기 바란다.

## 파일 수정하기 
---
드디어 파일을 수정해보자. 이제 저장소 내 대충 어떤 파일과 폴더가 있는지도 알았겠다 자신있게 `_config.yml`파일부터 수정해보자. 위에서 명시한바와 같이 가장 중요한 환경설정 파일으로 여러분의 개인화 정보와 관련된 거의 모든 환경변수가 존재한다. 반드시 수정해야 할 파일이다. 저장소 폴더 루트위치에 있는 _config.yml 파일을 아무 편집기로나 열어보면 주석에 자세한 사항이 명시가 되어있다. 주석의 지시대로 여러분의 환경에 맞게 수정하시기 바란다. 
> 참고로 필자의 경로는 `C:\githubPages\theorydb.github.io\_config.yml`이다.
  
더불어, 파일이 제대로 수정되었는지 파악하기 위해선 위에서 말씀드린 로컬사이트에 접속하면 바로 확인이 가능하다. 단, 지금 수정중인 _config.yml 파일의 경우 Jekyll을 껐다 켜줘야 반영된다. Jekyll 로컬 웹서버는 `[CTRL]+C` 단축키를 누르고 Y를 누르면 자동으로 꺼지고 `bundle exec jekyll serve` 명령어를 실행하면 다시 구동되니 참고하시기 바란다. 

  
## GitHub에 올리기
---
드디어 내가 수정한 파일을 GitHub 저장소에 올려보자. 여기까지 따라오시느라 정말 고생 많으셨다. 마지막 관문이니 만큼 조금만 더 힘을 내서 수정된 블로그를 웹에서 감상하시기 바란다.

* Git Bash를 실행한 후, 아래 코드와 같이 수정한 파일을 포함한 모든 파일을 `로컬 저장소에 업로드` 한다.
  ```git
  $ git add --all
  ```
  ![그림15](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-15.jpg)

* 수정된 파일들을 `로컬저장소에 커밋`한다. 
  ```git
  $ git commit -m "updates"
  ```
  ![그림16](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-16.jpg)

* 로컬저장소에 커밋된 파일을 `원격저장소`에 업로드한다. 업로드 도중 본인의 GitHub 아이디와 비밀번호 인증을 통과해야 업로드가   
  성공적으로 완료된다.
  ```git
  $ git push -u origin master
  ```
  ![그림17](https://theorydb.github.io/assets/img/envops/2019-05-03-envops-blog-github-pages-jekyll-17.jpg)

* 여러분의 블로그 URL(`https://[username].github.io`)에 접속하면 몇 초 뒤 수정된 사항이 반영된 것을 확인할 수 있다.

## 블로그 운영하기
--- 
위에서 열거한 방법은 최초 구축을 위한 방법으로 블로그 포스팅을 작성하고 운영하며 매일 다루게 되는 방법과는 다르다. 이에 운영하며 필요로 하게 되는 방법들은 간략하게 모아 별도의 포스팅으로 작성하였다. 관심있는 분들은 [[Jekyll Blog] (운영에 필요한) GitHub & Jekyll 사용법](https://theorydb.github.io/envops/2019/05/21/envops-blog-how-to-use-git/)을 참고하시기 바란다.


이로써 여러분의 블로그가 완성되었음을 축하드린다. 다만 Jekyll과 GitHub에 적응하기까지 제법 오랜 시간이 걸릴지도 모른다. 그래서 다음글 [Prose.io 연동으로 포스팅을 쉽게! 배포는 더 쉽게!](https://theorydb.github.io/envops/2019/05/04/envops-blog-posting-prose-io/)에서는 배포없이 좀 더 편하게 포스팅 할 수 있는 방법에 대해 알려드리고자 한다. 

> 필자가 수정 보완한 테마는 Free License이며 별도 동의없이 자유롭게 사용하실 수 있습니다. 마음에 드신다면 [필자의 블로그 저장소](https://github.com/theorydb/theorydb.github.io) [Fork] 버튼 왼쪽에 있는 `[★Star]` 버튼을 눌러주시면 큰 힘이 날 것 같네요. ^^. 긴 글 읽으시느라 고생 많으셨습니다.   