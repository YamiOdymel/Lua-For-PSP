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
