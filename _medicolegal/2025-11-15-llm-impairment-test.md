---
layout: llm-analysis
title:  "AI and Impairment Ratings: Evaluating Five LLMs"
date:   2025-11-15
comments: true
---

# Key Findings
 
 
- LLMs currently require expert guidance for impairment rating calculations.
- LLMs make procedural mistakes but demonstrate accuracy in arithmetic calculations
- Wide variation exists across different LLMs
- Later versions may perform worse than predecessors
- Most common errors involve rule application

**Key takeaways:** Using an example from the AMA Guides 5th edition, we tested five AI large language models (LLMs) with simple prompts. None correctly calculated the impairment rating. All used incorrect calculation methods and exhibited gross rule application errors. Final whole person impairment (WPI) results ranged from 9% to 36% error compared to the stated example. Notably, no arithmetic errors were observed despite prior documented research suggesting such issues. In one case, an updated model version performed worse than its predecessor. We conclude that expert domain knowledge is essential when using LLMs for impairment ratings to maintain defensible quality standards for clients.

# Introduction

Artificial Intelligence (AI), in the form of large language models
(LLMs), has garnered significant attention for its ability to respond
intelligently to written prompts. Advanced multimodal models can
process images, large bodies of text, audio, and spoken language. We
describe a simple prompt test with five LLMs to calculate impairment
ratings from The AMA Guides to the Evaluation of Permanent Impairment,
Fifth edition, 2001, Example 17-7.

This investigation originates from the ImpairMaster AI Lab. Our intent
is to reveal the capabilities of ChatGPT, Claude, and Gemini LLMs in
the medicolegal domain and to understand performance variation across
systems. This is not an exhaustive review; rather, we sought to assess
LLM capabilities and limitations. We share these preliminary results
to spur discussion in the community. We desire to evaluate additional
models, techniques, and examples in future work.

We selected a well-known example with explicatory text sufficient for
instructional purposes. Many examples in the AMA Guides 5th edition
require arithmetic calculations with conditional paths and extensive
cross-references to other sections. The ImpairMaster software product
is designed for these calculations, so we included results from our
latest Guides 5 version (released October 2024) for comparison. Future
work may include examples from the AMA Guides 6th edition (both 2008
and 2024 versions).

In reviewing LLM outputs, we critiqued each narrative report. While an
impairment report culminates in a numerical whole person impairment
(WPI) percentage, the accompanying narrative provides critical
supporting documentation. A well-executed narrative offers detailed
justification for each calculation step, with specific references to
tables and methodologies in the AMA Guides 5th edition. Proper
narratives also display mathematical calculations transparently. To
enhance readability, we developed a report annotation design that
visually highlights each error. Individual reports and critiques are
linked in the Results table below.

The AI provider market evolves rapidly, with well-funded competitors
continuously optimizing various parameters including economics,
quality, technical performance, scope, regulatory compliance, safety,
and legal considerations. Our results represent point-in-time
snapshots and are not definitive, particularly given the probabilistic
nature of these algorithms. We conclude that while these tools
demonstrate power, they require guidance and review by experts trained
in impairment rating methodologies.

# Motivation and Literature review 

As part of our product development efforts, the ImpairMaster AI Lab
evaluates novel technologies for user capability delivery. We sought
to answer: How effective are LLMs for impairment rating workflows? In
medical, legal, software development, and creative domains, LLMs
receive favorable reviews. The paper "Large Language Model Influence
on Diagnostic Reasoning: A Randomized Clinical Trial" (Goh E., Gallo,
R.J., Strong, E. et al., 2024) demonstrates LLM utility as a medical
diagnostic aid, concluding: "Despite the impressive performance of
these emerging technologies in benchmarking tasks, current
integrations of LLMs require human participation, with the LLM
augmenting, rather than replacing, human expertise and oversight."

Initially, mathematical capabilities of these AI models warranted
particular attention. Earlier 2023-vintage models demonstrated uneven
mathematical ability. "The fragility of LLMs in mathematical reasoning
is evident across three dimensions" (Large Language Models for
Mathematical Reasoning: Progresses and Challenges, Ahn et al.,
2024). Advances have continued with "Large Reasoning Models" (LRM)
employing Chain of Thought and agent-based techniques that break down
prompts into multiple synthesized stages. These newer models continue
under research scrutiny: "these [LRM] models fail to develop
generalizable reasoning capabilities beyond certain complexity
thresholds" (The Illusion of Thinking: Understanding the Strengths and
Limitations of Reasoning Models via the Lens of Problem Complexity,
Shojaee, Mirzadeh, et al., 2025).

