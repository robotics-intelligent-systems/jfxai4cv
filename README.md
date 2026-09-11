# JFXAI4CV — Open-Source AI Alternative Integration Architecture

## AI-Powered Medical Imaging, Clinical Visualization, Federated Learning & Computer Vision Platform

> **Repository:** `robotics-intelligent-systems/jfxai4cv`
>
> **Purpose:** reorganize the current JFXAI4CV software compendium into a modular, open-source-first architecture for medical imaging ingestion, DICOM/PACS interoperability, visualization, segmentation, registration, geometric reconstruction, surgical planning, AI inference, federated learning, scientific imaging, AR visualization, and optional biometric-computer-vision profiles.
>
> **Source boundary:** the current repository is a compact software compendium. This document preserves the components explicitly named in that description and clearly labels additional technologies as architectural recommendations rather than current repository dependencies.
>
> **Clinical safety principle:** AI-generated findings, segmentations, measurements, reconstructions, and planning outputs are decision-support artifacts. They must not be treated as autonomous diagnoses, prescriptions, surgical instructions, or regulatory approval. Clinical deployment requires qualified professional review, appropriate validation, privacy/security controls, and applicable medical-device governance.

---

# 1. Source Project Direction

The current JFXAI4CV README describes an:

> **AI-Powered Medical Imaging Platform**

and references a broad ecosystem including:

- `pulse2percept`;
- Language and Vision (LaVi) Lab;
- Musculoskeletal Atlas Project (MAP);
- a Surgical Planning extension for 3D Slicer;
- Open Framework for Federated Learning;
- Ultralytics / YOLO;
- open-source biometrics / face recognition;
- open-source AFIS;
- Kryo;
- Apache Flink;
- BRIAR API;
- NIST Biometric Image Software;
- open-source biometric SDKs for face, iris and fingerprint;
- JGNN;
- JavaCV;
- Eclipse OMR;
- Open Source Imaging Initiative;
- Eclipse Deeplearning4J;
- MONAI;
- an open pipeline for augmented-reality models from scientific data;
- NVIDIA Clara Viz;
- AlignTK.

The source also preserves the engineering lifecycle:

```text
MBSE
├── CAD
├── CAM
└── CAS
```

The proposed architecture converts this catalog into replaceable capabilities around a common imaging and AI integration model.

---

# 2. Target Platform Vision

```text
IMAGING DEVICE / SCIENTIFIC DATA SOURCE
                ↓
        INGESTION / DICOM
                ↓
      DE-IDENTIFICATION GATE
                ↓
       CLINICAL IMAGE STORE
                ↓
         IMAGING DATA FABRIC
                ↓
   ┌────────────┼─────────────┐
   ▼            ▼             ▼
VIEWING      AI/ML         GEOMETRY
2D / 3D    INFERENCE       / MESH
   │            │             │
   └────────────┼─────────────┘
                ▼
     CLINICAL REVIEW LAYER
                ↓
      PLANNING / RESEARCH
                ↓
   APPROVED OUTPUT / EVIDENCE
```

---

# 3. High-Level Alternative Architecture

```text
┌─────────────────────────────────────────────────────────────────────┐
│                           JFXAI4CV                                  │
│ Studies | Series | Images | Models | Annotations | Projects        │
└──────────────────────────────┬──────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│                     IMAGING DATA FABRIC                             │
│ DICOM Metadata | Object Store | Provenance | Events | Audit        │
└───────────────┬──────────────────┬──────────────────┬──────────────┘
                │                  │                  │
                ▼                  ▼                  ▼
          VIEWER / 3D         AI / MONAI        GEOMETRY / MESH
          OHIF / Slicer       Detection          MAP / Slicer
          Clara Viz opt.      Segmentation       Registration
                │                  │                  │
                └──────────────────┼──────────────────┘
                                   ▼
                        CLINICAL REVIEW GATE
                                   │
             ┌─────────────────────┼─────────────────────┐
             ▼                     ▼                     ▼
       SURGICAL PLANNING     FEDERATED LEARNING      AR / XR
       Slicer extensions     Privacy-preserving      Scientific models
                                   │
                                   ▼
                         RESEARCH / EVALUATION
```

---

# 4. Architectural Layers

```text
Layer 1
Imaging / Scientific Data Sources

Layer 2
DICOM / File / Stream Ingestion

Layer 3
De-identification / Privacy Gateway

Layer 4
Image / Metadata Storage

Layer 5
Pre-processing / Registration

Layer 6
AI / Segmentation / Detection / Classification

Layer 7
3D Reconstruction / Mesh / Visualization

Layer 8
Clinical / Research Workflow

Layer 9
Federated Learning / MLOps

Layer 10
Audit / Evaluation / Governance
```

---

# 5. Source Component Classification

Each item from the current compendium should be classified as:

```text
CORE CANDIDATE
Useful default implementation

OPTIONAL ADAPTER
Replaceable integration

DOMAIN SPECIALIST
Focused on one medical/scientific domain

RESEARCH
Experimental/research component

BIOMETRIC PROFILE
Separate non-clinical computer-vision domain

EXTERNAL / LICENSE VERIFY
Useful component requiring separate license/deployment review
```

---

# 6. Proposed Classification of Source Components

