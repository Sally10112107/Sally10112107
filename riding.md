sequenceDiagram
    participant User
    participant APP
    participant Bike
    participant Server
    participant 第三方
    User->>+APP: 尋車
    APP-->>-User: 車輛資訊(UWB)
    Note over APP,User: 車輛位置等資訊
    User->>+APP: 解鎖
    APP->>Bike: 解鎖指令
    Bike-->>APP: 解鎖確認
    APP-->>-User: 解鎖完成
    User->>+APP: 立即騎乘
    APP->>第三方: MAP API定位查詢
    第三方-->>APP: MAP API定位提供
    APP->>第三方: 天氣資訊查詢
    第三方-->>APP: 天氣資訊提供
    APP->>Bike: 硬體數據查詢
    Bike-->>APP: 硬體數據提供
    Note over APP,Bike: 電量/胎壓等
    APP-->>-User: 數據彙整儀表
    User->>+APP: 騎乘模式選擇
    APP->>Bike: 模式指令
    Bike-->>APP: 電力/檔位/輔助力確認
    APP-->>-User: 模式調整完畢
    User->>+Bike: 騎乘
    Bike-->>APP: 騎乘數據回饋
    APP->>Server: 騎乘數據上傳
    APP->>第三方: 心跳/血氧濃度數據查詢
    第三方-->>APP: 心跳/血氧濃度數據提供
    APP->>第三方: GPS點位記錄查詢
    第三方-->>APP: GPS點位記錄提供
    APP-->>User: 數據與路線圖顯示

    alt App手動調控
    User->>+APP: 輔助調控
    Note over User,APP: 用戶透過APP調整檔位
    APP->>Bike: 調整指令
    Bike-->>APP: 調整完成同步
    Bike->>User: 輸出功率改變
    APP-->>-User:  調整完成顯示
    else 車體手動調控
    User->>+Bike: 輔助調控
    Note over User,Bike: 用戶透過車身按鈕調整檔位
    Bike-->>APP: 調整完成同步
    APP-->>User: 調整完成顯示
    Bike->>-User: 輸出功率改變
    end
    User->>+Bike: 智慧調控
    Note over User,Bike: 依據操作行為偵測自動調整
    Bike-->>APP: 輔助輸出改變數據同步顯示
    APP-->>User: 輔助輸出改變數據顯示
    Bike->>-User:輸出功率改變

   alt App調控車燈
    User->>+APP: 車燈開/關指令
    Note over User,APP: 用戶透過APP點擊開/關燈
    APP->>Bike: 車燈指令
    Bike-->>APP: 車燈指令確認
    Bike->>User: 車燈開啟/關閉
    APP-->>-User: APP顯示車燈開/關
    else 車身按鈕調控車燈
    User->>+Bike: 車燈開/關指令
    Note over User,Bike: 用戶透過車身按鈕調控開/關燈
    Bike-->>APP: 車燈指令確認
    APP-->>User: 車燈開關顯示
    Bike->>-User: 車燈開啟/關閉
    end
    APP->>+User: 撞擊通知
    alt 用戶不需緊急服務
        User->>APP: 回覆撞擊通知
        APP-->>User: 確認關心
    else 用戶需要緊急服務
        User->>APP: 無回覆撞擊通知
        APP-->>第三方: 緊急聯絡
    end
    APP-->>Server: 撞擊記錄
    User->>+APP: 騎乘結束
    APP->>Server: 騎乘數據記錄上傳
    Server-->>APP: 騎乘數據呈現
    APP-->>-User: 騎乘數據觀看
    User->>+APP: 上鎖
    APP->>Bike: 上鎖
    Bike-->>APP: 上鎖確認
    APP-->>-User: 上鎖完成
