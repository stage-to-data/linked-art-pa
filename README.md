# Readme: Linked Art Extension for Performing Arts (LA-PA)

Version 0.9. May 2026
An extension of the [Linked Art](https://linked.art) data model for performing arts documentation


## **Overview**

LA-PA extends the [Linked Art](https://linked.art) data model to support the documentation of performing arts events, works, and associated entities. It is developed within the **LAPA (Linked Art Performing Arts) working group** as part of the ERC Advanced Grant project [**STAGE: From Stage to Data** (2024–2028)](https://stage-to-data.huma-num.fr/en/).

The primary corpus is the **Festival d'Avignon (1947–present)**, one of the world's most documented performing arts festivals, used as a longitudinal test case for the ontology.

LA-PA is designed to be:

* **Interoperable** with CIDOC-CRM and Linked Art  
* **Source-critical**:  every data point is traceable to a source and a data assignment  
* **Scalable**: from a single performance to thousands of performances

---

## **Full Model Documentation**

The complete LA-PA data model (all 13 models, 31 collections, 44 fields, and their ontological mappings) is documented and browsable on the **Pletka Semantic Platform**:

🔗 [https://dev.pletka.io/projects/STA](https://dev.pletka.io/projects/STA)

## **Implementation**

We are currently working on the implementation of the ontology. Updates will be shared in this repository as the work progresses.

---

## **The LAPA Working Group**

LA-PA is developed collaboratively by the **LAPA (Linked Art Performing Arts)** working group, which brings together researchers, ontologists, and cultural heritage professionals from multiple institutions. All interested parties are welcome to participate. 

### Get Involved

- Join the Slack workspace (email [robert.sanderson@yale.edu](mailto:robert.sanderson@yale.edu) for an invitation). \#performing-arts channel  
- Join the discussion group every two Thursdays (impair weeks) at 5 pm (Paris Time) (email [clarisse.bardiot@univ-rennes2.fr](mailto:clarisse.bardiot@univ-rennes2.fr) for an invitation)  
- Add to Issues / Questions

### Editorial Board

Starting in October 2024, the Linked Art Performing Arts initiative is managed by an editorial board, which currently consists of the following people:

Clarisse Bardiot (chair, Université Rennes 2). [https://orcid.org/0000-0002-8126-8249](https://orcid.org/0000-0002-8126-8249)   
George Bruseker (Takin Solutions) [https://orcid.org/0000-0001-7519-1970](https://orcid.org/0000-0001-7519-1970)   
Øyvind Eide (University of Cologne) [https://orcid.org/0000-0002-7766-6287](https://orcid.org/0000-0002-7766-6287)  
Brandon Farnsworth (Université Rennes 2\) [https://orcid.org/0000-0001-9095-2360](https://orcid.org/0000-0001-9095-2360)   
Jeanne Fras (Université Rennes 2\) [https://orcid.org/0009-0003-2633-8253](https://orcid.org/0009-0003-2633-8253)   
Bernard Jacquemin (Enssib, École nationale supérieure des sciences de l'information et des bibliothèques)  
Diane Jakacki (Bucknell University)  [https://orcid.org/0000-0002-7836-1223](https://orcid.org/0000-0002-7836-1223)   
Antonios Lagarias (Université Rennes 2\) [https://orcid.org/0009-0007-1895-8603](https://orcid.org/0009-0007-1895-8603)   
Anne Le Gall (TMNlab)  
Richard Palmer (Victoria and Albert Museum)  
Elena Pierazzo (University of Tours)  
Doug Reside (NYPL)  
Robert Sanderson (Yale University)

---

## **Key Design Principles**

### **1\. Work, Production, Performance — three distinct levels**

The central modelling decision in LA-PA is the distinction between **Work**, **Production**, and **Performance**.

A **Work** is the abstract artistic conception of a staging project — the creative vision of a director or collective. It is not a play text (documented as Textual Work) and not a performance event. It is the project itself, in the sense that Patrice Chéreau's staging of Hamlet (1988) is a recognisable artistic entity regardless of where it is performed.

A **Production** is a realisation of a Work in a specific context. The same Work may give rise to multiple Productions, eg. in Avignon (open-air, Cour d'honneur), in Paris (black box, Théâtre Nanterre-Amandiers, etc.), that, despite their differences, remain realisations of the same project.

A **Performance** is a single show on a given date. A Production may contain multiple Performances.

This three-level structure allows:

* Linking different stagings of the same project across venues and years  
* Documenting last-minute changes at the Performance level (cast replacements, cancellations) without affecting the Production record  
* Precise dating of each performance, independent of production-level timespans

### **2\. Textual Work as source text**

A **Textual Work** serves two distinct functions in LA-PA:

* As a **documentary source**: programme, review, contract, press release — any document that describes or evidences a performing arts entity  
* As a **source text**: the specific edition or translation used in the creation of a Work — e.g., the Yves Bonnefoy translation of Hamlet used by Chéreau, which is a Textual Work linked to the Work.

This distinction is critical: the Bonnefoy translation is not Chéreau's Work — it is the textual object that underpins it.

### **3\. Projected Event**

The **Projected Event** model (`CC12_Event_Trigger_Template`, CRMpro) models events *as planned*, typically as they appear in a printed programme. This is distinct from a Performance, which documents what actually occurred. The distinction is crucial for historical research: what was announced often differs from what was performed.

The link between a Projected Event and the Performance that realises it is documented via `CP4_projects`.

### **4\. Source attribution and provenance**

Every field in LA-PA includes:

* A **Source** field linking to the document from which the information was drawn  
* A **Data Assignment** field recording who encoded the information and when

This ensures full scholarly traceability following the principles of source-critical digital humanities research.

### **5\. Contextual classification**

LA-PA uses two AAAO extensions for context-dependent information:

* **ZE2 Appellative Status** — for names valid only within a specific institutional context (e.g., a production's sequence number within a festival)  
* **ZE4 Classificatory Status** — for genre/type classifications that vary by institution or period (e.g., "théâtre" in a festival programme vs "tragédie" in a BnF catalogue record)

### **6\. Actor in Role**

All contributions — performer, stage director, set designer, sponsor, funder, producer — are modelled as **Actor in Role** via `P9_consists_of → E7_Activity`, preserving:

* The normalised role type  
* The verbatim role name as it appears in the source  
* The source document  
* The data assignment

### **7\. Minimal class creation**

No new CRM classes were created. LA-PA uses and extends:

* **CIDOC-CRM** (core)  
* **Linked Art** (profile and patterns)  
* **CRMsoc** (social facts, audience, membership)  
* **CRMpro** (projected events, plans)  
* **CRMdig** (digital objects)  
* **AAAO** (appellative and classificatory status)

---

## **The Data Model**

LA-PA organises performing arts documentation around **13 models**, structured in three layers: **events**, **agents**, and **objects**.

### **Event Layer**

| Model | CRM Base | Linked Art Class | Definition |
| ----- | ----- | ----- | ----- |
| **Overall Event** | E7 Activity | `Activity` | A festival edition, theatrical season, or series — a bounded event that contains multiple unique productions. |
| **Work** | E89 Propositional Object | `PropositionalObject` | The abstract artistic conception of a staging project. A single Work may be realised by multiple Productions across different venues and contexts. |
| **Production** | E7 Activity | `Activity` | A realisation of a Work in a specific context — a particular venue, festival, or season. |
| **Performance** | E7 Activity | `Activity` | A single performance on a specific date and time. |
| **Projected Event** | CC12 (CRMpro) | *(LA-PA extension)* | An event as planned and announced, typically as it appears in a printed programme. It describes a scheduled event that may or may not have taken place, and is distinct from a Performance, which refers to an event that has actually occurred. |

### **Agent Layer**

| Model | CRM Base | Linked Art Class | Definition |
| ----- | ----- | ----- | ----- |
| **Person** | E21 Person | `Person` | An individual contributor to performing arts events. |
| **Group** | E74 Group | `Group` | A company, institution, or team. |
| **Animal** | WE5 Animal | *(LA-PA extension)* | A non-human animal performer or participant. |
| **Audience** | ZE37 (CRMsoc) | *(LA-PA extension)* | A group of spectators defined by category, demographic, or access type. |

### **Object Layer**

| Model | CRM Base | Linked Art Class | Definition |
| ----- | ----- | ----- | ----- |
| **Textual Work** | E33 Linguistic Object | `LinguisticObject` | Any document that describes, plans, or documents performing arts entities — programme, play text, review, translation, contract. Also used to document the source text on which a Work is based. |
| **Image** | E36 Visual Item | `VisualItem` | A photograph, poster, or illustration depicting a performing arts entity. |
| **Digital Object** | D1 (CRMdig) | `DigitalObject` | A digital resource  (e.g. website, PDF, video, database, IIIF manifest, etc.). |
| **Place** | E27 Site | `Place` | A performance venue or a geographic location (e.g. a city, a region, etc.). |

---

## **Running Example**

All documentation in this repository is illustrated with a single running example: the **production of Hamlet directed by Patrice Chéreau at the Festival d'Avignon, 1988**.

This production was chosen because:

* It involves the full range of LA-PA entities across all 13 classes  
* It exemplifies the Work / Production distinction: the same Work (Chéreau's staging project) was realised in Avignon, Milan, and Paris as three distinct Productions

| LA-PA Class | Example |
| ----- | ----- |
| Overall Event | 42e edition of the Festival d'Avignon, 1988 |
| Work | Hamlet — staging project by Patrice Chéreau |
| Production | Hamlet, Cour d'honneur, Festival d'Avignon, July 9–19, 1988 |
| Performance | Première, July 9th 1988, 21h30 |
| Projected Event | Hamlet announced in the 1988 programme |
| Textual Work | Programme du Festival 1988; Hamlet trad. Bonnefoy (source text) |
| Image | Photographs by Daniel Cande, Gallica BnF |
| Digital Object | festival-avignon.com/fr/archives |
| Person | Patrice Chéreau; Gérard Desarthe… |
| Group | Théâtre Nanterre-Amandiers; technical team… |
| Place | Cour d'honneur du Palais des Papes, Avignon |
| Audience | General Audience, ca. 2000 spectators |
| Animal | White horse |

---

## **Controlled Vocabularies**

| Domain | Source |
| ----- | ----- |
| Performing Arts | [Art & Architecture Thesaurus](https://www.getty.edu/research/tools/vocabularies/aat/) |
| Roles / Professions | [Library of Congress Relators](https://id.loc.gov/vocabulary/relators.htm) / [BnF Roles](https://data.bnf.fr/vocabulary/roles) |
| Languages | ISO 639 via E56 Language |
| Identifiers | VIAF, ISNI, ARK (BnF), Wikidata |

### **Proposed Getty AAT Additions**

* to complete

---

## **Related Publications**

* **Bardiot, Clarisse.** 2021\. *Performing Arts and Digital Humanities: From Traces to Data*. Hoboken: ISTE / Wiley.  
* **Bardiot et al.** 2025\. "Programme-to-Data: A Pipeline for Performing Arts Archives." *Information Technology and Libraries*. \[arXiv preprint\]  
* **Bollen, Jonathan.** 2016\. 'Data Models for Theatre Research: People, Places, and Performance'. *Theatre Journal* 68(4): 615–32. [DOI](https://doi.org/10.1353/tj.2016.0109)  
* **Oort, Thunnis van, and Julia Noordegraaf.** 2020\. 'Structured Data for Performing Arts History'. *Research Data Journal for the Humanities and Social Sciences* 5(2): 1–12. [DOI](https://doi.org/10.1163/24523666-bja10008)  
* **Peyre, E., Amarger, F., and Chauvat, N.** 2024\. *CapData Opéra*. [HAL](https://hal.science/hal-04639095)

---

## **How to Cite**

If you use LA-PA in your research, please cite it as follows:

Bardiot, Clarisse, George Bruseker, Øyvind Eide, Brandon Farnsworth, Jeanne Fras, Bernard Jacquemin, Diane Jakacki, Antonios Lagarias, Richard Palmer, Doug Reside, and Robert Sanderson. 2026\. *Linked Art Performing Arts Extension (LA-PA), v0.9*. STAGE Project / Université Rennes 2\. [https://github.com/stage-to-data/linked-art-pa](https://github.com/stage-to-data/linked-art-pa)

## **Funding and Acknowledgements**

This work is funded by the **European Research Council (ERC)** under the European Union's Horizon Europe programme, Advanced Grant **STAGE: From Stage to Data** (2024–2028).

---

## **License**

CC BY 4.0 