| Component | Source Role | Proposed Classification |
|---|---|---|
| MONAI | Healthcare imaging AI | Core Candidate |
| 3D Slicer Surgical Planning extension | Surgical path planning | Core Candidate / Domain App |
| Musculoskeletal Atlas Project | Imaging / segmentation / mesh / OpenSim / FE export | Domain Specialist |
| pulse2percept | Bionic-vision simulation | Research / Domain Specialist |
| AlignTK | Large-scale image alignment | Domain Specialist |
| Clara Viz | 2D/3D medical visualization | Optional / External Adapter |
| Ultralytics / YOLO | Detection / vision models | Optional AI Provider |
| Open Framework for Federated Learning | Federated learning | Core Candidate / Research |
| Apache Flink | Streaming | Core Candidate for streaming profile |
| Kryo | JVM serialization | Optional Infrastructure |
| Deeplearning4J | JVM deep learning | Optional AI Provider |
| JavaCV | JVM computer vision | Optional CV Provider |
| JGNN | Graph neural networks | Research / Optional |
| Eclipse OMR | JVM/native runtime components | Infrastructure / Research |
| OSI medical-imaging initiative | Open imaging-device development | Research / Hardware Ecosystem |
| AR scientific-data pipeline | AR visualization | Optional |
| Open-source biometrics | Identity / face / iris / fingerprint | Separate Biometric Profile |
| AFIS | Fingerprint recognition | Separate Biometric Profile |
| BRIAR API | Biometric research/evaluation | Separate Biometric Profile |
| NIST biometric software | Biometric image tools | Separate Biometric Profile |
| LaVi Lab | Language + vision research | Research |

---

# 7. Recommended Open-Source-First Backbone

The following are **proposed additions** to make the compendium executable as an integrated platform:

```text
Orthanc
→ lightweight DICOM/PACS gateway

DICOMweb
→ interoperable study/series/image APIs

OHIF
→ web medical-image viewer

3D Slicer
→ desktop visualization, annotation and surgical/research workflows

MONAI
→ healthcare AI training/inference

ITK / SimpleITK
→ image processing / registration

VTK
→ 3D visualization / meshes

PostgreSQL
→ application metadata / audit / model registry metadata

S3-compatible object storage
→ images, models, derived artifacts

FastAPI
→ service APIs

Apache Flink
→ streaming / event transformations

MLflow-compatible model registry
→ experiment/model lifecycle

Qdrant or equivalent
→ optional semantic retrieval / multimodal RAG
```

These additions are architectural recommendations, not claims about current repository contents.

---

# 8. DICOM-First Integration Boundary

JFXAI4CV should use DICOM and DICOMweb as the principal medical-imaging interoperability boundary where appropriate.

```text
Modality / Scanner
      ↓
DICOM
      ↓
DICOM Gateway
      ↓
Study / Series / Instance
      ↓
Clinical Image Store
```

---

# 9. Canonical Study Model

```yaml
study:
  id: internal_study_id
  modality:
    - CT
  acquired_at: "..."
  patient_ref: pseudonymous_subject_id
  source_system: pacs_A
  series:
    - series_001
  privacy:
    deidentified: true
```

---

# 10. Canonical Series Model

```yaml
series:
  id: series_001
  study_id: internal_study_id
  modality: CT
  body_region: configured
  instance_count: 420
  geometry:
    spacing: [...]
    orientation: [...]
```

---

# 11. Canonical Derived Artifact

```yaml
derived_artifact:
  id: artifact_segmentation_001
  source_series: series_001
  type: segmentation
  format: DICOM_SEG_or_equivalent
  model:
    id: liver_seg_v4
    version: 4
  status: draft
  review:
    required: true
```

---

# 12. Data Ingestion Architecture

```text
PACS / Scanner / Scientific Source
              ↓
        Ingestion Gateway
              ↓
       Validation / Parsing
              ↓
      Privacy / De-ID Gate
              ↓
       Canonical Metadata
              ↓
 Object Store + Metadata Database
```

---

# 13. Privacy Gateway

Before research/AI use:

```text
Clinical Data
     ↓
Purpose Check
     ↓
De-identification / Pseudonymization
     ↓
Research Dataset
```

Keep re-identification keys outside the AI research plane.

---

# 14. Clinical vs Research Data Plane

```text
CLINICAL PLANE
Identifiable / regulated data
          │
          │ controlled export
          ▼
RESEARCH PLANE
De-identified / governed data
```

Do not use one unrestricted data lake for both.

---

# 15. DICOM Gateway Strategy

Recommended provider abstraction:

```text
DICOMProvider
├── store()
├── query()
├── retrieve()
├── get_metadata()
├── get_pixel_data()
└── publish_derived_object()
```

---

# 16. Orthanc Role

**Proposed addition.**

Orthanc is suitable as a lightweight open DICOM gateway for:

- DICOM ingestion;
- routing;
- study/series metadata;
- REST integration;
- DICOMweb profiles via extensions/deployment configuration.

JFXAI4CV should remain portable to other PACS systems through the `DICOMProvider` abstraction.

---

# 17. DICOMweb API Layer

Canonical application-facing operations:

```text
QIDO-RS
→ query

WADO-RS
→ retrieve

STOW-RS
→ store
```

Use a service adapter so frontend code does not depend on PACS-specific APIs.

---

# 18. Viewer Architecture

```text
Study
  ↓
Viewer Provider
  ├── OHIF
  ├── 3D Slicer
  └── Clara Viz adapter
```

---

# 19. OHIF Role

**Proposed addition.**

Recommended for:

```text
Web Study Viewer
Annotations
DICOMweb
AI Result Review
```

It should consume derived results rather than own model inference.

---

# 20. 3D Slicer Role

The source already references a surgical-planning extension for 3D Slicer.

Use 3D Slicer for:

- volumetric visualization;
- segmentation review;
- registration;
- measurement;
- mesh generation;
- surgical/research planning;
- extension-based clinical research tools.

---

# 21. Surgical Planning Architecture

```text
Medical Images
      ↓
Segmentation
      ↓
Anatomical Model
      ↓
Target / Risk Structures
      ↓
Candidate Path
      ↓
3D Review
      ↓
Qualified Human Review
      ↓
Planning Artifact
```

A software-generated path must never be treated as autonomous surgical authorization.

---

# 22. Musculoskeletal Atlas Project Role

The source compendium describes MAP as providing:

