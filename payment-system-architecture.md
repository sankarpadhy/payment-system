graph LR
%% Style definitions
classDef default fill:#f9f9f9,stroke:#333,stroke-width:1px;
classDef layer fill:#e1f5fe,stroke:#01579b,stroke-width:2px;

%% CLIENT ACCESS LAYER
subgraph CL[Client Access Layer]
    direction TB
    A[ ]
    MP[Mobile Payment<br/>React Native/Flutter<br/>iOS/Android] --> PT[POS Terminal<br/>Spring Boot/JavaPOS<br/>EMV/Card Present]
    WP[Web Payment<br/>Next.js/React<br/>Checkout/Forms] --> SP[Smart POS<br/>Spring Boot/Android<br/>mPOS Support]
end

%% CHANNEL INTEGRATION LAYER
subgraph CI[Channel Integration Layer]
    direction TB
    A[ ]
    MS[Mobile SDK<br/>Native/WebView<br/>Secure Comm] --> PI[POS Integration<br/>JavaPOS/OPOS<br/>Terminal Mgmt]
    PS[Payment SDK<br/>JS/WebSocket<br/>Tokenization] --> TS[Terminal SDK<br/>Android/Native<br/>Device Mgmt]
end

%% EXTERNAL PAYMENT ECOSYSTEM
subgraph EP[External Payment Ecosystem]
    direction TB
    A[ ]
    CN[Card Networks<br/>Visa/MC] --> DW[Digital Wallets<br/>Apple/Google]
    BK[Banking<br/>SWIFT/ACH] --> AP[Alt. Payments<br/>Crypto/BNPL]
end

%% PAYMENT GATEWAY LAYER
subgraph PG[Payment Gateway Layer]
    direction TB
    A[ ]
    GW[Gateway<br/>Spring/Camel<br/>Protocol Handler] --> NI[Card Network<br/>ISO8583<br/>Socket Conn]
    BI[Bank Integration<br/>ISO20022<br/>SWIFT/ACH] --> WI[Wallet Integration<br/>SDK/REST<br/>OAuth]
end

%% SECURITY & COMPLIANCE LAYER
subgraph SC[Security & Compliance Layer]
    direction TB
    A[ ]
    AG[API Gateway<br/>Kong/Istio<br/>Rate Limit/LB] --> AU[Auth Service<br/>Keycloak<br/>OAuth/MFA]
    EN[Encryption<br/>Vault/HSM<br/>Key Mgmt] --> CO[Compliance<br/>PCI/KYC/GDPR]
end

%% BUSINESS SERVICES LAYER
subgraph BS[Business Services Layer]
    direction TB
    A[ ]
    MM[Merchant Mgmt<br/>Spring/PostgreSQL] --> CM[Customer Mgmt<br/>Spring/MongoDB]
    SS[Settlement<br/>Spring Batch] --> RS[Reconciliation<br/>Spark/Reports]
end

%% CORE PAYMENT SERVICES LAYER
subgraph CP[Core Payment Services Layer]
    direction TB
    A[ ]
    PO[Payment Orchestrator<br/>Spring Cloud/K8s] --> TP[Transaction Processor<br/>SAGA/ACID]
    FD[Fraud Detection<br/>ML/Rules Engine] --> RM[Risk Management<br/>Scoring/Rules]
end

%% DATA PERSISTENCE LAYER
subgraph DP[Data Persistence Layer]
    direction TB
    A[ ]
    TD[Transaction DB<br/>PostgreSQL/ACID] --> CD[Customer DB<br/>MongoDB/Scalable]
    MD[Merchant DB<br/>PostgreSQL/MySQL] --> AD[Audit DB<br/>Elastic/TimescaleDB]
end

%% MESSAGING & CACHING LAYER
subgraph MC[Messaging & Caching Layer]
    direction TB
    A[ ]
    ES[Event Stream<br/>Kafka/EventStore] --> MQ[Message Queue<br/>RabbitMQ/ActiveMQ]
    CS[Cache Service<br/>Redis/Hazelcast] --> ST[State Store<br/>Redis/etcd]
end

%% MONITORING & OPERATIONS LAYER
subgraph MO[Monitoring & Operations Layer]
    direction TB
    A[ ]
    SM[System Monitor<br/>Prometheus/Grafana] --> TM[Transaction Monitor<br/>Datadog/NewRelic]
    LA[Log Analytics<br/>ELK/Splunk] --> AL[Alerting<br/>PagerDuty/OpsGenie]
end

%% DEVOPS & DEPLOYMENT LAYER
subgraph DD[DevOps & Deployment Layer]
    direction TB
    A[ ]
    CD[CI/CD<br/>Jenkins/GitLab] --> CO[Container Orch<br/>K8s/Docker]
    CM[Config Mgmt<br/>Spring Cloud] --> IN[Infrastructure<br/>Terraform/Ansible]
end

%% Main Flow Connections
CL --> CI
CI --> EP
EP --> PG
PG --> SC
SC --> BS
BS --> CP
CP --> DP
DP --> MC
MC --> MO
MO --> DD

%% Cross-layer Dependencies
CP -.-> MC
BS -.-> MC
SC -.-> MO
PG -.-> MO

%% Apply styles
class CL,CI,EP,PG,SC,BS,CP,DP,MC,MO,DD layer
