# GPC Gran Quemado — JSON Microservice API

[![IEEE Latin America Transactions](https://img.shields.io/badge/Published-IEEE%20Latin%20America%20Transactions-blue)](https://latamt.ieeer9.org)
[![IMSS GPC 375-17](https://img.shields.io/badge/Guideline-IMSS--375--17-green)](https://www.imss.gob.mx)
[![HL7 FHIR R4](https://img.shields.io/badge/Standard-HL7%20FHIR%20R4-orange)](https://hl7.org/fhir/)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey)](https://creativecommons.org/licenses/by/4.0/)

---

## Manuscript Information

**Title:** Clinical Practice Guidelines as a JSON Service: A Proposed Architecture for Decision Support in Major Burning Management

**Submission ID:** 10745

**Journal:** IEEE Latin America Transactions

---

## Authors

**Jesús Ramírez** received the B.S. degree in software engineering from the Instituto Tecnológico de Sonora, Sonora, Mexico, in 2016, and the M.S. degree in information technology from the University of Guadalajara, Guadalajara, Jalisco, Mexico, in 2024. His major field of study includes software engineering, project management, and technological integration. He is currently pursuing research in the development of computational models for the classification and analysis of burn injuries. — Universidad de Guadalajara, CUCEA, Zapopan, México.

**Rocío Maciel** is responsible for outreach and talent management at the Center for Innovation in Smart Cities at the University of Guadalajara. She holds a Doctorate and a Master's degree in Administration and Teaching Methodology from the Instituto Mexicano de Estudios Pedagógicos (IMEP). She has more than 25 years of experience in Information Technologies, having served as Director of Information Technology, Coordinator of the Graphic Design area, Coordinator of the Bachelor's Degree in Information Systems, Legal Consultant, and Technical-Pedagogical Advisor. — Universidad de Guadalajara, Zapopan, México.

**Victor Larios** received his Ph.D. and a DEA in Computer Science at the Technological University of Compiegne, France, and a B.A. in Electronics Engineering at the ITESO University in Guadalajara, Mexico. He works at the University of Guadalajara (UDG) and holds a Full Professor-Researcher position at the Department of Information Systems where he is the Director of the Smart Cities Innovation Center at the CUCEA UDG Campus. Dr. Larios is the founder of the UDG Ph.D. in Information Technologies in 2007 and leads projects in the Guadalajara academia, government, and High Technology Industry local ecosystem (including IBM, Intel, and HPE), focusing on Distributed Systems, IoT, Data Analytics and Visualization, Serious Games, and Smart Cities. — Universidad de Guadalajara, CUCEA Smart Cities Innovation Center, Zapopan, México.

---

## Overview

Clinical Practice Guidelines (CPGs) encode evidence-based medical knowledge but are typically distributed as static PDF documents, making them inaccessible to automated clinical decision support (CDS) systems. This repository contains the formal JSON/REST API specification that formalizes the **IMSS Clinical Practice Guideline for Major Burn Management (GPC IMSS-375-17)** as a versioned microservice.

The specification makes clinical decision rules programmatically accessible for integration with Electronic Health Record (EHR) platforms, hospital information systems, and decision support tools, aligned with HL7 FHIR R4 interoperability standards.

---

## Repository Contents

| File | Description |
|------|-------------|
| `gpc_gran_quemado_api.json` | Full JSON schema defining all 7 clinical endpoints, request/response structures, GPC business rules, and integration standards. This file constitutes the complete API specification needed to implement the microservice described in the manuscript. |

---

## How to Use

The `gpc_gran_quemado_api.json` file is a self-contained API specification. A developer or institution can use it to:

1. **Implement the microservice** in any REST-compatible framework (e.g., FastAPI, Express, Spring Boot)
2. **Validate clinical inputs/outputs** against the defined JSON schemas
3. **Integrate with EHR systems** using the HL7 FHIR R4 alignment defined in the spec
4. **Reproduce the clinical scenarios** described in the manuscript by invoking the endpoints with the sample parameters provided in the paper

---

## API Endpoints

The specification defines 7 clinical decision endpoints, each encapsulating a specific recommendation from GPC IMSS-375-17:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/gpc/gran-quemado/clasificacion` | POST | Burn classification using Benaim scale and Baux prognostic index |
| `/api/v1/gpc/gran-quemado/evaluacion-inicial` | POST | ABCDE initial assessment checklist and first interventions |
| `/api/v1/gpc/gran-quemado/resucitacion-hidrica` | POST | Fluid resuscitation volume calculation using Parkland formula |
| `/api/v1/gpc/gran-quemado/manejo-dolor` | POST | Analgesia and sedation protocol by procedure type |
| `/api/v1/gpc/gran-quemado/prevencion-infeccion` | POST | Wound management and infection prophylaxis recommendations |
| `/api/v1/gpc/gran-quemado/soporte-nutricional` | POST | Caloric and protein requirements using Curreri formula |
| `/api/v1/gpc/gran-quemado/criterios-referencia` | POST | Evaluation of transfer criteria to a specialized burn unit |

---

## Clinical Rules Formalized

### Major Burn Definition (Gran Quemado)
A patient meets criteria if at least one of the following applies:
- Adult ≥ 65 years with BSA ≥ 10% second or third degree burns
- Adult < 65 years with BSA ≥ 20% second or third degree burns
- Any third-degree burn > 5% BSA
- Airway burn or smoke inhalation injury
- High-voltage electrical burn
- Severe chemical burn
- Burns to special areas: face, hands, feet, genitals, perineum, major joints
- Circumferential burns of extremities or thorax
- Pediatric patient with BSA ≥ 10% second or third degree burns
- Burn associated with polytrauma

### Key Clinical Formulas
- **Parkland Formula:** `Volume (ml) = 3–4 ml × weight (kg) × %BSA` — first half in 8h from injury, second half over next 16h
- **Baux Score:** `Age + %BSA` — score > 100: high mortality; > 140: critical prognosis
- **Curreri Formula:** `25 kcal/kg/day + 40 kcal/%BSA/day`

### Benaim Scale
| Type | Description |
|------|-------------|
| A | Superficial (1st degree): erythema, pain, no blisters |
| AB Superficial | 2nd degree superficial: blisters, pink base, painful, heals spontaneously in 14 days |
| AB Deep | 2nd degree deep: white/red base, less painful, may require grafting |
| B | 3rd degree: painless, leathery appearance, requires grafting if > 1 cm |

---

## Integration Standards

| Standard | Role |
|----------|------|
| HL7 FHIR R4 | Interoperability and resource alignment |
| SNOMED-CT | Clinical terminology coding |
| ICD-10-CM | Diagnostic coding (T31, T27) |
| LOINC | Laboratory and clinical observation codes |
| OAuth 2.0 / Bearer Token | Authentication |
| X-GPC-Version header | API versioning |

All API calls are logged with timestamp, user, endpoint, and parameter hash for full audit traceability compliant with **NOM-024-SSA3-2012**.

---

## Metadata

| Field | Value |
|-------|-------|
| Service ID | `IMSS-GPC-375-GRAN-QUEMADO` |
| Version | `2.1.0` |
| Source Guideline | IMSS-375-17 |
| Institution | Instituto Mexicano del Seguro Social (IMSS) |
| Care Level | Tertiary |
| ICD-10 Codes | T31, T27 |
| Guideline Date | 2017-03-09 |
| JSON Formalization Date | 2025-03-01 |

---

## Citation

If you use this specification in your research, please cite:

```
J. Ramírez, R. Maciel, and V. Larios,
"Clinical Practice Guidelines as a JSON Service: A Proposed Architecture
for Decision Support in Major Burning Management,"
IEEE Latin America Transactions, Submission ID: 10745, 2025.
```

---

## License

This API specification is released for academic and research use. Clinical deployment requires validation by certified medical personnel in accordance with institutional guidelines.
