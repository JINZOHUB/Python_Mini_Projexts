## 정규표현식으로 문자열 다루기 

```
import re

example = '이동민 교수님은 다음과 같이 설명했습니다(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)'

result = re.findall(r'\([A-Za-z가-힣]+, \d+\)', example)

result 


## match 메서드 사용법 

```

import re

pattern = r'life'    #패턴을 객체에 저장 , 패턴앞에는 r을 붙여줍니다.
script = 'life'      #패턴과 같은 스크립트를 다른 객체에 저장합니다. 
re.match(pattern, script)             #script에서 pattern을 찾으세요 
re.match(pattern, script).group()     #group()메서드를 사용해 매치된 내용을 반환합니다. 

```

## one line expression
```
  re.match(r'life.', 'life1life2life3').group()
```


``` 
def refinder(pattern, script):
    if re.match(pattern, script):
        print("Match")
    else:
        print('Not a match!')

pattern = r'Life'
script = 'Life is so cool'
refinder(pattern, script)

```

## can not find middle of spell

```
pattern = r'is'
script = 'Life is so cool'
refinder(pattern, script) 
Not a match!  가 출력됨. 
match 는 중간에 오는 문자를 못찾음 앞에만 찾을 수 있음
별 쓸모 없는것 같음
```

## search 매서드 문자열 전체에서 패턴찾기 

re.search(패턴, 문자열)
: search는 중간에 있는 문자열도 찾아줌. 

```
pattern = r'is'
script = 'Life is so cool'
re.search(pattern,script).group()

```

## 꼭 알아야 할 정규표현식 

[0-9] 또는 [a-zA-Z] 등은 무척 자주 사용하는 정규 표현식이다. 이렇게 자주 사용하는 정규식은 별도의 표기법으로 표현할 수 있다. 다음을 기억해 두자.

정규표현식 | 설명
--------- | ----
\d | 숫자와 매치, [0-9]와 동일한 표현식이다.
\D | 숫자가 아닌 것과 매치, [^0-9]와 동일한 표현식이다.
\s | whitespace 문자와 매치, [ \t\n\r\f\v]와 동일한 표현식이다. 맨 앞의 빈 칸은 공백문자(space)를 의미한다.
\S | whitespace 문자가 아닌 것과 매치, [^ \t\n\r\f\v]와 동일한 표현식이다.
\w | 문자+숫자(alphanumeric)와 매치, [a-zA-Z0-9_]와 동일한 표현식이다.
\W | 문자+숫자(alphanumeric)가 아닌 문자와 매치, [^a-zA-Z0-9_]와 동일한 표현식이다.
\\ | 메타 문자가 아닌 일반 문자 열슬래시 (\)와 매치. 메타 문자 앞에 \를 붙이면 일반 문자를 의미합니다. 

## \\\\ express examples
```
re.match(r'life..','Life\d is so cool').group()
re.match(r'Life\\d','Life\d is so cool').group()
```
>'Life\\d'


## findall 매서드 - 패턴을 모두 찾아 리스트로 반환하기 
```
re.findall(패턴, 찾으려는 문자열)
number ='My number is 511223-1****** and yours is 521012-2******'
re.findall('\d{6}',number)  #'\d{6}' 패턴은 숫자를 여섯 번 반복한 값의미
['511223','521012']

## 문자열 규칙에 r을 앞에 붙이는 이유 

만약 문자열에 '\' 문자가 있다면 파이썬은 그 다음에 나오는 문자를 그대로 인식하지 않고 컴퓨터에 명령어로 인식함. 

```

re.match(r'Life\\d', 'Life\d is so cool').group()
re.match('Life\\\d', 'Life\d is so cool').group()
r이 붙으면 string 이 되고 
없으면 raw string 이 된다 . 

```

에러

```
re.match('Life\\d', 'Life\d is so cool').group()
```
r이 붙으면 string 이 되고 
없으면 raw string 이 된다 . 

## 정규표현식의 탐욕 제어하기 : 마침표. 와 물음표 ?
: 마침표. 는 모든 문자를 의미해서 모든 문자를 다 집어 삼킨다고 하여 그리디 라는 개념이 붙게 됨. 
1) DOTALL
메타문자 .가 줄바꿈 문자 \n을 포함해 모든 문자의미

2)반복 (+)
*와 마찬가지로 반복을 의미하는 +는 해당 문자가 1번 이상의 패턴이 발생

3) ? 없거나 하나 있거나
? 앞에 있는 문자가 없거나 하나 있을 때 매치된다. 0 혹은 1번의 패턴이 발생


```
example = '저는 91 년에 태어났습니다. 97년에는 IMF가 있었습니다. 지금은 2020년입니다.'

re.findall(r'\d.+년', example)  #숫자 \d 로 시작하고 어떤문자든. 반복+되며 '년'으로 끝나는 문자열을 반환하라는 의미 
['91 년에 태어났습니다. 97년에는 IMF가 있었습니다. 지금은 2020년']
```

```
re.findall(r'\d.+?년', example)
['91 년', '97년', '2020년']
re.findall(r'\d+.년', example)
['91 년', '97년', '2020년']
```

```
example = '이동민 교수님은 다음과 같이 설명했습니다(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)'

result = re.findall(r'\(.+\)',example)
result
결과
['(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)']
```

```
example = '이동민 교수님은 다음과 같이 설명했습니다(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)'
result = re.findall(r'\(.+?\)',example)
result 
```

## split 메서드 - 문장나누기 패턴
re.split(패턴, 문자열)

