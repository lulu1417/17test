
2. PHP 當中的 interface 和 abstract ，分別適合於什麼時機使用。請描述對於這兩個保留字的看法。
    * interface：
        * 使用時機：
            * 當確認各個物件的規格或彼此間的溝通方式，卻未能知道其實做細節時，可使用interface。換句話說，就是當多個類別有共同的方法，但這些方法在不同類別有不同的實作時，可將這些方法寫成一個interface，讓那些類別來實作。
            * 可讓使用者在不須知道實作細節的情況下，依然能操縱物件的本質。
            * 例如：在多個資料庫訪問服務或多種不同的cache機制，可以透過interface擁有不同的實作而不需修改到這些類別的程式碼。
        * 原則：
            * interface只能有抽象方法，不能定義任何方法的實作細節，且都必須是public方法。
            * 當一個類別實作一個interface時，必須實作這個的interface的所有方法。
            * 類別能在繼承另一個類別時同時實作一個interface。
            * 一個interface可衍生(類似繼承的概念)另一個interface。
            * 一個類別可實作多個interface。
            * interface不能有property，但可以有constant。
    * abstract：
        * PHP有abstract類別和abstract方法。
        * 使用時機：
            * 讓程式碼再利用：當多個類別有共同的property或方法時，為了避免每個類別一直重複出現相同的部分，可將這些共同的地方寫成一個abstract類別，讓那些類別來繼承。
            * 例如：
        * 原則：
            * 類別可繼承abstract類別，一個類別只能繼承一個abstract類別。
            * abstract類別可有abstract方法或實體方法，但只要包含一個以上的abstract方法，就是abstract類別。
            * abstract方法不能有實作細節。
            * 當子類別繼承一個abstract的父類別時，必須實作出它宣告的abstract方法細節。
            * 一個abstract類別也可以實作interface。
    * 兩者的相同點：
        * 都不能被實例化。
    
| |  interface|abstract |
| -------- | -------- | -------- |
| 可否有property     | 不可   | 可  |
| 可視性     | 必須是public    | 可為public或protected  |
|可被實例化|不可|不可
|可實作方法內容|不可|可


