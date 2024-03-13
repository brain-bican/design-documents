# Purpose
The purpose of this diagram is to show how data and materials flow across the BICAN ecosystem.

# Definitions
| Node Name       | Definition                                             |
|----------------|------------------------------------------------------|
| NBB            | Neuro Bio Bank                                       |
| IMS            | Information Management Services (https://www.imsweb.com/) |
| BICAN Investigator | TODO                                               |
| Specimen Portal | The Specimen Portal focuses on tissue management from donors to brain slabs and annotated brain samples.|
| SeqLib Portal | The Sequence Library (SeqLib) Portal manages the workflow starting from tissue, all the way downstream to track data deposition to assay-dependent data-modality-specific archives.|
| SeqCores       | TODO                                                 |
| NeMO           | TODO                                                 |
| Terra Alignment | TODO                                                 |
| Data Catalog, BICAN Dashboard | TODO                               |
| Knowledge Base, BICAN Cell Atlas | TODO                           |

# Sequence Diagram
```mermaid
sequenceDiagram
    participant NBB
    participant IMS
    participant BICAN Investigator
    participant Specimen Portal
    participant SeqLib Portal 
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
    BICAN Investigator ->> SeqLib Portal: 4.Library & Pool Generation

    BICAN Investigator ->> SeqCores: 5. Library Shipment
    SeqLib Portal ->> SeqCores: 5. SeqCore Dashboard Update & Notification 
    SeqLib Portal ->> NeMO: 5. NeMO Dashboard Update & Notification

    SeqCores ->> NeMO: 6. Fastq File Deposition
    SeqCores ->> SeqLib Portal: 6. Run QC Metric

    NeMO ->> SeqLib Portal: 7. QC Metric Update

    Terra Alignment ->> NeMO: 8. Investigator validation


    Specimen Portal -->> SeqLib Portal: Information Flow
    Specimen Portal -->> DataCatalog: Information Flow
    Specimen Portal -->> KnowledgeBase: Information Flow
    SeqLib Portal -->> KnowledgeBase: Information Flow
    SeqLib Portal -->> NeMO: Information Flow
    NeMO -->> KnowledgeBase: Information Flow
    NeMO -->> DataCatalog: Information Flow
    BICAN Investigator -->> DataCatalog: Information Flow
    DataCatalog -->> NeMO: Information Flow
```