

## 圖表策略

在此章節之前，Primer 已涵蓋如何實施 Dynamo 的強大可視腳本功能。充分瞭解這些功能是重要的基礎，以及建置功能強大的視覺程式的第一步。當我們實際使用視覺程式、將其與同事共享、疑難排解錯誤或測試限制時，我們將需要處理其他問題。如果其他使用者將使用您的程式，或您預期六個月後將會打開它，程式則需要有直接、清晰的圖形和邏輯。Dynamo 有多個工具可管理您的程式的複雜性，本章節將提供有關何時使用它們的準則。

![群組](images/13-2/cad-chart-visual.jpg)

### 減少複雜性

當您開發 Dynamo 圖表和測試您的想法時，它的大小和複雜性可快速增加。建立可運行的程式和建立簡單的程式同樣重要。圖表不僅更快且更有預測性地執行，您與其他使用者亦將瞭解其邏輯。以下幾種方法可協助您闡明圖表的邏輯。

#### 模組化群組

* 群組可讓您在建置程式的時候**建立不同功能的部分**
* 群組可讓您**調動程式的大型部分**，同時保持模組性與對齊
* 您可以變更**群組的顏色以便區分**群組執行的內容 (輸入 vs 函數)
* 您可以使用群組來**組織圖表，以簡化自訂節點的建立**

![群組](images/13-2/groups.png)

> 此程式中的顏色用於識別每個群組的目的。此策略可用於建立任何您開發的圖形標準或樣板裡的架構。

> 1. 函數群組 (藍色)
2. 輸入群組 (橘色)
3. 腳本群組 (綠色)
> 若要瞭解如何使用群組，請參閱[〈管理您的程式〉](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html)。

#### 使用 Code Block 有效地開發

* 有時，您可以使用 Code Block，以**快於搜尋的方式輸入數字或節點方法** (Point.ByCoordinates、Number、String、Formula)

* **如果您要在 DesignScript 定義自訂函數以減少圖表中的節點數量**，Code Block 則非常有用

![codeblock](images/13-2/codeblock.png)

> 1 和 2 均執行相同的功能。寫入數行程式碼遠遠比搜尋並加入每個個別節點更快。Code block 也會更精確。

