sequenceDiagram
    participant web
    participant 申請人
    participant 申請人主管
    participant 財務
    participant 陳董
    participant Server

申請人->>web: 點選採購簽核申請
web-->>申請人: 採購申請頁面
申請人->>web: 採購標題內容、填寫，送出
alt 申請失敗
web-->>申請人: 調整/錯誤提醒
申請人->>web: 調整內容，送出
else 申請成功
web-->>申請人: 申請成功顯示
note over web,申請人: 採購單號提供
end
web->>Server: 申請成功同步
note over web,Server: 採購單號、內容記錄上傳
Server-->>申請人主管: 信件通知簽核
note over Server,申請人主管: 信件內提供簽核連結
申請人主管->>web: 點選連結
web-->>申請人主管: 採購單簽核頁面
alt主管不同意簽核
申請人主管->>web: 不同意採購
web-->>Server: 主管不同意採購
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知主管不同意簽核
申請人->>web: 搜尋採購單號
web-->>申請人: 顯示採購內容
申請人->>web: 調整內容或刪單
web-->>申請人: 調整內容或刪單完成
web->>Server: 調整內容或刪單記錄同步
Server-->>申請人主管: 信件通知簽核
note over Server,申請人主管: 調整完畢採購單簽核通知
else 主管同意簽核
申請人主管->>web: 同意採購
web-->>Server: 主管同意簽核
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知主管簽核完成
end

Server-->>財務: 信件通知採購簽核
note over Server,財務: 信件內提供簽核連結
財務->>web: 點擊連結
web-->>財務: 採購單簽核頁面
alt財務不同意簽核
財務->>web: 不同意採購
web-->>Server: 財務不同意採購
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知財務不同意簽核
申請人->>web: 搜尋採購單號
web-->>申請人: 顯示採購內容
申請人->>web: 調整內容或刪單
web-->>申請人: 調整內容或刪單完成
web->>Server: 調整內容或刪單記錄同步
Server-->>申請人主管: 信件通知簽核
note over Server,申請人主管: 調整完畢採購單簽核通知
else 財務同意簽核
財務->>web: 同意採購
web-->>Server: 財務同意簽核
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知財務簽核完成
end
note over web,Server: 單項10萬或單次總額20萬採購須陳董簽核
Server-->>陳董: 信件通知採購簽核
note over Server,陳董: 信件內提供簽核連結
陳董->>web: 點擊連結，前往簽核
web-->>陳董: 採購單簽核頁面
    alt陳董財務不同意簽核
陳董->>web: 不同意採購
web-->>Server: 陳董不同意採購
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知陳董不同意簽核
申請人->>web: 搜尋採購單號
web-->>申請人: 顯示採購內容
申請人->>web: 調整內容或刪單
web-->>申請人: 調整內容或刪單完成
web->>Server: 調整內容或刪單記錄同步
Server-->>申請人主管: 信件通知簽核
note over Server,申請人主管: 調整完畢採購單簽核通知
else 陳董同意簽核
陳董->>web: 同意採購
web-->>Server: 陳董同意簽核
note over web,Server: 簽核記錄上傳
Server-->>申請人: 信件通知陳董簽核完成
end
