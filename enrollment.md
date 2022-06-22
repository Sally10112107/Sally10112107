sequenceDiagram
 participant User
 participant APP
 participant 第三方
 participant Server
 User->>APP: 註冊
 alt 第三方登入註冊
User->>+APP: 第三方帳號登入
note over User,APP: Line/Facebook等社群軟體
APP->>第三方: 用戶資訊查詢
第三方-->>APP: 用戶資訊提供
APP-->>User: 完整資訊補充需求
User->>APP: 完整資訊填寫
APP->>Server: 會員資料上傳
Server-->>APP: 會員資料上傳完成
APP-->>-User: 註冊完成顯示
else mBike官方註冊
User->>+APP: 官方註冊入口
APP-->>User:註冊資料填寫需求
note over User,APP: 基本資料/手機/email等
User->>APP: 基本資料填寫
APP->>Server: 會員資料上傳
Server-->>APP: 會員資料上傳完成
APP-->>-User: 註冊完成顯示
end
APP-->>User: 用戶身體數據填寫提醒與說明
note over APP,User: inbody等資料
alt 略過填寫
User->>+APP: 下次填寫
APP-->>-User: 首頁畫面顯示
else 填寫inbody資訊
User->>+APP: 填寫身體數據資訊
APP->>Server: 上傳會員身體數據資訊
Server-->>APP: 數據上傳完成
APP-->>User: 填寫完成顯示
User->>APP: 確認返回首頁
APP-->>-User: 首頁畫面
end
