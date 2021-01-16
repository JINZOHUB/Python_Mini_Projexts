## 정규표현식으로 문자열 다루기 

'''
import re

example = '이동민 교수님은 다음과 같이 설명했습니다(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)'

result = re.findall(r'\([A-Za-z가-힣]+, \d+\)', example)

result 


## match 메서드 사용법 

'''

import re

pattern = r'life'    #패턴을 객체에 저장 , 패턴앞에는 r을 붙여줍니다.
script = 'life'      #패턴과 같은 스크립트를 다른 객체에 저장합니다. 
re.match(pattern, script)             #script에서 pattern을 찾으세요 
re.match(pattern, script).group()     #group()메서드를 사용해 매치된 내용을 반환합니다. 

'''

## one line expression
```
  re.match(r'life.', 'life1life2life3').group()
```


''' 
def refinder(pattern, script):
    if re.match(pattern, script):
        print("Match")
    else:
        print('Not a match!')

pattern = r'Life'
script = 'Life is so cool'
refinder(pattern, script)

'''

## can not find middle of spell

'''
pattern = r'is'
script = 'Life is so cool'
refinder(pattern, script) 
Not a match!  가 출력됨. 
match 는 중간에 오는 문자를 못찾음 앞에만 찾을 수 있음
별 쓸모 없는것 같음
'''

## search 매서드 문자열 전체에서 패턴찾기 

re.search(패턴, 문자열)
: search는 중간에 있는 문자열도 찾아줌. 

'''
pattern = r'is'
script = 'Life is so cool'
re.search(pattern,script).group()

'''

## 꼭 알아야 할 정규표현식 

[0-9] 또는 [a-zA-Z] 등은 무척 자주 사용하는 정규 표현식이다. 이렇게 자주 사용하는 정규식은 별도의 표기법으로 표현할 수 있다. 다음을 기억해 두자.


\d | 숫자와 매치, [0-9]와 동일한 표현식이다.
\D | 숫자가 아닌 것과 매치, [^0-9]와 동일한 표현식이다.
\s | whitespace 문자와 매치, [ \t\n\r\f\v]와 동일한 표현식이다. 맨 앞의 빈 칸은 공백문자(space)를 의미한다.
\S | whitespace 문자가 아닌 것과 매치, [^ \t\n\r\f\v]와 동일한 표현식이다.
\w | 문자+숫자(alphanumeric)와 매치, [a-zA-Z0-9_]와 동일한 표현식이다.
\W | 문자+숫자(alphanumeric)가 아닌 문자와 매치, [^a-zA-Z0-9_]와 동일한 표현식이다.

\\ | 메타 문자가 아닌 일반 문자 열슬래시 (\)와 매치. 메타 문자 앞에 \를 붙이면 일반 문자를 의미합니다. 

## \\\\ express examples
'''
re.match(r'life..','Life\d is so cool').group()
re.match(r'Life\\d','Life\d is so cool').group()
'''
>'Life\\d'


## findall 매서드 - 패턴을 모두 찾아 리스트로 반환하기 
'''
re.findall(패턴, 찾으려는 문자열)
number ='My number is 511223-1****** and yours is 521012-2******'
re.findall('\d{6}',number)  #'\d{6}' 패턴은 숫자를 여섯 번 반복한 값의미
['511223','521012']

## 문자열 규칙에 r을 앞에 붙이는 이유 

만약 문자열에 '\' 문자가 있다면 파이썬은 그 다음에 나오는 문자를 그대로 인식하지 않고 컴퓨터에 명령어로 인식함. 

'''

re.match(r'Life\\d', 'Life\d is so cool').group()
re.match('Life\\\d', 'Life\d is so cool').group()
r이 붙으면 string 이 되고 
없으면 raw string 이 된다 . 

'''

에러

'''
re.match('Life\\d', 'Life\d is so cool').group()
'''
r이 붙으면 string 이 되고 
없으면 raw string 이 된다 . 

## 정규표현식의 탐욕 제어하기 : 마침표. 와 물음표 ?
: 마침표. 는 모든 문자를 의미해서 모든 문자를 다 집어 삼킨다고 하여 그리디 라는 개념이 붙게 됨. 

'''
example = '저는 91 년에 태어났습니다. 97년에는 IMF가 있었습니다. 지금은 2020년입니다.'
re.findall(r'\d.+년', example)  #숫자 \d 로 시작하고 어떤문자든. 반복+되며 '년'으로 끝나는 문자열을 반환하라는 의미 
['91 년에 태어났습니다. 97년에는 IMF가 있었습니다. 지금은 2020년']
'''

'''
re.findall(r'\d.+?년', example)
['91 년', '97년', '2020년']
re.findall(r'\d+.년', example)
['91 년', '97년', '2020년']
'''

'''
example = '이동민 교수님은 다음과 같이 설명했습니다(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)'

result = re.findall(r'\(.+\)',example)
result
결과
['(이동민, 2019). 그런데 다른 교수님은 이 문제에 대해서 다른 견해를 가지고 있었습니다. (최재영, 2019). 또 다른 견해도 있었습니다(Lion, 2018)']
'''







