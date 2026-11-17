# Agent-architecture-design
<img width="701" height="493" alt="image" src="https://github.com/user-attachments/assets/17da65ed-22b9-48ac-804a-845b27f4242e" />

https://bytebytego.com/guides/how-to-ace-system-design-interviews-like-a-boss/
https://medium.com/@vipra_singh/ai-agents-multi-agent-architectures-part-7-0f0e185bb083
https://medium.com/@vipra_singh
https://www.mongodb.com/resources/basics/artificial-intelligence/agentic-systems
<img width="722" height="612" alt="image" src="https://github.com/user-attachments/assets/d67d6d73-adfe-4e63-b478-629d0a9c554c" />
One architecture diagram that explains every AI agent.

After building and scaling real agent systems in production, this same pattern keeps showing up — no matter the model or framework.

Here’s the universal anatomy:
→ Perception Layer
→ Reasoning Engine (LLM)
→ Planning Module
→ Tool Execution / Action Layer
→ Memory System
→ Guardrails & Safety
→ Observability Layer

Most people only focus on the RAG.

In production, the real complexity lives in how these layers work together.

This applies to ChatGPT, Claude, coding agents, enterprise agents, multi-agent systems… almost everything.
https://medium.com/@amarg3891/the-complete-guide-to-ai-agent-architecture-25dc2cbe7016
____________________________
Designing a multi-agent system (MAS) involves breaking complex tasks into autonomous, specialized workers that collaborate through clear communication and state-management patterns. [1] (https://mastra.ai/articles/multi-agent-systems), [2] (https://aws.amazon.com/marketplace/build-learn/ai-agent-learning-series/multi-agent-architectures)

Step 1: Choose the Right Architectural Pattern

Select a design pattern based on how much coordination or autonomy your workflow requires: [1] (https://medium.com/@princekrampah/multi-agent-architecture-in-multi-agent-systems-multi-agent-system-design-patterns-langgraph-b92e934bf843)
• Supervisor / Orchestrator-Worker Pattern: A central lead agent receives the user prompt, plans sub-tasks, delegates work to specialized sub-agents (as tools or distinct nodes), and aggregates the final output. Great for predictable multi-step workflows. [1] (https://www.youtube.com/watch?v=92KYqr4Fpf0), [2] (https://www.youtube.com/watch?v=fqvbxkgU6vE), [3] (https://medium.com/@princekrampah/multi-agent-architecture-in-multi-agent-systems-multi-agent-system-design-patterns-langgraph-b92e934bf843)
• Hierarchical Pattern: Nested teams where a top-level supervisor manages sub-supervisors, who in turn manage localized teams of agents. Best for massive enterprise domains. [1] (https://medium.com/@princekrampah/multi-agent-architecture-in-multi-agent-systems-multi-agent-system-design-patterns-langgraph-b92e934bf843), [2] (https://www.youtube.com/watch?v=92KYqr4Fpf0)
• Network Pattern: A fully connected system where any agent can talk to or hand off work to any other agent. [1] (https://medium.com/@princekrampah/multi-agent-architecture-in-multi-agent-systems-multi-agent-system-design-patterns-langgraph-b92e934bf843), [2] (https://www.youtube.com/watch?v=92KYqr4Fpf0)
• Swarm Pattern: Specialized agents dynamically pass control back and forth based on real-time expertise and active memory continuity without a rigid, pre-programmed path. [1] (https://medium.com/@princekrampah/multi-agent-architecture-in-multi-agent-systems-multi-agent-system-design-patterns-langgraph-b92e934bf843), [2] (https://www.youtube.com/watch?v=92KYqr4Fpf0)
• Creator-Verifier (Peer) Pattern: One agent builds or generates an artifact (e.g., code or text), and a separate verifier/judge agent reviews it with fresh context to catch flaws or enforce a pass/fail contract. [1] (https://www.youtube.com/watch?v=ow1we5PzK-o&t=110)

Step 2: Define Agent Boundaries and Personas

For each agent in your system, explicitly define:
• Scope and Objective: What single responsibility does this agent own? (e.g., a Researcher finds data, a Coder writes scripts, a Judge validates output). [1] (https://www.youtube.com/watch?v=j_l-9uNX2SA&t=18)
• System Prompt & Constraints: Instructions, tone, output schema (e.g., using Pydantic validation to force strict "pass" or "fail" outputs). [1] (https://www.youtube.com/watch?v=j_l-9uNX2SA&t=18)
• Assigned Tools: Restrict tools per agent via protocols like the Model Context Protocol (MCP) so agents only access the APIs and databases they actually need. [1] (https://developer.microsoft.com/blog/designing-multi-agent-intelligence/), [2] (https://aws.amazon.com/marketplace/build-learn/ai-agent-learning-series/multi-agent-architectures)

Step 3: Design Communication and State Management

Decide how information flows between agents: [1] (https://www.youtube.com/watch?v=4nZl32FwU-o&t=1), [2] (https://aws.amazon.com/marketplace/build-learn/ai-agent-learning-series/multi-agent-architectures)
• Shared State Object: Agents read and write to a centralized, shared state (common in graphs).
• Message Passing / Event Bus: Agents communicate via asynchronous publish-subscribe events or direct message protocols.
• Context Isolation: Keep individual sub-agent context windows small to prevent "context overload," leaking irrelevant chat history, or token explosion. [1] (https://www.langchain.com/blog/choosing-the-right-multi-agent-architecture), [2] (https://www.youtube.com/watch?v=4nZl32FwU-o&t=1), [3] (https://aws.amazon.com/marketplace/build-learn/ai-agent-learning-series/multi-agent-architectures), [4] (https://dev.to/leena_malhotra/the-architecture-of-multi-agent-ai-systems-explained-5440), [5] (https://claude.com/resources/articles/building-multi-agent-systems-when-and-how-to-use-them)

Step 4: Build Hybrid & Deterministic Fallbacks

• Skip the LLM Where Possible: Use standard deterministic code (algorithms, database lookups, state ticks) for routine logic instead of burning LLM tokens on every single step. [1] (https://www.youtube.com/watch?v=Fzd0BWMH65s)
• Add Guardrails at Boundaries: Implement circuit breakers, retries, and fallback strategies at the agent boundary so a failure in one sub-agent does not crash the entire pipeline. [1] (https://dev.to/leena_malhotra/the-architecture-of-multi-agent-ai-systems-explained-5440), [2] (https://aws.amazon.com/marketplace/build-learn/ai-agent-learning-series/multi-agent-architectures)

Step 5: Choose a Framework

Implement your design using production-ready orchestration frameworks:
• LangGraph (for graph-based stateful multi-agent flows)
• Google Agent Development Kit (ADK) paired with Agent-to-Agent (A2A) protocols
________________________________________________________________________________

• What specific workflow or problem are you trying to solve with these agents?
• Do you prefer a code-first framework (like LangGraph) or a managed platform?
SponsoredYou might consider these options:
Miro
Multi-Agent System (MAS) Design Workshop
Unleash Your Creative Ideas on an Infinite Canvas & Collaborate in Real-Time.
Udemy, Inc.
Agentic AI Mastery: Multi-Agent Systems in Practice
Learn Data Science online at your own pace. Start today and improve your skills.
_________________________________________________________________________________
<img width="858" height="635" alt="image" src="https://github.com/user-attachments/assets/ba254a12-4512-4f61-badf-6f8ec93502c7" />
_________________________________________________________________________________
I understand what you're trying to ask now. And I think there is a more fundamental problem underneath all your questions.

You're not asking me to give you another collection of engineering frameworks.

You're asking:

**"When I receive a completely new project, how do I systematically investigate it, generate all the important engineering questions myself, discover things I don't know I need to ask, and keep investigating until I understand what needs to be built and how the complete system must work?"**

You want a repeatable way to *produce the questions*, not just answer questions someone else has already written.

That's a different skill.

## **1. The right terminology for what you're trying to develop**

There are several established engineering disciplines that contribute to this capability.

| Discipline                               | Its practical contribution                                         |
| ---------------------------------------- | ------------------------------------------------------------------ |
| Requirements elicitation                 | Discover what the business and users actually need                 |
| Domain discovery                         | Discover the real-world entities, relationships and business rules |
| Systems analysis                         | Understand the complete system and its boundaries                  |
| Operational decomposition                | Break business activities into executable operations               |
| Scenario-based analysis                  | Discover what must happen in real situations                       |
| State and lifecycle analysis             | Discover how things change over time                               |
| Data modelling                           | Discover what information must exist and how it relates            |
| Failure Mode and Effects Analysis (FMEA) | Discover what can fail and what the consequences are               |
| Architecture trade-off analysis          | Discover which design decisions need to be made and why            |
| Verification engineering                 | Discover how to prove the system works correctly                   |

But I would not tell you to memorize these ten disciplines.

The capability you are looking for is better described as:

Your target capability

# **Systematic Engineering Discovery**

The ability to investigate an unfamiliar problem, reconstruct its complete operational reality, generate the necessary engineering questions, expose hidden requirements and derive an implementation-ready system design.

The important distinction:

- A question bank contains questions.
- A framework tells you how to organise questions.
- **Engineering discovery teaches you how to generate the next question from the answer to the previous one.**

That third capability is what you need.

## **2. Why your existing question bank isn't solving the problem**

Look at your agent question bank.

You have questions such as:

- How many agents do we need?
- What does each agent do?
- Which agent runs first?
- Which database does each agent use?
- What happens if an agent fails?
- How do agents communicate?

These are good questions.

But they are mostly disconnected questions.

Consider one real situation:

NuFlorist discovers a florist business in London.

You save the business in your database.

Now think about what happens next.

**One discovery event creates an entire investigation**

**Event**

A new florist business is discovered.

**Questions emerge**

- What makes this business unique?
- Has it already been discovered?
- How do we identify duplicates?
- Which fields must be extracted?
- Where did each field come from?
- What if its website is unavailable?
- Who is allowed to create the record?
- What happens if saving fails?
- Can another worker process it simultaneously?
- What status should the business have now?
- What should trigger the next operation?

**Engineering decisions emerge**

Identity rules, database schema, data provenance, validation, concurrency control, workflow states, error handling and agent handoffs.

Notice something important.

You did not need to remember a separate list of 100 database questions.

The situation itself generated the questions.

This is the shift I want you to make.

## **3. The practical method: investigate a system through its actual behaviour**

I recommend using a technique I will call **Scenario-Driven Engineering Discovery**.

It is not a new academic framework. It is a practical way to combine requirements discovery, domain modelling, operational analysis, data modelling and failure analysis.

Instead of starting with technologies or component names, start with a real situation that the system must handle.

Use this sequence.

### **Move 1 — Start with a real-world outcome**

Ask:

- What is the user or business trying to achieve?
- What does success actually look like?
- What is the starting situation?
- What must be true when the process finishes?
- What is outside the scope?

**NuFlorist example:** Produce a qualified, sufficiently researched and outreach-eligible florist prospect.

This gives you a concrete outcome to investigate.

### **Move 2 — Walk through one real scenario**

Don't ask "What are all the agents?"

Take one prospect and follow it.

For example:

1. A campaign is created.
2. A target location is selected.
3. Businesses are discovered.
4. Business information is extracted.
5. The business is checked for duplication.
6. The business is qualified.
7. A decision-maker is identified.
8. Contact information is discovered.
9. Research is performed.
10. Outreach eligibility is checked.
11. The prospect is handed to the outreach platform.

At every step, ask:

- What causes this step to happen?
- Who performs it?
- What must happen before it?
- What information does it need?
- What does it produce?
- What happens next?

This reveals the workflow before you decide how many agents to build.

### **Move 3 — Investigate each operation**

For every step, open it up.

Suppose the operation is:

"Identify the decision-maker."

Now investigate:

- What does decision-maker mean for this business?
- Which roles qualify?
- What sources can identify a person?
- What evidence is acceptable?
- How do we associate the person with the correct business?
- What happens when multiple people qualify?
- What if no person is found?
- What if the information conflicts?
- What is the required output?
- Where is that output stored?
- Who uses it next?

You have now moved from a vague business activity to an engineering specification.

### **Move 4 — Follow the information**

For every important piece of information, ask:

- Where is it created?
- Who creates it?
- Where does it originate?
- Is it extracted, inferred, calculated or supplied by a human?
- How do we know it is trustworthy?
- Where is it stored?
- Who owns it?
- Who reads it?
- Who can update it?
- How long is it retained?
- What happens when it changes?

This is how database questions emerge naturally.

For example, discovering a contact leads to the need for a contact record, business relationship, source evidence, discovery timestamp, verification status and possibly a history of changes.

You derive the columns from the information requirements instead of inventing a database schema first.

### **Move 5 — Follow the decisions**

At every operation, ask:

- What decisions must be made?
- Which decisions are simple rules?
- Which decisions require reasoning?
- What evidence is needed?
- What happens when the evidence is insufficient?
- Who has authority to make the decision?
- Can the decision be reversed?
- How do we record why it was made?

This reveals where an AI agent is useful and where deterministic software is preferable.

### **Move 6 — Break the scenario deliberately**

Now imagine the normal process does not work.

Ask:

- What if the input is missing?
- What if the information is incorrect?
- What if the API is unavailable?
- What if the same task runs twice?
- What if two workers process the same business?
- What if the server crashes?
- What if the database write succeeds but the agent never receives confirmation?
- What if an agent gives a plausible but unsupported answer?
- What if the next component cannot continue?

For each failure, investigate detection, impact, handling, recovery and prevention.

This is how failure engineering becomes part of the design rather than something added at the end.

### **Move 7 — Follow the system after deployment**

Ask:

- Who starts the workflow?
- Where does it execute?
- What schedules it?
- How is work distributed?
- How are permissions enforced?
- What is monitored?
- What is measured?
- How are failures surfaced?
- How is the system restarted?
- How are changes deployed?
- How are costs controlled?
- How is performance improved?

This uncovers infrastructure, harness engineering, orchestration, observability and FinOps requirements.

## **4. The most important technique: use question-generating triggers**

Here is something I particularly want you to adopt.

Don't try to remember thousands of questions.

Learn to recognise situations that automatically require investigation.

## **Engineering question generators**

When you encounter this situation, investigate these dimensions.

**A new thing is created**

Identity, required fields, validation, ownership, persistence, uniqueness.

**A thing changes**

Previous state, new state, who changed it, history, consistency, downstream effects.

**A task starts**

Trigger, prerequisites, inputs, permissions, resources, execution limits.

**A task finishes**

Output, validation, persistence, acknowledgement, next action, completion status.

**One component gives work to another**

Contract, payload, identifiers, transport, ownership, acknowledgement, retry.

**A decision is made**

Evidence, rules, authority, uncertainty, alternatives, audit trail.

**Two things happen simultaneously**

Concurrency, locking, race conditions, idempotency, conflicting writes.

**An external service is involved**

Authentication, API contract, rate limits, timeout, outage, cost, provider changes.

**Something can fail**

Detection, impact, containment, retry, recovery, escalation, prevention.

**Information is retrieved**

Source, freshness, relevance, access control, provenance, missing results.

**An AI agent is involved**

Context, instructions, tools, autonomy, state, verification, budgets, stopping rules.

**The system grows**

Throughput, bottlenecks, concurrency, cost, capacity, isolation, scaling.

These triggers are more useful than memorising isolated question banks.

Whenever you encounter one, you know which directions to investigate.

## **5. How to use this in a completely new project**

Let's say tomorrow someone gives you an unfamiliar project.

Don't start by asking:

"What architecture should I use?"

Don't start by asking:

"Which agents do I need?"

Start by creating an actual project investigation.

Use this working document.

# PROJECT ENGINEERING DISCOVERY WORKSPACE

## 1. Project outcome

- What business problem are we solving?
- Who experiences the problem?
- What outcome must the system produce?
- How will success be measured?
- What is outside the scope?

## 2. Real-world scenarios

List the important situations the system must handle.

For each scenario:

- What starts it?
- What happens?
- Who participates?
- What information is involved?
- What should happen at the end?

## 3. Operational breakdown

For each operation:

- What is its objective?
- What triggers it?
- What must happen first?
- Who or what executes it?
- What inputs does it need?
- What actions does it perform?
- What decisions does it make?
- What outputs does it create?
- What happens next?

## 4. Information and data investigation

For every important entity and data item:

- What is it?
- Where does it originate?
- Who owns it?
- Who creates and updates it?
- Where is it stored?
- How is it validated?
- How does it relate to other entities?
- What history must be preserved?
- What happens when it changes or becomes invalid?

## 5. Component and responsibility investigation

For every proposed component:

- Why does it exist?
- What responsibility does it own?
- What does it not own?
- What does it depend on?
- What does it provide?
- Does it need AI?
- Can deterministic software do the work?
- How does it interact with other components?

## 6. Decision investigation

- What decisions must the system make?
- What evidence is required?
- What rules constrain the decision?
- Who or what has authority?
- What happens when evidence is insufficient?
- How are decisions recorded and reviewed?

## 7. Integration investigation

For every external system:

- Why is it needed?
- What capabilities are required?
- What is the interface?
- What data enters and leaves?
- How is authentication handled?
- What limits apply?
- What happens when it is unavailable?
- How are external actions verified?

## 8. Failure investigation

For every operation:

- What can go wrong?
- How will failure be detected?
- What is the impact?
- Can it be retried?
- Can it be resumed?
- Could retrying cause duplication?
- When should it stop or escalate?
- How is recovery verified?

## 9. Security and governance

- What information is sensitive?
- Who can access it?
- Which actions need authorization?
- What external inputs are untrusted?
- How are secrets protected?
- What needs an audit trail?
- What legal or business policies apply?

## 10. Runtime and operations

- Where does the system run?
- What starts it?
- What schedules it?
- How is work distributed?
- What state survives restarts?
- What is monitored?
- How are deployments performed?
- How are backups and recovery handled?
- How is cost controlled?

## 11. Verification

- What does correct behaviour mean?
- What must be tested?
- What are the expected outputs?
- What edge cases must be covered?
- What metrics demonstrate success?
- How are regressions detected?
- How will production behaviour be monitored?

## 12. Engineering decisions

For each important decision:

- What requirement created the decision?
- What alternatives exist?
- What are their trade-offs?
- What evidence supports the recommendation?
- What is the simplest adequate solution?
- What could invalidate the decision?
- How will it be tested?

## 13. Unresolved questions

Maintain:

- Unknown requirements.
- Unverified assumptions.
- Missing evidence.
- Conflicting requirements.
- Open technical decisions.
- Risks requiring investigation.

Do not silently turn unknowns into assumptions.

## **6. Now, apply it to NuFlorist: don't investigate everything randomly**

Your 100+ agent questions are one part of a much bigger investigation.

I would organise NuFlorist into these connected investigation areas:

## **NuFlorist investigation map**

1. **Business and product discovery**

   Objective, ICP, acquisition economics, users, requirements and success metrics.
2. **Workflow and operational discovery**

   End-to-end business lifecycle, scenarios, triggers, schedules and state transitions.
3. **Domain and data discovery**

   Entities, relationships, identity, database, schema, ownership and data provenance.
4. **Component and agent discovery**

   Responsibilities, boundaries, agent count, deterministic services and decision rights.
5. **Harness and intelligence discovery**

   Context, tools, retrieval, memory, execution loops, autonomy and verification.
6. **Communication and orchestration discovery**

   Handoffs, contracts, queues, workflow engines, state and recovery.
7. **Integration and external dependency discovery**

   Search providers, email verification, Instantly, API contracts and provider constraints.
8. **Reliability and security discovery**

   Failures, duplicates, concurrency, permissions, privacy and auditability.
9. **Testing and evaluation discovery**

   Correctness, retrieval quality, agent trajectories, regression and business outcomes.
10. **Infrastructure and production discovery**

    Deployment, scaling, observability, cost, backups and operational ownership.

These are not ten separate projects. They are connected views of one system.

For example, deciding how to identify duplicate businesses affects:

- Domain modelling.
- Database constraints.
- Discovery-agent behaviour.
- Concurrent execution.
- Workflow orchestration.
- Testing.
- Monitoring.

A good discovery process follows these connections instead of completing one isolated checklist and forgetting the others.

## **7. The actual working method I recommend for you**

I want you to stop creating endless OneNote pages containing frameworks, thinking types and question lists.

Use this loop whenever you start a new investigation:

## **The engineering discovery loop**

1. **Choose one real scenario**

   Example: A florist is discovered.
2. **Walk through what must happen**

   Example: Extract its details, identify it and persist it.
3. **Generate questions using the triggers**

   Creation, identity, data, decisions, handoffs and failure.
4. **Investigate dependencies**

   What else must exist for this operation to work?
5. **Derive the engineering design**

   Components, schemas, contracts, state and implementation.
6. **Challenge the design**

   Simulate duplicates, missing data, crashes and concurrent execution.
7. **Produce and verify the artifact**

   Code, database migration, tests, diagrams or operational specification.
8. **Update the unresolved register**

   Record only the questions that genuinely remain unanswered.

Your working system should have only three living records:

1. **System Blueprint:** What we have established about the project.
2. **Engineering Decisions:** What we decided, why and what evidence supports it.
3. **Unresolved Register:** What we still need to discover or verify.

The question bank is a temporary investigation aid, not the final product.

## **8. The most important thing: what I want you to practise**

Don't practise remembering the eight-pass method.

Practise this ability:

**Take any statement about a system and turn it into the next layer of engineering questions.**

For example:

Someone says:

"We need an agent that finds florist owners."

You should immediately be able to investigate:

- What qualifies as an owner?
- How do we identify the business first?
- How do we associate a person with that business?
- What sources can establish the relationship?
- What happens if the sources disagree?
- How do we store the evidence?
- What should the agent return?
- How does the next component use the result?
- What happens if no owner is found?
- How do we know the agent is performing well?

That is the practical skill.

## **9. Let's test whether this approach works**

I don't want to give you another 200 questions and tell you to memorise them.

Let's start with one real NuFlorist scenario and use it to develop your discovery ability.

Practical engineering exercise

**Scenario**

A florist business has just been discovered by NuFlorist.

**Your task**

Before thinking about agents, databases or frameworks, write down what you believe must be investigated before this business can safely move to the next stage.

Review my engineering thinking

The objective is not to get the perfect answer. It is to develop the ability to discover what needs to be asked next, without needing someone to hand you the question bank.













        
