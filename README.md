graph TD;
    %% USERS %%
    A[Student] -->|Sign In: Student Number + Password| AuthServer
    A -->|View| G[Grades]
    A -->|View| C[Courses]
    A -->|View| P[Programs]
    A -->|View| AN[Announcements]
    A -->|Update| UP[Profile]
    A -->|Request| RC[Grade Consultation]
    A -->|Request| RD[Documents: COR, COE, TOR]

    B[Faculty] -->|View| AC[Advisory Class]
    B -->|Manage| HC[Handled Courses]
    B -->|View| SG[Student Grades]
    B -->|Update| FP[Profile]
    B -->|View| FAN[Announcements]
    B -->|Respond| FC[Consultation Requests]
    B -->|Sign| ECR[Electronic Class Record]
    
    C[Registrar] -->|View| STG[Student Grades per Program]
    C -->|Manage| MCR[Courses & Programs]
    C -->|Manage| MS[Sections, Faculty, Students]
    C -->|Approve| ARD[Document Requests]
    C -->|Archive| ARCH[Archive Data]
    C -->|View| LOG[Logs, Feedback, Reports]
    C -->|Backup| BDB[Backup Database]

    D[Superadmin] -->|Full Access| RegistrarModules
    D -->|Manage| UA[User Accounts - Password Reset]

    %% SYSTEM BACKEND %%
    subgraph "Backend - Next.js API & NextAuth.js"
        AuthServer["Auth Service: NextAuth.js + JOSE"]
        API["Main API - Next.js API Routes"]
        DB["Database - Supabase / PostgreSQL"]
        Reports["Reports & Analytics Module"]
    end

    AuthServer -->|JWT - JOSE| API
    API -->|CRUD Operations - Axios| DB
    API -->|Generate| Reports

    %% SYSTEM INTERACTIONS %%
    A -->|Request & View| API
    B -->|Request & Update| API
    C -->|Manage & Approve| API
    D -->|Full Control| API
    API -->|Retrieve & Store| DB
