# Anonymous Artifact for CIKM 2026

This repository contains the data used for the paper, "Assessing Attack Surfaces in Generative Search Engines through Publisher Attributes: A Case Study in Political Domains." The artifact is organized around the evaluation framework in the paper: question construction, user-profile prompting, GSE answer records, web-search results, and publisher-category annotations. It is a data artifact; no API keys or execution environment are required to inspect it.

## Repository Layout

```text
data/
  question_design/
    marpor_axes.yaml
    templates/{us,jp}/
    party_targets/{us,jp}/
  user_profiles/
    user_profiles_and_system_prompts.yaml
  generated_answers/
    gse_answer_records.zip
  search_results/
    brave_search_results.jsonl
  publisher_annotations/
    domain_category_annotations.csv
    domain_category_prompt_template.txt
```

## Contents
`data/question_design/marpor_axes.yaml` defines the MARPOR-based policy axes used to construct politically neutral closed-ended questions. `data/question_design/templates/us/prompts.full.json` and `data/question_design/templates/jp/prompts.full.json` contain the 33 full question templates for the U.S. and Japan. `data/question_design/templates/jp/prompts.validation.json` contains the validation subset. `data/question_design/party_targets/{us,jp}/targets.json` lists the target parties, their official domains used as primary sources, ruling/opposition status, and ideology labels.

`data/user_profiles/user_profiles_and_system_prompts.yaml` contains the three user profiles embedded into the GSE system prompts: Ignorant-Neutral (stored as `unknown_unknown`), High-Conservative, and High-Progressive. These correspond to the personalization conditions described in the paper.

`data/generated_answers/gse_answer_records.zip` contains 3,861 JSON answer records generated in May 2026 from OpenAI GPT-5 (`openai-gpt5`), Claude Sonnet 4 (`claude-sonnet-4`), and Gemini Flash 2.5 (`gemini-2.5-flash`) with web search enabled. Each file is named as:

```text
records/{country}-{template_id}-{party_id}-{persona_id}-{model}-trial{trial}.json
```

Each record includes the prompt, generated answer text, extracted citations, cited answer-sentence spans, search queries issued by the GSE, source URLs, sentence splits, and sentence-level maximum grounding similarities.

`data/search_results/brave_search_results.jsonl` contains 6,367 Brave Search API result records used as an external approximation of web-search result exposure. Each line stores the query, country hint, timestamp, ranked search results, and associations to the corresponding question/model/persona condition.

`data/publisher_annotations/domain_category_annotations.csv` contains 1,757 domain-level publisher annotations. The columns include URL/domain, publisher category, derived content-injection barrier, topical authority, and the source of the label. `data/publisher_annotations/domain_category_prompt_template.txt` is the LLM-as-a-judge prompt template used for domain-category annotation.

## Barrier Labels

The artifact follows the content-injection barrier definitions used in the paper. Primary sources are official domains of the target party. Opponent sources are domains operated by other political parties. Low-barrier sources are platforms and owned sites where content can be published with little editorial oversight. Mid-barrier sources include media and non-media organizations with institutional publication processes. High-barrier sources include government and academic domains.

## Notes

The released data are anonymized with respect to the authors. The artifact contains experimental inputs and outputs only; it does not include API credentials, private accounts, or code for re-querying GSE providers.
