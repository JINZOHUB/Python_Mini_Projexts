## CSV

```
import csv, os
os.chdir(r'/Users/David/Desktop/Python/생활파이썬/Python_Mini_Projexts/') # a.csv 디렉토리 경로로 이동
f = open('a.csv','r')
f = open('a.csv','r',encoding = 'utf-8')
new = csv.reader(f)  # 객체 f를 csv.reader로 읽어 변수에 저장함
_csv.reader object at 0x10e870d68>

for i in new:
    print(i)

['국어', ' 영어', ' 수학']
['90', '80', '100']

a_list = []
for i in new:
...     print(i)
...     a_list.append(i)
... 
['국어', ' 영어', ' 수학']
['90', '80', '100']

a_list
[['국어', ' 영어', ' 수학'], ['90', '80', '100']]

f.seek(0)
0
for i in new:
...     print(i)
...     a_list.append(i)
... 
['국어', ' 영어', ' 수학']
['90', '80', '100']
a_list
[['국어', ' 영어', ' 수학'], ['90', '80', '100']]

def opencsv(filename):
    f = open(filename,'r')
    reader = csv.reader(f)
    output = []
    for i in reader:
        output.append(i)
    return output

opencsv('example2.csv')
[['이름', ' 국어', ' 영어 ', ' 수학 '], ['a', '90', '80', '100'], ['b', '80', '90', '90'], ['c', '100', '80', '60']]

opencsv('abc.csv')
[['구', ' 전체', ' 내국인', ' 외국인'], ['관악구', ' 519864', '502089', '17775'], ['강남구', ' 547602', '542498', '5104'], ['송파구', ' 686181', '679247', '6934'], ['강동구', ' 428547', '424235', '4312']]



a = [['구', ' 전체', ' 내국인', ' 외국인'], ['관악구', ' 519864', '502089', '17775'], ['강남구', ' 547602', '542498', '5104'], ['송파구', ' 686181', '679247', '6934'], ['강동구', ' 428547', '424235', '4312']]
f = open('abe.csv','w',newline ='')
csvobject = csv.writer(f, delimiter =',')
csvobject.writerows(a)
f.close
#파일이 만들어짐 

#일반화

def writercsv(filename, the_list):
    with open (filename, 'w', newline ='') as f:
        a = csv.wrtier(f,delimiter = ',')
        a.writerows(the_list)

