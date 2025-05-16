%%{init: {'theme': 'neutral', 'flowchart': {'useMaxWidth': false}}}%%

%% Level 1: System Context Diagram
flowchart TB
    %% Title for Level 1
    subgraph Level1["System Context"]
        %% Actors and External Systems
        user["Person: User
        A person who manages their personal finances"]
        googleIdentity["External System: Google Identity
        External identity provider"]
        paymentProcessor["External System: Payment Processor
        Handles subscription payments"]
        
        %% Main System
        financialSystem["System: FinNatico
        Allows users to manage accounts, track expenses, and set budgets"]
        
        %% Relationships
        user -->|"Uses (HTTPS)"| financialSystem
        financialSystem -->|"Authenticates via OAuth2"| googleIdentity
        financialSystem -->|"Processes payments via API"| paymentProcessor
    end

    %% Level 2: Container Diagram (Cost-Optimized)
    subgraph Level2["Container Diagram (Cost-Optimized)"]
        %% External actors and systems for Level 2
        user2["Person: User
        A person who manages personal finances"]
        googleIdentity2["External System: Google Identity
        External identity provider"]
        paymentProcessor2["External System: Payment Processor
        Handles subscription payments"]
        
        %% System containers
        subgraph financialSystem2["System: FinNatico"]
            subgraph environments["Deployment Environments"]
                subgraph productionEnv["Production Environment"]
                    prodAppService["Container: Production App Service
                    Hosts all production components"]
                    
                    subgraph prodSlots["App Service Slots"]
                        prodApiGatewaySlot["Slot: YARP API Gateway
                        Routes and secures requests"]
                        prodSpaSlot["Slot: Quasar SPA
                        Vue.js, Quasar Framework"]
                        prodApiSlot["Slot: API Application
                        .NET Core, ASP.NET Core"]
                    end
                end
                
                subgraph stagingEnv["Staging Environment"]
                    stageAppService["Container: Staging App Service
                    Hosts all staging components"]
                    
                    subgraph stageSlots["App Service Slots"]
                        stageApiGatewaySlot["Slot: YARP API Gateway
                        Routes and secures requests"]
                        stageSpaSlot["Slot: Quasar SPA
                        Vue.js, Quasar Framework"]
                        stageApiSlot["Slot: API Application
                        .NET Core, ASP.NET Core"]
                    end
                end
                
                subgraph devEnv["Development Environment"]
                    devAppService["Container: Development App Service
                    Hosts all development components"]
                    
                    subgraph devSlots["App Service Slots"]
                        devApiGatewaySlot["Slot: YARP API Gateway
                        Routes and secures requests"]
                        devSpaSlot["Slot: Quasar SPA
                        Vue.js, Quasar Framework"]
                        devApiSlot["Slot: API Application
                        .NET Core, ASP.NET Core"]
                    end
                end
            end
            
            database["Container: Database
            SQL Server
            Stores user accounts, transactions, categories, and subscriptions"]
            cache["Container: Cache
            Redis
            Provides performance optimization"]
            keyVault["Container: Key Vault
            Azure Key Vault
            Secures sensitive configuration and secrets"]
            monitoring["Container: Monitoring
            Azure Monitor
            Provides application insights and logging"]
        end
        
        %% Relationships
        user2 -->|"Uses (HTTPS)"| prodApiGatewaySlot
        prodApiGatewaySlot -->|"Routes to"| prodSpaSlot
        prodApiGatewaySlot -->|"Routes to"| prodApiSlot
        prodApiSlot -->|"Reads/writes using EF Core"| database
        prodApiSlot -->|"Caches frequently accessed data"| cache
        prodApiSlot -->|"Retrieves secrets from"| keyVault
        environments -->|"Logs telemetry to"| monitoring
        prodApiSlot -->|"Authenticates via OAuth2"| googleIdentity2
        prodApiSlot -->|"Processes payments via API"| paymentProcessor2
    end

    %% Level 3: Component Diagram - API Application
    subgraph Level3["Component Diagram - API Application"]
        %% External components for Level 3
        apiGateway3["Slot: YARP API Gateway
        Routes and secures requests"]
        spaApplication3["Slot: Quasar SPA
        Vue.js, Quasar Framework"]
        database3["Container: Database
        SQL Server"]
        cache3["Container: Cache
        Redis"]
        googleIdentity3["External System: Google Identity"]
        paymentProcessor3["External System: Payment Processor"]
        
        %% API Application components
        subgraph apiApplication3["Slot: API Application"]
            %% Controllers
            userController["Component: User Controller
            ASP.NET Core API Controller
            Handles user operations and authentication"]
            accountController["Component: Account Controller
            ASP.NET Core API Controller
            Handles account management"]
            transactionController["Component: Transaction Controller
            ASP.NET Core API Controller
            Handles transaction operations"]
            categoryController["Component: Category Controller
            ASP.NET Core API Controller
            Handles category and budget management"]
            subscriptionController["Component: Subscription Controller
            ASP.NET Core API Controller
            Handles Pro subscription management"]
            
            %% Service Layers
            applicationServices["Component: Application Services
            C# Classes
            Implements application logic, coordinates domain objects"]
            
            subgraph securityServices["Component: Security Services"]
                authService["Identity Management"]
                dataProtection["Data Protection"]
                rbacService["Role-based Access Control"]
                encryptionService["Data Encryption"]
            end
            
            domainModel["Component: Domain Model
            C# Classes
            Implements domain entities, value objects, and business logic"]
            repositories["Component: Repositories
            C# Classes
            Provides data access abstraction"]
            infrastructure["Component: Infrastructure
            C# Classes
            Provides implementation for external services"]
        end
        
        %% Relationships - Internal
        apiGateway3 -->|"Routes API requests to"| apiApplication3
        apiGateway3 -->|"Routes frontend requests to"| spaApplication3
        
        userController --> applicationServices
        accountController --> applicationServices
        transactionController --> applicationServices
        categoryController --> applicationServices
        subscriptionController --> applicationServices
        
        applicationServices --> securityServices
        applicationServices --> domainModel
        applicationServices --> repositories
        repositories --> database3
        repositories --> cache3
        repositories --> domainModel
        infrastructure --> googleIdentity3
        infrastructure --> paymentProcessor3
        applicationServices --> infrastructure
    end

    %% Connect the levels for better visualization
    Level1 --- Level2
    Level2 --- Level3
    
    %% Styling
    classDef person fill:#08427B,color:#fff,stroke:#052E56
    classDef system fill:#1168BD,color:#fff,stroke:#0B4884
    classDef container fill:#438DD5,color:#fff,stroke:#2E6295
    classDef slot fill:#9370DB,color:#fff,stroke:#7B68EE
    classDef component fill:#85BBF0,color:#000,stroke:#5D82A8
    classDef database fill:#438DD5,color:#fff,stroke:#2E6295
    classDef securityComponent fill:#D9534F,color:#fff,stroke:#B82E29
    classDef external fill:#999999,color:#fff,stroke:#6B6B6B
    classDef environment fill:#20B2AA,color:#fff,stroke:#008B8B
    
    class user,user2 person
    class googleIdentity,googleIdentity2,googleIdentity3,paymentProcessor,paymentProcessor2,paymentProcessor3 external
    class financialSystem,financialSystem2 system
    class productionEnv,stagingEnv,devEnv environment
    class prodAppService,stageAppService,devAppService,database,cache,keyVault,monitoring container
    class prodApiGatewaySlot,prodSpaSlot,prodApiSlot,stageApiGatewaySlot,stageSpaSlot,stageApiSlot,devApiGatewaySlot,devSpaSlot,devApiSlot,apiGateway3,spaApplication3 slot
    class database3,cache3 database
    class userController,accountController,transactionController,categoryController,subscriptionController,applicationServices,domainModel,repositories,infrastructure component
    class securityServices,authService,dataProtection,rbacService,encryptionService securityComponent