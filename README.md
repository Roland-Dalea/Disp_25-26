# Disp_25-26

This is the repository for Disp 
Team members: Roland Dalea, James Hayes, Si Thu Soe, Wageesha Naiduwadura, and Sufyaan Baz.

see work plan for the methodology and expected milestones, 

see log book for the log of who has participated in what work

see i star diagrams for the SD and SR models

see Startegic model diagram for the bpmn of the strategic model.

see manual tests.xlsx for the manual tests

for a report of testing done and tools used see https://docs.google.com/document/d/1bByYy95ChWFX74I0uuu4gbr2iXtvAUxxchoqZfYsxEk/edit?usp=sharing

for the full model you will need to look accross 3 repo's

https://github.com/jhayes-s3/Probuild-API/

https://github.com/jhayes-s3/Probuild-worker

https://github.com/jhayes-s3/Probuild-Diagrams/tree/main/disp%20diagrams

To see how to run this model please see https://github.com/jhayes-s3/Probuild-API/blob/main/README.md

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
