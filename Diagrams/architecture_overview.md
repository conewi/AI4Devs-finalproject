---
title: FinNatico Architecture Overview (Cost-Optimized)
---
flowchart TD
    %% Define styles
    classDef userClass fill:#08427B,color:#fff,stroke:#052E56,stroke-width:2px
    classDef externalSystemClass fill:#999999,color:#fff,stroke:#6B6B6B,stroke-width:2px
    classDef frontendClass fill:#26A0DA,color:#fff,stroke:#1773A3,stroke-width:2px
    classDef backendClass fill:#5CB85C,color:#fff,stroke:#3D8B3D,stroke-width:2px
    classDef dataClass fill:#F0AD4E,color:#fff,stroke:#D58512,stroke-width:2px
    classDef infrastructureClass fill:#7B2490,color:#fff,stroke:#5B1769,stroke-width:2px
    classDef securityClass fill:#D9534F,color:#fff,stroke:#B82E29,stroke-width:2px
    classDef slotClass fill:#9370DB,color:#fff,stroke:#7B68EE,stroke-width:1px
    classDef envClass fill:#20B2AA,color:#fff,stroke:#008B8B,stroke-width:2px

    %% Actors and External Systems
    User([User])
    GoogleIdentity[Google Identity Provider]
    PaymentGateway[Payment Processor]

    %% Environments
    subgraph Environments["Deployment Environments"]
        direction LR
        
        %% Production Environment
        subgraph ProdEnv["Production Environment"]
            ProdAppService[Production App Service]
            
            subgraph ProdSlots["App Service Slots"]
                ProdAPIGatewaySlot["YARP API Gateway Slot"]
                ProdSPASlot["Quasar SPA Slot"]
                ProdAPISlot["API Application Slot"]
            end
            
            ProdAppService --- ProdSlots
        end
        
        %% Staging Environment
        subgraph StageEnv["Staging Environment"]
            StageAppService[Staging App Service]
            
            subgraph StageSlots["App Service Slots"]
                StageAPIGatewaySlot["YARP API Gateway Slot"]
                StageSPASlot["Quasar SPA Slot"]
                StageAPISlot["API Application Slot"]
            end
            
            StageAppService --- StageSlots
        end
        
        %% Development Environment
        subgraph DevEnv["Development Environment"]
            DevAppService[Development App Service]
            
            subgraph DevSlots["App Service Slots"]
                DevAPIGatewaySlot["YARP API Gateway Slot"]
                DevSPASlot["Quasar SPA Slot"]
                DevAPISlot["API Application Slot"]
            end
            
            DevAppService --- DevSlots
        end
    end

    %% Data Layer
    subgraph DataLayer["Data Layer"]
        Database[(SQL Server)]
        Cache[(Redis Cache)]
    end

    %% Infrastructure
    subgraph InfrastructureLayer["Infrastructure"]
        AzureKeyVault[Azure Key Vault]
        AzureMonitor[Azure Monitor]
    end

    %% Security
    subgraph SecurityLayer["Security Layer"]
        IdentityProvider[Identity Management]
        DataProtection[Data Protection]
        RBAC[Role-based Access Control]
        Encryption[Data Encryption]
    end

    %% Define relationships
    User -->|Uses| ProdAPIGatewaySlot
    
    ProdAPIGatewaySlot -->|Routes Frontend Requests| ProdSPASlot
    ProdAPIGatewaySlot -->|Routes API Requests| ProdAPISlot
    
    ProdAPISlot -->|Authenticates with| GoogleIdentity
    ProdAPISlot -->|Processes Payments| PaymentGateway
    
    ProdAPISlot -->|Stores/Retrieves Data| DataLayer
    ProdAPISlot -->|Enforces| SecurityLayer
    
    SecurityLayer -->|Uses| AzureKeyVault
    Environments -->|Monitored by| AzureMonitor
    
    %% Apply styles
    class User userClass
    class GoogleIdentity,PaymentGateway externalSystemClass
    class ProdSPASlot,StageSPASlot,DevSPASlot frontendClass
    class ProdAPIGatewaySlot,StageAPIGatewaySlot,DevAPIGatewaySlot,ProdAPISlot,StageAPISlot,DevAPISlot backendClass
    class Database,Cache dataClass
    class AzureKeyVault,AzureMonitor infrastructureClass
    class IdentityProvider,DataProtection,RBAC,Encryption securityClass
    class ProdAppService,StageAppService,DevAppService envClass