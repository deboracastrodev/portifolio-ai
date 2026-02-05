# UX Specification: The "Thinking Stream" Timeline

**Status:** Draft | **Owner:** Sally (UX Designer) | **Target:** MVP

## 1. Overview
The "Thinking Stream" is the core interaction pattern for DevMentor AI. It manages the inherent latency of multi-agent LLM processing by providing constant, streaming visual feedback, transforming "waiting time" into "insight time."

## 2. Visual Structure

### 2.1 The Timeline Container
- **Position:** Central column (Desktop: 60% width, Mobile: 100%).
- **Scroll Behavior:** Auto-scrolls to bottom as new events arrive, with a manual "Scroll to top" button if user interacts with history.
- **Theme:** Dark mode preferred (Glassmorphism effect) to emphasize the "AI Lab" feel.

### 2.2 Timeline Item (Agent Card)
- **Header:** Icon + Agent Name + Status Badge (e.g., "Thinking...", "Streaming...", "Completed").
- **Body:** 
    - **Streaming Text Area:** Where the agent's output appears word-by-word.
    - **Progress Bar:** A subtle, thin animated line below the header while the agent is active.
- **Actions:** 
    - **"View Raw Debate" (Toggle):** For power users (The "Carlos" Journey). Reveals the underlying logic/debate between agents for that specific finding.

## 3. Interaction States

| State | Visual Feedback | Trigger |
|-------|-----------------|---------|
| **Waiting** | Skeleton pulse in the next slot. | State Machine: Step queued. |
| **Processing** | Agent icon spins slowly; pulsing "..." indicator. | State Machine: Agent invoked. |
| **Streaming** | Text appears with "typewriter" effect; progress bar active. | SSE: Incoming text chunks. |
| **Completed** | Green checkmark next to header; progress bar disappears. | SSE: [DONE] signal. |
| **Conflict** | Amber warning icon; "Agent Critic is debating..." message. | State Machine: Disagreement detected. |

## 4. Animation Guidelines
- **Entry:** Items should "slide up" and "fade in" (Duration: 300ms, Easing: ease-out).
- **Text Streaming:** Smooth flow, not too fast to read, not too slow to annoy (aim for ~50-80 words per minute).
- **Consensus Pop:** When a skill is finalized, it should "fly" from the timeline to the sidebar Skill List.

## 5. Success Metric (Perceived Performance)
- **Time to First Byte (TTFB):** < 1s.
- **User Engagement:** User should start reading the first insight within 3s of clicking "Analyze".
- **Clarity:** 100% of users should understand which agent is currently contributing.

---
*Created by Sally (UX Designer) for portifolio-ai*
