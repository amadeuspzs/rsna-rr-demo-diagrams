# Team Lauterbur
## Brain CT Flow Chart

See [clinical scenario](https://docs.google.com/document/d/1AbMGfBinw8_epP9_cIjC8s-tYXvqS_8XI4lB4wp4Qxc/edit?tab=t.0#heading=h.bxasmyukr250)

```mermaid
 flowchart LR
    %% Current CT acquisition
    Gen2[Demo Generator] --> |1 DICOM| QveraIE[Qvera Interface Engine]
    QveraIE --> |2a ORM| Epic[EpicRadiant]
    QveraIE --> |2b ORM| Visage[Visage]
    QveraIE --> |2c ORM| NT[NewtonsTree]
    QveraIE --> |2d ORM| RadAI[RadAI]
    QveraIE --> |2e DICOM| NT
    QveraIE --> |2f DICOM| ACR[ACRAssess]
    QveraIE --> |2g DICOM| Visage

    %% Prior scan retrieval
    NT --> |3a Priors DICOM-QR| Visage
    Visage --> |3b Priors C-STORE| NT

    %% Send all scans to icometrix
    NT --> |4 All Studies Prior and Current| iCo[icometrix AI]

    %% DICOM Results include SCs, PDF as well as SR with precent change
    iCo --> |5 DICOM Results| NT

    %% FHIR Reporting and Alerting
    NT --> |6a FHIR Observation| ACR
    NT --> |6b FHIR Observation| RadAI

    %% Epic needs this over FHIRcast
    %% TODO - NT to decide if they want to do this, if not then Qvera
    NT --> |6c HL7 v2 ORU| Epic

    NT --> |7a Check if Percent Change > Threshold| NT
    %% TBD what mechanism used to trigger an alert in Epic %%
    NT --> |7b Worklist Priorization FHIR??| Epic

    %% For the Siemens usecase, AI review through a NT worklist then results are propagated

    %% Optional results distribution
    NT --> |8a DICOM Results| QveraIE
    NT --> |8b DICOM Results| Visage

    %% Reporting workflow
    Epic --> |9a FHIRcast Context Sync| Visage
    Epic --> |9b FHIRcast Context Sync| RadAI

    RadAI --> |10 Signed report ORU| Qvera

    Qvera --> |11a ORU| Visage
    Qvera --> |11b ORU| EpicRadiant
    Qvera --> |11c ORU| ACRAssess  
```
