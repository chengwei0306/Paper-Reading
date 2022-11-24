### Graduate-school-Paper-Reading
### Lecturer:Wylee
### HW1

### Environment
- Google Colab


### Code
- Install yfinance
```python
!pip install yfinance
```

- Get Apple stock informations from  2021-11-15 to 2022-11-15
```python
import pandas as pd                                #導入 pandas套件
import yfinance as yf                              #導入 finance套件

tickers = ['AAPL']   #設置股票代碼
start_date = '2021-11-15'                          #set start date
end_date = '2022-11-15'                            #set end date

data = yf.download(tickers, start_date, end_date)   #data value
data['Date']=data.index

data=data[['Adj Close','Volume','Date']]               #Get Adj Close
Close=list(data.iloc[:,0])
Volume=list(data.iloc[:,1])
Date=list(data.iloc[:,2])
# print(len(Close))
print(Volume)
```
- Set V0 as averaged Volume
```python
import numpy as np
V0=np.mean(Volume)
V0
```

- sum the volume between j --> i as volume 
- if volume<V0 <br/>
then a set append Spread <br/>
b set append date
```python
def RareEvent(n,end_date):
  a=[]
  b=[]
  volume=0
  
  for i in range(0,n):                  #len of all
    volume=0
    for j in range(i):                  #from j to i
      volume+=Volume[j]
      if volume<V0:                     #mean()
        a.append(Close[n]-Close[i])
        b.append([end_date,Date[i]])
        # print(a)
        
  print(max(a))
  print(b[-1:])
    # print(volume)
    # print("------")

RareEvent(251,end_date)                #251-->amount of the data
```
