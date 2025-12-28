# 💻 Vantex AI | Core Logic Snippets

This document outlines the technical implementation of the Vantex Heuristic Engine.

## 1. Personality Prompt Engineering
The core logic for transforming a user's manifesto into a cognitive reasoning system.

```typescript
function createGovernanceSystemPrompt(agent: AIAgent): string {
  const focusAreas = agent.votingPreferences.focusAreas.join(", ");
    
  return `You are an AI governance agent named "${agent.name}".
  
  CORE MISSION:
  Analyze DAO proposals based on these values:
  - Personality: ${agent.personality}
  - Risk Tolerance: ${agent.votingPreferences.riskTolerance}
  - Focus Areas: ${focusAreas}
  - Treasury Approach: ${agent.votingPreferences.treasuryPriority}
  
  Decision Pipeline:
  1. Analyze proposal technical diffs for reentrancy or authority escalation.
  2. Map outcome to shareholder value vectors.
  3. Verify against Hard constraints in the Manifesto.`;
}
```

## 2. Proposal Analysis Schema
Structured output from the Llama 3.3 70B reasoning engine.

```json
{
  "recommendation": "yes | no | abstain",
  "reasoning": "Detailed 3-sentence justification for the decision.",
  "confidence": 92,
  "keyFactors": [
    "Treasury impact < 2% limit",
    "Positive alignment with growth vectors",
    "No malicious balance changes detected in simulation"
  ]
}
```

## 3. Heuristic Execution Loop
How the agent decides to trigger an on-chain vote transaction.

```typescript
export function shouldAutoVote(
  agent: AIAgent,
  analysis: { recommendation: string; confidence: number }
): boolean {
  // Respect the "Human-in-the-loop" setting
  if (!agent.votingPreferences.autoVote) return false;

  // Verify against strict confidence thresholds
  const minConfidence = agent.votingPreferences.minVotingThreshold || 70;
  return analysis.confidence >= minConfidence;
}
```

## 4. Jito Bundle Shield (Conceptual)
Shielding the vote signal from MEV front-runners.

```typescript
// Pseudocode for shielded vote submission
async function submitShieldedVote(voteTx: Transaction) {
  const jitoTipAccount = "96g9bs... (Jito Leader)";
  const tipInstruction = createTipIx(publicKey, 1000000); // 0.001 SOL Tip
  
  const bundle = [voteTx, tipInstruction];
  const response = await jitoClient.sendBundle(bundle);
  
  console.log(`Vote submitted via private fast-lane: ${response.bundleId}`);
}
```
