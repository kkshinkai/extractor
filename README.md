# Extractor

## Idea

An organization can be modeled as an accountability DAG. Each node performs work within its own responsibility boundary and submits its result upward for approval. AI follows the same structure: an Agent performs work, and a human approves it. Humans also follow this structure: a human performs work, and a higher-level human approves it.

The key is that responsibility is layered, but full detail is not. A CEO should not need to inspect product details. A product lead should not need to inspect code details. A programmer should not need to inspect the internal implementation details of lower-level Agents. Each node only needs enough context to judge the work directly beneath it.

Therefore, execution is not the essential part of the organization; approval and accountability are. If a task previously performed by a human can be reliably performed by an Agent and consistently approved by the same upstream reviewer, then the original human execution node is no longer structurally necessary.

The framework models four kinds of nodes:

1. Root Governors  
   Root Governors are the top nodes of the DAG. They are human nodes that cannot be terminated, distilled, or replaced by the system. Inside the system, they have no upstream dependency and do not need approval from anyone else. Even if they are subject to external constraints in the real world, those constraints are outside the system model.

2. Human Governors  
   Human Governors are human nodes that approve other humans, and may also approve Agents. They still report upward to higher-level human nodes. They are not immediately targeted as the first replacement layer, because their role includes responsibility over other human nodes.

3. Human Operators  
   Human Operators are the lowest layer of human nodes. They do not approve any other humans. They may approve Agent outputs, or they may simply perform concrete work themselves and submit the result upward. This is the first layer the framework tries to observe, extract, distill, replace, and eventually terminate.

4. Agent Executors  
   Agent Executors are the bottom execution layer. They perform concrete tasks, either directly or under the supervision of Human Operators. They submit outputs upward into the same approval structure as human work.

The framework begins by routing work through Human Operators and recording how they perform their jobs: their outputs, reports, decisions, corrections, response times, approval results, rejection reasons, and failure cases. From this evidence, the system extracts their working patterns and distills them into Agent-supported Skills.

The system then periodically tests whether an Agent equipped with the distilled Skill can replace a Human Operator. The Agent performs the same kind of work, submits the same kind of result, and waits for the same upstream approval. If the Agent repeatedly passes upstream review under the same responsibility boundary — for example, ten consecutive approvals — the system can execute the approved termination process for the Human Operator.

After a Human Operator is removed, the Human Governor above that operator no longer needs to manage that human node. The Governor is now primarily approving Agent work or lower-level automated outputs. Structurally, that Governor has been converted into a new Human Operator.

The framework repeats this process upward. It distills the newly converted Human Operator, validates whether an Agent can replace that role, terminates the human node after successful approval, and continues collapsing the DAG. Over time, all non-root human nodes become candidates for extraction, distillation, replacement, and termination.

The end state is a minimized organization: all replaceable execution and intermediate review layers have been absorbed by Agents, leaving only one or several Root Governors as the stable, non-removable accountability roots of the system.