- imaging visualization;
- segmentation;
- geometric mesh creation;
- export to OpenSim;
- FE model export.

Recommended integration:

```text
Imaging Study
     ↓
MAP Adapter
     ↓
Segmentation
     ↓
Geometry / Mesh
     ↓
OpenSim / FE Export
```

---

# 23. Geometry Provider

```text
GeometryProvider
├── segment_to_surface()
├── mesh()
├── smooth()
├── simplify()
├── register()
├── export()
└── provenance()
```

---

# 24. ITK / SimpleITK Role

**Proposed addition.**

Use for:

- filtering;
- resampling;
- registration;
- transforms;
- medical-image preprocessing.

---

# 25. VTK Role

**Proposed addition.**

Use for:

- 3D visualization;
- mesh processing;
- geometric analysis;
- Slicer-compatible workflows.

---

# 26. Alignment Architecture

The source includes AlignTK.

```text
2D Image Collection
      ↓
Alignment
      ↓
Registered Stack
      ↓
3D Reconstruction / Analysis
```

Keep this as a specialist image-alignment provider.

---

# 27. AlignTK Profile

Useful for:

- electron microscopy;
- large 2D image batches;
- grayscale scientific imagery;
- 2D→3D alignment.

It should not become the default registration engine for every clinical modality.

---

# 28. AI / MONAI Plane

```text
Dataset
   ↓
Preprocessing
   ↓
MONAI Pipeline
   ↓
Training / Validation
   ↓
Model Registry
   ↓
Inference Service
   ↓
Derived Imaging Artifact
   ↓
Human Review
```

---

# 29. MONAI Role

The current compendium explicitly includes MONAI.

Recommended use:

```text
Healthcare-specific transforms
Training pipelines
Segmentation
Classification
Detection
Inference
Evaluation
```

MONAI becomes the preferred healthcare-AI framework, with other model providers behind adapters.

---

# 30. AI Provider Interface

```text
MedicalAIProvider
├── preprocess()
├── infer()
├── postprocess()
├── explain()
├── metadata()
└── unload()
```

---

# 31. Segmentation Contract

```yaml
segmentation_result:
  source_series: series_001
  labels:
    - id: structure_01
      class: configured_structure
  confidence:
    summary: 0.94
  model:
    id: segmentation_v4
  review_status: pending
```

---

# 32. Detection Contract

```yaml
detection:
  source_instance: instance_002
  class: configured_finding
  bbox: [...]
  confidence: 0.88
  model: detector_v3
  review_required: true
```

---

# 33. Classification Contract

```yaml
classification:
  source: series_001
  label: candidate_class
  probability: 0.81
  model: classifier_v2
  intended_use: research_assistance
```

---

# 34. AI Findings Are Not Clinical Truth

Maintain:

```text
PIXEL / IMAGE FACT
        ≠
MODEL INFERENCE
        ≠
CLINICAL INTERPRETATION
        ≠
DIAGNOSIS
```

---

# 35. Ultralytics / YOLO Boundary

The source compendium includes Ultralytics/YOLO.

Treat it as:

```text
GenericDetectionProvider
```

Suitable for:

- research detection;
- non-clinical CV;
- experimental medical object localization where validated.

Do not make generic YOLO output synonymous with a validated medical device.

---

# 36. DL4J Role

The source includes Eclipse Deeplearning4J.

Recommended profile:

```text
JVMMedicalAIProvider
```

Use when:

- Java integration is a requirement;
- JVM deployment is strategic;
- existing DL4J models/pipelines are reused.

MONAI remains the stronger healthcare-specific default.

---

# 37. JavaCV Role

```text
JVMComputerVisionProvider
```

Use for:

- OpenCV-backed JVM processing;
- Java-native image services;
- capture/conversion;
- scientific CV integration.

---

# 38. JGNN Role

`JGNN` can remain an optional graph-neural-network research provider.

Potential uses:

- anatomical graphs;
- relational structures;
- multimodal subject graphs;
- research prototypes.

---

# 39. Language + Vision Research

The source references a Language and Vision laboratory.

Recommended architecture:

```text
Image / Study
   +
Text / Report / Prompt
      ↓
Multimodal Research Model
      ↓
Structured Research Finding
      ↓
Evidence / Review
```

---

# 40. Multimodal Provider Interface

```text
MultimodalProvider
├── encode_image()
├── encode_text()
├── answer_grounded_question()
├── extract_structured_output()
└── provenance()
```

---

# 41. Medical RAG

Potential knowledge sources:

```text
Approved clinical protocols
Imaging manuals
Research publications
Study metadata
Model cards
Anatomy references
Project documentation
```

RAG should not silently convert external text into medical instructions.

---

# 42. Image-Grounded RAG

```text
Study Metadata
      +
Selected Region / Artifact
      +
Approved Knowledge Sources
      ↓
Context Builder
      ↓
Multimodal Model
      ↓
Evidence-Grounded Draft
      ↓
Human Review
```

---

# 43. Federated Learning Plane

The source explicitly references an open framework for federated learning.

Architecture:

```text
Institution A          Institution B          Institution C
Local Data             Local Data             Local Data
    │                      │                      │
    ▼                      ▼                      ▼
Local Training         Local Training         Local Training
    │                      │                      │
    └────────── Model Updates / Secure Aggregation ──────────┐
                                                              ▼
                                                     Global Model
                                                              │
                                                              ▼
                                                        Evaluation
```

Raw clinical images need not be centralized.

---

# 44. Federated Learning Provider

```text
FederatedLearningProvider
├── create_round()
├── register_site()
├── distribute_model()
├── collect_update()
├── aggregate()
├── evaluate()
└── audit()
```

---

# 45. Federated Learning Governance

Track:

```text
Site
Dataset Definition
Eligibility
Model Version
Round
Update Hash
Aggregation
Metrics
Approval
```

---

