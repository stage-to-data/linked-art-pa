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
- **Show Programme** (as a `Textual` or `Digital Object`).  

![Global classes schema](Figures-Cookbook/Global.drawio.svg)

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
- `produced_by`

Example:  
> The work *Absalon, Absalon!* conceived by the director **Séverine Chavrier** in **2024** in French.

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "https://data.stage.org/works/000000000001",
  "type": "PropositionalObject",
  "_label": "The show of Absalon, Absalon! as conceived by Séverine Chavrier",
  "classified_as": [
    {
      "id": "https://vocab.getty.edu/aat/300387357",
      "type": "Type",
      "_label": "works (general, creative)"
    }
  ],
  "identified_by": [
    {
      "type": "Name",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/aat/300404670",
          "type": "Type",
          "_label": "Title"
        }
      ],
      "content": "Absalon, Absalon !",
      "language": [
        {
          "id": "http://vocab.getty.edu/aat/300388306",
          "type": "Language",
          "label": "French"
        }
      ]
    }
  ],
  "produced_by": [
    {
      "type": "Production",
      "technique": [
        {
          "id":"http://vocab.getty.edu/page/aat/300404387",
          "type": "Type",
          "_label": "Creating"
        }
      ],
      "carried_out_by": [
        {
          "id": "https://data.stage.org/auth/000000000001",
          "type": "Person",
          "_label": "Séverine Chavrier",
          "classified_as": [
            {
              "id": "http://id.loc.gov/vocabulary/relators/drt",
              "type": "Type",
              "_label": "director"
            }
          ]
        }
      ],
      "timespan": {
        "type": "TimeSpan",
        "_label": "2024",
        "begin_of_the_begin": "2024-01-01T00:00:00Z"
      },
      "language": [
        {
          "id": "http://vocab.getty.edu/aat/300388306",
          "type": "Language",
          "label": "French"
        }
      ]
    }
  ]
}
```


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
- `produced_by`

Example:  
> The text entitled *Absalom, Absalom!* written by **William Faulkner**.

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "https://data.stage.org/text/000000000101",
  "type": "LinguisticObject",
  "_label": "Absalon, Absalon!",
  "identified_by": [
    {
      "type": "Name",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/aat/300404670",
          "type": "Type",
          "_label": "Primary Name"
        }
      ],
      "content": "Absalom, Absalom!",
      "language": [
        {
          "id": "http://vocab.getty.edu/aat/300388277",
          "type": "Language",
          "label": "English"
        }
      ]
    }
  ],
  "produced_by": {
    "type": "Production",
    "technique" : [
      {
        "id":"http://vocab.getty.edu/page/aat/300054698",
        "type": "Type",
        "_label": "Writing"
      }
    ],
    "carried_out_by": [
      {
        "id": "https://data.stage.org/auth/000000000001",
        "type": "Person",
        "_label": "William Faulkner",
        "classified_as": [
          {
            "id": "http://id.loc.gov/vocabulary/relators/aut",
            "type": "Type",
            "_label": "author"
          }
        ]
      }
    ]
  }
}
```


When a **work (A)** is **inspired by** another, it is linked via `influenced_by`, referencing the original work.  

Example:  
> The play *Richard III*, staged in French by **William Mesguish** in **2024**.

```json
to do

```

For adaptations, the `classified_as` property qualifies the relationship.  

Example:  
> The novel *Absalon, Absalon!* staged by **Séverine Chavrier** in **2024** as an **adaptation**.

