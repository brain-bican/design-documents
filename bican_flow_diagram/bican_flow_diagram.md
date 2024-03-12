# Purpose
- The purpose of this diagram is to show how data and materials flow across the BICAN ecosystem.

# Sequence Diagram
```mermaid
sequenceDiagram
    participant NBB
    participant IMS
    participant BICAN Investigator
    participant Specimen Portal
    participant Seq Library Portal 
    participant SeqCores
    participant NeMO
    participant Terra Alignment
    participant DataCatalog as Data Catalog, BICAN Dashboard
    participant KnowledgeBase as Knowledge Base, BICAN Cell Atlas 

    BICAN Investigator ->> Specimen Portal: 1. Tissue Request

    Specimen Portal ->> IMS: 2. Request Forward
    IMS ->> NBB: 2. Request Forward

    IMS ->> Specimen Portal: 3. Status Update
    NBB ->> IMS: 3. Status Update
    NBB ->> Specimen Portal: 3. Update ROI Drawing
    NBB ->> BICAN Investigator: 3. Tissue Shipment

    BICAN Investigator ->> Specimen Portal: 4. Tissue QC Free text & Structured
    BICAN Investigator ->> Seq Library Portal: 4.Library & Pool Generation

    BICAN Investigator ->> SeqCores: 5. Library Shipment
    Seq Library Portal ->> SeqCores: 5. SeqCore Dashboard Update & Notification 
    Seq Library Portal ->> NeMO: 5. NeMO Dashboard Update & Notification

    SeqCores ->> NeMO: 6. Fastq File Deposition
    SeqCores ->> Seq Library Portal: 6. Run QC Metric

    NeMO ->> Seq Library Portal: 7. QC Metric Update

    Terra Alignment ->> NeMO: 8. Investigator validation


    Specimen Portal -->> Seq Library Portal: Information Flow
    Specimen Portal -->> DataCatalog: Information Flow
    Specimen Portal -->> KnowledgeBase: Information Flow
    Seq Library Portal -->> KnowledgeBase: Information Flow
    Seq Library Portal -->> NeMO: Information Flow
    NeMO -->> KnowledgeBase: Information Flow
    NeMO -->> DataCatalog: Information Flow
    BICAN Investigator -->> DataCatalog: Information Flow
    DataCatalog -->> NeMO: Information Flow
```