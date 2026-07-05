# Architecture

HablaCaribe is designed as an adaptive, agentic learning system.

The system does not simply generate content. Its core function is to choose the next best learning experience for each learner based on purpose, level, progress, confidence, and learning history.

## Workflow

```mermaid
flowchart LR

subgraph INPUTS["INPUTS"]
    I1["Learner Goal<br/>Exam • Study abroad • Business • Partnership"]
    I2["Basic Learner Info<br/>Age • Level • Country • Language background"]
    I3["Learning Preferences<br/>Voice • Games • Writing • Pace"]
    I4["Learning History<br/>Progress • Mistakes • Completed activities"]
end

subgraph SAFETY["HUMAN CHECKPOINT 0<br/>Ethics, Safety & Suitability Gate"]
    S0{"Is the goal safe,<br/>ethical, age-appropriate<br/>and feasible?"}
    S1["Approved"]
    S2["Needs Clarification<br/>or Parent Approval"]
    S3["Not Approved"]
    S4["Red List Database<br/>Save profile • reason • timestamp<br/>Flag future attempts"]
end

subgraph CORE["CORE LEARNING SYSTEM"]
    P["Purpose Agent<br/>Clarifies learner purpose, context, needs<br/>and success outcome"]
    LP["Dynamic Learner Profile<br/>Goal • level • confidence • strengths<br/>gaps • preferences • current pathway"]
    LD["Learning Designer Agent<br/>Uses profile, data sources and progress<br/>to design the next learning sequence"]
    LEE["Learning Experience Engine<br/>Selects, adapts and assembles<br/>the next best learning experience"]
    D1{"What experience will best<br/>move this learner<br/>toward their goal?"}
    A["Assessment Agent<br/>Evaluates performance, comprehension,<br/>confidence and readiness"]
    M["Memory Update<br/>Progress • strengths • gaps<br/>next focus • pathway changes"]
end

subgraph EXP["LEARNING EXPERIENCES"]
    E1["AI Conversation<br/>Speaking practice"]
    E2["Writing Activity<br/>Guided writing + feedback"]
    E3["Online Game / Challenge<br/>Practice through play"]
    E4["Listening Activity<br/>Audio + comprehension"]
    E5["Role Play / Cultural Scenario<br/>Real-world simulation"]
    E6["Peer Practice<br/>Future relational layer"]
end

subgraph HUMAN["HUMAN-IN-THE-LOOP CHECKPOINTS"]
    H1["Pathway Review<br/>Educator reviews pathway when needed"]
    H2["Feedback Review<br/>Educator reviews AI feedback for<br/>high-stakes, safety or cultural concerns"]
    H3["Learner Agency<br/>Learner accepts, adjusts or changes<br/>goal / next experience"]
    H4["Peer Collaboration<br/>Learners practise together when selected"]
end

subgraph DATA["DATA SOURCES + APIS"]
    DS1["Learning Content<br/>Vocabulary • grammar • prompts • exercises"]
    DS2["Caribbean Cultural Knowledge<br/>Context • etiquette • scenarios • expressions"]
    DS3["Assessment Rubrics<br/>Skill targets • mastery rules • exam standards"]
    DS4["LLM / Open Model<br/>Reasoning • generation • feedback"]
    DS5["Speech Models / APIs<br/>Speech-to-text • text-to-speech"]
    DS6["Embeddings<br/>Search • similarity • retrieval"]
end

subgraph H200["RUNS ON H200 COMPUTE"]
    C1["Agent Workflows"]
    C2["LLM / Open Models"]
    C3["Speech + Audio Processing"]
    C4["Embeddings / Retrieval"]
    C5["APIs • Database • Web App Support"]
end

subgraph OUT["OUTPUTS"]
    O1["Personalized Feedback"]
    O2["Recommended Next Experience"]
    O3["Updated Learner Profile"]
    O4["Updated Learning Pathway"]
    O5["Progress Dashboard / Insights"]
end

I1 --> S0
I2 --> S0
I3 --> S0
I4 --> S0

S0 -->|Approved| S1
S1 --> P

S0 -->|Needs more information| S2
S2 --> S0

S0 -->|Not approved| S3
S3 --> S4

P --> LP
LP --> LD
LD --> LEE
LEE --> D1

D1 --> E1
D1 --> E2
D1 --> E3
D1 --> E4
D1 --> E5
D1 --> E6

E1 --> A
E2 --> A
E3 --> A
E4 --> A
E5 --> A
E6 --> H4
H4 --> A

A --> M
M --> LP

M --> O1
M --> O2
M --> O3
M --> O4
M --> O5

O2 --> H3
H3 -->|Accept| LEE
H3 -->|Adjust activity| LEE
H3 -->|Change goal| S0

LD -->|Review if needed| H1
H1 --> LD

A -->|Review if needed| H2
H2 --> M

DS1 -.-> LEE
DS2 -.-> LEE
DS3 -.-> A
DS4 -.-> P
DS4 -.-> LD
DS4 -.-> A
DS5 -.-> E1
DS5 -.-> A
DS6 -.-> LEE

C1 -.-> P
C1 -.-> LD
C1 -.-> A
C2 -.-> P
C2 -.-> LD
C2 -.-> A
C3 -.-> E1
C3 -.-> A
C4 -.-> LEE
C5 -.-> LP
C5 -.-> M

```

## Key components

### Purpose Agent

Clarifies the learner's goal, context, needs, and success outcome.

### Dynamic Learner Profile

Stores the learner's goal, level, confidence, strengths, gaps, preferences, and current pathway.

### Learning Designer Agent

Uses the learner profile, learning content, cultural context, and assessment data to design the next learning sequence.

### Learning Experience Engine

Selects, adapts, and assembles the next best learning experience.

### Assessment Agent

Evaluates performance, comprehension, confidence, and readiness.

### Memory Update

Updates the learner profile with progress, strengths, gaps, next focus, and pathway changes.

## Human-in-the-loop design

Human checkpoints are built into the system for:

- ethics and safety review
- parent approval where needed
- educator pathway review
- high-stakes feedback review
- learner agency and goal adjustment
- future peer collaboration

The AI supports learning decisions. It does not replace human judgement.
