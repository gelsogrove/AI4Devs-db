and Objective

**Role:** Act as an expert backend developer specialized in Prisma and PostgreSQL.  
**Objective:** Your mission is to extend the existing `schema.prisma` file by adding the necessary entities to implement the complete application and interview flow, using best practices in design, normalization, and migration of modern relational databases.

"Convert this ERD diagram into complete Prisma models, including relationships, foreign keys, appropriate types, and best practices such as indexes and referential integrity. Consider the use of `@relation`, `@index`, as well as normalization and consistent naming."

```
 erDiagram
    COMPANY {
        int id PK
        string name
    }
    EMPLOYEE {
        int id PK
        int company_id FK
        string name
        string email UK
        string role
        boolean is_active
    }
    POSITION {
        int id PK
        int company_id FK
        int interview_flow_id FK
        string title
        text description
        string status
        boolean is_visible
        string location
        text job_description
        text requirements
        text responsibilities
        decimal salary_min
        decimal salary_max
        string employment_type
        text benefits
        text company_description
        date application_deadline
        string contact_info
    }
    INTERVIEW_FLOW {
        int id PK
        string description
    }
    INTERVIEW_STEP {
        int id PK
        int interview_flow_id FK
        int interview_type_id FK
        string name
        int order_index
    }
    INTERVIEW_TYPE {
        int id PK
        string name
        text description
    }
    CANDIDATE {
        int id PK
        string firstName
        string lastName
        string email UK
        string phone
        string address
    }
    APPLICATION {
        int id PK
        int position_id FK
        int candidate_id FK
        date application_date
        string status
        text notes
    }
    INTERVIEW {
        int id PK
        int application_id FK
        int interview_step_id FK
        int employee_id FK
        date interview_date
        string result
        int score
        text notes
    }
    EDUCATION {
        int id PK
        int candidate_id FK
        string institution
        string title
        date startDate
        date endDate
    }
    WORK_EXPERIENCE {
        int id PK
        int candidate_id FK
        string company
        string position
        string description
        date startDate
        date endDate
    }
    RESUME {
        int id PK
        int candidate_id FK
        string filePath
        string fileType
        date uploadDate
    }

    %% Relazioni originali dell'esercizio
    COMPANY ||--o{ EMPLOYEE : employs
    COMPANY ||--o{ POSITION : offers
    POSITION ||--|| INTERVIEW_FLOW : assigns
    INTERVIEW_FLOW ||--o{ INTERVIEW_STEP : contains
    INTERVIEW_STEP ||--|| INTERVIEW_TYPE : uses
    POSITION ||--o{ APPLICATION : receives
    CANDIDATE ||--o{ APPLICATION : submits
    APPLICATION ||--o{ INTERVIEW : has
    INTERVIEW ||--|| INTERVIEW_STEP : consists_of
    EMPLOYEE ||--o{ INTERVIEW : conducts

    %% Relazioni aggiuntive dal sistema esistente
    CANDIDATE ||--o{ EDUCATION : has
    CANDIDATE ||--o{ WORK_EXPERIENCE : has
    CANDIDATE ||--o{ RESUME : has
```

update the file:  /backend/prisma/schema.prisma
 
 

##  Prompt 2 – Validate Before Migration

"Validate the Prisma schema before executing the `npx run prisma:migrate:dev` with the command `npx run prisma:validate`. Check for any potential issues with relationships, constraints, or data types that might cause problems during the migration process. Provide recommendations to fix any identified issues."



##  Prompt 3 – Updated ERD in Mermaid Format

"Generate a new complete ERD diagram in Mermaid format that includes both the new models added to the interview flow (`Company`, `Position`, `Application`, etc.) and the existing models (`Candidate`, `Education`, `Resume`, `WorkExperience`). The ERD should show all relationships with primary and foreign keys, following good design and normalization practices."