## 과거 날짜
```
date -d 'yesterday'		# 어제
date -d '1 day ago'		# 1일전 = 어제
date -d '2 day ago'		# 2일전
date -d '35 day ago'		# 20일전
date -d '1 week ago'		# 1주일전
date -d '2 month ago'		# 1달전
date -d '3 year ago'		# 3년전
date -d '10 second ago'		# 10초전
date -d '20 minute ago'		# 20분전
date -d '30 hour ago'		# 30시간전
date -d '3 year 7 month ago'	# 3년 7개월전
```

## 미래 날짜 
* 과거에서 ago 를 빼면 됨
```
date -d 'tomorrow'		# 내일
date -d '1 day'			# 1일후 = 내일
date -d '2 day'			# 2일후
date -d '35 day'			# 20일후
date -d '1 week'		# 1주일후
date -d '2 month'		# 1달후
date -d '3 year'		# 3년후
date -d '10 second'		# 10초후
date -d '20 minute'		# 20분후
date -d '30 hour'		# 30시간후
date -d '3 year 7 month'		# 3년 7개월후
```

## 요일 기준
```
date -d 'this friday'	# 이번주 금요일
date -d 'last monday'	# 지난 월요일
date -d 'next tuesday'	# 다음 화요일
```

## 특정 시간을 기준으로 날짜 더하고 빼기
```
date -d '2010-01-03 07:32:10 + 2 day 5 hours 17 minute'	
# 2010년 1월 3일 7시 32분 10초를 기준으로 2일 5시간 17분후
```

## 옵션 1
-d 는 --date 옵션으로 사용해도 됩니다. --date 로 쓸때에는 --date= 형식으로 사용하시면 됩니다.
```
date --date='2 month'
```

## 옵션 2
시간단위를 나타내는 day, week, month, year, second, minute, hour 등은 뒤에 s(복수)를 붙여도 되고 안붙여도 됩니다.
```
date -d '1 day ago'
date -d '1 days ago'
```

## 옵션 3
시간을 원하는 형식으로 뽑기위해서는 아래같이 하시면 됩니다.
현재 시간으로부터 2일전의 년-월-일 시:분:초 형식으로 표시하려면
```
date '+%Y-%m-%d %H:%M:%S' -d '2 day ago'
```

## 쉘스크립트에서 해당 시간을 변수에 담기
보통 위와 같은 date 함수는 주로 쉘스크립트에서 사용하게 됩니다. 리눅스 명령으로 가져온 결과값을 변수에 담으려면
```
yesterday=$(date -d '1 day ago')
```
또는
```
yesterday=`date -d '1 day ago'`
```
변수를 사용할때는
```
echo $yesterday
```
