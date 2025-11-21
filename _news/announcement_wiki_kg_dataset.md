---
layout: post
title: Introducing the Wikipedia Knowledge Graph Dataset in Wolfram Language
date: 2025-11-21 10:00:00-0000
inline: false
related_posts: false
---

We're releasing the Wikipedia Knowledge Graph Dataset: 49,897 Wikipedia articles transformed into structured, machine-readable knowledge graphs. This dataset demonstrates automated knowledge extraction at scale, converting free-text articles into formal representations suitable for AI reasoning and knowledge base applications.

## Dataset Overview

The dataset contains structured knowledge extracted from Wikipedia using two different AI models (sherlock_think and polaris_alpha). Each article is processed into Wolfram Language format, capturing entities, relations, properties, and timeline events with verifiable citations.

**Key Statistics:**
- **Total Articles:** 49,897
- **Source:** English Wikipedia
- **Format:** Parquet files with Wolfram Language knowledge graphs
- **License:** MIT
- **Coverage:** Diverse topics from aerodynamics to history, biology to mathematics

## Data Structure

Each row in the dataset contains:

- `article_name`: Wikipedia article title
- `sherlock_think`: Knowledge graph from the first extraction model
- `polaris_alpha`: Knowledge graph from the second extraction model
- `wiki_article`: Full Wikipedia article text or abstract
- `wiki_url`: Link to the original Wikipedia page
- `wiki_identifier`: Numeric Wikipedia page ID

The knowledge graphs use Wolfram Language syntax to represent structured knowledge with approximately 80+ relation types spanning domains including biography, warfare, astronomy, biology, linguistics, and mathematics.

## Usage

Load the dataset using the Hugging Face `datasets` library:

```python
from datasets import load_dataset

dataset = load_dataset("AutomatedScientist/wiki-kg-dataset")

# Access a sample
sample = dataset['train'][0]
print(f"Article: {sample['article_name']}")
print(f"Wiki abstract: {sample['wiki_article'][:200]}...")
print(f"Sherlock KG length: {len(sample['sherlock_think'])} chars")
print(f"Polaris KG length: {len(sample['polaris_alpha'])} chars")
```

## Example: Laura Bassi

To illustrate the dataset's structure, consider the entry for Laura Bassi, the 18th-century Italian physicist:

**Article Name:** Laura Bassi

**Wikipedia Excerpt:**
> Laura Maria Caterina Bassi Veratti (29 October 1711 – 20 February 1778) was an Italian physicist and academic

**Extracted Knowledge Graph:**

```wolfram
Entity["LauraBassi", <|
  "Name" -> "Laura Maria Caterina Bassi Veratti",
  "BirthDate" -> DateObject[{1711, 10, 29}],
  "DeathDate" -> DateObject[{1778, 2, 20}],
  "BirthPlace" -> Entity["City", "Bologna"],
  "Occupation" -> {"Physicist", "Academic"},
  "Spouse" -> Entity["GiuseppeVeratti"],
  "MarriageDate" -> DateObject[{1738}],
  "AlmaMater" -> Entity["University", "UniversityOfBologna"]
|>]

PATRONIZED_BY[
  Entity["LauraBassi"],
  Entity["PopeBenedictXIV"],
  <|"Citation" -> "Pope Benedict XIV supported her academic career"|>
]

MEMBER_OF[
  Entity["LauraBassi"],
  Entity["BolognaAcademy"],
  <|"Date" -> DateObject[{1732}],
    "Role" -> "First woman member"|>
]

ACHIEVED[
  Entity["LauraBassi"],
  "First salaried female university professor in Europe",
  <|"Date" -> DateObject[{1732}], "Institution" -> "University of Bologna"|>
]

APPOINTED_TO[
  Entity["LauraBassi"],
  "Chair of Experimental Physics",
  <|"Date" -> DateObject[{1776}], "Institution" -> "University of Bologna"|>
]
```

This structured representation captures biographical details as formal Wolfram Language entities with typed properties. The relations (`PATRONIZED_BY`, `MEMBER_OF`, `ACHIEVED`, `APPOINTED_TO`) link entities with metadata including dates and citations. This enables computational queries like "Who were the first female professors?" or "What scientific positions existed in 18th-century Bologna?" while maintaining traceability to source text.

## Citation Framework

The dataset implements a citation-tracking system where each extracted fact includes:

- **Verifiable citations** linking claims to source text
- **Regex patterns** for validating facts against original content
- **Metadata** for timeline events and entity properties
- **Evidentiary support** for scientific classifications

This citation framework enables fact-checking and traceability, critical for building trustworthy AI systems.

## Applications

This dataset supports multiple use cases:

1. **Knowledge Base Construction**: Build structured databases from unstructured text
2. **AI Training**: Train models for knowledge extraction and graph completion
3. **Question Answering**: Enable factual QA systems with citation support
4. **Scientific Discovery**: Identify patterns and connections across domains
5. **Educational Tools**: Create interactive learning systems with structured knowledge

## Technical Details

The knowledge graphs use Wolfram Language to represent:

- **Entities** with properties (birth dates, occupations, achievements)
- **Relations** between entities (IS_A, HAS_PART, CAUSES, INFLUENCES)
- **Timeline events** with dates and descriptions
- **Citations** with regex matching for verification

The dual-model approach (sherlock_think and polaris_alpha) provides complementary extractions, enabling ensemble methods and consistency checking.

## Access the Dataset

The dataset is available on Hugging Face:

**Dataset:** [AutomatedScientist/wiki-kg-dataset](https://huggingface.co/datasets/AutomatedScientist/wiki-kg-dataset)

We're excited to see what the research community builds with this resource. The dataset represents a step toward AI systems that can reason over structured knowledge while maintaining traceability to original sources.

## What's Next

This is version 0 of the dataset. In future versions, we will make the extraction pipeline fully verifiable, enabling complete reproducibility and transparency of the knowledge extraction process.

This release is part of our broader mission to build AI systems capable of autonomous scientific reasoning. By converting human knowledge into machine-readable formats, we enable AI to:

- Reason over existing scientific knowledge
- Identify gaps and inconsistencies
- Generate testable hypotheses
- Accelerate scientific discovery

Follow our progress:
- Twitter/X: [@autoscientist](https://x.com/autoscientist)
- Hugging Face: [AutomatedScientist](https://huggingface.co/AutomatedScientist)

We look forward to seeing how researchers leverage this dataset to advance knowledge extraction, representation, and reasoning systems.