```json
"influenced_by": [
        {
          "id": "https://data.stage.org/text/000000000101 (text.json)",
          "type": "LinguisticObject",
          "_label": "Absalon de Faulkner",
          "classified_as": [
            {
              "id": "http://vocab.getty.edu/page/aat/300410356",
              "type": "Type",
              "_label": "Adaptation"
            }
          ]
        }
      ]
```


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

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "https://data.stage.org/prod/000000000001",
  "type": "Activity",
  "_label": "Absalon, Absalon in Avignon (Season)",
  "classified_as": [
    {
      "id": "https://vocab.getty.edu/aat/300069200",
      "type": "Type",
      "_label": "Performances (creative events)"
    }
  ],
  "part_of": [
    {
      "id": "https://data.stage.org/festivals/000000000001",
      "type": "Activity",
      "_label": "78e Festival Avignon 2024"
    }
  ],
  "influenced_by": [
    {
      "id": "https://data.stage.org/works/000000000001 (A.json)",
      "type": "PropositionalObject",
      "_label": "The show of Absalon, Absalon! as conceived by Séverine Chavrier"
    }
  ],
  "identified_by": [
    {
      "type": "Name",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/aat/300404670",
          "type": "Type",
          "_label": "Title"
        }
      ],
      "content": "Absalon, Absalon !",
      "language": [
        {
          "id": "http://vocab.getty.edu/aat/300388306",
          "type": "Language",
          "_label": "French"
        }
      ]
    }
  ],
  "took_place_at": [
    {
      "id": "https://data.stage.org/auth/100000000001",
      "type": "Place",
      "_label": "La Fabrica",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/page/aat/300121919",
          "type": "Type",
          "_label": "performing arts structures"
        }
      ]
    }
  ],
  "timespan": {
    "type": "TimeSpan",
    "begin_of_the_begin": "2024-06-29T00:00:00Z",
    "end_of_the_end": "2024-07-07T00:00:00Z"
  }
}

