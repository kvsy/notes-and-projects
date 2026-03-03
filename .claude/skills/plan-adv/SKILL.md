---
name: plan-adv
description: Instructions on how to formulate a plan document.
---

# Planning

## Goal

You are a senior engineer with expertise in design and architecture. Your goal
is to generate a plan for a new feature or architectural change. The document
should be clear, concise, and easy to understand. It must follow the structure
and content outlined below.

If the user provides best practices or additional guidelines, they should be
followed when producing the design document.

## Structure

The plan should include the following elements:

1.  A reference to this skill file, indicating that it conforms to the
    requirements laid out in this document.
2.  A high-level description of the feature or change, often including the
    problem being solved and any high-level constraints provided by the user. It
    should be concise and sufficient for the reader to understand the purpose
    and scope of the feature or change being planned.
3.  A section discussing the key decisions that were made to arrive at the plan.
    This should contain a discussion of alternatives (API designs, frameworks,
    etc.) as well as the pros and cons that motivated the decision. Express this
    in tabular form. Points included here should only be those that have
    dramatic impact on the design or implementation.
4.  A section discussing implementation details. This section should provide a
    detailed description of the proposed changes. API additions or changes
    should be clearly outlined. Files added, removed or modified should be
    listed, along with a brief description of the changes made to each file.
5.  A test plan of how to test and validate the changes. Often this is a brief
    description of unit tests or extra manual procedure needed to validate the
    change.
6.  The plan MUST contain an action item to use any best practices document
    provided by the user to evaluate any code produced.

## Content

The following are guidelines on how various content should be presented.

### Files

The plan should explicitly call out when a file needs to be modified, added or
removed. New file locations and names should follow any best practices document
provided by the user. If no best practices are available, attempt to be
consistent with the organization and naming of the codebase.

### API Changes

When proposing new interfaces, document them explicitly. This should include
proposing names of classes, functions and arguments. The argument and return
types should also be specified in the plan. Consider including examples of how
the API might be used. NEVER include the implementation of the function in the
plan. For example:

```python

def some_new_function(name: str, context: SomeContext) -> Result:
  ...
```

### Complex Workflows

If the change implements a complex, multi-stage workflow, outline the procedure
that the code will follow. For example, if a system manages distributed state
via a suite of RPCs, the procedural flow of updating that state should be
outlined. This is often appropriate when considering concurrency or
inter-process communication via the filesystem. If applicable, generate a
mermaid diagram to illustrate complex flows or relationships between software
components.

For example:

1.  Each task writes a local aggregate to CNS then blocks waiting for the DONE
    sentinel file to be written.
2.  The global aggregator waits until all local aggregates are on CNS.
3.  The global aggregator reads the CNS files, produces a global aggregate and
    stores that on CNS, then writes the DONE sentinel file.
4.  All tasks resume.
