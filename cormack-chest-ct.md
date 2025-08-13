# Team Cormack
## Chest CT Flow Chart

```mermaid
flowchart LR
    Generator[Demo Generator] --> |1 DICOM| QveraIE[Qvera Interface Engine]
 
    QveraIE --> |2a ORM| Paxera
    QveraIE --> |2b ORM| Blackford
    QveraIE --> |2c ORM| SmartReporting
    QveraIE --> |2d DICOM| Blackford
    QveraIE --> |2e DICOM| Paxera
    QveraIE --> |2f DICOM| Fovia
    QveraIE --> |2g DICOM| ACRAssess
    QveraIE --> |2i FHIR Resources for GEIP| HAPI_FHIR
 
    Blackford --> |3a DICOM Study| CorelineAVIEW
    Blackford --> |3b DICOM Study| SiemensAIRC[Siemens AI Rad Companion]
 
    CorelineAVIEW --> |4a DICOM Results| Blackford
    SiemensAIRC --> |4b DICOM Results| Blackford
 
    %% As result data needs to be reviewed, it should only send to Fovia for review
    Blackford --> |5a Raw DICOM Results| Fovia
    Blackford --> |5b Raw DICOM Results| Paxera
    %% Tentative - Brian to confirm if he can do FHIR
    Blackford --> |5c Raw FHIR Results| ACRAssess
    Blackford --> |5d ORM Prioritization| Paxera
   
    Fovia --> |6 Review Results| Fovia
 
    %% Results combining to happen in Fovia - different results
    Fovia --> |7 Combine Results| Fovia
   
    %% return results
    Fovia --> |8 Reviewed DICOM Results| Blackford
 
    %% distribute results
    %% Blackford might be able to output in FHIR
    Blackford --> |9a Reviewed DICOM Results| Paxera
    Blackford --> |9b Reviewed ORU Results| SmartReporting
 
    SmartReporting --> |10a ORU| Paxera
    SmartReporting --> |10b ORU| Blackford

    %% Tentative - Brian to confirm if he can do FHIR
    Blackford --> |11 FHIR| ACRAssess
```
