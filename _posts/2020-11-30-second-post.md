---
title: "KMP : 문자열 검색 알고리즘"
date: 2020-11-30 17:23:28 -0400
categories: Algorithm Java
---
## KMP 알고리즘
KMP 알고리즘은 대표적인 문자열 검색 알고리즘이다. 워드프로세서나 한글, 브라우저에서 Ctrl+F를 누르면 나오는 검색 기능은 바로 이 알고리즘을 사용하여 구현한 기능이다.

#### 가장 단순한 문자열 검색
---
가장 단순한 방법으로 문자열 검색을 생각해보면  
"ABCABABCDE" 에서 패턴 "ABC"가 어디서 등장하는지 찾아보자  

패턴 "ABC"를 한자리씩 옮기면서 같은지 비교를 하면 된다.  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
|A|B|C||||||||

패턴과 문자열이 일치함  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
||A|B|C|||||||

패턴과 문자열이 일치하지 않음  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
|||A|B|C||||||

패턴과 문자열이 일치하지 않음  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
||||A|B|C|||||

패턴과 문자열이 일치함  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
|||||A|B|C||||

패턴과 문자열이 일치하지 않음  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
||||||A|B|C|||

패턴과 문자열이 일치함  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
|||||||A|B|C||

패턴과 문자열이 일치하지 않음  

|A|B|C|A|B|A|B|C|D|E|
|--|--|--|--|--|--|--|--|--|--|
||||||||A|B|C|
 
패턴과 문자열이 일치하지 않음  


위와 같은 과정을 진행 했을 때,  
텍스트 "ABCABABCDEFAAAB" 에서 패턴 "ABC"는 밑줄친 자리에서 총 두번 등장함을 알 수 있다.  

<u>ABC</u>AB<u>ABC</u>DEFAAAB  

이 과정의 시간 복잡도는 텍스트의 길이를 N, 패턴의 길이를 M이라 할 때, 각 테스트의 인덱스에 대해 패턴이 일치하는지 비교하므로 O(NM) 이다.  
  
이 보다 더 빠르고 효율적으로 하는 방법이 KMP 알고리즘이다.  
이 알고리즘을 이용하면 O(N+M)에 문자열을 검색할 수 있다.  

#### KMP 알고리즘이란?
---

KMP알고리즘은 만든 사람이름이 Knuth, Morris, Prett이기 때문에 앞 글자를 하나씩 따서 KMP알고리즘이라고 한다.


#### 접두사(prefix)와 접미사(suffix)
---
<apple의 접두사><br/>
a  <br/>
ap  <br/>
app  <br/>
appl  <br/>
apple  <br/>
<br/>
이 5개가 apple의 접두사(prefix) 이다.<br/><br/>
<apple의 접미사>  <br/>
e  <br/>
le  <br/>
ple  <br/>
pple  <br/>
apple  <br/>
<br/>
이 5개가 apple의 접미사(suffix) 이다.<br/>
  <br/>
  
  
<b>두번째로</b> pi배열 이다.  <br/>
pi[i]는 주어진 문자열의 0~i 까지의 부분 문자열 중에서 prefix == suffix가 될 수 있는 부분 문자열 중에서 가장 긴 것의 길이이다.  <br/>
(이때 prefix가 0~i 까지의 부분 문자열과 같으면 안된다.)  <br/>
<br/>
문자열 "ABAABAB" 의 pi배열을 구하면 다음과 같다  <br/>
<br/>

|i|부분 문자열|pi[i]|
|:--:|:-------:|:--:|
|0|A|0|
|1|AB|0|
|2|<font color="red">A</font>B<font color="blue">A</font>|1|
|3|<font color="red">A</font>BA<font color="blue">A</font>|1|
|4|<font color="red">AB</font>A<font color="blue">AB</font>|2|
|5|<font color="red">ABA</font><font color="blue">ABA</font>|3|
|6|<font color="red">AB</font>AAB<font color="blue">AB</font>|2|

