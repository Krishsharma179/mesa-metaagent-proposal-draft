# mesa-geo-proposal-draft
Documentation and draft for my GSoC 2026 proposal: Refactoring Mesa meta agent.This Includes technical research, proposal drafts, and system design diagrams.

# Mesa-Geo GSoC 2026 Proposal: Meta-agent Refactor

> **Applicant:** Krish Sharma  
> **Organization:** Mesa/Mesa-meta-agent   
> **Program:** Google Summer of Code 2026  
> **Status:** 🟡 Research & Draft Phase


## Overall Project goal
1.Implement a hypergraph-based backend using incidence tensors to track meta-agent membership, supporting overlapping memberships and nested hierarchies with sparse matrix optimization for large-scale simulations.
2.Introduce a configurable façade API that allows users to define diverse group behaviors (hierarchical, emergent, hybrid) through simple parameters like join_rule, leave_rule, exclusivity, and authority, eliminating the need for hardcoded group classes.
3.Build a bidirectional influence system enabling top-down (group→agent) and bottom-up (agent→group) state propagation with configurable aggregation methods (sum, mean, max, custom) and conflict resolution for multi-membership scenarios.
4.Integrate seamlessly with Mesa's existing architecture, ensuring compatibility with AgentSet, schedulers, and data collection, while providing comprehensive documentation, example models (military hierarchy, alliance formation), and benchmark tests.


## My understanding till now 

## 🎯 Project Overview

I understood the meta-agent.py it includes the the create of the meta agent add the meta agent and deleting the meta agent 

overall its is just a base architecture and the main goal of the project is to build upon the meta agent


## Relevant links 

Discussion links :https://github.com/mesa/mesa/discussions/3403

code link:https://github.com/mesa/mesa/tree/main/mesa/experimental/meta_agents

alliance formation:https://github.com/mesa/mesa/tree/main/mesa/examples/advanced/alliance_formation


## My contributions:

Pr:fix: use weakref in EventGenerator to prevent memory leak:https://github.com/mesa/mesa/pull/3360 status=Merged

PR:fix: prevent time rewind in _advance_time by adding early return:
https://github.com/mesa/mesa/pull/3329 status=Merged

Opened Issue:Adding rasie value error in DiscreteSpace.add_cell() on duplicate coordinates:
https://github.com/mesa/mesa/issues/3469

Pr:Fix duplicate coordinate validation:
https://github.com/mesa/mesa/pull/3473 status:Merged 

Buit a hierarchy model in order to understand the meta agent limitation 
link:https://github.com/Krishsharma179/GSoC-learning-space

## 💬 Get in Touch

I welcome feedback and collaboration! Feel free to:
- Open an issue in this repo for proposal questions
- Comment on Mesa-Geo discussions to coordinate efforts
- Reach out via Mesa community channels (Matrix)

---
*Last updated: March 2026*  
*This is a living document — check back for updates!*