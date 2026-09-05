# Breadth-First Map, Depth-First Explanation

## Purpose

Give the human a compact map of everything they need to understand before
deeply explaining a small number of nodes at a time.

This module controls the presentation lifecycle across turns. It does not limit
how much source the agent may inspect, how far a runtime path must be traced, or
whether an implementation task must be completed in the current turn.

## Inputs

- The human's question and demonstrated context.
- The goal-relevant mental model and source-backed path.
- Exact source identifiers, canonical document terms, and their locations.
- Dependencies and ordering relationships among candidate explanation nodes.
- Any explanation checkpoint from the previous turn.

## Terms

- **Breadth map**: a shallow inventory of the relevant nodes and their immediate
  relationships. It answers "what will I need to understand?"
- **Deep dive**: an end-to-end explanation of one selected node. It answers
  "how does this node actually work?"
- **Explanation node**: one source symbol, canonical term, component, contract,
  or complete plain-language actor-action relationship.

Breadth-first and depth-first describe explanation order only. They do not
authorize unsupported claims or replace source tracing.

## Node Identity

Classify every node before presenting it:

1. **Source identifier**: preserve the exact spelling and scope from code, such
   as `self.config_path`, `config_path`, or `load_config`.
2. **Canonical term**: preserve the exact name used by the source document or
   external system.
3. **Plain-language relationship**: write a complete clause naming who acts,
   what they act on, and what changes.
4. **Explanatory shorthand**: introduce it explicitly as "called X below" and
   never format it as though it were a source identifier.

When one value changes names across a call boundary, record the mapping instead
of silently treating the names as interchangeable:

```text
self.config_path
  -> passed as argument
load_config(config_path=...)
  -> referenced locally as
config_path
```

## Method

### 1. Build The Breadth Map

List the smallest complete set of goal-relevant nodes at one shallow level.
For each node record:

```text
ID:
Exact name or complete relationship:
Source location:
One-sentence responsibility:
Immediate parent or dependency:
Status: queued | active | explained | follow_up
```

Keep this pass shallow. Do not explain implementation details, nested helpers,
or full causal chains yet. Group obvious supporting helpers under their owning
node instead of presenting every function as a peer.

If the subject has three or fewer simple nodes, the map may be one sentence or
a compact list rather than a separate table.

### 2. Select The Active Nodes

Select no more than three nodes for deep explanation in one response unless the
human explicitly requests one exhaustive pass.

Choose nodes in this order:

1. nodes the human explicitly asked about;
2. prerequisites required to understand those nodes;
3. nodes that resolve a current contradiction or evidence gap;
4. remaining nodes in dependency order.

A follow-up question about an active node stays within that node. It does not
consume a queued node merely because the answer crosses another helper
function.

### 3. Explain Each Active Node Depth-First

Trace each active node as far as needed to reach its observable effect or
responsibility boundary:

```text
exact definition
  -> caller and concrete input
  -> internal decision or transformation
  -> callee and output
  -> observable effect
```

Depth is not capped. The three-node limit controls breadth per response, not
the number of source hops required to explain one node correctly.

At every source-dependent hop:

- preserve exact identifiers;
- show any identifier remapping;
- name the relationship using a verb such as calls, passes, reads, writes, or
  returns;
- place the source excerpt and precise location beside the claim;
- stop and mark an evidence gap if the edge cannot be supported.

Do not move to the next active node until the current node has been reconnected
to the breadth map and the human's question.

### 4. Produce A Turn Checkpoint

End an explanation turn with a compact visible checkpoint:

```text
Explained this turn:
Follow-up questions still open:
Remaining nodes:
Recommended next nodes:
```

Preserve node IDs and exact names across turns. New evidence may rename a
plain-language relationship, but source identifiers may change only when the
source itself proves a different scope or symbol.

When queued nodes remain, ask the human which node or recommended group to
continue with. Do not silently dump the remaining deep dives into the same
response.

## Explanation Ledger

Maintain this compact artifact:

```text
Goal:
Breadth map:
Active nodes (maximum three):
Identifier mappings:
Evidence per deep hop:
Explained nodes:
Follow-up nodes:
Remaining queue:
Recommended next group:
```

The ledger may be shown as a compact table or checkpoint. It must remain
recoverable from the conversation so the next turn can resume without
reconstructing the whole topic.

## Exceptions

- A one-node or otherwise simple question may skip a visible breadth map.
- An explicit request for a complete one-pass explanation may exceed three
  active nodes, but still starts with a breadth map and keeps exact identifiers.
- Debugging, implementation, and review work may inspect or modify any number
  of nodes internally; this module limits explanatory depth presented per turn,
  not task execution.

## Quality Gate

The module is complete for the current turn when:

1. the human can see the complete goal-relevant breadth map;
2. no more than three nodes received deep treatment unless explicitly allowed;
3. every source symbol is exact or its remapping is shown;
4. every retained deep hop has adjacent evidence or an explicit evidence gap;
5. each explained node returns to the overall map;
6. explained, follow-up, and remaining nodes are visible for the next turn.
