sequenceDiagram
 participant User
 participant APP
 participant Server
 participant 第三方
 participant Bike
 User->>+APP: 規劃行程輸入
 Note over User,APP: 起始點/終點、天數、出發日
 APP->>第三方: MAP路線圖查詢
 第三方-->>APP: MAP路線圖提供
 APP->>第三方: 天氣資訊查詢
 第三方-->>APP: 天氣資訊提供
 APP->>Server: 過往騎乘紀錄/車種資訊查詢
 Server-->>APP: 彙整紀錄
 APP-->>User: 數據彙整儀表
 Note over User,APP: 路線/體能建議/充電次數/裝備提醒等
 User->>APP: 規劃路線存檔
 APP->>Server: 規畫路線記錄上傳
 Server-->>APP: 規畫路線上傳完成確認
 APP-->>-User: 存檔成功通知
 User->>+APP: 查看規劃行程
 APP->>Server: 規劃行程紀錄查詢
 Server-->>APP: 規劃行程紀錄提供
 APP-->>-User: 規劃行程顯示
 User->>+APP: 選取欲騎乘之行程
 APP->>第三方: MAP即時路線圖查詢
 第三方-->>APP: MAP即時路線圖提供
 APP->>第三方: 天氣資訊即時查詢
 第三方-->>APP: 天氣資訊即時提供
APP->>Bike: 硬體數據查詢
Bike-->>APP: 硬體數據提供
Note over Bike,APP: 電量/胎壓等
APP-->>-User: 數據彙整儀表
User->>+APP: 騎乘模式選擇
APP->>Bike: 模式指令
Bike-->>APP: 檔位/輔助力調整確認
APP-->>-User: 模式調整完畢
User->>Bike: 騎乘
