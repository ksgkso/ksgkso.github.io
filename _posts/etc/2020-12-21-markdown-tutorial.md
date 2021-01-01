---
layout: post
title:  "마크다운 문법정리"
subtitle:   "나를 위한 Markdown 작성법"
categories: etc
tags: etc
comments: true
related_posts:
    - category/_posts/etc/2020-12-21-setting-start.md
---


## 개요
> 내가 보기위한 마크다운 `Markdown` 작성법  
  
- 목차
	- [마크다운이란?](#마크다운이란?) 
	- [마크다운의 장단점](#마크다운의-장단점)
	- [마크다운-문법](#마크다운-문법)
	- [코드](#3.1-코드)
  
  
## 마크다운이란?
---
Markdown은 텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌으며 쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게 컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다. 마크다운이 최근 각광받기 시작한 이유는 깃헙(https://github.com) 덕분이다. 깃헙의 저장소Repository에 관한 정보를 기록하는 README.md는 깃헙을 사용하는 사람이라면 누구나 가장 먼저 접하게 되는 마크다운 문서였다. 마크다운을 통해서 설치방법, 소스코드 설명, 이슈 등을 간단하게 기록하고 가독성을 높일 수 있다는 강점이 부각되면서 점점 여러 곳으로 퍼져가게 된다.

***

## 마크다운의 장단점
---
### 2.1.장점
    '''
    1. 간결하다.
    2. 별도의 도구없이 작성가능하다.
    3. 다양한 형태로 변환이 가능하다.
    4. 텍스트(Text)로 저장되기 때문에 용량이 적어 보관이 용이하다.
    5. 텍스트파일이기 때문에 버전관리시스템을 이용하여 변경이력을 관리할 수 있다.
    6. 지원하는 프로그램과 플랫폼이 다양하다.
    '''

### 2.2.단점
    '''
    1. 표준이 없다.
    2. 표준이 없기 때문에 도구에 따라서 변환방식이나 생성물이 다르다.
    3. 모든 HTML 마크업을 대신하지 못한다.
    '''
    
***

## 마크다운 문법
---
지금 위에서 설명한것만으로 벌써 마크다운의 문법을 사용하였다.
사용한것부터 시작하여 마크다운 문법을 봐보자.

### 3.1 코드
---
#### 3.1.1 코드블럭
위에서 장단점을 설명할때와 같이 회색 박스

4가지 방식을 사용할 수 있다.

(1. '<pre><code>{code}</code></pre>')

(2. ("\```") )

(3. 들여쓰기)

(4. 언어별 코드블럭)

* __1.'<pre><code>{code}</code></pre>' 이용방식__

```
<pre>
<code>
def func(a,b):
    return a+b
print(func(2,3))
</code>
</pre>
```

결과

<pre>
<code>
def func(a,b):
    return a+b

print(func(2,3))
</code>
</pre>
---
* __2.코드블럭코드("\```") 을 이용하는 방법__

<pre>
<code>
```
def func(a,b):
    return a+b

print(func(2,3))
```
</code>
</pre>

결과

```
def func(a,b):
    return a+b

print(func(2,3))
```
---
* __3.들여쓰기__

탭이나 스페이스 4번을 통해 코드블럭을 만들수 있다.

<pre>
<code>
    def func(a,b):
        return a+b

    print(func(2,3))
</code>
</pre>

결과

    def func(a,b):
        return a+b

    print(func(2,3))

---

* __4.언어별 코드블럭__

* _python_

<pre>
<code>

	```python
    def func(a,b):
        return a+b
    
    print(func(2,3))
    ```

</code>
</pre>

* 결과  

	```python
    def func(a,b):
        return a+b
    
    print(func(2,3))
    ```

---

* _css_
<pre>
<code>
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
</code>
</pre>


* 결과 
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

---

* 그밖에

    * Bash (bash)
    * C# (cs)
    * CSS (css)
    * Diff (diff)
    * HTML, XML (html)
    * Ini (ini)
    * JSON (json)
    * Java (java)
    * JavaScript (javascript)
    * PHP (php)
    * Perl (perl)
    * Python (python)
    * Ruby (ruby)
    * SQL (sql)

***


### 3.2 헤더
---
* 글머리: 1~6까지만 지원

<pre>
<code>
# this is a H1
## this is a H2
### this is a H3
#### this is a H4
##### this is a H5
###### this is a H6
</code>
</pre>

# this is a H1
## this is a H2
### this is a H3
#### this is a H4
##### this is a H5
###### this is a H6

***

### 3.3 BlockQuote
---
이메일에서 사용하는 '''>''' 블록인용문자를 이용한다.

<pre>
<code>
> This is a first blockque.
</code>
</pre>

> This is a first blockque.

<pre>
<code>
>   > This is a second blockque.
</code>
</pre>

>   > This is a second blockque.

<pre>
<code>
>   >   > This is a Third blockque.
</code>
</pre>

>   >   > This is a Third blockque.

BlockQuote 안에 다른 마크다운 요소를 포함할 수 있다.

<pre>
<code>
> ### This is a H3
> * List
>	```
>	code
>	```
</code>
</pre>

결과

> ### This is a H3
> * List
>	```
>	code
>	```

### 3.4 글머리 기호, 순서없는 목록

### 3.5 강조

### 3.6 수평

### 3.7 링크

### 3.8 이미지

### 3.9 줄바꿈


