# NS 網路模擬器

- [name=呂佳陵]

### 簡介
- NS是一系列網路模擬器，包括ns-1、ns-2和ns-3。NS主要用於模擬區域網和廣域網。
- NS是加州大學柏克萊分校開發的網路模擬器，可模擬各種IP網絡。它實現了TCP和UPD等網絡協議，FTP、Telnet、Web、CBR和VBR等流量源行為，Drop Tail，RED和CBQ等路由器隊列管理機制，Dijkstra等路由演算法。
- NS還實現了多點傳送(multicasting)和一些MAC層協議於LAN模擬。
- 雖然NS了解了模擬器就相當容易使用，但對於初次使用的用戶來說相當困難。
- REAL 是 ns 的原型，始於1989年。

### ns-1
- **模擬器的核心由C++寫成，以Tcl腳本為基礎的模擬場景。**
- 1995-1997年間，ns的第一版，由勞倫斯柏克萊國家實驗室 （LBNL）的Steve McCanne、Sally Floyd、Kevin Fall和其他貢獻者開發。
- 它常被稱為LBNL網絡模擬器（LBNL Network Simulator），源於早期的由S.Keshav編寫的REAL模擬器。

> 長期的貢獻來源於Sun、加州大學伯克利分校的Daedelus項目和卡內基梅隆大學Monarch項目。

### ns-2
- **由C ++和的OTcl為開發語言。**

- 1996-1997年間，ns的第二版最初由Steve McCanne重構而來並**用MIT的OTcl替代了Tcl語言**，OTcl是一個物件導向的Tcl方言。
- ns-2的核心部分依舊由C++ 寫成，但是C++ 模擬對象和變數也可在OTcl中使用。
- 模擬腳本由OTcl寫成。這樣的結構使得模擬方案能由直譯器運行，同時方便的更改而不用重新編譯模擬器。
- 在ns-2推出的時期（1990中葉），這樣的方式非常方便並且避免了浪費時間的編譯操作。而且腳本語言的語法更加清晰。
- 與ns-2一起配合的部件「Network Animator」（nam-1），由Mark Handley編寫，用來**圖形化**的展示模擬場景。

> 1997年，DARPA的Virtual InterNetwork Testbed（VINT）項目啟動，勞倫斯柏克萊國家實驗室、Xerox PARC、加州大學柏克萊分校和南加州大學信息科學研究所（ISI）參與其中。 **ns-2的迅速開發正是在這個時期。** 同時維護軟體的任務漸漸地由ISI接手，最終John Heidemann領導了這個維護任務。在完成了VINT項目後，ns-2在2001-2004年繼續由DAPRA SAMAN和NSF CONSER贊助，最終贈與USC/ISI。

> 現在，ns-2包含了超過30萬行代碼，並且存在相當多的一部分代碼未被合併到主線中。（因為有許多ns-2分支，包括被維護的和未維護的）它能夠運行在GNU/Linux、FreeBSD、Solaris、OS X和Windows 95/98/NT/2000/XP上。ns-2以GPL v2協議分發。

### ns-3
- 由C++和Python寫成，並且以這兩種作為編寫腳本的語言。
- 開始於2006年7月1日。
- 在ns-3的開發過程中，**開發者決定不再向下兼容ns-2，這主要是因為向後兼容需要太多的額外工作。新的模擬器將從頭編寫，使用C++**。
- ns-3主要用於Linux系統，也支持FreeBSD、Cygwin（for Windows）和Windows Visual Studio，持續開發中。
- ns-3可以與其他外部軟體結合一起。一些模擬平台為用戶提供了圖形用戶界面環境。
- ns3目前已可提供的功能有：multiple interfaces on nodes、使用IP address和更多的802.11模組。開發者們也正開發一個可以將ns-2 modules轉移到ns-3的工具。

> Tom Henderson（華盛頓大學）領導的一個團隊、George Riley（喬治亞理工學院）、Sally Floyd（國際計算機研究中心）和Sumit Roy（華盛頓大學），申請並受美國國家科學基金會（NSF）資助，共同開發ns-2的替代品，被稱作ns-3。於此同時，INRIA Sophia Antipolis的Planete研究小組內的Mathieu Lacage和Walid Dabbous開始尋找一個ns-2的替代品，以用於測試IEEE 802.11Wi-Fi模型。Lacage原先使用的模擬器名叫Yet Another Network Simulator（yans）。

> 代碼主要由Mathieu Lacage編寫，並利用了部分yans模擬器、喬治亞理工學院網絡模擬器（GTNetS）及ns-2的代碼。Gustavo Carneiro貢獻了一個框架，包括生成Python綁定（pybindgen）及**使用Waf編譯系統。**

>2008年6月，ns-3發布了ns-3.1，之後項目在每個季度發布，直到最近變成了1年3次發布。ns-3在2012年第三季度發布了它的第15版（ns-3.15）。

:::success
**Waf系統**
>
這套軟體也是 python-base，所以修改時較Makefile簡單。同樣的，並不需要去「了解」Waf，只要會下指令、修改即可。
:::

### 模擬流程
1. **拓撲定義**：創建基本設施和相互關係，ns-3有指南能夠幫助完成此過程。
2. **模型使用**：添加模型（例如UDP、IPv4、點對點設備和連結、應用），大多數操作可通過指南完成。
3. **節點和連接配置**：設置模型默認值。例如，一個程序發送的包的大小和點對點連接的MTU值(Maximum Transmission Unit)。
4. **執行**：模擬事件，用戶請求數據。
5. **性能分析**：在模擬完成後帶有時間戳記(Timstamp)的事件跟蹤記錄可供使用。例如R語言分析並且得到結論。
6. **圖形可視化**：原始或處理過的數據能被工具使用，例如Gnuplot、matplotlib或是Xgraph畫出。
:::success
**時間戳記 Timstamp**
>
數位通訊裡面常會用到的一種術語。當你把資料取樣，然後一筆筆(packet)傳輸，當到達接收端時，你再把資料一筆筆照原來順序組合起來，就還原了原本的資料。問題是，傳輸過程並不是100%可靠的，一筆筆的資料有些可能會掉了，或是受到干擾而毀損，或是因為介質傳遞的關係而混亂了到達順序，所以通訊協定就需要能夠有效的處理這些問題。Timstamp就是處理這些問題的一個技巧之一。
>
例如，我們在源頭取樣的時候，就記下取樣時的"時間"，然後塞在要傳輸的資料裡，當我們在接收端接收到資料時，我們就可以把這個時間資料讀出來，就能知道接收到的這筆資料是屬於哪一個時間點的了。
有些通訊協定在傳輸資料時，因為編碼的緣故，不一定會照著原本取樣的時間或是順序傳遞，這時timestamp的功能就更重要了。
>
RTP是用來在網路上傳輸影音資料的通訊協定，我們也知道在網路傳輸封包時，封包會因為各種原因(如碰撞，路由等等)而影響到到達順序，所以在封包中加入時間戳記(timestamp)就可以讓接收端收到封包時可以正確的依照原本的取樣時間順序重組出正確的影音資料。
:::



- 目前三個版本的狀態：
  - ns-1 > 不再開發和維護。
  - ns-2 > 只維護。
  - ns-3 > 處於活躍的開發中。



- 參考資料 
  - http://louisman0723.blogspot.tw/2013/12/network-simulator-3.html
  - https://zh.wikipedia.org/zh-tw/Ns_(%E6%A8%A1%E6%8B%9F%E5%99%A8)
  - https://www.nsnam.org/documentation/
  - http://csie.nqu.edu.tw/smallko/ns2_old/ns2.htm