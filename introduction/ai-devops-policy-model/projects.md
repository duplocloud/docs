# Projects

A Project is the primary unit of planned work in DuploCloud. It brings together everything needed to take a goal from idea to completion — a spec, an implementation plan, and a series of tickets that the AI Engineer executes.

## Structure of a Project

Every Project consists of three building blocks:

**Spec** — A detailed description of what needs to be accomplished. The spec is drafted collaboratively with the AI Engineer and approved before any implementation begins. It captures requirements across areas such as infrastructure, CI/CD, workloads, observability, compliance, security, and cost.

**Plan** — A step-by-step implementation plan derived from the approved spec. The plan is broken down into discrete tasks, organized into stages, and approved before execution starts.

**Tickets** — The individual units of work that the AI Engineer executes. Each ticket corresponds to a task in the plan and tracks everything that happens during execution — commands run, decisions made, context carried forward.

## Stages and Parallel Execution

Tasks in a plan are grouped into stages. Each stage contains tickets that are independent of one another — they have no dependencies on other tickets within the same stage, which means all tickets in a stage can be executed in parallel. Stages are completed in sequence: the next stage begins once all tickets in the current stage are done.

This structure gives you both predictability (stages enforce order where it matters) and speed (parallelism within each stage).

## Scope

Projects can optionally define their own Scope as a subset of the assigned Engineer's Scope. If no custom Scope is set, the Project defaults to the Engineer's full Scope — controlling exactly which cloud environments, clusters, and resources the AI Engineer can access when executing work for that Project.

## Creating a Project

Projects are created from the DuploCloud platform UI. Once a project exists, you can take all subsequent actions — drafting the spec, writing the plan, and executing tickets — directly from your IDE or terminal using the DuploCloud plugin.
