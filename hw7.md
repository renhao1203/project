## 實體關係圖
```mermaid
erDiagram

    ADMINISTRATOR {
        int admin_id PK
        string 姓名
        string 電子郵件
    }

    PATIENT {
        int patient_id PK
        string 姓名
        string 病歷號
    }

    NURSE {
        int nurse_id PK
        string 姓名
        string 電子郵件
    }

    DOCTOR {
        int doctor_id PK
        string 姓名
        string 專科別
        string 電子郵件
    }

    ACCOUNT {
        int account_id PK
        string 帳號
        string 密碼雜湊
        string 角色類型
        int 使用者參照ID
    }

    SURGERY_SCHEDULE {
        int schedule_id PK
        int patient_id FK
        int doctor_id FK
        date 手術日期
        string 手術時段
        string 狀態
    }

    STAFF_ASSIGNMENT {
        int assignment_id PK
        int schedule_id FK
        int staff_id
        string 人員類型
        string 手術職責
    }

    SCHEDULE_RESOURCE {
        int resource_id PK
        string 資源類型
        string 資源名稱
        string 可用狀態
    }

    NOTIFICATION {
        int notification_id PK
        int schedule_id FK
        int receiver_account_id FK
        datetime 發送時間
        string 通知管道
        string 已讀狀態
    }

    ADMINISTRATOR ||--o{ ACCOUNT : 管理
    ACCOUNT ||--o{ NOTIFICATION : 接收
    PATIENT ||--o{ SURGERY_SCHEDULE : 擁有
    DOCTOR ||--o{ SURGERY_SCHEDULE : 建立
    SURGERY_SCHEDULE ||--o{ STAFF_ASSIGNMENT : 需要
    NURSE ||--o{ STAFF_ASSIGNMENT : 指派
    DOCTOR ||--o{ STAFF_ASSIGNMENT : 指派
    SURGERY_SCHEDULE }o--o{ SCHEDULE_RESOURCE : 使用
    SURGERY_SCHEDULE ||--o{ NOTIFICATION : 產生

 ```