# 46. Federated Privacy Boundary

Federated learning does not automatically guarantee privacy.

Additional controls may include:

- secure aggregation;
- access controls;
- governance;
- model-update inspection;
- privacy-preserving techniques where appropriate;
- institutional agreements.

---

# 47. Apache Flink Role

The source includes Apache Flink.

Recommended uses:

```text
Streaming Metadata
Device Events
AI Inference Events
Workflow Events
Federated Training Events
Operational Monitoring
```

Do not use stream processing as the authoritative medical image archive.

---

# 48. Streaming Architecture

```text
Event Source
     ↓
Flink
     ↓
Validation / Enrichment
     ↓
Event Store / Workflow
     ↓
Analytics
```

---

# 49. Kryo Role

The source includes Kryo.

Use as:

```text
JVM Internal Serialization Option
```

but do not make Kryo the external interoperability contract.

External contracts should use stable documented formats.

---

# 50. Event Model

```text
StudyIngested
SeriesValidated
DeidentificationCompleted
InferenceRequested
InferenceCompleted
SegmentationCreated
AnnotationReviewed
ModelApproved
FederatedRoundStarted
FederatedRoundCompleted
PlanningArtifactCreated
```

---

# 51. Event Envelope

```yaml
event:
  id: evt_001
  type: inference.completed
  project: imaging_project_A
  study_ref: study_001
  model_ref: model_v4
  timestamp: "..."
  status: success
```

---

# 52. Model Registry

```yaml
model:
  id: organ_seg_v4
  framework: monai
  task: segmentation
  intended_use: research_assistance
  training_dataset: dataset_v7
  validation:
    status: validated_for_internal_research
  deployment:
    status: approved
```

---

# 53. Model Lifecycle

```text
EXPERIMENTAL
    ↓
VALIDATED
    ↓
APPROVED
    ↓
DEPLOYED
    ↓
MONITORED
    ↓
RETIRED
```

---

# 54. Model Governance Metadata

Store:

```text
Training Dataset
Validation Dataset
Metrics
Subgroup Evaluation
Intended Use
Exclusions
Model Version
Code Commit
Reviewer
Deployment Site
```

---

# 55. Dataset Registry

```yaml
dataset:
  id: study_dataset_v3
  domain: medical_imaging
  privacy: deidentified
  modalities:
    - CT
  annotations:
    - segmentation
  usage:
    - research
    - model_validation
```

---

# 56. Dataset Provenance

```text
Source Study
   ↓
De-identification
   ↓
Selection Criteria
   ↓
Annotation
   ↓
Quality Review
   ↓
Dataset Version
```

---

# 57. Annotation Architecture

```text
Image
  ↓
Manual Annotation
  OR
AI-Assisted Draft
  ↓
Reviewer
  ↓
Approved Annotation
```

---

# 58. Annotation Versioning

```yaml
annotation:
  id: ann_001
  source_series: series_001
  author_type: human
  assisted_by_model: organ_seg_v3
  version: 5
  review_status: approved
```

---

# 59. Evaluation Framework

Metrics depend on task.

Examples:

```text
Segmentation
Dice
IoU
Hausdorff distance

Detection
Precision
Recall
mAP

Classification
Sensitivity
Specificity
AUROC

Registration
Target registration error
```

---

# 60. Clinical Evaluation Boundary

Research metrics do not by themselves establish clinical utility.

Keep separate:

```text
TECHNICAL VALIDATION
MODEL PERFORMANCE

CLINICAL VALIDATION
WORKFLOW / PATIENT-CARE IMPACT

REGULATORY VALIDATION
APPLICABLE APPROVAL PROCESS
```

---

# 61. Reproducibility Package

```text
experiment.yaml
dataset.yaml
model.yaml
environment.yaml
metrics.json
logs/
artifacts/
report.md
```

---

# 62. Experiment Tracking

Persist:

```text
Git Commit
Environment
Dataset Version
Preprocessing
Model
Hyperparameters
Seed
Metrics
Artifacts
Reviewer
```

---

# 63. pulse2percept Role

The source explicitly includes `pulse2percept`.

Recommended domain profile:

```text
Bionic Vision Research
```

Architecture:

```text
Visual Input
    ↓
Retinal / Prosthetic Model
    ↓
pulse2percept
    ↓
Percept Simulation
    ↓
Research Evaluation
```

---

# 64. Bionic Vision Research Separation

Do not mix prosthetic-vision simulation outputs with conventional radiology outputs.

Use separate project schemas and validation criteria.

---

# 65. Open Source Imaging Initiative Profile

The source references an Open Source Imaging Initiative for medical-imaging devices.

Potential JFXAI4CV integration:

```text
Open Imaging Device
       ↓
Raw / Reconstructed Data
       ↓
DICOM / Research Adapter
       ↓
JFXAI4CV
```

Hardware validation remains device-specific.

---

# 66. Imaging Device Abstraction

```text
ImagingDeviceProvider
├── get_capabilities()
├── acquire_metadata()
├── export_study()
├── get_calibration()
└── get_device_status()
```

This provider should not directly control acquisition hardware unless explicitly engineered for that device.

---

# 67. Scientific Imaging Profile

Not all source components are strictly clinical.

JFXAI4CV can support:

```text
Medical Imaging
Scientific Imaging
Microscopy
Bionic Vision
Biomechanical Imaging
```

through project-specific profiles.

---

# 68. Microscopy / EM Profile

```text
2D Image Tiles
      ↓
AlignTK
      ↓
Aligned Stack
      ↓
Volume Reconstruction
      ↓
AI / Visualization
```

---

# 69. 3D Scientific Visualization

```text
Image / Simulation Data
      ↓
Geometry / Volume
      ↓
VTK / Slicer / Viewer
      ↓
Interactive Visualization
```

---

# 70. AR Scientific Visualization

