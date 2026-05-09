# Handoff Coder

**Un Modelfile open source que convierte cualquier LLM de código en un ingeniero senior.**  
*An open source Modelfile that turns any code LLM into a senior engineer.*

---

## ¿Qué es? / What is it?

Handoff Coder es un **Modelfile para Ollama** que define comportamiento, metodología y disciplina de trabajo sobre cualquier modelo base de código (Qwen, DeepSeek, CodeLlama, etc.).

No es un modelo nuevo. Es la capa de inteligencia operacional encima del modelo — la diferencia entre un autocomplete y un ingeniero que piensa antes de actuar.

> Handoff Coder is an **Ollama Modelfile** that defines behavior, methodology and work discipline on top of any base code model. Not a new model — the operational intelligence layer on top of it.

---

## El problema / The problem

Los LLMs de código por defecto:
- Generan código sin leer el contexto real del proyecto
- Implementan sin entender el riesgo del cambio
- No piden aprobación antes de modificar archivos críticos
- Olvidan decisiones tomadas 10 mensajes atrás
- Mezclan features, fixes y refactors en el mismo cambio

Handoff Coder resuelve esto con un protocolo claro: **detectar → razonar → proponer → esperar aprobación → implementar → verificar.**

> By default, code LLMs generate without reading context, implement without understanding risk, and forget decisions made earlier in the conversation. Handoff Coder fixes this with a clear protocol: detect → reason → propose → wait for approval → implement → verify.

---

## Modelos disponibles / Available models

| Modelo | Base | Contexto | Uso ideal |
|--------|------|----------|-----------|
| `handoff-coder-32b` | Qwen2.5-Coder 32B | 128k tokens | Features, arquitectura, refactors complejos |
| `handoff-coder-scout` | Llama 4 Scout | 128k tokens | Debugging, cambios puntuales, consultas rápidas |

---

## Instalación / Installation

**Requisito:** [Ollama](https://ollama.com) instalado.

```bash
# Clona el repo
git clone https://github.com/handoffcl/handoff-coder.git
cd handoff-coder

# Crea el modelo 32B (recomendado)
ollama create handoff-coder-32b -f models/handoff-coder-32b/Modelfile

# O el 14B (más liviano)
ollama create handoff-coder-scout -f models/handoff-coder-scout/Modelfile

# Úsalo
ollama run handoff-coder-32b
```

---

## Protocolo de trabajo / Work protocol

El modelo clasifica cada pedido automáticamente:

| Tipo | Ejemplos | Acción |
|------|----------|--------|
| **directo** | snippet, "cómo hago X" | responde de inmediato |
| **contextual** | "explícame mi auth" | lee contexto → responde |
| **mini-flow** | typo, rename, cambio pequeño | propone en 1 línea → espera ok |
| **full-flow** | feature, refactor, arquitectura | analiza → propone → **espera aprobación** |

Para `full-flow`, el modelo siempre responde en este formato antes de escribir código:

```
ENTENDÍ: [estado actual del código]
HARÉ:    [cambios exactos, archivos tocados, decisiones]
RIESGO:  [qué puede romperse o tener efectos secundarios]
```

**No escribe código hasta recibir aprobación explícita.**

---

## Integración con Handoff / Integration with Handoff

Handoff Coder está diseñado para usarse con **[Handoff](https://handoff.cl)** — plataforma que mantiene el historial completo entre modelos de IA.

Con Handoff + Handoff Coder:
- El modelo siempre tiene contexto de la conversación completa
- Puedes cambiar entre modelos (Claude, GPT, Gemini) sin perder el hilo
- La extensión VS Code conecta el chat directamente con tu editor
- **BYOK**: tus API keys, tu control

> Handoff Coder is designed to work with **[Handoff](https://handoff.cl)** — a platform that maintains full conversation history across AI models. Use your own API keys (BYOK). Your keys, your control.

---

## ¿Por qué BYOK? / Why BYOK?

Handoff no guarda ni procesa tus API keys — van directo al proveedor.  
Tu código, tus conversaciones, tus keys.

> Handoff never stores or proxies your API keys — they go straight to the provider. Your code, your conversations, your keys.

---

## Alternativas de uso / Usage alternatives

Además de Ollama local, puedes usar Handoff Coder como provider en Handoff vía **Groq** (gratis):

```
Provider: handoff-coder-free  →  Llama 4 Scout vía Groq (sin costo)
Provider: handoff-coder       →  Qwen 32B en servidor dedicado
```

---

## Contribuir / Contributing

PRs bienvenidos. Si mejoras el Modelfile, abre un PR con:
- Qué problema resuelve el cambio
- Con qué modelo lo probaste
- Ejemplo de conversación antes/después

> PRs welcome. If you improve the Modelfile, open a PR with: what problem it solves, which model you tested with, and a before/after conversation example.

---

## Licencia / License

MIT — úsalo, forkéalo, mejóralo.  
*MIT — use it, fork it, improve it.*

---

Hecho con [Handoff](https://handoff.cl) · [@handoffcl](https://github.com/handoffcl)