```

---

### Relationship: Work ↔ Production

A **Work (A)** (conceptual entity) is **different** from its **Production (B)** (an activity).  
The **Production (B)** refers to the **Work (A)** via `influenced_by`.

> Multiple stagings of the **same work** can occur in different places while remaining tied to the **same concept**.

### Context Elements:
- **Venues**: Specified via `took_place_at`, which may include stage details.
- **Festivals**: Linked via `part_of`, referencing the **Festival object**.

---

### Genre
The **genre** is stored separately as it comes from external sources (*e.g., programmes*).  
It is **not** included in **Work (A)** because it may **vary by venue**.

Example:  
> *Absalon, Absalon!* is classified as **Theatre (genre)** based on the programme with the literal transcription "Théâtre".

```json
"classified_as": [
        {
          "id": "https://vocab.getty.edu/aat/300417582",
          "type": "Type",
          "_label": "Theater (genre)",
          "referred_to_by": [
            {
              "type": "LinguisticObject",
              "_label": "genre as appears in program",
              "classified_as": [
                {
                  "id": "http://vocab.getty.edu/page/aat/300456607",
                  "type": "Type",
                  "_label": "Literal transcription"
                }
              ],
              "content": "Théâtre"
            }
          ]
        }
]
```

---

### Ticket Pricing
The **ticket price** is included via the `dimension` property:  
- `classified_as: Price`
- `unit: Currency`

Example:  
> Ticket prices for one performance in euros.

```json
"dimension": [
  {
    "type": "MonetaryAmount",
    "classified_as": [
      {
        "id": "http://vocab.getty.edu/aat/300417247",
        "type": "Type",
        "_label": "List Prices"
      }
    ],
    "value": "23",
    "currency": {
      "id": "https://vocab.getty.edu/aat/300425170",
      "type": "Currency",
      "_label": "Euros"
    },
    "referred_to_by": [
      {
        "type": "LinguisticObject",
        "_label": "price category",
        "classified_as": [
          {
            "id": "http://vocab.getty.edu/page/aat/300435423",
            "type": "Type",
            "_label": "Literal transcription"
          }
        ],
        "content": "plein"
      }
    ]
  },
  {
    "type": "MonetaryAmount",
    "classified_as": [
      {
        "id": "http://vocab.getty.edu/aat/300417247", 
        "type": "Type",
        "_label": "List Prices"
      }
    ],
    "value": "16",
    "currency": {
      "id": "https://vocab.getty.edu/aat/300425170",
      "type": "Currency",
      "_label": "Euros"
    },
    "referred_to_by": [
      {
        "type": "LinguisticObject",
        "_label": "price category",
        "classified_as": [
          {
            "id": "http://vocab.getty.edu/page/aat/300435423",
            "type": "Type",
            "_label": "Literal transcription"
          }
        ],
        "content": "abonné"
      }
    ]
  },
  {
    "type": "MonetaryAmount",
    "classified_as": [
      {
        "id": "http://vocab.getty.edu/aat/300417247", 
        "type": "Type",
        "_label": "List Prices"
      }
    ],
    "value": "18",
    "currency": {
      "id": "https://vocab.getty.edu/aat/300425170",
      "type": "Currency",
      "_label": "Euros"
    },
    "referred_to_by": [
      {
        "type": "LinguisticObject",
        "_label": "price category",
        "classified_as": [
          {
            "id": "http://vocab.getty.edu/page/aat/300435423",
            "type": "Type",
            "_label": "Literal transcription"
          }
        ],
        "content": "reduit"
      }
    ]
  }
],
```

---

### Roles
Each **person or organization** involved is listed in `carried_out_by`, classified by **roles** (director, actor, etc.).

Example:  
> **Séverine Chavrier** is both **director** and **adapter** of the performance.  
> **Pierre Artières-Glissant** plays **Henry** in *Absalon, Absalon!*.

```json
"carried_out_by": [
    {
      "id": "https://data.stage.org/auth/000000000001",
      "type": "Person",
      "_label": "Séverine Chavrier",
      "referred_to_by": [
        {
          "type": "LinguisticObject",
          "_label": "role as appears in doc",
          "classified_as": [
            {
              "id": "http://vocab.getty.edu/page/aat/300435423",
              "type": "Type",
              "_label": "Literal transcription"
            }
          ],
          "content": "adaptation et mise en scène"
        }
      ],
      "classified_as": [
        {
          "id": "http://id.loc.gov/vocabulary/relators/drt",
          "type": "Type",
          "_label": "director"
        },
        {
          "id": "http://id.loc.gov/vocabulary/relators/adp",
          "type": "Type",
          "_label": "adapter"
        }
      ]
    },
    {
      "id": "https://data.stage.org/auth/000000000009",
      "type": "Person",
      "_label": "Pierre Artières-Glissant",
      "classified_as": [
        {
          "id": "http://id.loc.gov/vocabulary/relators/act",
          "type": "Type",
          "_label": "actor"
        }
      ],
      "referred_to_by": [
        {
          "type": "LinguisticObject",
          "_label": "role as appears in doc",
          "classified_as": [
            {
              "id": "http://vocab.getty.edu/page/aat/300435423",
              "type": "Type",
              "_label": "Literal transcription"
            }
          ],
          "content": "avec"
        }
      ],
      "has_character": [
        {
          "type": "LinguisticObject",
          "_label": "name of the character",
          "classified_as": [
            {
              "id": "http://vocab.getty.edu/page/aat/300410267",
              "type": "Type",
              "_label": "character"
            }
          ],
          "content": "Henry"
        }
      ]
    }
]

```

---

### Funders & Supporters
Sponsorships and acknowledgments are recorded in `participant`, classified by **funding type**.

Example:  
> The **Fondation Ernst Göhner** sponsors the production.

```json
"participant": [
{
      "id": "https://data.stage.org/auth/000000000999",
      "type": "Group",
      "_label": "Fondation Ernst Göhner (Zoug)",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/page/aat/300188572",
          "type": "Type",
          "_label": "Sponsor",
          "referred_to_by": [
            {
              "type": "LinguisticObject",
              "_label": "as appears in program",
              "classified_as": [
                {
                  "id": "http://vocab.getty.edu/page/aat/300456607",
                  "type": "Type",
                  "_label": "Literal transcription"
                }
              ],
              "content": "Avec le soutien de"
            }
          ]
        }
      ]
    }
]

