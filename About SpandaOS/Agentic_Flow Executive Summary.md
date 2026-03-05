# Agentic Flow: Executive Summary

## Overview
This document outlines the **Executive Summary** flow in SpandaOS. It explains the step-by-step process of how the system transitions from a standard RAG query to utilizing a Context-Aware XML Few-Shot prompt to generate a structured, C-suite ready summary.

## Step-by-Step Flow

### Step 1
After the end of RAG based queries we will have three agentic buttons. One of the Button is 'Executive Summary'.

![Executive Summary Step 1](Media/Agentic/Summary1.png)

### Step 2
Once clicked, It uses a Context-Aware XML Few-Shot prompt to build an authoritative, C-suite ready summary. It guarantees a 200-300 word response divided into specific sections: Core Findings, Key Metrics, Strategic Implications, and Recommended Actions.

![Executive Summary Step 2](Media/Agentic/Summary2.png)

### Step 3
Once finished it generates a detailed Summary and present it to user.

![Executive Summary Step 3](Media/Agentic/Summary3.png)

### Step 4
At the End of the response we gets AI Predicted next steps. if user clicks on any one of them then response based on that query will get generated (Currently n R&D phase about How to make them more useful)

![Executive Summary Step 4](Media/Agentic/Summary4.png)

---

## Agentic Flow: Executive Summary Architecture

Below is a detailed Mermaid.ai flow diagram mapping out the complete Agentic Flow for the Executive Summary generation.

```mermaid
flowchart TD
    %% Styling Profiles
    classDef userAction fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef stateNode fill:#2c3e50,stroke:#1a252f,stroke-width:2px,color:#ecf0f1,rx:5px,ry:5px
    classDef agentCore fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef processing fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef uiElement fill:#16a085,stroke:#1abc9c,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef finishNode fill:#27ae60,stroke:#2ecc71,stroke-width:2px,color:#fff,rx:5px,ry:5px

    A[User Completes Standard RAG Query]:::stateNode --> B{Agentic Action Buttons UI Displayed}:::uiElement
    
    B -->|User Clicks| C(Executive Summary Button clicked):::userAction
    B --> btn2(Other Agentic Function...):::uiElement
    B --> btn3(Other Agentic Function...):::uiElement

    C --> D[Initialize Executive Summary Agent]:::agentCore
    
    subgraph Execution Pipeline [Executive Summary Generation Pipeline]
        direction TB
        D --> E[Retrieve Previous RAG Query Context]:::processing
        
        E --> F[Inject Context-Aware XML Few-Shot Prompt]:::agentCore
        
        F --> G{LLM Processing}:::stateNode
        
        G --> H1[Extract Core Findings]:::processing
        G --> H2[Extract Key Metrics]:::processing
        G --> H3[Derive Strategic Implications]:::processing
        G --> H4[Formulate Recommended Actions]:::processing
        
        H1 --> I[Format into 200-300 word C-Suite ready structure]:::processing
        H2 --> I
        H3 --> I
        H4 --> I
    end
    
    I --> J[Generate Final Detailed Summary]:::stateNode
    J --> K[Present Executive Summary UI to User]:::uiElement
    
    K --> L[Generate AI Predicted Next Steps]:::agentCore
    L --> M{Display Prediction Action Tags}:::uiElement
    
    M -->|User Clicks AI Suggestion| N[Trigger Next Generative RAG/Agentic Context Query]:::userAction
    M -->|User Ignores Recommendations| O([End of Current Summary Flow]):::finishNode
    
    N --> A
```
