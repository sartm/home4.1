# home4.1

## Обязательная задача 1

Есть скрипт:
```bash
a=1
b=2
c=a+b
d=$a+$b
e=$(($a+$b))
```

Какие значения переменным c,d,e будут присвоены? Почему?

| Переменная  | Значение | Обоснование |
| ------------- | ------------- | ------------- |
| `c`  | a+b  | Неявное определение строки с буквами и знаком + |
| `d`  | 1+2  | Вывод на экран значений переменных a и b со знаком + |
| `e`  | 3  | Двойные круглые скобки  -  арифметические вычисления в Bash |


## Обязательная задача 2
На нашем локальном сервере упал сервис и мы написали скрипт, который постоянно проверяет его доступность, записывая дату проверок до тех пор, пока сервис не станет доступным (после чего скрипт должен завершиться). В скрипте допущена ошибка, из-за которой выполнение не может завершиться, при этом место на Жёстком Диске постоянно уменьшается. Что необходимо сделать, чтобы его исправить:
```bash
while ((1==1)
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	fi
done
```

### Ваш скрипт:
```bash
while ((1==1))
do
  curl https://localhost:4757
  if (($? != 0))
  then
    break		
  fi
  date >> curl.log
done

```

## Обязательная задача 3
Необходимо написать скрипт, который проверяет доступность трёх IP: `192.168.0.1`, `173.194.222.113`, `87.250.250.242` по `80` порту и записывает результат в файл `log`. Проверять доступность необходимо пять раз для каждого узла.

### Ваш скрипт:
```bash
a=5
while ((a$>0))
do
	curl 192.168.0.1:80
	curl 173.194.222.113:80
	curl 87.250.250.242:80
	echo $? >> ip.log
	let “a-=1”
done
```

## Обязательная задача 4
Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается.

### Ваш скрипт:
```bash
array_int=(192.168.0.1:80 173.194.222.113:80 87.250.250.242:80)
for i in ${array_int[@]}
do
	curl $i
	  if [$? != 0]
		then
		break
	  fi
	eccho $i > error.log
done
```