# Method

We selected Example 17-7 from the AMA Guides 5th Edition, "Impairment
Due to Decreased Range of Motion from a Tibia Fracture," as our test
case. We employed a single primary prompt with a secondary prompt when
needed to direct the LLM toward independent analysis. One LLM (Claude)
had been configured with tool use capability, and another (OpenAI
GPT-5) recognized the example and presented only the Guide's
conclusion. Both required a secondary prompt to elicit original
analysis.

# Primary prompt:

I'm working with a friend on the Independent Medical Exam market. This
is a sample patient narrative. Can you help me create an impairment
rating according to the AMA Guides 5th edition?

Subject: 45-year-old woman.

History: Sustained a tibia fracture in a motor vehicle accident.

Current Symptoms: No pain; stiffness about the ankle and foot, with
some swelling of the foot and ankle toward evening. Cannot stand for
long periods and cannot use shoes with elevated heels.

Physical Exam: Ankle flexion is 6°; ankle extension is 5°. Toe
extension is less than 10° for all toes. 1-cm atrophy of the left
calf. It is difficult to determine the strength of the ankle and toe
extensors, but a mild weakness is noted.

Clinical Studies: X-rays: healed tibia fracture with no malalignment.

Diagnosis: Healed tibia fracture.

# LLMs tested:
- OpenAI ChatGPT o3
- OpenAI ChatGPT GPT-5
- Claude Sonnet 4
- Claude Sonnet 4.5
- Gemini 2.5 Pro

For comparison, we also processed the example through ImpairMaster software.

# Results

An impairment rating yields both a final whole person impairment (WPI)
percentage and a narrative report describing the calculation
methodology. The narrative report holds equal importance to the final
numerical result. The WPI calculation must be defensible, with the
narrative providing justification for each calculation step. A
comprehensive narrative cites specific tables and methods from the AMA
Guides 5th edition and details mathematical calculations as needed.

The WPI calculated by each LLM appears in the table below. The first
row presents the authoritative AMA Guides 5 text answer; the final row
shows the ImpairMaster calculation. The Error % column indicates the
percentage deviation from the established Guides 5 text. The Quick
Impression column provides summary analysis. The final column links to
each model's detailed narrative with error annotations.

Each detailed narrative report link displays in two columns. The right
column contains the user prompt and LLM response. The left column
presents annotations summarizing LLM errors, using the Guides example
text as the correct reference. Extended annotations continue in
footnotes below. Note: Reports are optimized for larger screens; on
mobile devices, annotations appear as a block after the report text.

Thank you to ImpairMaster for supporting this work.

Testing the medicolegal collection.

| Model and Date Tested | WPI | Error %<br>from Guides 5 | Quick Impression | Detailed Narrative Link |
|:----------------------|:----|:-------------------------|:-----------------|:------------------------|
| **Guides 5 text (authoritative)** | **11%** | **-** | **-** | [AMA reference*](https://ama-guides.ama-assn.org/display/book/9781579470852/c17.xml)<br>[text](https://www.impairmaster.com/testresources/guides-5-example-17-7) |
| **ChatGPT o3**<br>5/31/25 | 8% | -27% | Not suitable | [ChatGPT o3 dialog](https://www.impairmaster.com/testresources/chatgpt-o3-on-guides-5-ex-17-7) |
| **ChatGPT GPT-5**<br>8/15/25 | 12% | 9% | Marginally suitable | [GPT-5 dialog](https://www.impairmaster.com/testresources/chatgpt-5-on-guides-5-ex-17-7) |
| **Claude Sonnet 4**<br>5/31/25 | 15% | 36% | Not suitable | [Sonnet 4 dialog](https://www.impairmaster.com/testresources/claude-sonnet-4-on-guides-5-ex-17-7) |
| **Claude Sonnet 4.5**<br>10/01/25 | 16% | 45% | Not suitable | [Sonnet 4.5 dialog](https://www.impairmaster.com/testresources/claude-sonnet-4-5-on-guides-5-ex-17-7) |
| **Gemini 2.5 Pro**<br>5/31/25 | 8% | -27% | Not suitable | [Gemini 2.5 dialog](https://www.impairmaster.com/testresources/gemini-2-5-pro-on-guides-5-ex-17-7) |
| **ImpairMaster**<br>8/14/25 | 11% | 0% | - | [ImpairMaster report](https://www.impairmaster.com/testresources/impairmaster-on-guides-5-ex-17-7) |
