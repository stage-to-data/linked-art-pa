# Readme: Linked Art Extension for Performing Arts

## Project Overview

This project extends the Linked Art ontology to better represent performing arts data. It was developed as part of the ERC-funded project **STAGE (From Stage to Data)**, which explores the paradigm shift of digital traces for contemporary performing arts historiography.  

- **Project Website**: STAGE  
- **Contributors**: Clarisse Bardiot, Bernard Jacquemin, Antonios Lagarias, Jeanne Fras  
- **Contact**: clarisse(dot)bardiot(at)univ-rennes2(dot)fr  

Our work builds on state-of-the-art ontologies for performing arts (see below) and is based on case studies from the **Avignon Festival (In and Off)**.  

## Key Contributions

### 1. General Structure

To precisely encode performing arts works, this extension is based on a **three-object composition**. This schema allows the separation between the concept of a work, as well as the different productions. It also enables signaling each of the performances individually, accommodating unforeseen events not described at the production level.

These three objects consist of:

- **A: Work** (*Getty AAT "works (general, creative)"*)  
  - A `PropositionalObject`, representing the concept behind the performance.  

- **B: Production** (*Getty AAT "Performances (creative events)"*)  
  - An `Activity` element encompassing multiple performances in a specific context (venue, festival, event, etc.).  

- **C: Show** (*Getty AAT "Performances (performing arts show)"*)  
  - An `Activity` element referring to the individual show occurring on a precise date.  

This structure allows:
- Listing and distinguishing variations when the same production is presented in multiple locations, such as during a tour.
- Capturing last-minute changes (e.g., cast replacements).
- Precise listing of all performance dates, as level B only captures first and last dates without detailing rest days or multiple performances per day.

Additional objects can be incorporated:
- **Text** (as a `Textual Object`, e.g., the play).
- **Festival** (as an `Activity`, to be developed).
- **Season Programme** (as a `Textual` or `Digital Object`, to be developed).
- **Show Programme** (as a `Textual` or `Digital Object`, to be developed).

### 2. Source Attribution

- Explicit citation of a source at the data level, ensuring traceability and scholarly rigor.
- Primary source for general information (e.g., a show or season programme).
- Secondary source for specific information when necessary.  
- See the **cookbook** for examples.

### 3. Minimal Class Creation

- No additional class creation was necessary; modifications focus on **property extensions and refinements**.

### 4. New Property for Roles (e.g., an actor interpreting Hamlet)

- Introduction of a new property: `has_character`, refining role descriptions.
- Enhances existing **Linked Art** and **CIDOC CRM** frameworks.

### 5. Class Extensions for Existing Properties

- **Event Dimension**:  
  - Extends `Activity` to include the existing `dimension` property, categorizing ticket prices and performance duration.
  - Using `used_specific_object` would require the creation of a non-existent ticket source, which is inaccurate.
  - This extension would require an evolution of **CIDOC**.  
  - `timespan` is already used for production start and end dates (*see **cookbook** for examples*).

- **Language Property for Events**:  
  - Adding language at the **B (Event) level** rather than **A (Work) level** allows multilingual performances to be accurately modeled.
  - Example: *Germinal* was performed in different languages depending on the venue.
  - Requires an extension of **CIDOC CRM**.

### 6. Getty AAT Vocabulary Enhancements

We propose additions to the **Getty Art & Architecture Thesaurus (AAT)** to better represent performing arts venues and events:

- **"Performing Arts Festival"** (or `"Festival (Art)"`), since only `"Art Festivals"`, `"Film Festivals"`, and `"Music Festivals"` exist in the current hierarchy (`"Celebrations"`).  
  - The definition of `"Art Festival"` does not align with theatre festivals, creating confusion.  

- **"Performance (Performing Arts Show)"**:  
  - One representation from a defined production that occurs at a specific time and place.  
  - One production may have several performances.  
  - `"Performance (Performing Arts Show)"` is an instance of `"Performances (Creative Event)"` (**AAT 3000069200**).  
  - This distinction is crucial, as performances can differ between iterations.  

### 7. Controlled Vocabulary for Roles (Professions)

For profession-related vocabulary, we use the **Library of Congress** vocabulary:  
🔗 [https://id.loc.gov/vocabulary/relators.htm](https://id.loc.gov/vocabulary/relators.htm)  

- The Getty vocabulary was insufficient for our needs.
- The **Library of Congress** vocabulary is aligned with the **BnF controlled vocabulary**, offering a **bilingual (English/French) thesaurus**:  
  🔗 [https://data.bnf.fr/vocabulary/roles](https://data.bnf.fr/vocabulary/roles)

---

## Dataset

This repository includes:

- **JSON files** for *Absalon, Absalon !* (directed by Séverine Chavrier, Avignon 2024).  
  - 🔗 [Show programme](https://festival-avignon.com/storage/document/53/349953_667c39485f230.pdf)  

- **JSON files** for *Richard III* (directed by William Mesguich, Avignon OFF 2024).  
  - 🔗 [Season programme of the festival (see p. 238)](https://www.calameo.com/festivaloffavignon/read/007594426b67887e9569e?trackersource=library)

- **Cookbook file** explaining modeling decisions and methodology.

---

## Methodology & References

Our work is informed by:

- **Review of existing performing arts ontologies** *(to be published)*:
  - **CIDOC CRM** (event-based modeling for cultural heritage data)
  - **FRBRoo / LRMoo** (bibliographic and archival structures)
  - **AusStage** (Australian performing arts data model)
  - **ECLAP, EDM, SPA, CapData Opéra**

- **Empirical data** extracted from **Avignon Festival theatre programmes**.

### References:

- **Bardiot, Clarisse.** 2021. *Performing Arts and Digital Humanities: From Traces to Data*. Hoboken: ISTE / Wiley.  
- **Bollen, Jonathan.** 2016. ‘Data Models for Theatre Research: People, Places, and Performance’. *Theatre Journal* 68 (4): 615–32. [🔗 DOI](https://doi.org/10.1353/tj.2016.0109).  
- **Oort, Thunnis van, and Julia Noordegraaf.** 2020. ‘Structured Data for Performing Arts History’. *Research Data Journal for the Humanities and Social Sciences* 5 (2): 1–12. [🔗 DOI](https://doi.org/10.1163/24523666-bja10008).  
- **Peyre, E, Amarger, F., and Chauvat, N.** 2024. *CapData Opéra: Faciliter l’interopérabilité Des Données Des Maisons d’opéra*. [🔗 HAL](https://hal.science/hal-04639095).  
- **Roussillon, Marine, and Christophe Schuwey, eds.** 2020. *Revue d’historiographie du théâtre* 5. Paris: Société d’histoire du théâtre. [🔗 SHT](https://sht.asso.fr/revue/ecrire-lhistoire-des-spectacles-avec-des-bases-de-donnees/).

---

## Future Work

- Modeling **festivals, season programmes, and show programmes** for better structured performing arts data.
- Further refinements based on case studies and community feedback.
- **Collaboration with Getty Vocabulary Program** for proposed term additions.
