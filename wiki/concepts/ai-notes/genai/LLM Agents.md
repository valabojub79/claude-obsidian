---
type: concept
title: "LLM Agents"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - agents
complexity: intermediate
domain: generative-ai
status: developing
address: c-000331
related:
  - "[[LangChain]]"
  - "[[Large Language Models]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/Agents/Agents.md]]"
---

# LLM Agents

LLM-driven systems that plan, call **tools** and take multi-step actions toward a goal. From [[ai-notes|AI-Notes]] (CrewAI tutorials; "18 Months of Building Autonomous AI Agents in 42 Minutes").

## Frameworks mentioned

- **CrewAI**: role-based "crews" of agents with tools and tasks (`pip install crewai 'crewai[tools]'`).
- **LangGraph**: graph-structured, stateful agent workflows (from the [[LangChain]] team).
- **AutoGen** (Microsoft): multi-agent conversations.

## The author's project idea: a research-writing assistant

Features listed: research-paper reference tapping, Harvard-style citation formatting, author info finder, comparison and similarity analysis across papers, a "humanizer", about 10 templates, format-specific embedding of content.

## Ancestors in the paper notes

Text-action RL agents ([[Deep Reinforcement Learning with a Natural Language Action Space]]) and web navigation ([[WebNav - A New Large-Scale Task for Natural Language Based Sequential Decision Making]]) prefigure today's browsing and tool-using agents.
