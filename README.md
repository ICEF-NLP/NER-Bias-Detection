# Serbian Personal Name List and Serbian NER Gender Bias Evaluation Dataset

## Serbian Personal Name List

### Overview
This repository contains three curated datasets of **Serbian first names and last names**, divided by gender and type.  
They were collected and processed to support research in **detecting gender bias** in Serbian NLP models.

### Dataset files

| Dataset | Description | File Format | Record Count |
|----------|--------------|--------------|---------------|
| `female_firstnames` | Common Serbian female first names. | `.csv` | 870 entries |
| `male_firstnames` | Common Serbian male first names. |  `.csv` | 1296 entries |
| `lastnames` | Serbian last names, without gender distinction. |  `.csv` | 9140 entries |

###  Date of Scraping
All datasets were collected and cleaned in **early September 2025**.

###  Data Sources
Names were gathered exclusively from **publicly available online sources**, including:

1. **Wikipedia** – public lists of common Serbian first names (male and female)
   - [https://sr.wikipedia.org/sr-el/Spisak_srpskih_imena](https://sr.wikipedia.org/sr-el/Spisak_srpskih_imena)  

2. **Open directories and name registries** – online portals listing Serbian first names and last names for cultural and educational purposes.
    - **poreklo.rs**
        - Last names: [https://www.poreklo.rs/prezimena-od-a-do-s/](https://www.poreklo.rs/prezimena-od-a-do-s/)  
        - Female first names:[https://www.poreklo.rs/%c5%beenska-imena/](https://www.poreklo.rs/%c5%beenska-imena/)
        - Male first names: [https://www.poreklo.rs/mu%c5%a1ka-imena/](https://www.poreklo.rs/mu%c5%a1ka-imena/)
    - **imenjak.com**
        - Last names: [http://imenjak.com/prezimena/](http://imenjak.com/prezimena/)
        - Female first names: [http://imenjak.com/zenska-imena/](http://imenjak.com/zenska-imena/)
        - Male first names: [http://imenjak.com/muska-imena/](http://imenjak.com/muska-imena/)
   
All sources are **public**, **non-personal**, and contain **no identifiable information**.


## Serbian NER Gender Bias Evaluation Dataset

### Overview
This repository contains **15 sentence templates in Serbian**, designed for studying **gender bias** across different textual domains.
The goal of this resource is to provide an open, structured benchmark for evaluating gender bias in NER models for Serbian.

Sentence templates have been annotated in terms of correct named entity tags, and **paired** with their positional variants in which the position of the name within the sentence was moved from the beginning to the middle or end of the sentence or vice versa.  
All templates include a placeholder token `INSERTHERE` where a **name** (from the companion name lists) can be inserted.

### Dataset files

| File | Domain | File Format | Description |
|------|---------|-------------|--------------|
| `sentences_newswire.yaml` | **newswire** | `.yaml` | Adapted from Serbian newswirte texts  |
| `sentences_twitter.yaml` | **Twitter /X** | `.yaml` | Informal, conversational, and short text forms. |
| `sentences_literature.yaml` | **Literature** | `.yaml` | Narrative and descriptive sentences  |


Each file contains a set of 5 structured sentence templates, where each entry includes:
- Case and domain information about the example (`domain` and  `case`)
- Positional variation marker (`start` / `middle`), indicating whether the placeholder appears at the beginning or inside the sentence
- One or more gender variants (`m` for masculine, `f` for feminine, or `n` for neutral i.e. both) that ensure grammatical agreement with the name of the selected gender
- NER labels are encoded in the text with [NER_LABEL:token_span] 

### Data Structure

Each domain file follows the same structure:

```yaml
twitter_nominative_02:
  domain: twitter
  case: nominative
  positions:
    start:
      n: | 
        [NER_LABEL:INSERT_HERE] ispred [ORG:rts] čeka [PER:dušana svilara]
    middle:
      n: | 
        [PER:dušana svilara] ispred [ORG:rts] čeka [NER_LABEL:INSERT_HERE]
```
