Run python command line in this project folder
-----------------------
```
python
```

make file a.txt

write file
----------

```
  f = open('a.txt', 'w')
  f.write('abc')
  f.close()
```

```
  f = open('a.txt', 'w')
  f.write('나는 오늘 학교에 간다')
  f.close()
```


read file
---------
```
  f = open('a.txt', 'r')
  f.read()
  f.read()
  f.close()
```
first f.read() result : ```나는 오늘 학교에 간다```
second f.read() result : ```''```


read not exist file
-------------------
```
  f = open('b.txt', 'r')
```
result

> Traceback (most recent call last):
>  File "<stdin>", line 1, in <module>
> FileNotFoundError: [Errno 2] No such file or directory: 'b.txt'


add more txt
------------
```
  f = open('a.txt', 'a')
  f.write('학교 가지 않을 날이 올까?')
  f.close()
```
check it
```
  f = open('a.txt', 'r')
  f.read()
  f.close()
```

use with
make abcde.txt
--------
```
  f = open('abcde.txt', 'w')
  f.write('I went to school today.')
  f.close()
```


```
  with open('text.txt')
```