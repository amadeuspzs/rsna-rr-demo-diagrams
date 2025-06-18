# Team Cormack
## Chest CT Flow Chart

```mermaid
flowchart TD
    Generator[Demo Generator] --> |1 DICOM| QveraIE[Qvera Interface Engine]

    QveraIE --> |2a ORM| GEIP[GE Intelligent Protocoling]
    QveraIE --> |2b ORM| Paxera
    QveraIE --> |2c ORM| Blackford
    QveraIE --> |2d ORM| SmartReporting
    QveraIE --> |2e DICOM| Blackford
    QveraIE --> |2f DICOM| Paxera
    QveraIE --> |2g DICOM| Fovia
    QveraIE --> |2h DICOM| ACRAssess
    QveraIE --> |2i FHIR Resources for GEIP| HAPI_FHIR

    Blackford --> |3a DICOM Study| CorelineAVIEW
    Blackford --> |3b DICOM Study| SiemensAIRC[Siemens AI Rad Companion]

    CorelineAVIEW --> |4a DICOM Resuls| Blackford
    SiemensAIRC --> |4b DICOM Resuls| Blackford

    %% If Blackford has a good viewer. Maybe we review one study in their viewer? 
    Blackford --> |5 Review Results??| Blackford

    Blackford --> |6a DICOM Results| QveraIE
    Blackford --> |6b DICOM Results| Paxera
    Blackford --> |6c DICOM Results| Fovia
    Blackford --> |6d ORU Prioritization| Paxera
    Blackford --> |6e ORU Results| ACRAssess
    Blackford --> |6f FHIR Results| SmartReporting
    
    %% Will we modify the results and broadcast the updated version? Opporunity for AIRA
    %% TODO: Check whether updated results are sent to Blackford or Qvera
    Fovia --> |7 Review Results| Fovia

    %% Results combining to happen in Fovia
    Fovia --> |8 Combine Results| Fovia
    
    SmartReporting --> |8a ORU| Paxera
    %% Can we do this over FHIR?!?
    SmartReporting --> |8b ORU| ACRAssess
```
