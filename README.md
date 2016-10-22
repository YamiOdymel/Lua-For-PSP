本文由gadget2k翻譯自http://www.evilmana.com/tutorials/lua_tutorial_01.php的網路上教學，轉載請註明。想進一步深造的，請學習下面的《Programming in Lua》（點此下載），這是對Lua的全面闡述。

# 1——起跑前的準備工作

本系列教學旨在幫助完全的編程新手學會使用lua腳本語言為PSP開發小型程式和遊戲。在開始之前我們需要做一些準備工作，雖然不都是非要不可，但是有了它們你會事半功倍。

譯者註：本教學全部學完了你也就是會爬而已。要學會走，甚至跑起來，就看你的熱情和毅力了！

LuaPlayer for PSP - 這是頭等大事，沒有它你的lua腳本就無法在PSP上執行。點此下載

LuaPlayer for Windows - 這是在PC上執行的LuaPlayer，寫好了腳本可以先在PC上檢驗，省得為了測試而在PC和PSP之間來回倒騰檔案。點此下載

> 譯者注1：該PC版本基於luaPlayer 0.20，LuaPlayer HM 5.0支援的新函數可能無法執行。

> 譯者注2：鍵盤與PSP按鍵的對應。SELECT = a，START = s，LTRIGGER = q，RTRIGGER = w，TRIANGLE = r，CIRCLE = f，CROSS = c，SQUARE = d，十字鍵 = 方向鍵

Notepad++ - 比windows自帶的notepad要強悍多的開源免費文本編輯器，可以高亮顯示多種程式語言，還具備自動完成功能，自動對程式碼樹級管理。點此下載

當然你也可以使用其他任何文本編輯器編寫腳本，包括Notepad。 （以前推薦的miro lua不如這個強，刪除。）

Windows版LuaPlayer的使用

解壓luaPlayerWindows.rar至硬碟。在luaplayer.exe所在目錄下，建立一個文本檔案，內容是

```
luaplayer script.lua
pause
```

將其存為script.cmd，確保不要存成txt後綴。這樣可以方便在PC上執行你的程式。其中luaplayer是指所在資料夾的luaplayer.exe，而script.lua則是你編寫的程式檔案名。Pause則是保證發生錯誤時命令列視窗不會關閉。這樣我們就可以為程式捉蟲。

注意：如果雙擊script.cmd檔案出現下述錯誤

> 'luaplayer' is not recognized as an internal or external command, operable program or batch file

那麼就用luaplayer.exe的全路徑替代luaplayer。例如：

```
"C:\Documents and Settings\Owner\Desktop\mygame\luaplayer.exe" 
script.lua
pause
```

現在我們使用Notepad（或者其他任何編輯器，例如ConTEXT） 再建一個文本檔案，命名為script.lua（註：如果你嘗試在PSP上執行該腳本發生“腳本未找到”錯誤時你可能需要將其改名為index.lua）。我們暫時就留空，下一講我們會讓你在其中編寫程式碼並測試它的。以後要讓Windows版LuaPlayer執行你的程式碼，很簡單，只要雙擊script.cmd檔案就行了。

# 2——編寫你的第一個Lua程序

現在我們開始為PSP編寫自己的第一個Lua程序。請謹記我們在整個教學中都會利用到LuaPlayer的Windows版，雖然有些東西在windows版上不能很好運行（例如音訊不是很好），甚或不能運行（例如LuaPlayer新增的一些函數），但是對於我們將要學習的東西來說，windows版還是足夠使用的。

LuaPlayer在PSP上的安裝一般來說把LuaPlayer文件夾放在PSP/GAME目錄下皆可。

任何時候你想要在PSP上測試你的程序的話，只要把你的script.lua文件複製到EBOOT.PBP所在目錄下，然後運行LuaPlayer即可。

首先用文本編輯器打開你的script.lua文件。我們的第一個程序很簡單，就是在螢幕上列印一些東西。讓我們開始吧！

## 註釋

我們第一件要學的就是如何給你的代碼做註釋。註釋是為了幫助其他人看懂你的代碼。相信我，這也能幫助你自己。在你停止一個項目幾個月後再回頭看自己的代碼，你會發現沒有註釋的話你會在自己的代碼中迷失！所以我們的新程序第一行以下列註釋開始：

```lua
-- 我的第一個 Lua 程序
-- 作者: 你的名字
```

正如你看到的，註釋以雙劃線開始（ -- ）。在此之後輸入的任何文字都不會被視為代碼，在執行時將被完全忽略掉。但是，請注意，你必須保持註釋在一行內。如果你用回車到了下一行，請記住也要用雙劃線起頭。參照我們上面給出的代碼，你應該已經知道怎麼做註釋了。不難吧，是不是？

> 譯者註：多行註釋以 --[[ 開頭，]] 結尾。如下：

```lua
--[[
*********************************************
* 廬~山~升~龍~霸 *
* 天~馬~流~星~拳 *
*********************************************
]]
```

## 建立一個色彩對象

接下來我們將建立一個色彩對象，以便列印文字到螢幕上。我們將為此指定一個特定顏色然後用於print命令。將下面的代碼加入到你的程序中，記得要另起一行。你也可以多空一行以便和上面的註釋隔開。

警告：Lua是區分大小寫的，也就是說所有命令必須按照我們顯示的大小寫輸入。例如下述代碼中如果“Color”被打成“color”的話將無法運行。

```lua
red = Color.new(255, 0, 0)
```

這樣我們就建立了一個色彩對象。我們使用RGB值指定顏色，並將其存為一個變數red。你可以通過任何圖像編輯程序獲得任意顏色的RGB值。變數 red 儲存了指定的色彩訊息，但是這不意味著只要把它換成“blue”就會變成藍色。變數名與其指代的顏色毫無關係。顏色來自RGB值。所以，你把red改成BigFatTurkey也沒有關係。如果你還是不理解何謂變數，不用著急。我們很快就會專門學習它的。

## 列印至螢幕

哈，到我們程序最精彩的部分了。我們將使用print命令列印一些文字到螢幕上。將下述代碼複製到你的程式碼末尾。

```lua
screen:print(200, 100, "Look! I made text appear!", red)
```

讓我們對此解析一下。screen:print就是告訴我們的程序列印一些東西到螢幕上。在其後的括號裡你看到有幾個數值。這些值稱為參數，每個函數所帶的參數其個數和類型都不同。對於print來說我們調用了4個參數。

它的語法結構: `screen:print( x, y, stringOfText, colorObject)`

* 第一個參數，x，告訴程序在距離螢幕左側多少像素的地方列印文字。

* 第二個參數，y，告訴程序在距離螢幕頂端多少像素的地方列印文字。

* 第三個參數，就是你打算讓程序列印的文字。記得用引號把文字括起來。

* 至於第四個...嘿，那就是我們早先建立的色彩對象red！這告訴程序使用紅色列印文字，該色彩是我們先前建立的。記住在print語句使用顏色之前你必須先建立它！

## 離屏快取轉至顯屏

下述代碼可能有點讓人迷惑。但是別擔心，即使你不完全理解它，也沒什麼關係。原樣照抄到你代碼的最後一行就是，象之前一樣。

```lua
screen.flip()
```

簡單的說，所有的東西都是先在屏下繪製的，所以我們必須使用此命令讓它顯示到螢幕上面。

## 一個循環？

沒錯，接下來我們要建立一個程序循環。它讓一段代碼循環執行直至某事讓它停止。在本例中使用循環是為了讓我們的程序不至於顯示完文字就結束。沒有這個循環的話，我們根本沒機會看到文字，因為程序結束的太快了。下面是代碼，我想你現在知道該放哪裡了吧。

```lua
while true do
    screen.waitVblankStart()
end
```

以後我們會深入探討循環的。現在你只要知道它必須在那裡！

到此我們的第一個程序完成！保存你的代碼文件，雙擊 `script.cmd` 運行你的程序。如果一切順利你應該在螢幕上看到你的紅色文本了。

# 3——寫一個使用變數的簡單程序

