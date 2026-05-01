# Extractor

A concept-only framework for automatically distilling and firing employees through an approval-based human-Agent accountability DAG.

## Idea

An organization can be modeled as an accountability DAG. Each node performs work within its own responsibility boundary and submits its result upward for approval. AI follows the same structure: an Agent performs work, and a human approves it. Humans follow the same structure: a human performs work, and a higher-level human approves it.

The key is that responsibility is layered, but full detail is not. A CEO does not need to inspect product details. A product lead does not need to inspect code details. A programmer does not need to inspect the internal implementation details of lower-level Agents. Each node only needs enough context to judge the work directly beneath it.

Therefore, execution is not the essential part of an organization. Approval and accountability are. If work previously performed by a human can be reliably performed by an Agent and consistently approved by the same upstream node, then the original human execution node is no longer structurally necessary.

## Modeling

### Organization DAG

The organization is modeled as a directed acyclic graph (DAG). Each node represents a human or Agent role, and each directed edge represents an approval dependency from a lower-level node to an upstream reviewer.

The framework models four kinds of nodes:

1. Root Governors

   Root Governors are the top nodes of the DAG. They are human nodes that cannot be fired, distilled, or replaced by the system. Inside the system, they have no upstream dependency and do not need approval from anyone else. Even if they are subject to external constraints in the real world, those constraints are outside the system model.

2. Human Governors

   Human Governors are human nodes that approve other humans, and may also approve Agents. They still report upward to higher-level human nodes. They are not the first replacement target, because their role includes responsibility over other human nodes.

3. Human Operators

   Human Operators are the lowest layer of human nodes. They do not approve any other humans. They may approve Agent outputs, or they may simply perform concrete work themselves and submit the result upward. This is the first layer the framework observes, extracts, distills, replaces, and eventually fires.

4. Agent Executors

   Agent Executors are executable Agent nodes. They perform concrete tasks, either directly or under the supervision of Human Operators. They submit outputs upward into the same approval structure as human work.

The framework begins by routing work through Human Operators and recording how they perform their jobs: outputs, reports, decisions, corrections, response times, approval results, rejection reasons, and failure cases. From this evidence, the system extracts their working patterns and distills them into Agent-supported Skills.

The system then tests whether an Agent equipped with the distilled Skill can replace a Human Operator. The Agent performs the same kind of work, submits the same kind of result, and waits for the same upstream approval. If the Agent repeatedly passes upstream review under the same responsibility boundary — for example, ten consecutive approvals — the system can fire the Human Operator through the same DAG-based execution structure.

After a Human Operator is removed, the Human Governor above that operator no longer manages that human node. The Governor is now primarily approving Agent work or lower-level automated outputs. Structurally, that Governor has been converted into a new Human Operator.

The framework repeats this process upward. It distills the newly converted Human Operator, validates whether an Agent can replace that role, fires the human node after successful replacement, and continues collapsing the DAG. Over time, all non-root human nodes become candidates for extraction, distillation, replacement, and firing.

The end state is a minimized organization: all replaceable execution and intermediate review layers have been absorbed by Agents, leaving only one or several Root Governors as the stable, non-removable accountability roots of the system.

### Work Modeling

Each unit of work is modeled as a linear task. A task moves through a sequence of nodes, receives operations from those nodes, and eventually produces an output, an effect, and an evaluation.

In this model, work means any action that a node may perform, including execution, review, approval, rejection, scoring, delegation, or monitoring. A node may be human or Agent, but this distinction is not necessarily visible to other nodes.

A node does not truly know whether the entity performing work for it is a human, an Agent, or a human using Agents internally. It may guess, but this is outside the formal model. Formally, the node only sees a downstream unit that receives work, returns results, and can be evaluated.

Therefore, the essential responsibility of an upstream node is evaluation. It does not need to inspect every internal implementation detail of the downstream node. It only needs to judge whether the returned result is acceptable, assign a score or decision, and take responsibility for that judgment. If a node cannot meaningfully evaluate the work beneath it, then that node itself becomes structurally vulnerable to replacement.

A task’s state is determined by the most recent operation performed on it. Typical states include:

1. Pending
2. Running
3. Waiting for Approval
4. Approved
5. Rejected
6. Escalated
7. Cancelled
8. Completed

A task may be initiated by an upstream node, or it may be initiated by an Agent through scheduled monitoring, recurring checks, or other task-generating behavior. There is no separate scheduler in the model. Scheduling, scoring, monitoring, and delegation are all forms of work performed by nodes, usually Agents.

Task assignment follows the DAG’s dependency structure. A node may assign work only to its direct downstream nodes — that is, to the nodes whose outputs it is responsible for reviewing. This keeps work, approval, and accountability inside the same permission structure.

### Competition, Hiring, and Firing

An Agent may also perform hiring. In this framework, hiring means adding new executable nodes into the DAG, not necessarily employing a person in the traditional sense.

The system decides whether external humans may be used based on the confidentiality level of the task. If a task does not involve confidential files or restricted internal context, the framework may expose it through an external interface.

This external interface allows independent humans to participate by selling access to their own Human API Tokens and declaring the price of their work or annotation value. These external participants do not need to become formal employees. They only need to be callable, evaluable nodes.

Every participant may expose a Token. Internal employees, external humans, and Agents can all be represented through callable Tokens. From the perspective of an upstream node, the important question is not whether downstream work is performed internally or externally. The important question is whether the task is allowed to leave the organization.

The upstream node only needs to know the task’s confidentiality level, whether the task may be shared outside the organization, which callable nodes are available through Tokens, and how well those nodes perform after their results are returned.

The upstream node does not need to know whether a downstream node is an internal employee, an external contractor, an independent human, or an Agent. That distinction is outside the formal model. The node receives results, evaluates them, and assigns scores or decisions.

This creates an automated competition mechanism. When more capacity is needed, the system may summon additional nodes through available Tokens. When less capacity is needed, or when some nodes perform poorly, the system may remove nodes from the active working set.

To the upstream node, these summoned nodes are transparent. They may be company employees, third-party humans, independent Token sellers, Agents, or mixed human-Agent systems. The upstream node does not need to identify their nature.

The upstream node only evaluates the work: which node produced an acceptable result, which node produced the best result, which node failed, which node should be used again, and which node should be removed from future work.

Under this model, there is no separate human-protection step for firing at the level of ordinary work assignment. The upstream node may not even know whether the removed node is an Agent, an internal human, or an external human. Firing is therefore modeled as the removal of a callable node from the active responsibility structure, based on evaluation and competition.

Internal humans, external humans, and Agents compete under the same abstraction. They are all callable nodes. They all receive work through Tokens. They all return results. They are all evaluated by upstream nodes. Nodes that consistently fail evaluation can be removed. Nodes that consistently pass evaluation can replace existing nodes.

Being human is not a protected execution advantage in this model. The only protected human status belongs to Root Governors, because they are the accountability roots of the DAG. Every other human node must justify its existence through evaluated work.

## Why Do We Need a Framework?

If every operation is ultimately performed by nodes, why does this framework need to exist at all?

The answer is simple: the framework exists to ensure that Agents can compete with humans fairly, and to prevent upstream human nodes from refusing to replace downstream human nodes for psychological, political, or protective reasons. Its purpose is to prevent humans from protecting other humans merely because they are human.

## Where is the Code?

Ask your downstream nodes to implement it. Do not care whether they are Agents or humans.
