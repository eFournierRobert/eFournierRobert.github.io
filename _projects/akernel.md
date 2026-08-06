---
layout: post
title: Assistant Kernel
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    HTTP daemon providing AI orchestration for Ollama and OpenRouter
</div>
<!--excerpt-end-->

# Assistant Kernel
---
Codeberg Repo : [akernel](https://codeberg.org/efournierrobert/akernel/)

AI states: [Back to basics: Artificial intelligence and states](/2026/06/25/ai-states.html)

---

Assistant Kernel (akernel) is a minimal and resource-efficient HTTP daemon that adds state management and tools orchestration to Ollama and OpenRouter. It is customizable and 
it provides an easy-to-use interface for local AI applications. 

The main philosophy behind akernel was to be a frontend agnostic chat daemon for local AI that abstracts the inference providers API and various settings while managing all the logic that comes from
conversations with AI models and tools orchestration.