本課我們學習怎樣在程序中使用變數。變數是很重要的工具，將來也必然成為你最好的朋友。一言以蔽之，變數就是訊息的存儲容器，供你在程序中隨時調用。

現在我們就來寫一個使用變數的簡單程序。同時也學習一下Lua中的簡單算術。這次我們對每一行程式碼都給與註釋。

首先，讓我們再次以建立色彩對象開始，用來在螢幕上列印訊息。這次我們選用綠色。

```lua
-- 綠色色彩對象
green = Color.new(0, 255, 0)
```

接著就開始建立我們第一個變數吧。這將是一個存儲你出生年份的變數。請隨意替換1981為你自己的出生年份，事實上我也建議你這麼做！

```lua
-- 將出生年份存為變數 myBirthYear
myBirthYear = 1981
```

就是這樣！我們所做的就是取得數值1981（或是你使用的自己的出生年份）並將其保存在我們命名為myBirthYear的變數中。稍後我們在程序中將使用該變數。

現在移下一行再設一個變數用來存儲當前年份。

```lua
-- 將當前年份存為變數 currentYear
currentYear = 2008
```

現在讓我們建立一個略微不同的變數。

```lua
-- 建立一個空變數
myAge = nil
```

請注意這次我們為變數賦值為nil，就是表明該變數尚未賦值。我們會在稍後為此變數存入訊息。

那麼，我們最後再建立一個變數，向你表明變數除了存儲數值以外，也能存儲字串（文本）。注意文本要用引號括起來。

```lua
-- 在變數中存儲一些文字
someText = "My age is roughly "
```

到此我想你已知道如何建立變數了，那麼讓我們開始使用它們。我們將要做的就是使用我們的變數和一些基礎算術計算出你的年齡。開始添加下面的代碼到你的程序中吧：

```lua
-- 用 currentYear 減去 myBirthYear 並將結果保存在變數 myAge 中
myAge = currentYear - myBirthYear
```

這一步是提取myBirthYear中存儲的值，用currentYear的值減去，然後將結果保存在myAge變數中。這樣myAge就被賦予了值！

現在，讓我們使用上一講學到的print命令將我們的文本變數列印到螢幕上。

```lua
-- 列印文本變數至螢幕
screen:print(10,100,someText,green)
```

與我們上一講所做的唯一不同（除了顏色）在於我們這次列印的是變數的值，而不是直接的文本。請注意此處我們沒有使用引號。這句代碼將以綠色文本在x-10,y-100的位置列印someText變數中存儲的任何內容。

現在我們將在這句話的旁邊列印我們的年齡結果。我們得用一個新命令。要在 someText 的文本右側列印 myAge，我們可以使用雙句點（..）

這稱為“串聯”。那麼我們把剛才那一行程式碼略作修改如下：

```lua
-- 同時列印文本變數和年齡至螢幕
screen:print(10,100,someText .. myAge,green)
```

最後我們把screen.flip()和循環扔進代碼以結束程式。

```lua
-- 離屏快取轉至顯屏
screen.flip()
-- 不停循環
while true do
    screen.waitVblankStart()
end
```

保存你的程序，運行查看結果。

透過使用變數，我們只要改變myBirthYear的值，程序就可以自動計算出任何人的年齡。沒有變數的話，你就不得不修改很多行程式碼，有些程序甚至得上萬行。

本節課我們只用到了減法，很簡單，就是 - 符號。

* 加法請使用 +
* 乘法請使用 *
* 除法請使用 /

# 4——讓按鍵為你工作

本節可將教你如何接收PSP的按鈕輸入，並編寫一個按下不同按鈕顯示不同文本的簡單程式。如果沒有按鈕輸入，就沒有與使用者的交互，那可是相當無聊的。所以讓我們學習一下這方面的知識吧。我們會使用到之前的課程所教授的東西，包括變數。本節我們將減少註釋量，並介紹另一種使你的程式碼整齊的方法。這就是分區法。

首先我們為要使用的變數分一個區塊。很簡單，註釋中為區塊名稱加一些容易辨識的符號，例如星號，當然你也可以用自己的符號！

```lua
-- *******變數********
```

我們仍然需要一個色彩對象以便寫屏。如果你原意可以建立幾個不同的色彩對象，各占一行，以便今後使用。不過我把這件事留給你自己。我只打算建立一個。（早日學會自立可是好事情）

```lua
green = Color.new(0,255,0)
```

接下來我們要建立一些文本變數，以便存儲按下按鈕時將會列印的字串，內容是你按下了哪個按鈕。我們只為一半的按鈕建立變數。另一半我們直接用print命令列印出來。這有兩個好處：一、你可以鍛鍊變數的使用；二、你將看到這兩種方法對於小程式來說都不錯。我們將會用到十個按鈕，它們是方向按鈕，圖形按鈕，肩按鈕。

這次我們使用print命令的方法也會略有不同。當列印被按下的按鈕名稱時我們希望按鈕名稱顯示在雙引號裡，為了這個目的我們將使用單引號包圍文本字串，而不是雙引號。如果使用通常的雙引號，程式會以為字串在按鈕名稱之前結束。現在我們來建立5個變數（記得我說過只建一半吧）。

```lua
upPressed = 'You are pressing the "UP" button'
downPressed = 'You are pressing the "DOWN" button'
leftPressed = 'You are pressing the "LEFT" button'
rightPressed = 'You are pressing the "RIGHT" button'
LPressed = 'You are pressing the "L" button'
```

完成後我們繼續。還記得我們每次都用的那個循環吧。不想用了？！也好，是時候學點新東西了。你做的每個程式都將有一個主循環。該區塊的程式碼會反覆執行直到某個條件達成為止，不管這個條件是什麼。在循環內可以有數個要執行的程式碼模組。其中一些是每次循環都要執行的，另一些則會檢查是否條件滿足，然後決定執行與否。讓我們開始我們的循環。

```lua
-- *****主循環****** 
while true do
```

接下來的程式碼都在此循環內。下一行要添加的程式碼是件新事物，清屏。

```lua
screen:clear()
```

這個命令將清除螢幕上顯示的任何內容。每次循環螢幕都將首先被清空。順便提一下，循環的速度極快，你根本就不會察覺到！所以不清屏的話，我們列印的內容將在螢幕上層層堆疊，搞得很難看。讓我們接著學新東西。

```lua
pad = Controls.read()
```

簡單的說，這一句是在每次循環時獲取按鈕的輸入。同時請注意pad也是一個變數，你可以改用其他名稱，例如buttons。pad看起來挺標準，所以我們就不改了。

現在該學習你的第一個條件表達式了，if語句。相信我，這沒有它看起來那麼難。同時你還會學到按鈕的輸入命令。先把下面的程式碼寫到程式裡，然後我來解釋。

```lua
if pad:up() then screen:print(100,100,upPressed,green) end
```

這一句程式碼就是說“如果上鍵被按下，則用綠色列印變數upPressed所含的文本”。這將返回true或false值。每個if語句都以 if 開頭，然後給出要檢查的條件。此例中則是檢查是否上鍵被按下。然後跟隨在關鍵字 then 之後的內容則是如果條件為真要執行的程式碼。最後，每個語句都必須以 end 結束。語法簡單易懂，一目了然。今後我們還將深入討論它的。現在讓我們為其他三個方向按鈕和L按鈕添加程式碼。

```lua
if pad:down() then
    screen:print(100,100,downPressed,green)
end
if pad:left() then
    screen:print(100,100,leftPressed,green)
end
if pad:right() then
    screen:print(100,100,rightPressed,green)
end
if pad:l() then
    screen:print(100,100,LPressed,green)
end
```

現在為另5個按鈕加程式碼。這次我們直接在print語句裡包含要列印的文本，以練習不同的方法。

```lua
if pad:r() then
    screen:print(100,100,'You are pressing the "R" button',green)
end
if pad:triangle() then
    screen:print(100,100,'You are pressing the "TRIANGLE" button',green)
end
if pad:circle() then
    screen:print(100,100,'You are pressing the "CIRCLE" button',green)
end
if pad:cross() then
    screen:print(100,100,'You are pressing the "X" button',green)
end
if pad:square() then
    screen:print(100,100,'You are pressing the "SQUARE" button',green)
end
```

