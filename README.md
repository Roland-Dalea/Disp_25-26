# Disp_25-26

This repository contains the deliverables and supporting documentation for the DISP project completed by Team 5.

Team Members:
- Roland Dalea
- James Hayes
- Si Thu Soe
- Wageesha Naiduwadura
- Sufyaan Baz

## Repository Contents

- `Work Plan`  
  Contains the project methodology, timeline, and expected milestones.

- `Log Book`  
  Records individual contributions and participation throughout the project.

- `i* Diagrams`  
  Includes the Strategic Dependency (SD) and Strategic Rationale (SR) models.

- `Strategic Model Diagram`  
  Contains the BPMN 2.0 strategic business process model.

- `manual tests.xlsx`  
  Contains the manual testing records and outcomes.

- `Group5 DISP Report.pdf`  
  Provides the full testing report, including testing approaches, tools used, and evaluation results.

## Full Project Repositories

The complete system is distributed across three repositories:

- API Repository  
  [Probuild-API](https://github.com/jhayes-s3/Probuild-API/?utm_source=chatgpt.com)

- Worker Repository  
  [Probuild-worker](https://github.com/jhayes-s3/Probuild-worker?utm_source=chatgpt.com)

- BPMN and Diagram Repository  
  [Probuild-Diagrams](https://github.com/jhayes-s3/Probuild-Diagrams/tree/main/disp%20diagrams?utm_source=chatgpt.com)

## Running the System

Instructions for setting up and running the project can be found in the API repository README:

[Probuild-API README](https://github.com/jhayes-s3/Probuild-API/blob/main/README.md?utm_source=chatgpt.com)

Repo structures 
```
├── DISP-Diagrams/                        # BPMN & forms workspace
│   ├── Examples/                         # reference BPMN samples (not deployed)                                                                                                                       
│   ├── FormsWithValidation/              # archived form drafts                                                                                                                                      
│   ├── OldForms/                         # archived form drafts
│   ├── Probuild/                         # archived Probuild drafts
│   ├── manual_tests.csv                  # 45 manual test cases
│   └── disp diagrams/                    # ← deploy.py reads this folder
│       ├── Operational model.bpmn        # the main collaboration diagram
│       ├── *.form                        # ~30 task forms (Camunda Forms JSON)
│       ├── deploy.py                     # POST every .bpmn/.form to :8080
│       ├── start.py                      # publish Message-new-purchase-order
│       └── publish.py                    # generic message publisher
│
├── Probuild-API/                         # Spring Boot REST API on :8081
│   ├── data/probuilddb.mv.db             # H2 file-based DB (persists)
│   ├── pom.xml, mvnw, mvnw.cmd
│   ├── README.md
│   └── src/
│       ├── main/java/com/probuild/
│       │   ├── ProbuildApiApplication.java
│       │   ├── controller/
│       │   │   ├── ProbuildController.java       # REST endpoints
│       │   │   └── SeedController.java           # POST /seed
│       │   ├── model/                            # JPA entities
│       │   │   ├── Booking, Customer, Invoice,
│       │   │   ├── PurchaseOrder, ServiceJob,
│       │   │   ├── StockRecord, Tool, TradeCard
│       │   ├── repository/                       # Spring Data JPA repos
│       │   └── scheduled/
│       │       └── TradeCardAnnualResetService.java
│       ├── main/resources/application.properties
│       └── test/java/com/probuild/               # repo + controller tests
│
└── Probuild-worker/                      # Spring Boot Camunda workers
    ├── pom.xml, mvnw, mvnw.cmd
    ├── README.md
    └── src/
        ├── main/java/com/probuild/
        │   ├── ProbuildWorkerApplication.java
        │   └── worker/
        │       ├── MessagePublisher.java         # shared helper
        │       ├── SupplierSimulatorController.java  # /sim/supplier/start
        │       ├── PlaceOrderWorker, UpdateStockWorker,
        │       ├── AddPointsToCardWorker, NotifyTeamOfNewOrderWorker,
        │       ├── SendItemsToBeSentWorker, GiveDigitalHandoverWorker,
        │       ├── …~25 other @JobWorker classes
        │       └── customer/                     # POS-side workers
        │           ├── CardPaymentWorker, BankLogicWorker,
        │           └── Send{BankLogic,LoanInformation,PaymentInfo}Worker
        ├── main/resources/application.properties
        └── test/java/com/probuild/               # worker unit tests
        ```
