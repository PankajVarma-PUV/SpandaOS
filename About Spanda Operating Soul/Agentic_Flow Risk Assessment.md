# Agentic Flow: Risk Assessment

## Overview
This document details the **Risk Assessment** flow in SpandaOS. It explains how the system transitions from a Grounded Cognitive Query to a dedicated "Vulnerability Scanner" that strictly outputs JSON data to render a dynamic risk widget and table.

## Step-by-Step Flow

### Step 1
After the end of Grounded Cognitive queries we will have three agentic buttons. One of the Button is 'Risk Assessment'.

![Risk Assessment Step 1](Media/Agentic/Risk1.png)

### Step 2
Once clicked, It scans the semantic context specifically for risks, biases, and vulnerabilities (acting as a "Vulnerability Scanner"). It forces the LLM to output ONLY a strict JSON object (via Ollama JSON mode). This JSON contains an overall_score (0-100), a risk_level (CRITICAL, HIGH, MEDIUM, LOW), and an array of individual risks with mitigations. The UI then parses this JSON to render a dynamic risk widget.

![Risk Assessment Step 2](Media/Agentic/Risk2.png)

### Step 3
Once finished it generates a detailed Risk score based Table and present it to user.

![Risk Assessment Step 3](Media/Agentic/Risk3.png)

### Step 4
At the End of the response we gets AI Predicted next steps. if user clicks on any one of them then response based on that query will get generated (Currently n R&D phase about How to make them more useful)

![Risk Assessment Step 4](Media/Agentic/Risk4.png)

---

## Agentic Flow: Risk Assessment Architecture

Below is a detailed Mermaid.ai flow diagram mapping out the complete Agentic Flow for the Risk Assessment.

```mermaid
flowchart TD
    %% Styling Profiles
    classDef userAction fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef stateNode fill:#2c3e50,stroke:#1a252f,stroke-width:2px,color:#ecf0f1,rx:5px,ry:5px
    classDef agentCore fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef scanNode fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef uiElement fill:#16a085,stroke:#1abc9c,stroke-width:2px,color:#fff,rx:5px,ry:5px
    classDef finishNode fill:#27ae60,stroke:#2ecc71,stroke-width:2px,color:#fff,rx:5px,ry:5px

    A[User Completes Grounded Cognitive Query]:::stateNode --> B{Agentic Action Buttons UI Displayed}:::uiElement
    
    B -->|User Clicks| C(Risk Assessment Button clicked):::userAction
    B --> btn2(Other Agentic Function...):::uiElement
    B --> btn3(Other Agentic Function...):::uiElement

    C --> D[Initialize Vulnerability Scanner Agent]:::agentCore
    
    subgraph JSON Enforcement Pipeline [Strict JSON Enforcement Pipeline]
        direction TB
        D --> E[Enable Ollama Strict JSON Mode]:::agentCore
        E --> F[Inject Context for Risk/Bias/Vulnerabilities Analysis]:::scanNode
        
        F --> G{LLM Generation}:::stateNode
        
        G --> H1[Determine overall_score 0-100]:::scanNode
        G --> H2[Determine risk_level CRITICAL/HIGH/MEDIUM/LOW]:::scanNode
        G --> H3[Identify Array of Individual Risks]:::scanNode
        G --> H4[Identify Array of Mitigations]:::scanNode
        
        H1 --> I[Construct Final Strict JSON Object]:::agentCore
        H2 --> I
        H3 --> I
        H4 --> I
    end
    
    I --> J[UI Parses JSON Object]:::stateNode
    J --> K[Render Dynamic Risk Widget & Table]:::uiElement
    
    K --> L[Generate AI Predicted Next Steps]:::agentCore
    L --> M{Display Prediction Action Tags}:::uiElement
    
    M -->|User Clicks AI Suggestion| N[Trigger Next Context-Aware Synthesis Query]:::userAction
    M -->|User Ignores Recommendations| O([End of Current Risk Flow]):::finishNode
    
    N --> A
```