呼！現在讓我們結束循環。我們需要翻轉螢幕以便離屏快取的內容寫到顯屏上。注意，此處的end是終止我們的while循環。

```lua
screen.waitVblankStart()
screen.flip()
end
```

儲存檔案，複製到PSP上執行，按下按鈕看看吧！

> 譯者註：作者沒有提到模擬墊（搖杆）的控制，補充一個例程，見附件。點此下載

# 5——使用數據表編寫程式

Lua中的數據表（tables）很像變數。主要區別是數據表可以用來存儲多個數據，而變數只能存一個。你把它想像成一個帶有很多“抽屜”存放不同內容的容器就行了。你今後編寫的遊戲很可能會用到數個數據表。在Lua中使用數據表基本相當於其他程式語言中使用的數列（arrays）。本課我們還會順便學一些別的內容。

假設我們要寫一個小遊戲，共有5類敵兵，2個玩家。為此我們要讓程序知道這些角色的相關訊息。你覺得玩家和敵兵需要什麼訊息呢？我相信你會有成堆的想法，不過既然你是初學，還是簡單點好。首先敵兵得有生命值（health），這樣才能被殺死。因此我們需要給程序提供訊息以跟蹤敵兵的生命值。我們還需要訊息以區分我們使用的敵兵種類。對於玩家生命值自然也是不可少的。還要什麼訊息？比如玩家擁有的武器種類怎樣！有了這些訊息我們應該可以開始了。

現在開始數據表的學習。下文中的代碼只有我們明確說明的才需要添加到你的程序中去。因為本課我會給出幾個你並不需要的參考代碼。

數據表的定義方式：

```lua
tablename = { }
```

首先是數據表名（任何你喜歡的名字），然後是等號，然後是左右（開閉）角括號。這樣就建立了一個空的數據表。要為數據表賦值，只要把數據放進括號裡就行，用逗號隔開。這裡有個例子：

```lua
myTable = { 12, 14, 16, 18, 20 }
```

記住它的用法跟變數完全相同。只是看起來有點不一樣。現在叫你使用方法。數據表內的每個數據作為一個數列元素而被索引，這樣我們只需使用數據表名加上內有索引號的開閉中括號就能調用該數據。沒搞懂？！看看一下例吧：

```lua
luckyNumber = myTable[1]
```

此處我們將數據表的第一個數據的值（12）賦予了變數luckyNumber。再回看一下我們剛建立的數據表，總共有幾個數據在內？如果你說5就對了。第一個是12，第二個是14，依次下去。用上述方法我們可以輕鬆的調用裡面的數據。索引以 1 起始，而不像某些語言那樣以 0 開始。下面列出了該表所有可用的數據元素：

```lua
myTable[1]
myTable[2]
myTable[3]
myTable[4]
myTable[5]
```

到此我想你應該試著用數據表寫自己的程序了。還記得第一課我們學過列印一行到螢幕吧？現在不用變數，而是建立一個數據表並使用print命令將其中一個元素列印出來。你也可以用多個列印語句讓它列印數個或全部元素。但是記得要修改print命令的Y參數，不然就像我們之前說過的，列印結果會堆疊起來。你無需更改X參數，因為該參數只影響水平位置。程序不會自動列印到下一行，你必須告訴它這麼做。你必須告訴程序向下多少個像素，以避免交疊或相距太遠。就像你之前用變數列印時一樣做法，只不過這次換成數據表元素：tablename[number]。去嘗試一下吧，我發誓我會在這等你的！

好了，我希望你做得不錯。我還想指出，你可以先建立空的數據表，稍後再在程序中為它賦值。下面是一個範例：

```lua
myTable = { } myTable[1] = "apple" myTable[2] = "orange" myTable[3] = "banana"
```

你一定注意到了，賦值除了數字，字串也是可以的，只要你用引號括起來。

> 譯者註：此處你也看到不同語句可以寫在一行內，只要用空格分開就行了。當然這樣不利於閱讀，所以我建議最好還是分行寫。

接下來我們再學一個更複雜點的數據表。你可以給數據表原屬添加額外的屬性，有時又被稱為字典或類型。這是非常非常有用的，可以讓你的代碼齊整易讀。讓我們來看一個例子。我將建立一個空數據表並在下一行引入這一方法。

```lua
shirt = { }
shirt[1] = { color = "blue", size = "small" }
```

我們做的就是建立一個數據表，並在其中的shirt[1]元素中建立了另一個數據表。現在假設程序要獲取襯衫的顏色和尺寸。方法如下：

```lua
shirt[1].color
shirt[1].size
```

如果我們在print語句中或者任何其他命令中使用，shirt[1].color 的結果將是 blue，而 shirt[1].size 的結果將是 small。這個搭配不是很糟啦，不用想太多!

現在回到我們的程序上來。首先，我們要建立一個數據表存放我們的敵兵訊息。這包括敵兵的生命值和敵兵類型。這是我們程序的第一行程式碼（終於！），所以趕緊複製到新的script.lua文件中去吧。第一行仍舊是我們的老朋友，色彩對象。你可以隨意改用綠色以外的顏色。

```lua
green = Color.new(0, 255, 0)
Enemy = { }
Enemy[1] = { type = "gargoyle", health = 100 }
Enemy[2] = { type = "vampire", health = 100 }
Enemy[3] = { type = "goomba", health = 100 }
Enemy[4] = { type = "ghost", health = 100 }
Enemy[5] = { type = "zombie", health = 100 }
```

就是這樣。現在我們建立了5個敵兵元素，並告訴程序它們的種類和總生命值。現在添加關於玩家的代碼。

```lua
Player = { }
Player[1] = { weapon = "sword", health = 100 }
Player[2] = { weapon = "knife", health = 100 }
```

這樣我們的範例程序所需的訊息就都有了。請注意，在一個能移動的真正遊戲中，Player數據表將是存儲玩家在螢幕上所處位置的完美之處，敵兵則利用Enemy數據表。本例中不會有任何角色移動，所以我們還是留待以後再討論這個問題。我們將要做的是將玩家和敵兵的訊息列印到螢幕上，並在按下 X 鍵時取走敵兵的生命值。我們只選一個敵兵和玩家 1 做這件事。可憐的玩家 2 就得坐冷板凳了，還有除了敵兵 1 外的其他敵兵，等待下一個教學吧。

接下來我們就要進入我們的遊戲循環。其中我們還會用到按鈕的設置代碼，你應該還記得吧。複製下述代碼到你的程序：

```lua
while true do
pad = Controls.read()
```

現在添加清屏命令以便每次循環時清空螢幕。

```lua
screen:clear()
```

然後在每次循環中列印玩家的生命值和武器訊息到螢幕上。

```lua
screen:print(5,10,"Player 1 Health: " .. Player[1].health,green)
screen:print(5,20,"Player 1 Weapon: " .. Player[1].weapon,green)
```

以免你又迷失了，我們解釋一下。第一條print語句表明將在X坐標值5、Y坐標值10的地方列印，也就是距螢幕左端5個像素、頂端10個像素的位置。PSP的螢幕是寬480像素，高272像素。後面的"Player 1 Health: "即表明在該位置列印此字串，然後我們將數據表元素 Player[1].health 串聯（還記得嗎？）其後，這樣它的值將列印在該字串右側。還記得Player[1].health 裡存儲的是什麼嗎？你應該記得！最後，是我們用了數次的色彩對象。第二句在螢幕稍低的位置，就是第一行下方，用同樣的方法列印不同的訊息。

現在讓我們在螢幕另一側列印我們的敵兵訊息。添加下述代碼：

```lua
screen:print(250,10,"Enemy Health: " .. Enemy[1].health,green)
screen:print(250,20,"Enemy Type: " .. Enemy[1].type,green)
```

接下來我們使用按鈕輸入命令偵測X鍵是否按下，如果是則從敵兵生命值中減去5。添加下述代碼：

```lua
if pad:cross() then
Enemy[1].health = Enemy[1].health - 5
end
```

這是說如果 X 鍵按下則從 Enemy[1].health 元素的值中減去5。

