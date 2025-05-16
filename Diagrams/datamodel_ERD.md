erDiagram
    User ||--o{ Account : "owns"
    User ||--o{ Category : "creates"
    User ||--o| Subscription : "has"
    Account ||--o{ Transaction : "contains"
    Category ||--o{ Budget : "has"
    Transaction }o--|| Category : "belongs to"
    
    User {
        UUID id PK
        string email
        string name
        enum userType
        datetime createdAt
        datetime updatedAt
    }
    
    Account {
        UUID id PK
        string name
        UUID ownerId FK
        datetime createdAt
        datetime updatedAt
    }
    
    Transaction {
        UUID id PK
        UUID accountId FK
        UUID categoryId FK
        decimal amount
        datetime date
        enum type
        string description
        boolean isRecurring
        UUID recurrencePatternId FK
        datetime createdAt
        datetime updatedAt
    }
    
    Category {
        UUID id PK
        string name
        UUID ownerId FK
        boolean isSystemCategory
        datetime createdAt
        datetime updatedAt
    }
    
    Budget {
        UUID id PK
        UUID categoryId FK
        decimal amount
        enum periodType
        int periodValue
        datetime startDate
        datetime createdAt
        datetime updatedAt
    }
    
    Subscription {
        UUID id PK
        UUID userId FK
        datetime startDate
        datetime endDate
        boolean isActive
        enum plan
        datetime createdAt
        datetime updatedAt
    }
    
    RecurrencePattern {
        UUID id PK
        enum type
        int interval
    }
    
    SystemSettings {
        string key PK
        string value
        datetime updatedAt
    }
    
    UserPreferences {
        UUID userId PK
        string currency
        boolean darkMode
        string language
        datetime updatedAt
    }