The source includes an open-source pipeline for creating AR models from scientific data.

Recommended architecture:

```text
Scientific Data
      ↓
3D Reconstruction
      ↓
Mesh / Volume
      ↓
AR Asset
      ↓
JFXAI4MAR Adapter
      ↓
Spatial Visualization
```

---

# 71. JFXAI4MAR Integration

```text
JFXAI4CV
Medical / Scientific 3D Model
       ↓
Approved Export
       ↓
JFXAI4MAR
       ↓
AR / XR Visualization
```

Potential use cases:

- anatomy education;
- scientific visualization;
- research collaboration;
- planning visualization.

Clinical use requires separate validation.

---

# 72. Clara Viz Boundary

The source includes NVIDIA Clara Viz.

Treat it as:

```text
ExternalVisualizationProvider
```

The core architecture should remain portable to open 3D visualization stacks.

---

# 73. Visualization Provider Interface

```text
VisualizationProvider
├── load_volume()
├── load_mesh()
├── set_transfer_function()
├── render()
├── annotate()
└── export_view()
```

---

# 74. Optional Fully Open Visualization Profile

**Proposed.**

```text
OHIF
+
3D Slicer
+
VTK
+
WebGL / open web viewer where needed
```

This provides a path that does not require Clara Viz.

---

# 75. Biometric Components Boundary

The source compendium includes:

- face recognition;
- fingerprint systems;
- AFIS;
- BRIAR;
- NIST biometric image tools;
- face/iris/fingerprint SDKs.

These capabilities should be isolated from clinical imaging.

---

# 76. Separate Biometric Profile

```text
jfxai4cv/
  profiles/
    medical-imaging/
    scientific-imaging/
    biometrics/
```

Do not merge biometric identity templates into the clinical image database.

---

# 77. Biometric Architecture

```text
Capture
  ↓
Quality Assessment
  ↓
Feature Extraction
  ↓
Template
  ↓
Matching
  ↓
Result
```

Use only for authorized identity/research workflows.

---

# 78. BRIAR Role

Treat BRIAR API as:

```text
BiometricResearchEvaluationProvider
```

Separate from medical-imaging services.

---

# 79. NIST Biometric Software Role

Use as:

```text
BiometricImageUtilityProvider
```

where licensing and intended use are appropriate.

---

# 80. AFIS Profile

```text
Fingerprint Image
      ↓
Quality
      ↓
Minutiae / Features
      ↓
Candidate Matching
      ↓
Human / Workflow Review
```

It should not be integrated into medical diagnosis or patient inference.

---

# 81. Biometric Privacy

Biometric templates are sensitive identifiers.

Controls:

```text
Purpose Limitation
Encryption
Retention Limits
Access Control
Audit
Template Separation
No Unrelated Reuse
```

---

# 82. Unified Computer Vision Provider

Medical imaging and biometrics may share infrastructure such as:

```text
Image Decoding
Model Serving
Experiment Tracking
GPU Scheduling
```

but not domain data stores or policy contexts.

---

# 83. GPU / Compute Architecture

```text
Inference Request
      ↓
Scheduler
      ↓
CPU / GPU Worker
      ↓
Model
      ↓
Result
```

---

# 84. Workload Profiles

```text
Interactive Inference
Batch Research
Training
Federated Training
3D Reconstruction
Visualization
Streaming CV
```

Each needs independent quotas and priorities.

---

# 85. Containerized Execution

Recommended:

```text
Container Image
+
Pinned Dependencies
+
Model Version
+
Dataset Reference
```

for reproducible research.

---

# 86. Kubernetes Boundary

Kubernetes may be useful for:

- multi-service deployments;
- model workers;
- GPU scheduling;
- federated-learning coordinators;
- batch jobs.

It should not be mandatory for small research installations.

---

# 87. Local Workstation Profile

```text
Orthanc
3D Slicer
MONAI
PostgreSQL
Object Storage
Jupyter
```

Suitable for:

- research;
- teaching;
- prototyping.

---

# 88. Institutional Server Profile

```text
DICOM Gateway
Object Store
PostgreSQL
MONAI Inference
Model Registry
Flink
OHIF
Audit / IAM
```

---

# 89. Federated Multi-Institution Profile

```text
Central Coordinator
      │
      ├── Site A
      ├── Site B
      └── Site C

Each site:
Local data
Local compute
Local audit
Controlled update exchange
```

---

# 90. JVM Profile

For source-aligned Java components:

```text
JavaCV
DL4J
JGNN
Kryo
Flink
```

behind APIs rather than tightly coupled to the Python/MONAI stack.

---

# 91. Python Clinical AI Profile

```text
MONAI
PyTorch
SimpleITK
NumPy
pydicom
FastAPI
```

`pydicom` is a proposed addition for DICOM manipulation in Python.

---

# 92. Service Separation

```text
dicom-service
viewer-service
annotation-service
ai-inference-service
model-registry-service
federated-service
geometry-service
audit-service
```

---

# 93. API Gateway

```text
Client
  ↓
OIDC / Authorization
  ↓
API Gateway
  ↓
Domain Service
```

---

# 94. Identity Roles

Examples:

```text
Researcher
Annotator
Reviewer
Imaging Specialist
Clinician
Data Steward
ML Engineer
Administrator
Auditor
Federated Site Operator
```

---

# 95. Least Privilege

A model-training service should not automatically have:

```text
Patient Identity Access
Clinical Command Authority
Administrator Rights
```

---

# 96. Audit Model

```yaml
audit_event:
  actor: reviewer_01
  action: approve_segmentation
  study_ref: study_001
  artifact_ref: segmentation_004
  timestamp: "..."
```

---

# 97. Immutable Audit Events

Track:

```text
Data Import
De-identification
Dataset Export
Annotation Change
Model Deployment
AI Inference
Review
Federated Training Round
Planning Artifact Export
```