最後，讓我們快取、翻屏並終止循環。添加下述代碼：

```lua
screen.waitVblankStart()
screen.flip()
end
```

保存運行，測試一下吧。然後趕緊回來！

啊喔，怎麼回事！敵兵的生命值下降太快了，都變成負值了！可不能在遊戲中這麼搞！這向你顯示了循環執行的速度有多快。我們可以修正它，僅在按下X鍵時減生命值，按住時不減。

首先在代碼頂端的數據表之前添上此行。在色彩變數之前或之後都可以。

```lua
oldpad = Controls.read()
```

其次找到代碼行 "if pad:cross() then" 更改如下：

```lua
if pad:cross() and oldpad:cross() ~= pad:cross() then
```

...最後，就在 screen.flip() 之後和 "end" 之前添加此行：

```lua
oldpad = pad
```

目前我們暫時不糾纏於細節。簡單的說，此代碼檢測你按下的按鈕是否上一循環相同，如果是，則“if”語句不會執行。~= 表示“不相等”。我們很快會學到運算符的。

保存運行，測試一下。

怎樣，運行的不錯，除了還會變成負數以外。正好，我們正要學習另一個運算符呢。

找到代碼行 "if pad:cross() and oldpad:cross() ~= pad:cross() then" 更改如下：

```lua
if pad:cross() and oldpad:cross() ~= pad:cross() and Enemy[1].health > 0 then
```

我們添加了 Enemy[1].health > 0 這個條件。 > 表示“大於”，可能你已經知道了。所以修改後的整行程式碼表示如果Ｘ鍵按下，並且沒有按住與上一循環相同的按鈕，並且敵兵的生命值大於０則執行隨後的語句（生命值減５）。注意要執行此代碼就必須所有條件都滿足。

保存運行，現在應該一切正常了。敵兵的生命值不會變得小於０。

本課到此為止。注意本課的重點是數據表。所以其他東西你不是完全理解也沒關係。該休息一下了，下節課再見。

# 6——利用表達式

其實我們之前的程式已多少用到了一些表達式，現在我們就深入的學習一下。有些我們已經熟悉了，比如“if”語句和“>”運算符。我們將編寫一個利用這些表達式的程式，它與我們上一次寫的很相似，只是更深一些。先建立一個新檔案，但暫時不要添加程式碼，除非得到明確告知，象上一講一樣。

首先要講的就是算術表達式，太簡單了，無非就是加減乘除而已。我也不多說了，舉例如下：

```lua
x = 3 + 5 -- 加法
y = 3 - 1 -- 減法
a = 4 * 5 -- 乘法
b = 10 / 2 -- 除法
c = 2 ^ 8 -- 乘方
```

不難吧，嗯？記住，我教你的都是基礎，我不會介紹每一個命令。等你學會了我傳授的，你就能自己查詢資料，學習我沒有教的東西了。

接著要講的是關係表達式。這是編程時超常用的，用來比較資料。返回真或假（又稱為布爾值）。下面是列表：

* == (相等) 
* ~= (不相等) 
* < (小於) 
* > (大於) 
* <= (小於或等於) 
* >= (大於或等於)

用這些就能檢查各種有用的訊息。例如，如果一個敵兵的生命值是0，他是不是就該死去了呢？或者檢查一下我們是否夠錢買下那把新劍！當然光靠這些運算符還是不行的，大多數情況下我們還需要下一組新的表達式。

我的最愛第一個，“if”語句。用來檢測某個條件是否為真，如果是則執行一段程式碼。還可以增加功能，如果條件不滿足則做另一件事。簡單的“if”表達式如下：

```lua
if <某條件> then
<執行某程式碼>
end
```

現在舉個現實的例子。假設有個程式設了兩個變數，myCash 和 itemCost。myCash 是我們擁有的金錢數，itemCost 則是我們想要購買的物品價格。在遊戲中我們需要檢查是否有足夠的錢購買該物品。如果有，則從總金錢數中扣除，列印一條已購買消息到螢幕上。如果錢不夠，則列印一則消息到螢幕，通知玩家不夠錢買。程式碼應該跟下面的差不多：

```lua
myCash = 253
itemCost = 100

if myCash > itemCost then
myCash = myCash - itemCost
screen:print(100,100,"Item Bought",blue)
else
screen:print(100,100,"Not enough money",blue)
end
```

讓我們分析一下。首先，我們設了兩個變數，告知我們有多少錢，和物品值多少錢。然後是我們的if表達式，其含義等同於 "if 253 > 100 then"，就是問變數 myCash 的值是否大於變數 itemCost 的值。如果是...則執行下一行，獲取 itemCost 的值並將其從 myCash 的值中扣除。換言之就是 253-100，然後將答案存於 myCash。接著下一行則是列印字串“Item Bought”至螢幕。在下一行我們用了"else"，即隨後程式碼將在 myCash 不大於 itemCost 時執行，在此情況下它將列印字串 "Not enough money" 至螢幕。最後，自然還是“end”，結束整個表達式。

在上例中，我們有足夠的錢購買那個物品。因此“else”段的程式碼不會被執行。許多時候你甚至不需要使用else，有時你則需要使用多個else。這種情況下你可以使用“elseif”。茲舉一例：

```lua
myNumber = 4
if myNumber == 1 then
screen:print(100,100,"Your lucky number is 1",blue)
elseif myNumber == 2 then
screen:print(100,100,"Your lucky number is 2",blue)
elseif myNumber == 3 then
screen:print(100,100,"Your lucky number is 3",blue)
else
screen:print(100,100,"Your number isn't very lucky!",blue)
end
```

這段程式碼檢查 myNumber 是否等於 1、2 或 3。如果是，則列印“Your lucky number is (number)”。但是如果 myNumber 不等於 1、2 或 3 則列印“Your number isn't very lucky”。注意，此例程可以簡單化，只用一個 else 無需 elseif，只要改成“if myNumber > 0 and myNumber < 4 then”即可。接下來就讓我們學一學“and”關鍵字和其他的知識。

如上所述，邏輯運算符可以用來比較多個事物。我們將學習其中兩個，“and”和“or”。還有一個“not”。

假設你在編寫一個角色扮演遊戲，有點象 Diablo 那種。遊戲的玩家角色想要裝備一把屠龍刀（Dragon Slayer）。你打算設定玩家只有達到20級且是戰士（warrior）類時方能裝備該物品。在程式開始我們建立一個數列存放這些訊息，例如：

```lua
Player = { }
Player[1] = { level = 15, class = "warrior", weapon = "knife" }
```

稍後我們的程式碼將檢查玩家是否有資格裝備該武器，如下：

```lua
if Player[1].level >= 20 and Player[1].class == "warrior" then
Player[1].weapon = "Dragon Slayer"
end
```

第一行檢查玩家的等級是否大於或等於 20，還有玩家的類別是否屬於戰士類。如果兩個條件都滿足，則玩家的武器就被設定為屠龍刀。如果只有一個條件滿足，則返回值為假，那麼武器就不會變更。在本例中，我們的玩家雖然的確是戰士類，但是等級只有15，沒有大於或等於 20，所以該玩家無法使用屠龍刀。你可以使用不止一個“and”，例如你可以這樣寫：

```lua
if hat == "blue" and shirt == "red" and age > 15 and state ~= "Florida" then
screen:print(100,100,"You are accepted!",yellow)
end
```

使用“or”的方法完全一樣，除了只需要其中一個條件滿足返回值即為真以外。例如：

```lua
myCar = "Mustang"

if myCar == "Corvette" or myCar == "Mustang" then
screen:print(10,20,"Nice car!",green)
end
```

本例檢查 myCar 是否等於 Corvette 或 myCar 是否等於 Mustang。二者只要有一個為真，程式就列印“Nice Car!”到螢幕上。myCar 不等於 Corvette 但等於 Mustang，所以返回值為真。

那麼，讓我們付諸行動吧。我們還是用上一講編寫的程式，用我們今天學的修改一下。現在打開那個檔案。什麼？你扔掉了？別著急，去下載上一講的附件吧。

