---
layout: post
title: Assistant Kernel
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    HTTP daemon for state management and tools for Ollama
</div>
<!--excerpt-end-->

# Assistant Kernel
---
Codeberg Repo : [akernel](https://codeberg.org/efournierrobert/akernel/)

AI states: [Back to basics: Artificial intelligence and states](/2026/06/25/ai-states.html)

---

Assistant Kernel (akernel) is a daemon that adds state management, like conversations and system prompts, and tools support for Ollama. 

It exposes a documented HTTP API so any front end can implement AI interactions with it. It is written in Go and uses an SQLite database to be a minimal and resource efficient alternative to similar software.