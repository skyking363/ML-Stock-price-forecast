# I. 研究目的
隨著年紀的增長，如何理財這個事情變得相當重要，一般人會做被動型投資，像是定存或是基金投資，但是如果想要讓財富顯著的增加，
許多人會選擇股票作為投資標的。但是，如何選擇一隻會讓自己賺錢的股票，可說是長久以來的難題，且市面上充斥著良莠不齊的分析師，
有許多的不同的投資策略和技術指摽，讓人無所適從。我們期望可以利用機器學習的方法，在眾多的技術指標中，預測未來股票漲或跌的可能性，提升投資的報酬率。

# II.	資料描述
1.	收盤價： 
    為個股當天收盤的價格。
2.	相對強弱指標(RSV)：
    (今日收盤價-九日內最低價)/(九日內最高價-九日內最低價)*100，該指標值介於0到100之間。
3.	隨機指標(KD)：
    可分為K值與D值。當K值由下而上穿越D值，為黃金交叉，行情看好；當K值由上而下跌破D值，為死亡交叉，行情看壞。
    K值：前日K值*(2/3) + 當日RSV*(1/3)，該指標值介於0到100間。
    D值：前日D值*(2/3) + 當日K值*(1/3) ，該指標值介於0到100間。
4.	動量指標(Mom)：
    Mom為當日股價及前九天的股價差值，由此可以看出股價在其中波段漲跌幅度。
5.	移動平均線(SMA)：
    SMA：N日收盤價總和/N。這邊我們採用了五日，十日及二十日，若股票向上突破SMA則代表股價走強，為買進訊號，反之亦然。
6.	加權移動平均線(WMA)：
    WMA：(十日前收盤價*1+九日前收盤價*2+…+今日收盤價*10) / (1+2+…+10) 。我們採用十日的WMA，為十日的股價加權平均。
7.	相對強弱指標(RSI)：
    RSI：（九日股價上漲幅度的加總/（九日股價上漲幅度的加總 + 九日股價下跌幅度的加總））*100 。越高時代表市場越熱絡，越低時越冷清。其中RSI值大於80時，股價下跌的機率大；RSI值小於20時，上漲的機率高。
8.	三大法人：
    分別為外資，投信，自營商，所佔的持股比例。一般而言，若外資持股比例在股票市場中佔有較大，則股價的漲跌會容易受到外資的買賣而影響。
# III.資料檢視&初步分析
## ![image](https://github.com/skyking363/ML-Stock-price-forecast/blob/master/data.png)
## ![image](https://github.com/skyking363/ML-Stock-price-forecast/blob/master/Rplot01.png)
* 股價動態圖 : <http://rpubs.com/skyking363/499515>
# IV.	研究方法
將每日收盤價的漲跌作為反應變數(Y)，各種技術指標(RSV、Mom、SMA、WMA、RSI、…等)以及三大法人資訊當作解釋變數(X<sub>1</sub>,X<sub>2</sub>,…,X<sub>p</sub>)，
希望透過這些重要的技術建立模型並預測未來股價的漲跌趨勢。
* 資料蒐集：
這次的股價取得是由台灣證卷交易所的網站上集看盤軟體中取得個股的交易股價資訊，之後利用這些資料去計算得出代表股價的一些技術指標。 
* 資料處理：
將每日收盤價與前一日做比較得到當日股價的漲跌。(Y=+1代表漲，Y=-1代表跌。)
當日的技術指標及三大法人資訊(X<sub>1</sub>,X<sub>2</sub>,…,X<sub>p</sub>)值轉換為±1。(+1代表看漲，-1代表看跌。)
* 問題討論：
目前，利用Random Forest or boosting的方法，我們藉由當日技術指標及三大法人資訊做出當日股票漲跌的判斷。
