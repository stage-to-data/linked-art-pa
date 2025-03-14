# Cookbook: Performing Arts Works

This cookbook provides an in-depth presentation of the **performing arts extension of Linked Art**. It primarily uses the controlled vocabulary developed by the **Getty (AAT)**, except for person roles, as gaps frequently exist in this area within the performing arts field.  

For **profession-related vocabulary**, we use the **Library of Congress vocabulary**:  
🔗 [https://id.loc.gov/vocabulary/relators.html](https://id.loc.gov/vocabulary/relators.html)  

This vocabulary is also aligned with the **BnF controlled vocabulary**, providing a **bilingual (English/French) thesaurus**:  
🔗 [https://data.bnf.fr/vocabulary/roles](https://data.bnf.fr/vocabulary/roles)  

---

## General Structure

To precisely encode **performing arts works**, this extension is based on a **three-object composition**. This schema allows the **separation** between:
1. The concept of a **work**.
2. Its various **productions**.
3. Individual **performances**.

This distinction ensures precise documentation, including unforeseen changes not recorded at the **production level**.

### These three objects consist of:
- **A: Work** (*Getty AAT "works (general, creative)"*)  
  - A `PropositionalObject`, representing the concept behind the performance.  

- **B: Production** (*Getty AAT "Performances (creative events)"*)  
  - An `Activity` element encompassing multiple performances in a specific context (venue, festival, event, etc.).  

- **C: Show** (*Getty AAT "Performances (performing arts show)"*)  
  - An `Activity` element referring to the individual show occurring on a precise date.  

### This structure allows:
- **Listing and distinguishing variations** when the same production is presented in multiple locations (e.g., during a tour).  
- **Capturing last-minute changes** (e.g., cast replacements).  
- **Precise listing of all performance dates**, as level **B** only captures first and last dates without detailing rest days or multiple performances per day.  

### Additional objects:
- **Text** (as a `Textual Object`, e.g., the play).  
- **Festival** (as an `Activity`, to be developed).  
- **Season Programme** (as a `Textual` or `Digital Object`, to be developed).  
- **Show Programme** (as a `Textual` or `Digital Object`, to be developed).  

---

## Work (A)

A **work concept** is classified as a `PropositionalObject`, as it does not have a tangible existence. It consolidates general information such as:
- **Title**  
- **Director**  
- **Premiere year**  

This allows differentiation between **adaptations and re-creations** over time.

### Key properties:
- `classified_as`
- `identified_by`
- `created_by`

Example:  
> The work *Absalon, Absalon!* conceived by **Séverine Chavrier** in **2024**.

---

### Re-Staging and Re-Enactment
Directors often **re-stage** previous works after a significant period. Each re-staging is considered a **separate work**, ensuring a **clear distinction** between:
- **Production teams** (actors, technical staff, funding, etc.).
- **Time-based evolution** (*timespan* property within `created_by`).

---

### Plays and Adaptations
Many performing arts works are **interpretations or adaptations** of texts (*plays, novels, etc.*).  
A text is a `LinguisticObject`, following the same structure as **Work (A)**, with at least:
- `identified_by`
- `created_by`

Example:  
> The text entitled *Absalom, Absalom!* written by **William Faulkner**.

When a **work (A)** is **inspired by** another, it is linked via `subject_of`, referencing the original work.  

Example:  
> The play *Richard III*, staged by **William Mesguish** in **2024**.

For adaptations, the `classified_as` property qualifies the relationship.  

Example:  
> The novel *Absalon, Absalon!* staged by **Séverine Chavrier** in **2024** as an **adaptation**.

---

## Production (B)

Works are performed within **specific places and timeframes**.  
A **group of performances (B)** represents all performances in a **short period** at the same location or context.  
This corresponds to `"Performances (creative events)"` in the **Getty AAT**.  

A **production** is modeled as an `Activity`, similar to an **exhibition** in the **Linked Art** model.

### Key properties:
- **Identifier** (`id`)
- **Type** (`Activity`)
- **Label** (`_label`)
- **Classification** (`classified_as`), e.g., `"Performances (creative events)"`
- **Temporal scope** (`timespan`)
- **Location** (`took_place_at`)
- **Participants** (`carried_out_by`)

Example:  
> The production of *Absalon, Absalon!* by **Séverine Chavrier**, presented in **July 2024** at **La Fabrica (Avignon Festival)**.

---

### Relationship: Work ↔ Production

A **Work (A)** (conceptual entity) is **different** from its **Production (B)** (an activity).  
The **Production (B)** refers to the **Work (A)** via `influenced_by`.

> Multiple stagings of the **same work** can occur in different places while remaining tied to the **same concept**.

### Context Elements:
- **Venues**: Specified via `took_place_at`, which may include stage details.
- **Festivals**: Linked via `part_of`, referencing the **Festival object**.

Example:  
> The production of *Absalon, Absalon!* is based on a work conceived by **Séverine Chavrier**.

---

### Genre
The **genre** is stored separately as it comes from external sources (*e.g., programmes*).  
It is **not** included in **Work (A)** because it may **vary by venue**.

Example:  
> *Absalon, Absalon!* is classified as **Theatre (genre)** based on the programme.

---

### Ticket Pricing
The **ticket price** is included via the `dimension` property:  
- `classified_as: Price`
- `unit: Currency`

Example:  
> The ticket price for *Absalon, Absalon!* was **€25**.

---

### Roles
Each **person or organization** involved is listed in `carried_out_by`, classified by **roles** (director, actor, etc.).

Example:  
> **Séverine Chavrier** is both **director** and **adapter** of the performance.  
> **Pierre Artières-Glissant** plays **Henry** in *Absalon, Absalon!*.

---

### Funders & Supporters
Sponsorships and acknowledgments are recorded in `participant`, classified by **funding type**.

Example:  
> The **Fondation Ernst Göhner** sponsors the production.

---

## Show (C)

A **specific performance date** is modeled as a **separate Activity**, linked to **Production (B)** via `part_of`.

### Key properties:
- **Precise timespan** (date and duration).
- **Part of** (Production B).
- **Classification** (`classified_as`).

Example:  
> The *Absalon, Absalon!* performance on **29 June 2024 at 16:00**, as part of the **Avignon season**.

---

## Sources & Citations

- Performance details should link to **primary sources** (`subject_of`).
- Exact transcriptions from sources use **`referred_to_by`**.
- Visual materials (**stage design photos**) use `representation`.

Example:  
> The genre of *Absalon, Absalon!* ("Théâtre") is cited from the **show programme** and linked via **IIIF**.