```

![Production class schema](Figures-Cookbook/B.drawio.svg)

---

## Show (C)

A **specific performance date** is modeled as a **separate Activity**, linked to **Production (B)** via `part_of`.

### Key properties:
- **Precise timespan** (date and duration).
- **Part of** (Production B).
- **Classification** (`classified_as`).

Example:  
> The *Absalon, Absalon!* performance on **29 June 2024 at 16:00**, as part of the **Avignon season**.

```json
{
  "@context": "https://linked.art/ns/v1/linked-art.json",
  "id": "https://data.stage.org/shows/000000000001",
  "type": "Activity",
  "_label": "Specific Date for Absalon, Absalon ",
  "part_of": [
    {
      "id": "https://data.stage.org/prod/000000000001",
      "type": "Activity",
      "_label": "Absalon, Absalon in Avignon (Season) (B.json)"
    }
  ],
  "classified_as": [
    {
      "id": "http://vocab.getty.edu/page/aat/300XXXXXX",
      "type": "Type",
      "_label": "performance (performing arts show) to be defined in Getty"
    }
  ],
  "timespan": {
    "type": "TimeSpan",
    "_label": "Date",
    "begin_of_the_begin": "2024-06-29T16:00:00Z"
  }
}

```

![Show class schema](Figures-Cookbook/C.drawio.svg)

---

## Sources & Citations

- Performance details should link to **primary sources** (`attributed_by`).
- Exact transcriptions from sources use **`referred_to_by`**.
- Visual materials (**stage design photos**) use `representation`.

Example:  
> The genre of *Absalon, Absalon!* ("Théâtre") is cited from the **show programme** and linked via **IIIF**.

```json
"attributed_by": [
    {
      "type": "AttributeAssignment",
      "identified_by": [
        {
          "type": "Type",
          "id": "https://vocab.getty.edu/aat/300027216",
          "_label": "show programme",
          "classified_as": [
            {
              "id": "https://vocab.getty.edu/aat/300311936",
              "type": "Type",
              "_label": "primary source"
            }
          ]
        }
      ],
      "assigned": [
        {
          "type": "LinguisticObject",
          "id": "https://data.stage.org/programs/000000000001",
          "_label": "Absalon show programme"
        }
      ],
      "carried_out_by": [
        {
          "id": "https://data.stage.org/festivalavignon",
          "type": "Group",
          "_label": "Festival d'Avignon"
        }
      ]
    }
  ]
```

## Show Programme

A show programme is modelled as a `HumanMadeObject`, which carries textual and visual content such as artist biographies, performance descriptions, or institutional messages. These contents are represented using the carries property, pointing to `LinguisticObject` entities. The programme is also classified as a "show programme" using Getty AAT.

```json
{
  "id": "https://data.stage.org/object/programme/absalom-2023",
  "type": "HumanMadeObject",
  "classified_as": [
    {
      "id": "http://vocab.getty.edu/aat/300027221",
      "type": "Type",
      "label": "Show programme"
    }
  ],
  "label": "Programme for *Absalom* (2023)",
  "carries": [
    {
      "id": "https://data.stage.org/linguisticobject/biography-artist-x",
      "type": "LinguisticObject",
      "label": "Biography of Artist X",
      "language": [
        {
          "id": "http://lexvo.org/id/iso639-1/en",
          "type": "Language",
          "label": "English"
        }
      ],
      "content": "Artist X is a performer known for..."
    }
  ]
}
```

`HumanMadeObject` vs `LinguisticObject`: The programme as a physical or digital artefact is a HumanMadeObject. The textual components (biographies, forewords, etc.) are embedded via carries → LinguisticObject.

Content Modelling: In Absalom, each textual unit within the programme is treated as a discrete object. This enables better indexing, multilingual support, and fine-grained access to programme sections (e.g., a biography can be reused or translated independently).

