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
- **Participants** (`produced_by`)

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
  "produced_by": [
    {
      "type": "Production",
      "part": [
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
          ]
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

### Roles
Each **person or organization** involved is listed in `produced_by`.

Example:  
> **Séverine Chavrier** is both **director** and **adapter** of the performance.  

```json
"produced_by": [
  {
    "type": "Production",
    "part": [
      {
        "type": "Production",
        "technique": [
          {
            "id": "http://vocab.getty.edu/page/aat/300404387",
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
        ]
      }
    ]
  }
],
```

---

### Funders & Supporters
Sponsorships and acknowledgments are included in produced_by.

Example:  
> The **Fondation Ernst Göhner** sponsors the production.

```json
"produced_by": [
  {
    "type": "Production",
    "part": [
      {
        "technique" : [
          {
            "id": "production/soutien/financement",
            "type": "Type",
            "_label": "production/soutien/financement"
          }
        ],
        "carried_out_by" : [
          {
            "id": "https://data.stage.org/auth/000000000999",
            "type": "Group",
            "_label": "Fondation Ernst Göhner (Zoug)",
            "classified_as": [
              {
                "id": "http://id.loc.gov/vocabulary/relators/spn",
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
      }
    ]
  }  
]
```

![Production class schema](Figures-Cookbook/B.drawio.svg)

---
### Characters
For characters we suggest a new property : portrayed

> **Pierre Artières-Glissant** plays **Henry** in *Absalon, Absalon!*.

```json

"produced_by": [
    {
      "type": "Production",
      "part": [
        {
          "technique": [
            {
              "id": "http://id.loc.gov/vocabulary/relators/act",
              "type": "Type",
              "_label": "actor"
            }
          ],
          "carried_out_by": [
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
              "portrayed": [
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
                  "content": "Henry",
                }
              ]
            }
          ]
        }
      ]
    }
  ]
            


```


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

---
## Practical Informations
We use the class "set" to describe the ticket prices and the duration of the show. Indeed activities in Cidoc-CRM can not accept dimensions nor multiple timespans. These characteristics apply to the B Level (Production).

The Set has to be linked with the corresponding B with the `used_for` property.
In C individual shows are member of the Set. The link is made via the `member_of` property used in C.

### Ticket Pricing
The **ticket price** is included via the `dimension` property:  
- `classified_as: Price`
- `unit: Currency`

### Duration
The duration of the show is indicated via the `TimeSpan` property. If the duration of one specific show differs, it has to be indicated in the C.

### Example
The ticket price of the show Abasalon in Avignon is 30 euros. The duration of the show is 5 hours. In this case, the general program gives the information for the ticket price while the show program gives the information for the duration.

```json
{
    "@context": "https://linked.art/ns/v1/linked-art.json",
    "id": "https://data.stage.org/sets/Absalon",
    "type": "Set",
    "_label": "practical information Absalon",
    "classified_as": [
        {
            "id": "http://vocab.getty.edu/page/aat/300419392",
            "type": "Type",
            "_label": "practical information"
        }
    ],
    "subject_of": [
        {
            "type": "LinguisticObject",
            "_label": "Information as appears in general program",
            "classified_as": [
                {
                    "id": "https://vocab.getty.edu/aat/300311936",
                    "type": "Type",
                    "_label": "primary source"
                }
            ]
        }
    ],
    "used_for" : [
        {
          "id": "https://data.stage.org/prod/000000000001",
          "type": "Activity",
          "_label": "Absalon, Absalon in Avignon (Season) (B.json)" 
        }
    ],
    "member_of": [
        {
        "id": "https://data.stage.org/sets/Absalom",
        "type": "Set",
        "_label": "Absalon, Absalon in Avignon (set of shows)"
        }
    ],
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
            "value": "30",
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
                    "content": "Tarif Plein - C"
                }
            ]
        }
    ],
    "timespan": {
        "type": "TimeSpan",
        "_label": "5h",
        "duration": {
            "type": "Dimension",
            "value": 300,
            "unit": {
                "id": "http://vocab.getty.edu/aat/300379240",
                "type": "MeasurementUnit",
                "_label": "minutes"
            }
        },
        "referred_to_by": [
            {
                "type": "LinguisticObject",
                "_label": "Information as appears in show program",
                "classified_as": [
                    {
                        "id": "https://vocab.getty.edu/aat/300311936",
                        "type": "Type",
                        "_label": "primary source"
                    }
                ],
                "content": "5h",
                "subject_of": [
                    {
                        "id": "https://data.stage.org/prog/000000000001",
                        "type": "LinguisticObject",
                        "_label": "Information as appears in show program",
                        "classified_as": [
                            {
                                "id": "https://vocab.getty.edu/aat/300311936",
                                "type": "Type",
                                "_label": "primary source"
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```

---
## Programme

Show programmes and general programmes are the main source in this project to describe the shows. They are `HumanMadeObject` in order to keep visual and textual information. 

### Example
The show programme of Absalon, Absalon edited by the Festival d'Avignon, with quotations featuring the biography of Severine Chavrier, the abstract of the work in several languages and an interview.

```json
{
    "@context": "https://linked.art/ns/v1/linked-art.json",
    "id": "https://data.stage.org/programs/000000000001",
    "type": "HumanMadeObject",
    "_label": "Absalon Absalon show programme",
    "classified_as": [
        {
            "id": "https://vocab.getty.edu/aat/300027216",
            "type": "Type",
            "_label": "show programme"
        }
    ],
    "attributed_by": [
        {
            "type": "AttributeAssignment",
            "carried_out_by": [
                {
                    "id": "https://data.stage.org/festivalavignon",
                    "type": "Group",
                    "_label": "Festival d'Avignon"
                }
            ]
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
            "content": "Absalon, Absalon ! show programme",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300388306",
                    "type": "Language",
                    "label": "French"
                },
                {
                    "id": "http://vocab.getty.edu/aat/300388277",
                    "type": "Language",
                    "_label": "English"
                },
                {
                    "id": "http://vocab.getty.edu/aat/300389311",
                    "type": "Language",
                    "_label": "Spanish"
                }
            ]
        }
    ],
    "carries": [
        {
            "type": "LinguisticObject",
            "_label": "bio as appears in doc",
            "classified_as": [
                {
                    "id": "http://vocab.getty.edu/page/aat/300435422",
                    "type": "Type",
                    "_label": "Artist's Biography"
                }
            ],
            "content": "Actuelle directrice de la Comédie de Genève, actrice et metteuse en scène, Séverine Chavrier est reconnue pour son théâtre engagé. À travers des spectacles pluridisciplinaires, elle explore des sujets tels que les inégalités sociales, les questions d’identité, les conflits contemporains et les enjeux environnementaux, offrant ainsi au public des réflexions profondes et stimulantes sur le monde qui nous entoure. En tant que comédienne ou musicienne, elle a multiplié les compagnonnages avec Rodolphe Burger, François Verret et Jean-Louis Martinelli, tout en dirigeant sa propre compagnie, La Sérénade interrompue, avec laquelle elle développe une approche singulière de la mise en scène, où le théâtre dialogue avec la musique, mais aussi avec l’image et la littérature. Séverine Chavrier construit en effet son expression à partir de toutes sortes de matières : le corps de ses acteurs, le son de son piano préparé, les vidéos qu’elle réalise souvent elle-même, sans oublier la parole. Une parole erratique qu’elle façonne en se plongeant dans l’univers des auteurs qu’elle affectionne. D’abord avec Hanokh Levin pour Épousailles et Représailles, puis aujourd’hui avec J.G. Ballard. Au Festival d’Avignon, on a pu la voir en 2011 dans le spectacle de François Verret, Courts-Circuits, et dans un concert d’improvisation avec Jean-Pierre Drouet.",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300388306",
                    "type": "Language",
                    "_label": "French"
                }
            ],
            "subject_of": [
                {
                    "id": "https://data.stage.org/auth/000000000001",
                    "type": "Type",
                    "_label": "Person"
                }
            ]
        },
        {
            "type": "LinguisticObject",
            "_label": "description of the show in french as appears in doc",
            "classified_as": [
                {
                    "id": "http://vocab.getty.edu/aat/300435416",
                    "type": "Type",
                    "_label": "Description"
                }
            ],
            "content": "Après avoir marqué les esprits avec Les Palmiers sauvages, Séverine Chavrier retrouve l’univers de William Faulkner en adaptant librement le monumental Absalon, Absalon ! Œuvre-monde, ce roman transpose dans l’Amérique de la Guerre de Sécession un épisode biblique : le destin maudit du fils de David, marqué du sceau du fratricide et de l’inceste. Absalon, Absalon !, c’est l’ascension et la chute de Sutpen, enfant né plus bas que bas et devenu un homme assoiffé de reconnaissance sociale. Mais dans le Mississipi hanté par l’esclavage et le génocide autochtone, les rêves de gloire sont voués à l’échec. Dans ce récit à quatre voix aux accents de tragédie grecque, la metteuse en scène trouve de quoi nourrir son théâtre toujours affamé : avec un art consommé du débordement, elle électrise les mots de Faulkner tout en ménageant le mystère d’une écriture qu’elle aime passionnément. Dans un dispositif qui superpose les échelles et les temporalités, les interprètes racontent leurs personnages autant qu’ils se racontent. Hantés par les fantômes de l’enfance, ils errent dans un monde en décomposition. ",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300388306",
                    "type": "Language",
                    "_label": "French"
                }
            ],
            "subject_of": [
                {
                    "id": "https://data.stage.org/auth/000000000001",
                    "type": "Type",
                    "_label": "Person"
                }
            ]
        },
        {
            "type": "LinguisticObject",
            "_label": "description of the show in english as appears in doc",
            "classified_as": [
                {
                    "id": "http://vocab.getty.edu/aat/300435416",
                    "type": "Type",
                    "_label": "Description"
                }
            ],
            "content": "After making a lasting impression with The Wild Palms, Séverine Chavrier returns to the universe of William Faulkner with a free adaptation of the monumental Absalom, Absalom! A beast of a novel, it transposes into the America of the Civil War a biblical episode: the cursed fate of David, marked by the seal of fratricide and incest. Absalom, Absalom! chronicles the rise and fall of Thomas Sutpen, a child born in poverty who becomes a man hungry for social recognition. But in a Mississippi haunted by slavery and the genocide of the natives, dreams of glory are doomed to failure. In this narrative with its four voices reminiscent of Greek tragedies, the director finds much to feed her always hungry theatre: with her characteristic sense of flair, she electrifies Faulkner’s words while preserving the mystery of a work she loves passionately. Superimposing scales and temporalities, she lets the actors tell as much about themselves as about their characters. Haunted by the ghosts of childhood, they wander a decaying world.",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300388277",
                    "type": "Language",
                    "_label": "English"
                }
            ],
            "subject_of": [
                {
                    "id": "https://data.stage.org/auth/000000000001",
                    "type": "Type",
                    "_label": "Person"
                }
            ]
        },
        {
            "type": "LinguisticObject",
            "_label": "description of the show in spanish as appears in doc",
            "classified_as": [
                {
                    "id": "http://vocab.getty.edu/aat/300435416",
                    "type": "Type",
                    "_label": "Description"
                }
            ],
            "content": "En este espectáculo épico a varias voces, la guerra de Secesión supone un antes y un después para esta familia cuya estirpe se derrumba. Es la adaptación de la novela homónima de Faulkner donde los fantasmas conviven con los vivos.",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300389311",
                    "type": "Language",
                    "_label": "Spanish"
                }
            ],
            "subject_of": [
                {
                    "id": "https://data.stage.org/auth/000000000001",
                    "type": "Type",
                    "_label": "Person"
                }
            ]
        },
        {
            "type": "LinguisticObject",
            "_label": "the director's interview",
            "classified_as": [
                {
                    "id": "http://vocab.getty.edu/aat/300192825",
                    "type": "Type",
                    "_label": "Artist's Statement"
                }
            ],
            "content": "**Qu’est-ce qui vous a décidée à adapter le roman de Faulkner Absalon, Absalon ! ?**\nSéverine Chavrier\nJ’aborde régulièrement des thèmes tels que la question de l’héritage d’une génération à l’autre, les relations fraternelles, la jeunesse face à l’autorité parentale, la folie comme revanche sociale… Pour ce spectacle, le déclic est venu lorsque je me suis rendu compte que, dans mes pièces précédentes, je n’avais pas encore abordé certains sujets essentiels, notamment la question de la cohabitation, de la violence et de la légitimité de la fondation d’une nation nord-américaine.\n\n**Votre adaptation est libre et repose en partie sur l’appropriation du texte par les comédiens. Pouvez-vous nous parler de votre processus de création ?**\nPlutôt que de suivre une chronologie stricte ou de reproduire les temps forts du roman, nous explorons différentes configurations et relations entre les personnages. Notre démarche est davantage centrée sur les rapports de parole et les interactions entre les acteurs, ce qui permet une réinterprétation vivante et dynamique de l’œuvre de Faulkner. Nous avons cherché à explorer le jeu entre le récit et la scène, en mettant l’accent sur la façon dont chaque scène est racontée plusieurs fois, révélant différentes perspectives.\n\n**« Ce qui m’intéresse, c’est de comprendre comment la manière de parler d’une scène révèle la personne qui la raconte. »**\n\nJ’ai cherché à créer une expérience immersive où le public est plongé dans l’univers de Faulkner, tout en laissant place à l’interprétation et à l’émotion. Tout comme les actrices et les acteurs, je souhaite que le public trouve sa propre connexion avec l’histoire et les personnages.\n\n**Vous intégrez également des éléments de la vie des comédiennes et comédiens…**\nOui, j’intègre ces éléments biographiques pour garantir la sincérité du spectacle. J’ai choisi des artistes dont les histoires familiales ou professionnelles résonnent avec les thèmes de la pièce, comme la lutte contre la domination et l’exploitation. Je m’appuie sur leurs contributions pour construire le texte et les scènes, et j’assure le montage final en réinjectant l’essence de Faulkner dans la pièce. C’est un équilibre entre improvisation et direction artistique. Nous naviguons entre improvisation et réécriture pour créer une dramaturgie qui émerge organiquement du processus de travail. Chaque acteur apporte son interprétation et ses propres mots, ce qui enrichit la pièce et lui donne une dimension unique : le spectacle évoluerait différemment si nous travaillions avec d’autres acteurs…\n\n**Comment la complexité narrative du roman de Faulkner est-elle mise en œuvre dans votre adaptation théâtrale ? Comment abordez-vous la thématique de la domination patriarcale et économique des Blancs dans votre adaptation ?**\n\n**« Je souligne la multiplicité des narrateurs dans le roman et je recherche le poids émotionnel plutôt que la vérité factuelle dans la narration. »**\n\nJe privilégie une approche archaïque et brutale, en utilisant le maquillage et les costumes pour transformer les acteurs et en jouant avec les échelles temporelles. Mon objectif est de capturer l’essence shakespearienne de Faulkner, en mettant l’accent sur la virtuosité du jeu plutôt que sur la sophistication technique. J’essaie de mettre en lumière l’évolution des États-Unis, du bruit et de la fureur à l’essor mercantile, en montrant comment cette trajectoire écrase les individus. C’est une réflexion sur l’impact de l’histoire nationale sur les destins individuels. Je contextualise la pièce dans la guerre de Sécession et je montre comment cette domination influence les relations familiales et sociales. C’est une critique subtile de l’exploitation continue du Sud par le Nord. Dans le spectacle, la voiture représente à la fois la modernité, la liberté et l’oppression industrielle. Elle devient un lieu de travail et de confession, reflétant ainsi les rapports de pouvoir et l’exploitation de la classe ouvrière. La transformation des techniques de production de l’esclavagisme à l’industrie automobile souligne la continuité des schémas de domination économique.\n\n**L’enfance est un thème central du roman : comment se traduit-il dans votre adaptation ?**\nLe thème de l’enfance est lié chez Faulkner à l’innocence, à une forme de pureté perdue qui s’oppose à la faute et à la culpabilité. Il y a aussi la question de la mémoire et des traumatismes qui lui sont liés…\n\n**Pouvez-vous nous présenter les différents espaces scéniques et la façon dont ils s’articulent ?**\nJ’ai créé différents espaces pour représenter la maison historique, le présent du travail et l’université contemporaine.\n\n**Entretien avec Séverine Chavrier**",
            "language": [
                {
                    "id": "http://vocab.getty.edu/aat/300388306",
                    "type": "Language",
                    "_label": "French"
                }
            ],
            "subject_of": [
                {
                    "id": "https://data.stage.org/prod/000000000001",
                    "type": "Type",
                    "_label": "Activity"
                },
                {
                    "id": "https://data.stage.org/auth/000000000001",
                    "type": "Type",
                    "_label": "Person"
                }
            ]
        }
    ]
}
```

