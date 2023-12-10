# 資料集欄位說明

本資料集的原始數據來自 [SeanLahman.com](http://seanlahman.com/download-baseball-database/)，經過前處理和合併以符合期末報告所需要的格式。主要針對投手、打者和薪資等相關數據進行調整，相關說明如下。
1. 1985 ~ 2016 年有大聯盟出賽紀錄的投打者數據，投手(11,953筆)、打者(25,441筆)，合計(37,394筆)，請參閱 [各年度資料筆數](#各年度資料筆數) 有說明。
2. 投打者資料集僅會包含`有薪資的出賽年份`，該年度若無薪資資料將會移除。
3. 部分資料欄位因為不可能出現浮點數，例如，故意四壞球、觸身球等欄位，這些欄位皆替換成整數，並且將原資料集 Nan 欄位補 0。
4. 投打數據有部分欄位跟報告需要的分析數據較無直接關係，有刪除。 
5. 打者的數據可能包含投手的數值。
6. `使用前請注意，資料集部分欄位可能有缺失值`，詳見 [投打共用欄位說明](#投打共用欄位說明)、[投手欄位說明](#投手欄位說明)、 [打者欄位說明](#打者欄位說明) 的欄位說明。
7. 資料集使用範例請參考 [範例程式碼](#資料集使用方式)。

<br>

## 投打共用欄位說明
欄位|說明|類型|缺失值
---|---|---|---
playerID|識別碼|字串|
nameFirst|名字|字串|v
nameLast|姓氏|字串|
nameGiven|名字（通常是名字和中間名)|字串|v
birthday|生日（yyyy-MM-dd)|字串|v
birthCountry|出生國家|字串|v
weight|球員的體重（磅）|整數|v
height|球員的身高（英吋）|整數|v
bats|左右打（left, right, or both)|字串|v         
throws|左右投（left or right)|字串|v
debut|大聯盟初登板日期（yyyy-MM-dd)|字串|v
yearID|出賽年份|整數|
age|出賽年 - 當時年紀|整數|
teamID|出賽年 - 所屬球隊|字串|
lgID|出賽年 - 所屬聯盟|字串|
salary|出賽年 - 薪資（美金)|整數|

<br>

## 投手欄位說明
欄位|說明|類型|缺失值
---|---|---|---
W|勝投|整數|
L|敗投|整數|
G|出賽數|整數|
IPouts|出局投球數（投球局數 x 3）|整數|
H|被安打數|整數|
ER|自責分|整數|
HR|被全壘打|整數|
BB|四壞球|整數|
SO|三振|整數|
BAOpp|被打擊率|浮點數|v
ERA|自責分率|浮點數|v
IBB|故意四壞球|整數|
WP|暴投|整數|
HBP|觸身球|整數|
BK|失投球|整數|
BFP|投手面臨的打者數|整數|
GF|完投比賽|整數|
R|失分|整數| 
SH|對手擊球出局犧牲打|整數|
SF|對手擊球飛球犧牲打|整數|
GIDP|對手擊打雙殺打|整數|

<br>

## 打者欄位說明
欄位|說明|類型|缺失值
---|---|---|---
G|出賽數|整數| 
AB|打數|整數|
R|得分|整數|
H|安打|整數|
2B|二壘打|整數|
3B|三壘打|整數|
HR|全壘打|整數|
RBI|打點|整數|
SB|盜壘成功|整數|
CS|盜壘失敗|整數|
BB|保送|整數|
SO|三振|整數|
IBB|故意四壞球|整數|
HBP|被觸身球|整數|
SH|犧牲觸擊|整數|
SF|犧牲飛球|整數|
GIDP|打擊擊出雙殺打|整數|

<br>

## 各年度資料筆數
年度|投手紀錄|打者紀錄|合計筆數
---|---|---|---
1985|215|530|745
1986|306|702|1,008
1987|257|604|861
1988|270|643|913
1989|298|684|982
1990|353|789|1,142
1991|300|667|967
1992|318|730|1,048
1993|405|897|1,302
1994|386|853|1,239
1995|454|964|1,418
1996|419|904|1,323
1997|425|895|1,320
1998|454|957|1,411
1999|455|970|1,425
2000|373|801|1,174
2001|375|814|1,189
2002|383|804|1,187
2003|372|800|1,172
2004|381|800|1,181
2005|380|796|1,176
2006|378|790|1,168
2007|396|806|1,202
2008|396|812|1,208
2009|388|787|1,175
2010|388|790|1,178
2011|400|812|1,212
2012|398|811|1,209
2013|404|809|1,213
2014|388|801|1,189
2015|418|814|1,232
2016|416|805|1,221
總計|11,949|25,441|37,390

<br>

## 資料集使用方式
### 載入投手數據
``` python
import pandas as pd
pd.set_option('display.max_columns', None)

# 讀取投手數據
df_pitching = pd.read_csv('https://raw.githubusercontent.com/lawrence8358/MLBDataSet/main/data/pitching.csv')

# 王建民的數據
result = df_pitching[df_pitching['playerID'] == 'wangch01']
result
```

### 載入打者數據
``` python
import pandas as pd
pd.set_option('display.max_columns', None)

# 讀取打者數據
df_batting = pd.read_csv('https://raw.githubusercontent.com/lawrence8358/MLBDataSet/main/data/batting.csv')

# 胡弟的數據
result = df_batting[df_batting['playerID'] == 'huch01']
result
```

### 檢查投手數據缺失值
``` python
import pandas as pd
pd.set_option('display.max_columns', None)

# 讀取投手數據
df_pitching = pd.read_csv('https://raw.githubusercontent.com/lawrence8358/MLBDataSet/main/data/pitching.csv')

# 王建民的數據
result = df_pitching[df_pitching['playerID'] == 'wangch01']
result
```