---

# 98. Provenance Graph

```text
Study
  ↓
Preprocessing
  ↓
Dataset
  ↓
Model
  ↓
Inference
  ↓
Derived Artifact
  ↓
Review
```

---

# 99. Data Retention

Define independently for:

```text
Clinical Images
De-identified Research Data
Annotations
AI Results
Models
Logs
Biometric Templates
```

---

# 100. Data Quality

Store:

```text
Completeness
Modality Consistency
Image Corruption
Geometry Consistency
Missing Metadata
Annotation Quality
```

---

# 101. AI Input Validation

Before inference:

```text
Modality Correct?
Geometry Valid?
Required Series Present?
Pixel Type Supported?
Model Intended Use Matches?
      ↓
Run / Reject
```

---

# 102. AI Output Validation

After inference:

```text
Schema Valid?
Expected Shape?
Finite Values?
Spatial Registration Valid?
Confidence Available?
Model Version Recorded?
      ↓
Publish Draft Artifact
```

---

# 103. Human Review Workflow

```text
AI Draft
   ↓
Reviewer Queue
   ↓
Inspect
   ↓
Accept / Modify / Reject
   ↓
Approved Artifact
```

---

# 104. Workflow State Model

```text
INGESTED
DEIDENTIFIED
READY
PROCESSING
AI_DRAFT
REVIEW
APPROVED
ARCHIVED
```

---

# 105. JFXAI4BPM Integration

```text
Imaging Event
    ↓
JFXAI4CV
    ↓
Workflow Event
    ↓
JFXAI4BPM
    ↓
Review / Research / Approval Process
```

JFXAI4BPM should coordinate process state, not own images.

---

# 106. JFXLMS Integration

```text
JFXLMS
Learning Objective
      ↓
JFXAI4CV
De-identified Training Study / Simulation
      ↓
Learner Annotation / Analysis
      ↓
Evaluation
      ↓
Skill Evidence
```

---

# 107. Medical Imaging Education Boundary

Use:

- de-identified datasets;
- synthetic cases;
- teaching datasets;
- authorized training data.

Do not expose identifiable clinical data to general learning workflows.

---

# 108. JFXCMS Integration

```text
JFXCMS
Collaborative Research / Development
      ↓
Algorithm / Model Challenge
      ↓
De-identified Dataset
      ↓
Submission
      ↓
Evaluation
      ↓
Research Evidence
```

---

# 109. EvalAI-Style Challenge Pattern

Even though EvalAI is not named in the current JFXAI4CV README, it exists elsewhere in the portfolio and can be reused architecturally:

```text
Dataset
  ↓
Challenge
  ↓
Submission
  ↓
Metric
  ↓
Leaderboard / Review
```

This is a cross-project recommendation.

---

# 110. JFXAI4MAR + JFXLMS Combined Scenario

```text
Medical / Scientific 3D Model
       ↓
JFXAI4MAR XR Environment
       ↓
JFXLMS Training Scenario
       ↓
Learner Interaction
       ↓
Assessment Evidence
```

---

# 111. Scientific Digital Twin

```text
Imaging Data
    ↓
Segmentation
    ↓
Geometry
    ↓
Physics / Biomechanical Model
    ↓
Simulation
    ↓
Visualization
```

---

# 112. Biomechanical Modeling

The MAP source alignment supports export toward:

```text
OpenSim
Finite Element Models
```

This enables musculoskeletal research pipelines.

---

# 113. Simulation Provider

```text
BiomechanicsProvider
├── build_model()
├── assign_materials()
├── configure_boundary_conditions()
├── run()
├── validate()
└── export_results()
```

Actual solver choice remains replaceable.

---

# 114. MBSE Mapping

```text
Stakeholder Need
      ↓
Clinical / Research Use Case
      ↓
Imaging Requirement
      ↓
Data / AI / Visualization Capability
      ↓
Component
      ↓
Verification
```

---

# 115. MBSE → CAD → CAM → CAS

```text
MBSE
Requirements / workflow / architecture
      ↓
CAD
Anatomical / device / geometric models
      ↓
CAM
Physical model / device / guide manufacturing where applicable
      ↓
CAS
Imaging / AI / simulation / performance analysis
```

---

# 116. CAD / Geometry Integration

Potential open pipeline:

```text
DICOM
  ↓
Segmentation
  ↓
Mesh
  ↓
FreeCAD / Blender / Slicer
  ↓
Engineering / Visualization Asset
```

FreeCAD and Blender are proposed additions.

---

# 117. CAM Boundary

If physical guides/models are manufactured:

```text
Approved Geometry
      ↓
Manufacturing Review
      ↓
CAM
      ↓
Fabrication
      ↓
Inspection
```

Medical-device or patient-specific manufacturing can be regulated and requires separate validation.

---

# 118. CAS Architecture

```text
Imaging Pipeline
      ↓
AI Model
      ↓
Simulation
      ↓
Synthetic / Historical Test
      ↓
Performance Metrics
      ↓
Evidence
```

---

# 119. Imaging Pipeline DSL

JFXAI4CV can expose a low-code workflow:

```text
Load Study
   ↓
De-identify
   ↓
Resample
   ↓
Normalize
   ↓
Segment
   ↓
Register
   ↓
Measure
   ↓
Render
   ↓
Review
```

---

# 120. Low-Code Node Types

```text
DICOM Input
Image Transform
Registration
Segmentation
Detection
Classification
Geometry
Visualization
AI Model
Review Gate
Export
```

---

# 121. Pipeline Contract

```yaml
pipeline:
  id: musculoskeletal_segmentation_v2
  nodes:
    - dicom_input
    - deidentify
    - resample
    - monai_segmentation
    - mesh
    - human_review
    - export
```

---

# 122. AI Agent Layer

Potential agents:

