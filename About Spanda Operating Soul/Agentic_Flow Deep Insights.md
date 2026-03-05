# Agentic Flow: Deep Insights

## Overview
This document explains the Deep Insights flow in SpandaOS, detailing the step-by-step process of how the **DeepInsightAgent** uses a Multi-Agent Reflection Loop to deeply interrogate the context and provide comprehensive, thoroughly analyzed answers to the user.

## Step-by-Step Flow

### Step 1
After the end of RAG based queries we will have three agentic buttons. One of the Button is 'Deep Insight'.

![Deep Insight Step 1](Media/Agentic/Deep1.png)

### Step 2
Once clicked, It triggers a dedicated DeepInsightAgent which runs a "Multi-Agent Reflection Loop." Rather than a single pass, it simulates a debate between different analytical personas (an Analyst, a Skeptic, and a Synthesizer) to deeply interrogate the context and find hidden insights before returning a final agreed-upon answer.

![Deep Insight Step 2](Media/Agentic/Deep2.png)

### Step 3
Once finished it generates a detailed analysis based on the debate and present it to user.

![Deep Insight Step 3](Media/Agentic/Deep3.png)

### Step 4
At the End of the response we gets AI Predicted next steps. if user clicks on any one of them then response based on that query will get generated (Currently n R&D phase about How to make them more useful)

![Deep Insight Step 4](Media/Agentic/Deep4.png)

---

## Agentic Flow: Deep Insights Architecture

Below is an extremely detailed flow diagram explaining the internal mechanics and sequence of the Agentic Flow for Deep Insights.

```mermaid
flowchart TD
    %% Styling Profiles
    classDef userAction fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef stateNode fill:#2c3e50,stroke:#1a252f,stroke-width:2px,color:#ecf0f1,rx:5px,ry:5px
    classDef agentCore fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef debatePersona fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef uiElement fill:#16a085,stroke:#1abc9c,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef finishNode fill:#27ae60,stroke:#2ecc71,stroke-width:2px,color:#fff,rx:5px,ry:5px

    A[User Completes Standard RAG Query]:::stateNode --> B{Agentic Action Buttons UI Displayed}:::uiElement
    
    B -->|User Clicks| C(Deep Insight Button clicked):::userAction
    B --> btn2(Other Agentic Function...):::uiElement
    B --> btn3(Other Agentic Function...):::uiElement

    C --> D[Initialize Dedicated DeepInsightAgent]:::agentCore
    
    subgraph Multi-Agent Reflection Loop [DeepInsightAgent: Multi-Agent Reflection Loop]
        direction TB
        D --> E{Context Interrogation Phase}:::agentCore
        
        E --> F1[Analyst Persona: Generates Initial Deep Insights]:::debatePersona
        E --> F2[Skeptic Persona: Challenges Assumptions & Biases]:::debatePersona
        E --> F3[Synthesizer Persona: Reconciles Perspectives]:::debatePersona
        
        F1 --> G[Simulated Internal Debate Platform]:::stateNode
        F2 --> G
        F3 --> G
        
        G --> H{Convergence Reached & Hidden Insights Found?}:::stateNode
        H -->|No - Needs deeper reflection| E
        H -->|Yes - Unified robust understanding| I[Draft Final Agreed-Upon Answer]:::agentCore
    end
    
    I --> J[Compile Detailed Analysis Report]:::stateNode
    J --> K[Present Detailed Analysis UI to User]:::uiElement
    
    K --> L[Generate AI Predicted Next Steps]:::agentCore
    L --> M{Display Prediction Action Tags}:::uiElement
    
    M -->|User Clicks AI Suggestion| N[Trigger Next Generative RAG/Agentic Context Query]:::userAction
    M -->|User Ignores Recommendations| O([End of Current Insight Flow]):::finishNode
    
    N --> A
```