```
sentence = 'I have a lovely dog, really. I am not telling a lie. What a pretty dog! I love this dog.'

re.split(r'[.?!]',sentence)

['I have a lovely dog, really', ' I am not telling a lie', ' What a pretty dog', ' I love this dog', '']
```
대괄호안에 들은건 .?! 일반 문자가의 패턴을 말함 정규표현식이 아님 


data = 'a:3; b:4; c:5'
for i in re.split(r';',data): #세미콜론으로 전체데이터를 한번 구분함
  print(re.split(r':',i))


## sub 메서드 - 문자열 바꾸기 

re.sub(찾을패턴, 대체할문자, 찾을 문자열)

```
sentence = 'I have a lovely dog, really. I am not telling a lie. What a pretty dog! I love this dog.'

re.sub('dog','cat',sentence)

words = 'I am home now. \n\n\nI am with my cat. \n\n'
print(words)

re.sub(r'\n', '',words)
'I am home now. I am with my cat.'
```

## ly로 끝나는 단어 추출하기 
sentence = 'I have a lovely dog, really. I am not telling a lie.'
re.findall(r'\w+ly',sentence)



## 프렌즈 대본파일 실습


```
import os, re, codecs    #codecs(파일코덱변경)

os.chdir(r'C:\Users\songs\OneDrive\바탕화면\python_11_projects') # 파일 들어있는 디렉토리로 이동

f = codecs.open('friends101.txt','r', encoding = 'utf-8') #파일열기

script101 = f.read() #파일읽기 

print(script101[:100]) 

결과
The One Where Monica Gets a New Roommate (The Pilot-The Uncut Version)Written by: Marta Kauffman &      #100번째 글자 까지 출력됨. 즉 , 문자하나당 하나의 인덱스 씩 저장 되어있음.


Line = re.findall(r'Monica:.+', script101) #Monica 다음 아무문자 반복되는 패턴을 스크립트101에 찾아서 저장함. 즉, 모니카 대사가 다 저장됨.

print(Line[:3]) #모니카의 대사 3개가 찍히게 됨. 출력했을때 한 문장 끝나고 다 \r이라고 띄워쓰기가 보이지 않지만 들어가있는데 정규표현식은 한 줄씩 인식함.그래서 모니카가 세번째 있는 범위까지 모든 스크립트만 나온게 아니라 모니카의 대본만 딱 세줄이 나오게됨.

for item in Line[:3]:
  print(item) 

f = open('monica.txt','w', encoding = 'utf-8') #monica.txt라는 파일을 만듦
monica = ''   #빈문자열을 만듦
for i in Line:
  monica += i   #한줄씩 추가하도록 함 

f.write(monica)   #파일에 한줄씩 추가한 모든걸 넣음 
4542
f.close()

# 리눅스와 맥은 \n 으로 개행문자로 인식하고 , 나는 윈도우를 실습해서 \r ,\n 둘다 개행문자로 인식하기 때문에 monica.txt 가 들어가도 다 띄어쓰기 해서 들어갔다. 추가적으로 윈도에서 ATOM 으로 열면 리눅스에서 연거 처럼 띄어쓰기 안들어가서 나오고 실제로 윈도우 창 메모장이나 vscode로 열면 띄어쓰기 되서 보임

#리눅스 맥이었다면 이렇게 for문 안에 +'\n' 추가해줘야 띄어써서 들어감
f = open('monica.txt','w', encoding = 'utf-8') 
monica = ''   #빈문자열을 만듦
for i in Line:
  monica += i +'\n'
f.write(monica) 
f.close()

```

## 등장인물 리스트 만들기 

```
char = re.compile(r'[A-Z][a-z]+:')   #대문자로 시작하고 소문자가 반복되는패턴: 을 찾아서 저장함.

지금까지 import re를 사용하여 re로부터 직접 메서드를 호출해왔다. re.match, re.sub 등이 그 예시이다.

이 방식은 한두번 쓰고 말기에는 괜찮지만, 같은 정규식 패턴을 반복문 내에서 반복적으로 사용해야 할 경우 성능상의 부담이 있다.
이는 정규식은 컴파일이란 과정을 거치기 때문인데, re 모듈로부터 직접 갖다 쓰면 매번 컴파일이란 비싼 계산을 해야 하기 때문에 성능이 떨어진다.

지금까지,

re 모듈로부터 직접 match, search 등 메서드를 써 왔다.
인자는 기본적으로 1) 정규식 패턴과 2) 찾을 문자열이 있었다.
컴파일을 미리 하는 버전은,

re.compile 메서드로부터 reObj를 만든다.
인자는 기본적으로 1) 정규식 패턴 하나이다.
reObj.match 혹은 search 등으로 문자열을 찾는다.
인자는 정규식 패턴은 이미 저장되어 있으므로 search 메서드에는 1) 찾을 문자열 하나만 주면 된다.

re.findall(char, script101) # 이름이 중복되서 모두 다 출력이 됨


set 키워드로 중복된 원소 지우기 

a = [1,2,3,4,5,2,2]
set(a)   # set 키워드를 사용하면 집합으로 형변환하면서 중복 없앰.
{1,2,3,4,5}

set(re.findall(char,script101))

{'Rachel:', 'Monica:', 'Waitress:', 'Paul:', 'Note:', 'Frannie:', 'Customer:', 'Chandler:', 'Phoebe:', 'Scene:', 'Ross:', 'All:', 'Joey:'}