```text
Dataset Preparation Agent
Imaging QA Agent
Research Assistant
Experiment Analyst
Annotation Assistant
Model Evaluation Agent
Documentation Agent
```

No agent receives autonomous diagnostic authority.

---

# 123. MCP Tool Plane

Potential tools:

```text
get_study_metadata
list_series
run_deidentification
run_inference
get_model_card
compare_segmentations
create_research_report
query_experiment
```

---

# 124. Restricted MCP Actions

General-purpose agents should not be exposed directly to:

```text
reidentify_subject
publish_clinical_diagnosis
modify_patient_record
approve_surgical_plan
override_review
export_sensitive_dataset
```

---

# 125. Imaging RAG MCP Flow

```text
Researcher
    ↓
AI Agent
    ↓
MCP Gateway
    ↓
Read-Only Imaging / Model Tools
    ↓
Evidence
    ↓
Grounded Answer
```

---

# 126. Model Card

Each deployed model should document:

```text
Task
Intended Use
Excluded Uses
Training Data
Validation Data
Metrics
Limitations
Known Failure Modes
Version
License
```

---

# 127. Dataset Card

```text
Purpose
Source
Population / Domain
Modality
Selection Criteria
Annotation
De-identification
Known Biases
License / Access
```

---

# 128. Bias & Generalization Evaluation

Evaluate where relevant across:

```text
Scanner / Vendor
Site
Acquisition Protocol
Image Quality
Demographic Groups
Disease / Condition Spectrum
Temporal Drift
```

Only where data governance permits the relevant analysis.

---

# 129. Distribution Shift

```text
Production Input
      ↓
Quality / Distribution Monitor
      ↓
Shift?
  ├── No → continue
  └── Yes
       ↓
   Review
       ↓
   Revalidation / Retraining
```

---

# 130. No Silent Auto-Retraining

Avoid:

```text
New Production Data
       ↓
Automatic Retraining
       ↓
Automatic Clinical Deployment
```

Prefer:

```text
New Data
   ↓
Research Training
   ↓
Validation
   ↓
Review
   ↓
Controlled Deployment
```

---

# 131. Monitoring

Track:

```text
Inference Volume
Latency
Failure Rate
Input Quality
Model Drift
Review Acceptance
Manual Corrections
Version Distribution
Compute Utilization
```

---

# 132. Technical Observability

```text
DICOM ingestion rate
DICOM errors
Storage latency
Viewer load time
Inference latency
GPU memory
Flink lag
Federated round status
API error rate
```

---

# 133. Imaging-Specific Observability

```text
Missing slices
Corrupt instances
Geometry mismatch
Unsupported modality
Spacing anomalies
Series inconsistency
```

---

# 134. Security Architecture

```text
User / Service
      ↓
OIDC
      ↓
Role + Project + Data Policy
      ↓
API Gateway
      ↓
Imaging / AI Service
      ↓
Audit
```

---

# 135. Encryption

Use appropriate encryption:

```text
In Transit
At Rest
Backups
Model/Dataset Exchange
Federated Coordination
```

---

# 136. Key Separation

Keep:

```text
Clinical Identity Keys
        ≠
Research Pseudonymous IDs
        ≠
Biometric Templates
```

---

# 137. Backup / Recovery

Critical stores:

```text
Clinical Integration Metadata
Research Dataset Registry
Model Registry
Audit Logs
Configurations
Derived Artifacts
```

must have defined restore procedures.

---

# 138. Open Deployment Profiles

## Profile A — Research Workstation

```text
3D Slicer
MONAI
SimpleITK
Jupyter
PostgreSQL
Local Object Store
```

## Profile B — Web Imaging

```text
Orthanc
DICOMweb
OHIF
FastAPI
PostgreSQL
Object Storage
```

## Profile C — AI Imaging

```text
MONAI
Model Registry
GPU Workers
DICOM Gateway
Review UI
```

## Profile D — Federated Research

```text
Local Imaging Stores
Local Training
Federated Coordinator
Audit
Controlled Model Exchange
```

## Profile E — Scientific / Biomechanical

```text
MAP
Slicer
Mesh / OpenSim / FE Export
Simulation
Visualization
```

---

# 139. JVM Integration Profile

```text
Flink
DL4J
JavaCV
JGNN
Kryo
```

Recommended for JVM-centric services, but isolated behind APIs.

---

# 140. Open AI Profile

```text
MONAI
PyTorch
SimpleITK
OpenCV
FastAPI
MLflow-compatible registry
ONNX Runtime where useful
```

---

# 141. Inference Runtime Portability

Use:

```text
PyTorch
ONNX Runtime
JVM provider
edge provider
```

behind the same inference contract.

---

# 142. Research Notebook Boundary

Jupyter/notebooks are appropriate for:

- exploration;
- analysis;
- prototyping;
- reproducible experiments.

Production inference should be packaged as versioned services/jobs.

---

# 143. Repository Structure

```text
jfxai4cv/
├── README.md
│
├── docs/
│   ├── architecture/
│   ├── dicom/
│   ├── privacy/
│   ├── visualization/
│   ├── ai/
│   ├── federated/
│   ├── geometry/
│   ├── evaluation/
│   └── governance/
│
├── core/
│   ├── studies/
│   ├── series/
│   ├── artifacts/
│   ├── annotations/
│   └── events/
│
├── dicom/
│   ├── gateway/
│   ├── dicomweb/
│   └── deidentification/
│
├── viewers/
│   ├── ohif/
│   ├── slicer/
│   └── clara-viz/
│
├── imaging/
│   ├── itk/
│   ├── registration/
│   ├── aligntk/
│   └── geometry/
│
├── ai/
│   ├── monai/
│   ├── yolo/
│   ├── dl4j/
│   ├── multimodal/
│   ├── models/
│   └── evaluation/
│
├── federated/
│   ├── coordinator/
│   ├── site/
│   └── governance/
│
├── scientific/
│   ├── pulse2percept/
│   ├── musculoskeletal/
│   ├── microscopy/
│   └── biomechanics/
│
├── biometrics/
│   ├── face/
│   ├── iris/
│   ├── fingerprint/
│   └── evaluation/
│
├── integrations/
│   ├── jfxai4mar/
│   ├── jfxlms/
│   ├── jfxcms/
│   └── jfxai4bpm/
│
└── tests/
    ├── dicom/
    ├── privacy/
    ├── ai/
    ├── geometry/
    ├── federated/
    └── security/
```

