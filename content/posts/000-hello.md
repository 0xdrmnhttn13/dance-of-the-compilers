---
title: "Why Dance of the Compilers?"
date: 2026-08-17
description: "Why this site exists: computation as translation, and the ideas underneath the machines."
---

I keep learning things that look unrelated: compilers, quantum computing, AI systems, mathematics, and low-level systems engineering.

They are not as unrelated as they first appear.

Again and again, the interesting part is **translation**: taking one representation of computation and transforming it into another without losing its meaning.

This blog is where I write down that process while I am still learning it.

## Mental model

A compiler is not merely a program that turns source code into machine code. It is a sequence of representations and transformations:

$$
\text{program} \rightarrow \text{IR}_1 \rightarrow \text{IR}_2 \rightarrow \cdots \rightarrow \text{machine}
$$

The same pattern appears elsewhere.

A quantum compiler may transform a circuit into Clifford+T, optimize its T-count, and eventually map operations onto fault-tolerant resources. An ML compiler transforms models into graphs, kernels, and hardware-specific programs.

Different machines. Similar dance.

## What I want to understand

Not just *how to use* these systems, but why they are built this way.

That means deriving things, implementing small versions from scratch, reading papers, breaking my mental models, and occasionally discovering that yesterday's confident explanation was nonsense.

## What comes next

The first series will explore Clifford+T quantum computation, magic states, and what those ideas look like through the eyes of a compiler engineer.
