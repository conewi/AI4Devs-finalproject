%% Level 4: Class Diagram - Domain Model for FinNatico
classDiagram
    %% Domain Aggregates
    namespace Domain.Aggregates {
        class User {
            +Id: UserId
            +Email: string
            +Name: string
            +UserType: UserType
            +Accounts: List~Account~
            +CreateAccount(name: string): Account
            +UpgradeToPro(subscription: Subscription): void
            +DowngradeToFree(): void
        }

        class Account {
            +Id: AccountId
            +Name: string
            +OwnerId: UserId
            +Transactions: List~Transaction~
            +AddTransaction(transaction: Transaction): void
            +GetLedgerBalance(): Money
            +GetAvailableBalance(): Money
        }

        class Transaction {
            +Id: TransactionId
            +Amount: Money
            +Date: DateTime
            +CategoryId: CategoryId
            +Type: TransactionType
            +Description: string
            +IsRecurring: bool
            +RecurrencePattern: RecurrencePattern
        }

        class Category {
            +Id: CategoryId
            +Name: string
            +OwnerId: UserId?
            +IsSystemCategory: bool
            +Budgets: List~Budget~
            +AssignBudget(amount: Money, period: TimePeriod): Budget
        }

        class Subscription {
            +Id: SubscriptionId
            +UserId: UserId
            +StartDate: DateTime
            +EndDate: DateTime
            +IsActive: bool
            +Plan: SubscriptionPlan
            +Renew(endDate: DateTime): void
            +Cancel(): void
        }

        class Budget {
            +Id: BudgetId
            +CategoryId: CategoryId
            +Amount: Money
            +Period: TimePeriod
            +StartDate: DateTime
        }
    }
    
    %% Domain Value Objects
    namespace Domain.ValueObjects {
        class Money {
            +Amount: decimal
            +Currency: string
            +Add(other: Money): Money
            +Subtract(other: Money): Money
        }

        class RecurrencePattern {
            +Type: RecurrenceType
            +Interval: int
        }

        class TimePeriod {
            +Type: TimePeriodType
            +Value: int
        }
    }
    
    %% Domain Enums
    namespace Domain.Enums {
        class UserType {
            <<enumeration>>
            Free
            Pro
            Admin
        }

        class TransactionType {
            <<enumeration>>
            Income
            Outcome
        }

        class RecurrenceType {
            <<enumeration>>
            Daily
            Weekly
            Monthly
            Yearly
        }

        class TimePeriodType {
            <<enumeration>>
            Days
            Months
            Years
        }

        class SubscriptionPlan {
            <<enumeration>>
            Monthly
            Yearly
        }
    }
    
    %% Relationships
    Domain.Aggregates.User *-- Domain.Aggregates.Account : owns
    Domain.Aggregates.User *-- Domain.Aggregates.Subscription : has
    Domain.Aggregates.Account *-- Domain.Aggregates.Transaction : contains
    Domain.Aggregates.Category *-- Domain.Aggregates.Budget : has
    Domain.Aggregates.Transaction -- Domain.Aggregates.Category : categorized by
    Domain.Aggregates.Transaction *-- Domain.ValueObjects.Money : has amount
    Domain.Aggregates.Transaction *-- Domain.ValueObjects.RecurrencePattern : has pattern
    Domain.Aggregates.Budget *-- Domain.ValueObjects.Money : has amount
    Domain.Aggregates.Budget *-- Domain.ValueObjects.TimePeriod : has period
    Domain.Aggregates.User -- Domain.Enums.UserType : has type
    Domain.Aggregates.Transaction -- Domain.Enums.TransactionType : has type
    Domain.ValueObjects.RecurrencePattern -- Domain.Enums.RecurrenceType : has type
    Domain.ValueObjects.TimePeriod -- Domain.Enums.TimePeriodType : has type
    Domain.Aggregates.Subscription -- Domain.Enums.SubscriptionPlan : has plan