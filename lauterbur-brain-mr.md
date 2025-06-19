# Team Lauterbur
## Brain MR Flow Chart

```mermaid
flowchart TD
    Generator[Demo Generator] --> |1 DICOM| QveraIE[Qvera Interface Engine]

    QveraIE --> |2a ORM| EpicRadiant
    QveraIE --> |2b ORM| PACS
    QveraIE --> |2c ORM| NewtonsTree
    QveraIE --> |2d ORM| RadAI
    QveraIE --> |2e DICOM| NewtonsTree
    %% Does ACR want DICOM?!?
    QveraIE --> |2f DICOM ??| ACRAssess

    NewtonsTree --> |3 DICOM Study| SiemensAIRC[Siemens AI Rad Companion]

    SiemensAIRC --> |4 DICOM Resuls| NewtonsTree

    %% AI results reviewed on the screen
    NewtonsTree --> |5 Review Results| NewtonsTree

    NewtonsTree --> |6a DICOM Resuls| QveraIE
    NewtonsTree --> |6b DICOM Results| PACS
    %% Check if ACR can do FHIR instead
    NewtonsTree --> |6c ORU Results ??| ACRAssess
    NewtonsTree --> |6d FHIR Results| EpicRadiant
    NewtonsTree --> |6e FHIR Results| RadAI

    %% Assuming we choose to report this study
    RadAI --> |7a ORU| PACS
    RadAI --> |7b ORU| EpicRadiant
    RadAI --> |7c ORU| ACRAssess
```