> 1. 使用 Code Block 編寫的設計腳本
2. 節點中的相等程式
> 若要瞭解如何使用 Code Block，請參閱[〈什麼是 Code Block〉](http://primer.dynamobim.org/en/07_Code-Block/7-1_what-is-a-code-block.html)。

#### 使用 Node to Code 進行壓縮

* 您可以**使用 Node to Code 減低圖表的複雜性**，它會集合簡單的節點並在單一的 Code Block 裡寫入與其對應的 DesignScript。
* Node to Code 可以** 壓縮程式碼，而不會減低程式的清晰度**
* 以下是使用 Node to Code 的**優勢**：
* 輕鬆地將程式碼壓縮為仍可編輯的元件
* 可以簡化圖表的重要部分
* 如果不會對「小型程式」進行頻密的編輯，它將會很有用處
* 用於整合其他 code block 功能，如函數

* 以下是使用 Node to Code 的**缺點**：
* 一般命名使其不易辨認
* 其他使用者比較難以瞭解
* 較難返回視覺程式版本

![nodetocode](images/13-2/nodetocode.png)

> 1. 既有的程式
2. 從 Node to Code 建立的 Code Block
> 若要瞭解如何使用 Node to Code，請參閱[〈設計腳本語法〉](http://primer.dynamobim.org/en/07_Code-Block/7-2_Design-Script-syntax.html)。

#### 使用 List@Level 存取資料彈性

* 使用 List@Level 可以協助您**取代可能會佔用大量圖元區空間的 List.Map 和 List.Combine 節點，從而降低圖表的複雜性**。
* List@Level 是**比 List.Map/List.Combine 更快的建構節點邏輯的方法**，可讓您從節點的輸入連接埠存取清單中任何層級的資料。

![listatlevel](images/13-2/listatlevel.png)

> 我們可以透過啟用 CountTrue「清單」輸入的 List@Level 來確認 BoundingBox.Contains 在哪些清單中傳回多少 True 值。List@Level 可讓使用者決定輸入將在哪個層級取得資料。使用 List@Level 更為彈性、有效，強烈建議您以它來取代涉及 List.Map 和 List.Combine 的其他方式。

> 1. 計算 List Level 2 的 true 值
2. 計算 List Level 3 的 true 值
> 若要瞭解如何使用 List@Level，請參閱[〈清單的清單〉](http://primer.dynamobim.org/en/06_Designing-with-Lists/6-3_lists-of-lists.html#list@level)。

### 保持可讀性

除了使圖表更為簡單和高效外，您亦應致力於維持它的清晰度。即使您盡最大的努力讓圖表擁有直覺式的邏輯分組，關係仍然可能不會立即顯現。在群組裡加入簡單的註記或更名滑棒可以幫助您或其他使用者避免不必要的混淆或橫跨圖表的麻煩。以下幾種方法可協助確保您的圖表的一致性。

#### 視覺連續性與對齊節點

* 為減少您在完成建構圖表的後續工作，您應該**時常對齊節點**以嘗試確保節點配置易於辨認
* 如果其他人將會處理您的圖表，您應**確保節點配線的配置在傳輸前能夠輕鬆地流動**
* 為了協助您對齊，**請使用「清理節點配置」功能以自動對齊**圖表，即使它未能如您自己手動對齊般精確

![定線](images/13-2/alignment.png)

> 1. 未組織的圖表
2. 對齊的圖表
> 若要瞭解如何使用節點的對齊方式，請參閱[〈管理您的程式〉](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html)。

#### 透過更名以進行描述性標示

* 更名輸入可協助他人輕鬆瞭解您的圖表，**尤其是當他們插入的不會在螢幕上顯示**
* **慎防更名節點。**另一種替代方法是從節點叢集建立自訂節點並對其進行更名；這會被瞭解為它包含其他內容

![輸入](images/13-2/inputs.png)

> 1. 操控曲面的輸入
2. 建築參數的輸入
3. 排水模擬腳本的輸入
> 若要更名節點，在其名稱上按一下右鍵，然後選擇「更名節點...」。

#### 使用註記進行解釋

* 如果**圖表需要節點未能表達的普通語言說明**，您應該加入註記。
* 如果**節點集或群組太大或太複雜，並且無法輕鬆瞭解**，您應該加入註記。

![註解](images/13-2/notes.png)

> 1. 註記描述傳回原始轉換距離的程式部分
2. 註記描述對映這些值至正弦波形的程式碼
> 若要瞭解如何加入註記，請參閱[〈管理您的程式〉](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-4_best_practices.html)。

### 連續地調整

建置視覺腳本時，請務必確認所傳回的與您所預期的相符。並非所有錯誤或問題都會導致程式立即失敗，尤其是可能會影響下游遠處的 null 或零值。此策略亦在 [撰寫腳本策略](http://primer.dynamobim.org/en/12_Best-Practice/13-2_Scripting-Strategies.html)中以文字腳本的層面討論。以下練習將有助於確保您取得預期的內容。

#### 使用觀看和預覽標示圈監視資料

* 建立程式時，使用觀看或預覽標示圈以**確認關鍵輸出傳回您所預期的內容**

![watch](images/13-2/watch.png)

> Watch 節點被用於比較：

> 1. 原始轉換距離
2. 通過正弦方程式的值
> 若要瞭解如何使用 Watch，請參閱[〈資源庫〉](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-2_dynamo_libraries.html)。

### 確保可重複使用性

即使您獨立工作，其他使用者亦很有可能會開啟您的程式。他們應該可以快速瞭解程式需要，以及使用程式的輸入與輸出執行作業。如果開發自訂節點是為了與 Dynamo 社群共用和用於其他人的程式，這點尤其重要。這些做法導致強大的、可重複使用的程式和節點。

#### 管理 I/O

* 若要確保易讀性和可調整性，您應嘗試**儘量最小化輸入與輸出**
* 加入任何節點之前，您應該嘗試**策劃您要建置的邏輯，方法是先為這個邏輯建立粗略的大綱**。當您建立粗略的大綱時，您應該保持追蹤哪些輸入和輸出將被加入至腳本中。

#### 使用「預置」以嵌入輸入值

* 如果您有**想要嵌入至圖表中的特定選項或條件**， 您應該使用「預置」以快速存取。
* 您也可以使用「預置」來**降低複雜性，方法是在執行時間較長的圖表中快取特定的滑棒值**。

> 若要瞭解如何使用「預置」，請參閱[〈使用「預置」管理您的資料〉](http://primer.dynamobim.org/en/03_Anatomy-of-a-Dynamo-Definition/3-5_presets.html)。

#### 包含自訂節點的程式

* 如果您的**程式可以收集到單一容器**，您應該使用自訂節點。
* **當圖表的部分經常在其他程式中重複使用**，您應該使用自訂節點。
* 如果您想要**與 Dynamo 社群共用功能**，您應該使用自訂節點。

![customnode](images/13-2/customnode.png)

> 將點轉換程式收集至自訂節點可建立一個功能強大的、唯一的、可攜式和更易於瞭解的程式。清晰地命名輸入連接埠將協助其他使用者瞭解如何使用節點。請記得為每個輸入加入描述和所需的資料類型。

> 1. 既有牽引程式
2. 收集此程式 「PointGrid」的自訂節點
> 若要瞭解如何使用自訂節點，請參閱[〈自訂節點簡介〉](http://primer.dynamobim.org/en/09_Custom-Nodes/9-1_Introduction.html)。

#### 建立樣板

* 您可以建立樣板來**建立視覺圖表的圖形標準，以確保協同合作者使用標準化的方式瞭解圖表**
* 建立樣板時，您可以標準化**群組顏色和字體大小**，以為工作流程類型或資料動作分類。
* 建立樣板時，您甚至可以標準化您想要如何在圖表中**為前端與後端工作流程之間的差異進行標示、著色或型式化**。

![](images/13-2/templating.jpg)

> 1. 程式的使用者介面或前端包括專案名稱、輸入滑棒和匯入幾何圖形。
2. 程式的後端。
3. 群組顏色品類 (一般設計、輸入、Python 腳本、匯入的幾何圖形)。

### 練習 - 建築的屋頂

> 下載此練習隨附的範例檔案 (按一下右鍵，然後按一下「連結另存為...」)。附錄中提供範例檔案的完整清單。[RoofDrainageSim.zip](datasets/13-2/RoofDrainageSim.zip)

現在我們已建立多個最佳作法，讓我們將它們套用至一個快速建置的程式。雖然程式成功產生屋頂，但圖表的狀態是作者的思維導圖。它缺少任何組織或有關使用它的說明。我們將檢視最佳實踐，以組織、描述和分析程式，以便其他使用者可以瞭解如何使用它。

![mindmap](images/13-2/1.jpg)

> 程式正常運作，但圖表缺乏組織。

讓我們先確定程式傳回的資料和幾何圖形。

![資料](images/13-2/1-1.JPG)

> 瞭解資料會在何時發生重大變化對於建立邏輯分割或模組性至關重要。請嘗試利用 Watch 節點來檢查程式的其餘部分，以查看您是否可以先確定群組，然後才移至下一個步驟。

> 1. 這個擁有數學方程式的 Code Block 似乎是程式的關鍵部分。Watch 節點會顯示其正在傳回轉換距離的清單。
2. 此區域的目的並不明顯。BoundingBox.Contains 在 List level L2 的 True 值排列，以及 List.FilterByBoolMask 的存在表示我們正在對點網格的一部分進行取樣。

一旦我們瞭解程式的元素部分，就可將其置於群組。

![群組](images/13-2/1-2.jpg)

> 群組可讓使用者從視覺上區分程式的各個部分。

> 1. 匯入 3D 敷地模型
2. 根據正弦方程式轉換點網格
3. 點網格的範例部分
4. 建立建築屋頂的曲面
5. 建立玻璃帷幕牆

建立群組後，對齊節點以建立圖表的視覺連續性。

![對齊](images/13-2/2.jpg)

> 視覺連續性可協助使用者查看程式流程和節點之間的隱含關係。

透過加入另一層圖形改進來使程式更容易存取。加入註釋以描述程式中特定區域的運作方式、為輸入自訂名稱，以及指定顏色到不同類型的群組。

![notes-rename](images/13-2/2-2.jpg)

> 這些圖形改進可讓使用者瞭解更多有關程式的執行。不同的群組顏色有助於區分輸入與函數。

> 1. 註釋
2. 輸入的描述性名稱

在開始壓縮程式之前，讓我們先尋找關鍵位置引入 Python 腳本排水模擬器。將第一個已調整比例的屋頂曲面的輸出插入至各自的腳本輸入。

![integratescripting](images/13-2/3.jpg)

> 我們選擇將腳本整合到程式，以便可以在原始、單一的屋頂曲面執行排水模擬。指定的曲面無法被預覽，但它可讓我們不必選取倒角 Polysurface 的頂部表面。

> 1. 腳本輸入的來源幾何圖形
2. Python 節點
3. 輸入滑棒
4. 打開/關閉開關

一切就緒，讓我們來簡化圖表。

![customnode-notetocode](images/13-2/3-2.jpg)

> 透過使用 Node to Code 和自訂節點來壓縮程式，令圖表的大小大幅減少。建立屋頂曲面和牆的群組已轉換為程式碼，因為它們特定於此程式。點轉換群組包含在自訂節點中，並且可以用於其他程式。在範例檔案中，從轉換點群組建立您的自訂節點。

> 1. 包含「轉換點網格」群組的自訂節點
2. 壓縮「建立建築屋頂的曲面和帷幕牆」群組的 Node to Code

最後一個步驟是建立典型屋頂塑形的預置。

![預置](images/13-2/3-3.jpg)

> 這些輸入是屋頂塑形的主要驅動程式，並將協助使用者發現程式的潛能。

我們的程式隨附兩個預置視圖。

![預置](images/13-2/3-4.jpg)

![預置](images/13-2/3-5.jpg)

> 屋頂排水樣式為使用者提供各個預置的解析視圖。

