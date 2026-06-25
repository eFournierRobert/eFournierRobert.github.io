---
layout: post
title: Assistant Kernel
excerpt_separator: <!--excerpt-end-->
---

<div class="muted">
    A minimal, resource-efficient HTTP daemon that adds state management and tools to Ollama written in Go.
</div>
<!--excerpt-end-->

# Assistant Kernel
---
Codeberg Repo : [akernel](https://codeberg.org/efournierrobert/akernel/)

---

## Key Features
- **Persistence**: Persistent chat history with SQLite
- **Tool integration**: Ability to create and provide tools to the model
- **System prompt support**: loaded from `$XDG_CONFIG_HOME/akernel/system.md`
- **Lightweight** : Optimized to be a local daemon with minimal resource usage
- **Frontend agnostic**: Fully documented OpenAPI spec for easy usage.

## Quick Start
**Ensure [Ollama](https://ollama.com/) is installed and running.**

```bash
# clone and run
git clone https://codeberg.org/efournierrobert/akernel.git
go build -o akernel cmd/main.go
./akernel
```

## Example usage
```bash
# Start a new conversation using conversationId: -1
curl -X POST http://localhost:50500/chat -d '{"model": "gemma4:31b-it-qat", "message": "Could you tell me what is 2 + 2?", "conversationId": -1}'

# Response: [
# {
#   "role":"assistant",
#   "conversationId":6,
#   "message":"2 + 2 = 4",
#   "thinking":"The user is asking a simple arithmetic question:...",
#   "conversationTokenCount":178
#  }
# ]  
```

## Documentation
- Full API specification is available at `openapi/doc.yaml`
- Reference CLI implementation can be found in `example/acli.go`