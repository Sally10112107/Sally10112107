sequenceDiagram
    participant User
    participant APP
    participant Server
    User->>+APP: 登入會員
    APP->>Server: 會員資訊查詢
    Server-->>APP: 會員資訊回報
    APP-->>-User:登入成功
    User->>APP: 查看方案
    APP-->>User: 方案顯示
    User->>APP: 方案購買
    APP-->>User: 付款畫面
   alt 付款失敗
    User->>+APP: 付款失敗
    Note over APP,User: 用戶取消/信用卡額度不足/交易逾時等
    APP->>Server: 購買方案失敗
    Note over APP,Server: 失敗訂單資訊（付款時間/金額/方案）
    Server-->>APP: 權鑑確認
    Note over APP,Server: 服務不開通
    APP-->>-User: 付款失敗
    else 付款成功
    User->>+APP: 付款成功
    APP->>Server: 購買方案完成
    Note over APP,Server: 訂單資訊（付款時間/金額/方案）
    Server-->>APP: 權鑑確認
    Note over APP,Server: 服務開通
    APP-->>-User: 付款完成
    end
    User->>APP: 服務使用
