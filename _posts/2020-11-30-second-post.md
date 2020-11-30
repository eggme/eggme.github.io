---
title: "KMP: 문자열 검색 알고리즘"
date: 2020-11-30 17:23:28 -0400
categories: Algorithm Java
---
## KMP 알고리즘
KMP 알고리즘은 대표적인 문자열 검색 알고리즘이다. 워드프로세서나 한글, 브라우저에서 Ctrl+F를 누르면 나오는 검색 기능은 바로 이 알고리즘을 사용하여 구현한 기능이다.

#### 가장 단순한 문자열 검색
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


​```python
def print_hi(name):
  print("hello", name)
print_hi('Tom')
​```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
