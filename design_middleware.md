3. Laravel 當中的 middleware 能夠在進入 controller 和離開 controller 後提供額外的操作，參考 官方文件 。若換成自己設計類似的 middleware ，請描述一下會如何設計以及設計的做法。

    我實在不知道要怎麼設計出middleware，但可以大概講一下它的特性和運作流程：
    * Laravel的middleware可將controller裡多個action的共同部分拆出來，達到邏輯實現解耦的目的。
    * middleware處理流程：   
        1. 在index.php中初始化app後，會解析出http kernel物件。（Http Kernel就是Laravel裡負責HTTP請求和回應的核心）
        2. 將請求傳給kernel的handle方法，在這個方法中處理請求物件並return response物件。
        middleware就在這個方法裡被使用：`$this->sendRequestThroughRouter($request)`
        3. Laravel透過Pipeline來傳輸請求物件，在Pipeline中可將請求物件依次透過Http Kernel里定義對middleware的前置操作，到某個controller的action或直接到next的closure處理，得到response物件 
        4. closure next()這邊會以遞迴的方式來執行，以達成route定義的middleware前置處理與後製處理的順序
        5. 依handle內`$next`的操作和回傳值來決定middleware的執行動作發生在請求處理前還是請求後
   * middleware的特性：
        * 耦合度低、易於修改、好擴充。
        * 要達成模組化，必須擁有統一的介面，例如都必須有共同的方法handle()處理`$request`的參數。
        * middleware本身沒有狀態，也不依賴於其他元件（不知道來源、也不關心return對象)，需要靠provider引入外部資源。
        * 為了達到以上特性，避免使用繼承而讓子類別臃腫，middleware使用的是裝飾模式取代繼承，更靈活的來達成增加物件功能的目的。
    
    