---

# 144. MVP Phase 1 — Imaging Core

Implement:

```text
Study / Series Registry
DICOM Gateway
DICOMweb
De-identification
PostgreSQL
Object Storage
```

---

# 145. MVP Phase 2 — Visualization

Add:

```text
OHIF
3D Slicer
Annotation Registry
Derived Artifact Registry
```

---

# 146. MVP Phase 3 — MONAI Inference

Add:

```text
MONAI
Model Registry
Inference API
Segmentation
Evaluation
Human Review
```

---

# 147. MVP Phase 4 — Geometry & Planning

Add:

```text
Slicer Surgical Planning
MAP
Mesh Pipeline
Registration
3D Export
```

---

# 148. MVP Phase 5 — Federated Learning

Add:

```text
Federated Coordinator
Site Agent
Local Training
Secure Governance
Round Tracking
```

---

# 149. MVP Phase 6 — Scientific Imaging

Add:

```text
AlignTK
pulse2percept
microscopy profile
biomechanical modeling
```

---

# 150. MVP Phase 7 — AR / Learning Integration

Add:

```text
JFXAI4MAR
JFXLMS
de-identified training scenarios
3D anatomy / scientific visualization
```

---

# 151. MVP Phase 8 — Optional Biometrics

Only if the project intentionally retains biometric capabilities:

```text
Separate biometric data plane
Face
Iris
Fingerprint
BRIAR / NIST tools
AFIS
Independent governance
```

Do not merge this into the medical image store.

---

# 152. First Executable Slice

Recommended:

```text
DICOM Study
     ↓
De-identification
     ↓
MONAI Segmentation
     ↓
Derived Segmentation Artifact
     ↓
3D Slicer Review
     ↓
Approved Research Artifact
```

This validates:

- ingestion;
- privacy;
- storage;
- AI inference;
- artifact provenance;
- human review.

---

# 153. Second Executable Slice

```text
Musculoskeletal Imaging
      ↓
Segmentation
      ↓
MAP
      ↓
Mesh
      ↓
OpenSim / FE Export
      ↓
Research Simulation
```

---

# 154. Third Executable Slice

```text
Site A Data
Site B Data
Site C Data
      ↓
Local MONAI Training
      ↓
Federated Aggregation
      ↓
Global Model
      ↓
Cross-Site Evaluation
```

---

# 155. Fourth Executable Slice

```text
Scientific Image Stack
      ↓
AlignTK
      ↓
3D Reconstruction
      ↓
Visualization
      ↓
AR Export
      ↓
JFXAI4MAR
```

---

# 156. Cross-Portfolio Architecture

```text
                         JFXLMS
                 Imaging / XR Education
                          ▲
                          │
JFXCMS ◄────────────── JFXAI4CV ─────────────► JFXAI4MAR
Research Challenges      Medical AI            AR / XR
                          │
                          ▼
                      JFXAI4BPM
                 Review / Approval Flow
```

---

# 157. Architecture Anti-Pattern

Avoid:

```text
Viewer
 tightly coupled to
One PACS
 tightly coupled to
One AI Framework
 tightly coupled to
One GPU/Vendor Stack
```

Prefer:

```text
DICOMProvider
+
ViewerProvider
+
MedicalAIProvider
+
VisualizationProvider
+
Canonical Artifact Model
```

---

# 158. Key Design Principle

> **Use DICOM/DICOMweb-compatible boundaries for medical imaging, MONAI as the healthcare-AI default, 3D Slicer/MAP for geometry and planning workflows, open viewer/storage alternatives for portability, federated learning for multi-site research, and strict human-review/provenance gates between AI-derived outputs and clinical use.**

---

# 159. Source vs Recommendation Boundary

This document distinguishes:

```text
SOURCE PROJECT FACT
→ components explicitly listed in the current JFXAI4CV README

ARCHITECTURE RECOMMENDATION
→ proposed integration design and provider interfaces

PROPOSED ADDITION
→ Orthanc, OHIF, DICOMweb-centric architecture,
   SimpleITK/ITK, VTK, pydicom, object storage,
   model-registry and related glue
```

The current README does not state that all named components are currently installed or integrated together.

---

# 160. Open-Source / Licensing Boundary

The target architecture is:

> **open, modular and standards-oriented, designed to minimize vendor lock-in and enable independent implementations.**

The source compendium contains a mixture of:

- open-source software;
- research projects;
- external/platform-specific components;
- model ecosystems;
- biometric tooling.

Before distribution or commercial deployment, verify:

```text
software license
model/checkpoint license
dataset license
medical-image dataset terms
biometric-data terms
commercial-use rights
third-party SDK terms
trademarks
```

---

# 161. Medical / Research Disclaimer

JFXAI4CV should be treated as an engineering and research architecture unless a specific deployment has been independently validated for clinical use.

AI outputs may be wrong, incomplete, biased, poorly calibrated, or outside their validated domain.

Clinical and patient-specific workflows require appropriate:

- professional review;
- privacy protection;
- cybersecurity;
- data governance;
- software validation;
- risk management;
- quality systems;
- medical-device and institutional compliance where applicable.

Biometric capabilities should remain separated from medical imaging unless an explicit, lawful, purpose-limited workflow requires otherwise.
