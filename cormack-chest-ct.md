# Team Cormack
## Chest CT Flow Chart

```mermaid
flowchart LR
    Generator[Demo Generator] --> |1 DICOM| QveraIE[Qvera Interface Engine]
 
    QveraIE --> |2a ORM| GEIP[GE Intelligent Protocoling]
    QveraIE --> |2b ORM| Paxera
    QveraIE --> |2c ORM| Blackford
    QveraIE --> |2d ORM| SmartReporting
    QveraIE --> |2e DICOM| Blackford
    QveraIE --> |2f DICOM| Paxera
    QveraIE --> |2g DICOM| Fovia
    QveraIE --> |2i FHIR Resources for GEIP| HAPI_FHIR
 
    Blackford --> |3a DICOM Study| CorelineAVIEW
    Blackford --> |3b DICOM Study| SiemensAIRC[Siemens AI Rad Companion]
 
    CorelineAVIEW --> |4a DICOM Results| Blackford
    SiemensAIRC --> |4b DICOM Results| Blackford
 
    %% As result data needs to be reviewed, it should only send to Fovia for review
    Blackford --> |5a DICOM Results| Fovia
    Blackford --> |5a ORM Prioritization| Paxera
   
    Fovia --> |6 Review Results| Fovia
 
    %% Results combining to happen in Fovia
    Fovia --> |7 Combine Results| Fovia
   
    %% return results
    Fovia --> |8 Reviewed DICOM Results| Blackford
 
    %% distribute results
    Blackford --> |9a Reviewed DICOM Results| Paxera
    Blackford --> |9b Reviewed DICOM Results| ACRAssess
    Blackford --> |9c Reviewed ORU Results| ACRAssess
    Blackford --> |9d Reviewed ORU Results| SmartReporting
 
    SmartReporting --> |10a ORU| Paxera
    %% Can we do this over FHIR?!?
    SmartReporting --> |10b ORU| ACRAssess
```
