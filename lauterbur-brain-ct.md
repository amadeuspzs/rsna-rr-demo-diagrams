# Team Lauterbur
## Brain CT Flow Chart

```mermaid
flowchart TD
    %% Prior CT acquisition
    subgraph CT_Prior
        Gen1[Demo Generator Prior] --> |1a DICOM| QveraIE1[Qvera Interface Engine Prior]
        QveraIE1 --> |2a ORM| Epic1[EpicRadiant]
        QveraIE1 --> |2b ORM| PACS1[PACS]
        QveraIE1 --> |2c ORM| NT1[NewtonsTree]
        QveraIE1 --> |2d ORM| RadAI1[RadAI]
        QveraIE1 --> |2e DICOM| NT1
        QveraIE1 --> |2f DICOM| ACR1[ACRAssess]
        NT1 --> |3 DICOM Study| iCo1[icometrix]
        iCo1 --> |4 Results Baseline| NT1
    end

    %% Current CT acquisition
    subgraph CT_Current
        Gen2[Demo Generator Current] --> |1b DICOM| QveraIE2[Qvera Interface Engine Current]
        QveraIE2 --> |2a ORM| Epic2[EpicRadiant]
        QveraIE2 --> |2b ORM| PACS2[PACS]
        QveraIE2 --> |2c ORM| NT2[NewtonsTree]
        QveraIE2 --> |2d ORM| RadAI2[RadAI]
        QveraIE2 --> |2e DICOM| NT2
        QveraIE2 --> |2f DICOM| ACR2[ACRAssess]
        NT2 --> |3 DICOM Study| iCo2[icometrix]
        iCo2 --> |4 Results Current| NT2
    end

    %% AI comparison and alert logic
    NT1 --> |5 Compare Prior & Current| NT2
    NT2 --> |6a Alert Trigger| CDS[CDS Hooks]
    CDS --> |6b Notify| Epic2
    CDS --> |6c Notify| RadAI2

    %% Results distribution
    NT2 --> |6d DICOM Results| QveraIE2
    NT2 --> |6e DICOM Results| PACS2
    NT2 --> |6f FHIR Results| ACR2
    NT2 --> |6g FHIR Results| Epic2
    NT2 --> |6h FHIR Results| RadAI2

    %% Reporting back
    RadAI2 --> |8a ORU| PACS2
    RadAI2 --> |8b ORU| Epic2
    RadAI2 --> |8c ORU| ACR2


```
