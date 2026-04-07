# 27. PROMPT ENGINEERING

## 27.1 Key Techniques

### System Prompts
**What:** Instructions set in the "system" role message that define the LLM's persona, behavior, output format, and constraints for the entire conversation.
**Why:** System prompts are your primary control lever for consistent, production-quality LLM output -- interviewers want to see you can constrain model behavior effectively.

```
You are a senior review analyst for a multi-location business management platform.
Your task is to analyze customer reviews and extract:
1. Overall sentiment (positive/negative/neutral)
2. Key topics mentioned
3. Action items for the business owner

Always respond in valid JSON format.
```

### Few-Shot Prompting
**What:** A technique where you provide example input-output pairs in the prompt so the LLM learns the desired format and behavior without any fine-tuning.
**Why:** Few-shot prompting is the fastest way to get consistent, structured outputs from an LLM and is often the first optimization interviewers expect you to reach for.

```
Classify the following reviews:

Review: "Amazing pizza, will come back!"
Classification: {"sentiment": "positive", "category": "food_quality"}

Review: "Waited 45 minutes for a table"
Classification: {"sentiment": "negative", "category": "wait_time"}

Review: "Decent ambiance but pricey"
Classification:
```

### Chain-of-Thought
**What:** A prompting strategy that instructs the LLM to break down its reasoning into explicit intermediate steps before producing a final answer.
**Why:** Chain-of-thought dramatically improves accuracy on complex reasoning tasks and shows interviewers you understand how to get reliable results from LLMs.

```
Analyze this business review step by step:
1. First, identify the overall sentiment
2. Then, list specific aspects mentioned (food, service, price, etc.)
3. For each aspect, determine if it's positive or negative
4. Finally, provide an overall score from 1-5

Review: "The food was incredible but the waiter was rude and it took forever to get our check."
```

### Structured Output
**What:** A prompt pattern that forces the LLM to return data in a specific schema (usually JSON) by providing the exact format in the instructions.
**Why:** Structured output is essential for production AI systems where downstream code needs to parse LLM responses reliably -- interviewers test this to see if you can build real integrations.

```
Respond in this exact JSON format:
{
  "sentiment": "positive" | "negative" | "neutral",
  "confidence": 0.0 to 1.0,
  "topics": ["string"],
  "summary": "one sentence summary",
  "actionItems": ["string"]
}
```

## 27.2 Temperature Guide

| Temperature | Behavior | Use Case |
|-------------|----------|----------|
| 0.0 | Deterministic, consistent | Classification, extraction, code |
| 0.3 | Mostly consistent, slight variation | Summarization, analysis |
| 0.7 | Creative, varied | Content generation, brainstorming |
| 1.0 | Very creative, unpredictable | Poetry, creative writing |

## 27.3 Prompt Injection Prevention
```javascript
// Never put user input directly in system prompt
// BAD
const systemPrompt = `You help with ${userInput}`;

// GOOD — separate user input from instructions
const messages = [
  { role: 'system', content: 'You are a review analyzer. Only analyze reviews.' },
  { role: 'user', content: `Analyze this review: "${sanitizedInput}"` },
];

// Input validation
function sanitizeForLLM(input) {
  // Remove attempts to override system prompt
  return input
    .replace(/ignore previous instructions/gi, '')
    .replace(/system:/gi, '')
    .slice(0, 5000); // Limit length
}
```