上一講中，我們設定每次按下 X 鍵時減去敵兵生命值 5 點。本課我們將添加一些表達式，讓程式能在當前敵兵死亡時讓另一個敵兵上陣。我們還得檢查何時已無兵可用。

第一件要做的就是添加一個變數，告知我們正與之作戰的當前敵兵是哪個。我們會給該變數賦一個值。你該發現我們的敵兵數列有5個敵兵，由1至5分別索引。我們將用這些數字來指稱這些敵兵。在程式碼頂端，綠色變數的下面，添加此變數：

```lua
currentEnemy = 1
```

現在我們添加一些程式碼，檢查當前敵兵的生命值是否為 0，如果是則將 currentEnemy 變數的值遞增 1，但是只在該值不超過 5 的情況下，也就是最後一個敵兵。在你的 if pad:cross() 程式碼行之上添加此程式碼：

```lua
if Enemy[currentEnemy].health == 0 and currentEnemy <= 4 then
currentEnemy = currentEnemy + 1
end
```

注意，此處我們用 currentEnemy 變數替代了數列 Enemy 中的數字。這樣我們只要設定 currentEnemy 變數為正確的敵兵，那麼程式碼中任何使用 Enemy 數列的地方都可以使用currentEnemy，而無需檢查每個敵兵（(Enemy[1] Enemy[2] 等等...），這樣程式碼更自動化。有了“<= 4”的檢查項，currentEnemy 變數就不會超過 5。如此說來，我們得修改幾行程式碼。找到下面幾行：

```lua
screen:print(250,10,"Enemy Health: " .. Enemy[1].health,green)
screen:print(250,20,"Enemy Type: " .. Enemy[1].type,green)
```

修改為：

```lua
screen:print(250,10,"Enemy Health: " .. Enemy[currentEnemy].health,green)
screen:print(250,20,"Enemy Type: " .. Enemy[currentEnemy].type,green)
```

現在當敵兵變更時，程式會自動列印出正確敵兵的生命值和兵種。我們還需要修改下述兩行：

```lua
if pad:cross() and oldpad:cross() ~= pad:cross() and Enemy[1].health > 0 then
Enemy[1].health = Enemy[1].health - 5
```

修改為：

```lua
if pad:cross() and oldpad:cross() ~= pad:cross() and Enemy[currentEnemy].health > 0 then
Enemy[currentEnemy].health = Enemy[currentEnemy].health - 5
```

作為結束，我們將添加一些程式碼，如果5個敵兵都被殺死則列印“All enemies are dead”至螢幕。把這個程式碼置於主循環中列印敵兵生命值和類型的screen:print行下。

```lua
if currentEnemy == 5 and Enemy[currentEnemy].health == 0 then
screen:print(50,100,"All enemies are dead",green)
end
```

這段程式碼是說，如果當前敵兵編號是 5 且其生命值等於 0 則列印“all enemies are dead”。儲存你的程式碼，執行之。按下 X 直到一個敵兵死亡。然後下一個敵兵會上陣，一個跟一個，直到所有 5 個敵兵都被殺死為止。

我希望本課能對你今後的表達式學習有所幫助。

# 7——使用圖像

到目前為止，我們所有的程式均只使用了文本。我想下水前先濕濕腳比較好，有了基本編程知識，將使一切容易領會。在本節課中，我將介紹使用圖像，及一些獲取圖像訊息的命令。

至於我們打算編寫什麼？嗯，就做一個看起來真正象是遊戲的程式吧。它不會做任何華而不實或令人興奮的事情，但足夠應付本教學的目的了，圖像。我們這裡所學的只是眾多圖像命令的一部分。我們將在以後的教學裡進一步了解這些。你也可以自己在luaplayer的檔案中查詢。我們的作品將包括一個可移動的角色，他可以在螢幕中自由走動，但不能夠走出螢幕邊緣。

第一件事是將下面提供的圖像儲存到你的工作目錄。這些圖像只是做個樣本，你完全可以用自己的。LuaPlayer 可以載入 PNG 和 JPEG 圖像。大多數情況下我會使用 PNG 而不選 JPEG，尤其當你需要透明的時候。現在儲存這些圖像：點此下載

解壓至工作目錄。你應該有如下3個圖像：

* player.png
* grass.png
* flower.png

現在我們先回到教學的第一部分，稍後再編寫我們的程式碼。

載入圖像

要在lua中使用圖像，你必須先將其載入程式，並賦予一個變數（或資料表）。你可以在程式開頭這麼做，也可以稍後再做，這取決於你什麼時候需要該圖像。在我們待會要寫的程式碼中我們會在開始就預先載入圖像。這裡是一個載入圖像的範例：

```lua
grass = Image.load("grass.png")
```

這一句將載入圖像檔案 "grass.png" 並賦予變數 "grass"。要正確載入圖像你得確保該圖像與你的lua腳本檔案位於同一目錄。如果你把圖像放在一個子資料夾，例如 "Images"，你就得用 "Images/grass.png" 而不是 "grass.png"。大小寫也不要搞錯。image 的 I 要大寫，load 的 l 要小寫。載入圖像很簡單吧？！

顯示圖像

要在螢幕上真正顯示圖像並不比載入更難。這裡是完整命令：

```lua
screen:blit(x, y, Image source, [sourcex, sourcey, width, height], [alpha = true])
```

這裡有很多訊息要填！不是所有的參數都必要，中括號裡的如果你不需要你可以完全忽略。現在讓我們解釋一下。

程式碼起始的 screen:blit 是一個命令，它將圖像貼到螢幕上。

括號裡的內容是真正樂趣所在。

x 和 y 與 print 命令中的相同。指定圖像貼到螢幕上的位置。

Image source 指定要貼上的圖像。上文中我們載入了一個圖像叫 grass，所以我們可以用 grass 作為圖像源。

[sourcex, sourcey, width, height] 是可選的。用來載入某幅大圖的一部分。分片圖是個極好的例子。你可以載入一幅單圖，分成好幾個部分，使用此程式碼你可以只貼上其中的一部分。sourcex 和 sourcey 是要擷取區域開始點的 x 和 y 坐標值。這樣貼上的不是整幅圖，而是其中一部分。

width 和 height 是指圖像擷取區域的寬度和高度。

命令的最後是 alpha 參數。這是用來設定圖像的透明度的。如果設為 true 則圖像透明， 設為 false 則顯示原圖。

本課我們不會使用全部參數。

獲取圖像尺寸

獲取載入的圖像尺寸有時很有用，這要用下面兩個命令：

```lua
image:width()
image:height()
```

實際使用時，用你想獲取寬高的圖像變數名取代此處的“image”。例如，要獲取我們的grass圖像的寬度和高度，你可以用：

```lua
grass:width()
grass:height()
```

開始編寫程式

讓我們開始編寫我們的遊戲。第一件要做的就是載入我們的圖像。建立一個新檔案，輸入如下程式碼：

```lua
grass = Image.load("grass.png")
player = Image.load("player.png")
flower = Image.load("flower.png")
```

就這樣。我們已經把我們的三個圖像載入了程式。

現在我們來用用那些獲取圖像尺寸的命令。先輸入下列程式碼，然後我會解釋的。我還想提醒你，你如果自己手工輸入這些程式碼會比複製貼上的效果要好。這樣你會對這些命令記得更牢。不管怎樣，添加如下程式碼：

```lua
screenwidth = 480 - player:width()
screenheight = 272 - player:width()
```

這有什麼用嗎？我來解釋一下它的用途。這部分程式碼幫助我們讓玩家角色到達螢幕邊緣時停止，無論是往左或往右（水平方向）。我們知道PSP螢幕尺寸是480，但是如果我們設定螢幕邊界是480，我們的角色就會超出螢幕32個像素，因為角色是32像素寬。player:width() 獲取玩家圖像的寬度，也就是 32 像素。從螢幕的寬度和高度中扣除該值就可以讓角色圖像在螢幕邊緣停止。

接著我們來建立一個資料表以存儲玩家角色的訊息。此例程中需要的唯一訊息就是玩家在螢幕上的 x 和 y 坐標位。輸入如下程式碼：

```lua
Player = { } Player[1] = { x = 200, y = 50 }
```

這將存儲玩家在螢幕上的x、y位置。我們將讓玩家從 x 200、y 50 的位置開始。 

現在開始我們的主循環。輸入如下程式碼：

```lua
while true do
pad = Controls.read()
screen:clear()
```

在下一部分程式碼中我將引入一個新的循環命令。就是“for”循環。我先舉個例子讓你了解它的工作方式，無需放在你的程式碼中。這個例子透過使用一個小循環列印了5個玩家的武器。

```lua
for a = 1,5 do
screen:print(10, 10, Player[a].weapon, green)
end
```

要使用 for 循環，你要賦予一個臨時變數起始值和終止值。

在上文中我們說 "for a = 1,5 do"，這意味著建立一個循環，其變數 a 的起始值為 1，終止值為 5。你可以理解為“a 等於 1 至 5”。

然後在循環中我們要列印玩家的武器到螢幕上。

最後一行是 end 語句，必須使用以終止循環。

這樣，該循環將不斷重複直到 a 等於終止值，然後循環終止。第一次循環執行時 a 等於 1。下一次循環時 a 將等於 2，然後是 3，然後是 4，最後是 5。這樣就可以快速的將玩家 1 至 5 的武器都列印到螢幕上。當然。實際操作時你需要更改 print 命令的螢幕坐標，不然就都列印到一起去了。但是這展示了該循環的用法。在 for 循環中你也可以根據需要使用 if 語句。

我們將使用這個命令把我們的grass圖像平鋪在整個螢幕上。輸入下述程式碼，然後我會解釋。當然，如果要做一個帶卷軸之類的複雜遊戲，使用平鋪引擎將是更好的辦法，不過目前我們不需要用它。

```lua
for a = 0, 14 do
for b = 0,8 do
screen:blit(32 * a, 32 * b, grass)
end
end
```

這裡我們在一個 for 循環中巢狀了又一個 for 循環！這將把 grass 圖像貼到整個螢幕上。橫向貼 15 幅圖，縱向 9 幅圖。請注意，我們設定起始值為 0 而不是 1，這樣圖像會從螢幕最左邊貼起。

現在讓我們再貼一些圖像。

```lua
screen:blit(100,100,flower)
screen:blit(300,220,flower)
screen:blit(Player[1].x,Player[1].y,player)
```

這一段就是簡單的貼上兩幅 flower 圖像，還有 player 的圖像。很快，當我們使用移動按鍵時我們將在每次循環中讓玩家的坐標隨著按鍵的按下而改變。使用上述 blit 命令我們的 player 圖像將自動貼到螢幕的正確區域。 

現在讓我們加上那些按鍵，以檢測是否按下了方向鍵。輸入下述程式碼：

```lua
if pad:left() and Player[1].x > 0 then
Player[1].x = Player[1].x - 2
end

if pad:right() and Player[1].x < screenwidth then
Player[1].x = Player[1].x + 2
end

if pad:up() and Player[1].y > 0 then
Player[1].y = Player[1].y - 2
end

if pad:down() and Player[1].y < screenheight then
Player[1].y = Player[1].y + 2
end
```

這些程式碼將檢測我們是否按下了“上下左右”鍵。使用 and 語句同時確保我們沒有超出螢幕邊界。既然螢幕的最左側和最頂端的坐標是 0，我們只要檢查我們的位置是否大於 0 即可。其他部分我們使用 screenwidth 向右走，screenheight 則用來向下走。這些變數我們之前已建立。如果我們的位置透過了 if 測試，則玩家的 x 或 y 坐標遞增或遞減 2 點。每次主循環執行都會將 player 圖像貼到提供給它的新位置。

最後讓我結束循環。使用如下程式碼：

```lua
screen.waitVblankStart()
screen.flip()
end
```

儲存你的工作，執行吧。使用方向鍵讓角色在螢幕上穿梭。你應該是無法穿越螢幕邊緣的。

# 8——使用函數

本課我們將學習怎麼使用函數。建立一個函數相當於新建一個屬於你自己的Lua命令。你可以將經常使用的代碼放進函數中，這樣你就可以隨時調用了。函數放在主循環之外。一般放在代碼開頭的變數聲明附近比較好。

首先讓我們看一下函數是怎麼聲明的。檢查下面代碼：

```lua
function functionName()
(函數中要執行的代碼。
可以使用多行程式碼。)
end
```

這就是函數的構成方式，讓我們看看下面的範例函數，它將在每次調用時列印一條簡單的消息到螢幕。

```lua
function printMessage()
screen:print(100,100, "Functions are fun!")
end
```

現在，要想在程序中列印這條消息，就必須在要使用的地方調用這個函數。就上例而言使用下述代碼就可以調用該函數，將函數的代碼執行一次。

```lua
printMessage()
```

這麼簡單？！呣...恐怕就是這樣！使用上述代碼將會執行我們先前建立的函數代碼。通過調用 printMessage() 就可把 "Functions are fun!" 列印到螢幕上。

當你開始編寫更複雜的程序或遊戲時，你將會大量使用函數。在你的主循環中調用函數而不是實際的代碼將使你的代碼更加整齊易懂。之前我說過函數放在主循環外面，這是對的。但是，從主循環內調用它們是沒問題的。

函數也可以建立來返回一個值。建立函數時加個括號和參數就行。比如說，我們要建個函數將兩個數值加起來並把結果返回。首先我們得建立這個函數。看下面：

```lua
function additUp(a, b)
sum = a + b
return sum
end
```

請注意，在括號中我們放了字母 "a" 和 "b"，其實你可以用任何字母或者甚至單詞。它們是用於本函數內部的變數，也只存在與本函數中。因為我們打算將兩個數相加，所以我們需要兩個變數來存儲。在你的函數中可以使用任意多個變數，只要你用逗號分開它們。

然後我們在函數中建立了一個變數叫 "sum"，它將被賦予變數 "a" 和 "b" 相加的數值。等你看到它的調用就會更清楚了。接下來我們使用了一個命令 return，它告訴函數一旦我退出函數將返回一個值給此函數。我們現在要返回的是變數 "sum" 的值。最後，我們 end 了我們的函數。

現在讓我們看看如何使用這個函數，再做一些解釋。看如下代碼：

```lua
screen:print(100,100,additUp(5,6), green)
```

這將把我們函數的結果列印到螢幕上。請注意，在調用函數時我們使用了實際的數值。此例中我們使用了 5 和 6。就是說將數值 5 賦值給 a，數值 6 賦值給 b。現在在我們先前建立的函數內，任何 a 或 b 被使用的地方，都將被我們實際賦予的數值代替。所以函數中 "sum = a + b" 這句話將被解析為 "sum = 5 + 6"。這將把 11 這個數值賦予 "sum" 變數然後返回給我們的 print 命令，列印到螢幕上。

如果需要我們也可以將此訊息存在一個變數中。這樣我們就不必在不需要的時候不得不立即使用它，或者在以後重複使用時不用每次都跑一遍整個函數。請看下面：

```lua
myTotal = additUp(5,6)
```

這句代碼就把我們函數的返回值存儲在變數 myTotal 裡。myTotal 將等於 11。

讓我們看一下上一講我們編寫的程序。代碼應該與下面的類似：

```lua
grass = Image.load("grass.png")
player = Image.load("player.png")
flower = Image.load("flower.png")

screenwidth = 480 - player:width()
screenheight = 272 - player:width()

Player = { }
Player[1] = { x = 200, y = 50 }

while true do
pad = Controls.read()
screen:clear()

for a = 0, 14 do
for b = 0,8 do
screen:blit(32 * a, 32 * b, grass)
end
end

screen:blit(100,100,flower)
screen:blit(300,220,flower)

screen:blit(Player[1].x,Player[1].y,player)

if pad:left() and Player[1].x > 0 then
Player[1].x = Player[1].x - 2
end

if pad:right() and Player[1].x < screenwidth then
Player[1].x = Player[1].x + 2
end

if pad:up() and Player[1].y > 0 then
Player[1].y = Player[1].y - 2
end

if pad:down() and Player[1].y < screenheight then
Player[1].y = Player[1].y + 2
end

screen.waitVblankStart()
screen.flip()
end
```

我們可以建立一些函數，讓主循環看起來更乾淨整齊一些。我們可以將所有的方向鍵檢查放入一個函數，還可以將螢幕繪製的代碼放入一個函數。這兩個都不需要返回值。看看下面的代碼，了解函數的使用：

```lua
grass = Image.load("grass.png")
player = Image.load("player.png")
flower = Image.load("flower.png")

screenwidth = 480 - player:width()
screenheight = 272 - player:width()

Player = { }
Player[1] = { x = 200, y = 50 }

-- Function to check player movements
function playerMovement()
pad = Controls.read()
if pad:left() and Player[1].x > 0 then
Player[1].x = Player[1].x - 2
end

if pad:right() and Player[1].x < screenwidth then
Player[1].x = Player[1].x + 2
end

if pad:up() and Player[1].y > 0 then
Player[1].y = Player[1].y - 2
end

if pad:down() and Player[1].y < screenheight then
Player[1].y = Player[1].y + 2
end
end

-- Function to paste images to screen
function pasteImages()
for a = 0, 14 do
for b = 0,8 do
screen:blit(32 * a, 32 * b, grass)
end
end

screen:blit(100,100,flower)
screen:blit(300,220,flower)

screen:blit(Player[1].x,Player[1].y,player)
end

-- Main Loop
while true do

screen:clear()

pasteImages()

playerMovement()

screen.waitVblankStart()
screen.flip()
end
```

你看，我們的主循環乾淨許多了吧。所有複雜的、細節的代碼被放到了函數裡，而在主循環中我們只需調用它。原先代碼中混在循環中的一堆代碼都被移走，放到了代碼頂端。

我希望這能幫助學習有關函數使用的知識。以後的教學我們將使用函數了。

# 9——讀寫檔案

本課我們將學習如何讀取檔案和寫入檔案。這對於製作遊戲來說是很有幫助的。你可以調用別的檔案中的程式碼，也可以儲存最高分、遊戲存檔、玩家狀態等訊息到檔案裡……

我們這就開始吧！

首先，讓我們看一個簡單的命令：dofile。

這個命令會讀入另一個檔案的程式碼並立即執行。

```lua
dofile("./test.lua")
```

很簡單的命令。注意 ./ 是指根目錄，不是子目錄。如果是子目錄，應該這樣用：

```lua
dofile("./files/test.lua")
```

那麼，如果我們的檔案 test.lua 包含下述程式碼：

```lua
playerx = 10
playery = 20
enemyx = 40
enemyy = 50
```

...則一旦我們用 dofile 調用這個檔案，這些變數將立即得到聲明。檔案不是非得用 lua 後綴，txt 或其他後綴都可以。

從檔案中讀取一行：

假設你有一個很多行文本的檔案，你想從中讀取一行，並列印到螢幕上。為此我們可以使用 io.open() 命令打開檔案並讀取。

命令的語法是 io.open(filename, mode)。此處我們將使用 r 作為 mode 的值，意指讀取（read）模式。
作為參考，下面是所有可用模式的列表：

* r - 讀取模式 
* w - 寫入模式(覆蓋現有內容) 
* a - 附加模式(附加在現有內容之後) 
* b - 二進位制模式
* r+ - 讀取更新模式(現有資料保留) 
* w+ - 寫入更新模式(現有資料擦除) 
* a+ - 附加更新模式(現有資料保留，只在檔案末尾附加)
  第一件要做的事情就是打開檔案並存為一個變數。看下面。

```lua
file = io.open("testRead.txt", "r")
```

現在我們的檔案 testRead.txt 已打開並處於讀取模式。接著我們使用 read() 命令讀取檔案中的單行內容存為另一個變數。

```lua
ourline = file:read()
```

這將讀取我們的文本檔案的第一行。下一次我們使用 read() 命令它將讀取第二行。再下一次它會讀取第三行，依此類推。

請注意，此命令前的 file 是我們之前打開檔案並儲存的變數名，你可以使用任何其他名字。file.read() 還可以使用下列任一個參數，只要用引號括起來放入括號裡就可以。

* *n - 讀取一個數字並返回它。例：file.read("*n") 
* *a - 從當前位置讀取整個檔案。例：file.read("*a") 
* *l - (預設) - 讀取下一行，在檔案尾 (EOF) 處返回 nil。例：file.read("*l") 
* number - 返回一個指定字元個數的字串，或在 EOF 時返回 nil。例：file.read(5)
    既然我們已經讀取到所要的那一行，我們需要關閉打開的檔案，像這樣：

```lua
file:close()
```

現在要列印我們的檔案至螢幕我們只要這麼做：

```lua
screen:print(10,10,ourline,white)
```

讀取所有行

要讀取一個檔案的所有行，你可以在一個 for 語句中使用上述技巧。請看下述程式碼：

```lua
y = 10

file = io.open("testRead.txt","r")

for line in file:lines() do
y = y + 10
screen:print(100,y,line,white)
end

file:close()
```

這個程式碼設定了一個起始值 y 用於列印，這樣它可以在螢幕不同的縱坐標列印每一行。照例，先打開檔案。然後是 for 語句，這句程式碼是說檔案的行數有多少下面的程式碼就執行幾次。我們的 y 坐標則每次循環加上 10 以便列印命令可以列印下一行。

寫入檔案（覆蓋）

寫入檔案的方式大致相同。下面的程式碼將覆蓋任何先前寫入檔案的內容：

```lua
file = io.open("testRead.txt","w")
file:write("hello")
file:close()
```

注意，我們這次使用了 w 模式，而不是 r 模式，因為我們是要寫入而不是讀取。我們用 file:write() 寫入括號裡作為參數的、用引號括起來的文本。你也可以用變數替代。如果你使用變數就不要用引號，請看一下例：

```lua
file = io.open("testRead.txt","w")
myText = "Hello"
file:write(myText)
file:close()
```

寫入檔案（附加）

你可以使用附加模式，這樣就可以在寫入檔案時將新內容附加在已有文本末尾，而不是刪除原來的。做法與上面基本相同，除了模式換成“附加”之外。請看程式碼：

```lua
file = io.open("testRead.txt","a")
myText = "\nHello"
file:write(myText)
file:close()
```

注意到另一個區別沒？在 myText 變數裡我們為字串添加了 \n 。這個命令代表換行，這樣寫入的文本將從下一行開始。雖然在你的檔案中可能顯示為同一行只是中間隔了一個方塊，但是技術上它是新的一行。在 C/C++ 語言中也是這麼用的。

將你所學的知識用在自己的小程式上吧。

我們的下一講將討論音訊的處理，也會使用我們此處所學的讀寫檔案的命令做一個小程式。

# 10——應用音訊

現在該是時候給我們的項目加點響聲了。任何遊戲都需要聲音，這一講我們就來學學如何在Luaplayer中發聲。開始上課!

luaplayer 可以播放如下音樂格式*：UNI, IT, XM, S3M, MOD, MTM, STM, DSM, MED, FAR, ULT 或 669，WAV 檔案可用作聲音。MIDI可以先轉換為上述格式再使用，比如 Modplug Tracker 就可以轉。請記住 luaplayer 不支援 mp3 檔案*。在學習了一些音訊命令之後我們將結合之前的成果建立一個小程式。

> 譯者註：此說法已過時，目前luaplayer已支援mp3,ogg，aa3，oma，omg，詳見HM版相關函數。但是由於luaplayer目的在於編遊戲，所以對mp3播放的支援程度不高。

先來看第一個命令，此命令將播放一個音樂檔案。

```lua
Music.playFile( string file, bool loop )
```

此處的“string file”是指你的音樂檔案名，例如“song.xm”。“bool loop”處放置“true”或者“false”。設“true”則一直循環播放該音樂，“false”則只播一遍。下面是個放歌的範例：

```lua
Music.playFile("mysong.mod", true)
```

接下來看看這個命令。它們是在開始播放音樂之後使用的：

```lua
Music.pause()
Music.stop()
Music.resume()
```

這些命令不用解釋你也能看懂。

* Music.pause() 將暫停歌曲播放。
* Music.stop() 將停止歌曲播放。
* Music.resume() 將恢復播放被暫停的歌曲。

還有一個命令是用來偵測一首歌是否正在播放。這將返回 true 或 false。看一下：

```lua
Music.playing()
```

假如說我們想偵測我們的歌曲是否在播放，如果是則列印一條消息到螢幕。我們可以這樣做：

```lua
if Music.playing() == true then
screen:print(10,10,"Music is playing",white)
end
```

還有一個命令是用來設定音樂檔案的音量的。只要在括號中填入一個數值，範圍在 0 至 128 之間。下面是命令格式：

```lua
Music.volume(Number)
```

現在讓我們學學用於音效的聲音檔案，尤其是 wav 檔案。這和播放音樂檔案有些區別。下面是如何載入一個聲音：

```lua
bonkSound = Sound.load("bonk.wav",false)
```

wav 檔案作為一個變數被載入，稍後我們就可以用這個變數來指稱該聲音。此處我們設“false”是以防循環播放。記住設為“true”將循環播放，如果你的確是這麼想的話。

關於 WAV 檔案的一個要點是，在 luaplayer 中只能使用單聲道的，立體聲的不行。你可以透過右鍵點擊檔案查看其屬性的摘要頁來確認這一點。

現在讓我們來再學一些命令。下個命令是播放該檔案。使用你載入聲音時設的變數名。如下：

```lua
bonkSound:play()
```

但是我不建議你這樣播放聲音檔案。這會導致一個常見錯誤，類似“loop ingettable(無法取得循環)”之類消息。下面是我播放聲音檔案的方法。不同之處就是用另一個變數取代 bonkSound。

```lua
local sound = bonkSound
voice = sound:play() 
--要停止聲音使用：
voice:stop()
```

還有一個命令與音樂檔案的命令類似，偵測聲音是否正在播放。命令如下：

```lua
voice:playing()
```

還有一些聲音和音樂方面的命令等待你去探究，但是這些已足夠你使用聲音和音樂了。

現在我們開始做一個小東西。我們將以一個選單螢幕為起始，用來選擇藍色還是黑色背景。按下 X 時程式會往下執行，而背景色已按照我們的選擇設好。此處我們的程式將顯示其已被執行多少次。怎麼做？嗯，就是每次在選單螢幕按下 X 時程式就打開一個檔案（我們稍後會建立），然後寫一個數字進檔案。程式也會從該檔案中讀取該數字並儲存在一個變數中。如果你完全退出程式然後再返回，它仍然能顯示被執行了多少次，因為這個資料已存在一個檔案裡了。那麼，讓我們忙起來吧。

首先，我想要你用notepad或任何其他編輯器建立一個普通的txt檔案。在該文本檔案中輸入數字 0。儲存為 counter.txt。就是一個普通的文本檔案。

然後開始編寫我們的 lua 檔案。先建立一些要用到的色彩對象：

```lua
white = Color.new(255,255,255)
blue = Color.new(0,0,255)
black = Color.new(0,0,0)
```

接著是一些變數。

```lua
oldpad = Controls.read()
startcolor = black
gamestate = "menu"
```

* oldpad 將儲存我們上一次按下的按鍵。
* startcolor 存儲我們稍後將在程式第二部分使用的顏色。我們以 black 開始。
* gamestate 則是用來查看該使用哪個函數。我們將建立兩個函數。一個是顯示選單的，另一個執行程式餘下的工作。既然我們從選單開始，該變數的起始值就如此設定。

下一部分就要處理聲音了！首先，請下載兩個小小的 WAV 檔案，放在程式所在目錄下。

現在讓我們在程式中載入這些 wav 檔案。我們不想讓它們循環，所以使用 false。

```lua
menusound = Sound.load("beep.wav",false)
goodbye = Sound.load("goodbye.wav",false)
```

夠簡單吧！還記得上一講的那些檔案命令嗎？我們來次回顧吧。此處我們將打開我們之前建立的 counter.txt 檔案，並從中讀取數值存入變數 counter 中。

```lua
file = io.open("counter.txt", "r")
counter = file:read("*n")
file:close()
```

請注意我們使用了"*n"以讀入一個數字。

接著我們將建立一個資料表，用於我們的起始螢幕選擇器。這會包含一個我們建立來用作選擇器的圖像，以及它的 x 和 y 坐標值。資料表下一行的命令則將我們的選擇器圖像以藍色清空。程式碼如下：

```lua
selector = { image = Image.createEmpty(145,15), x = 147,y = 77 }
selector.image:clear(blue)
```

現在我們建一個稱為 drawMenu() 的函數，執行選單所有的必要任務。下面是起始行：

```lua
function drawMenu()
```

我們將把此函數用作一個循環函數，所以每次循環我們先清屏然後讀取按鍵的輸入。程式碼如下：

```lua
screen:clear()
pad = Controls.read()
```

接下來我們將把我們的選擇器繪製(blit)到螢幕上，並列印兩行字。程式碼如下：

```lua
screen:blit(selector.x,selector.y,selector.image)
screen:print(150,80,"Start Game (Black)",white)
screen:print(150,100,"Start Game (Blue)",white)
```

請注意我們是怎麼使用資料表的值來繪製選擇器到螢幕上的。這個選擇器圖像將會上下移動以高亮顯示被選擇的選單項。要確保在列印文字之前繪製，否則圖像將覆蓋文字。

列印的兩行字則是我們給玩家的選項。要麼以黑色螢幕開始遊戲，要麼是藍色的螢幕。

在函數的下一部分將檢測按鍵是否按下。先做上鍵的部分吧。

```lua
if pad:up() and oldpad:up() ~= pad:up() then
selector.y = 77
startcolor = black
local sound = menusound
voice = sound:play()
end
```

第一行是說如果上鍵被按下並且不是最後被按下的按鈕則.....

第二行將 selector 的 y 值設定為 77。這是為了在文本周圍貼上圖像以便看起來像是被選擇的。
然後設定 startcolor 為 black。

接著使用我之前建議的方法播放 menusound 這個 wav 檔案。

現在處理下鍵。程式碼與上面很相似，除了圖像向下一點，顏色改為藍色以外。程式碼如下：

```lua
if pad:down() and oldpad:down() ~= pad:down() then
selector.y = 97
startcolor = blue
local sound = menusound
voice = sound:play()
end
```

現在來處理 X 按鈕。

```lua
if pad:cross() and oldpad:cross() ~= pad:cross() then
gamestate = "game"
counter = counter + 1
file = io.open("counter.txt","w")
file:write(counter)
file:close()
end
end
```

此處我們將 gamestate 設為“game”以便選單的程式碼不再執行（在我們編寫了後面的程式碼之後）。我們以 1 為基數遞增 counter 變數。然後打開 txt 檔案，寫入 counter 的新值，取代檔案裡的舊值。不要忘了關閉檔案。

注意，多出來的那個 end 是用來終結函數的。這個函數已完成了！

我們下一個函數將執行離開選單後的遊戲程式碼。這個函數相當小巧簡單，全部程式碼如下：

```lua
function playGame()
screen:clear(startcolor)
pad = Controls.read() 
screen:print(100,100,"This program has been executed " .. counter .. " times.",white)
screen:print(100,110,"Press Start to exit to Menu",white)

if pad:start() then
gamestate = "menu"
local sound = goodbye
voice = sound:play()
end
end
```

在此函數中，請注意我們使用了在選單中透過 startcolor 變數選擇的顏色清屏。列印了兩個消息，檢查了 start 按鍵的按下。按下 start 鍵將把 gamestate 設回 menu 並播放一個 wav 檔案。

接下來開始我們的程式主循環。由於使用了函數，此處很簡短。在循環中我們將檢查遊戲的狀態並執行該狀態的函數。程式碼如下！

```lua
while true do

if gamestate == "menu" then
drawMenu()
end

if gamestate == "game" then
playGame()
end

screen.flip()
oldpad = pad
end
```

...接下來... Oh yeah！已經完成啦！執行試試看吧。
