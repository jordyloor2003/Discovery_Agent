# Discovery Agent

> Convierte conocimiento de negocio crudo en artefactos de producto validables.
> Agente de [Claude Code](https://claude.ai/code) para la asignatura de Ingeniería de Software — Maestría en Software, UPS.

---

## Qué es

**Discovery Agent** estructura el proceso de descubrimiento de producto *antes* de escribir una sola línea de código.

Dado un conjunto de entrevistas en crudo, el agente extrae **personas**, **dolores**, **requisitos**, **user stories** y un **MVP Canvas**; luego convierte los supuestos más riesgosos en **hipótesis falsables** con experimentos baratos para validarlas.

El agente es **genérico**: no está atado a ningún dominio. Cada caso de negocio es un *discovery* independiente bajo `discoveries/`.

---

## Flujo de trabajo

```
Entrevistas en Markdown
         │
         ▼
/discovery:analyze       →  personas.md · requisitos.md · evidence-map.json
         │
         ▼
/discovery:generate-mvp  →  user-stories.md · mvp-canvas.md
         │
         ▼
/discovery:experiments   →  hypotheses.md · experiment-board.json
         │
         ▼
/discovery:report        →  report.html  (dashboard visual autocontenido)
```

---

## Estructura del repositorio

```
discovery-agent/
├── .claude/
│   ├── commands/discovery/     # Cuatro comandos: analyze · generate-mvp · experiments · report
│   ├── hooks/                  # readiness-gate.py · hypothesis-gate.py
│   ├── scripts/                # build-report.py (generador de HTML)
│   └── skills/discovery/       # Estándar de formato y trazabilidad
├── discoveries/
│   ├── _template/              # Plantilla vacía para nuevos casos
│   │   ├── interviews/
│   │   └── outputs/
│   └── citasalud/              # Discovery de ejemplo completo
│       ├── interviews/         # recepcionista.md · doctora.md · paciente.md
│       └── outputs/            # Todos los artefactos generados
└── CLAUDE.md                   # Reglas y flujo de trabajo del agente
```

---

## Requisitos previos

| Herramienta | Versión |
|---|---|
| [Claude Code](https://claude.ai/code) | latest |
| Python | 3.x |

---

## Uso rápido

```bash
# 1. Copia la plantilla para tu nuevo caso
cp -r discoveries/_template discoveries/mi-caso

# 2. Agrega entrevistas en discoveries/mi-caso/interviews/
#    Cada archivo debe tener frontmatter (rol_entrevistado, primera_persona, anonimizada)
```

Luego, dentro de Claude Code:

```
/discovery:analyze discoveries/mi-caso
/discovery:generate-mvp discoveries/mi-caso
/discovery:experiments discoveries/mi-caso
/discovery:report discoveries/mi-caso
```

Los artefactos se generan automáticamente en `discoveries/mi-caso/outputs/`.

---

## Artefactos generados

| Archivo | Comando | Contenido |
|---|---|---|
| `personas.md` | `:analyze` | Personas + stakeholders con diagrama Mermaid |
| `requisitos.md` | `:analyze` | Requisitos funcionales y no funcionales (R-NN) |
| `evidence-map.json` | `:analyze` | Mapa de trazabilidad entre entrevistas, personas y dolores |
| `user-stories.md` | `:generate-mvp` | User stories en formato INVEST con criterios de aceptación |
| `mvp-canvas.md` | `:generate-mvp` | Canvas de 7 bloques con flujo Output → Outcome → Impact |
| `hypotheses.md` | `:experiments` | Test cards ordenadas por nivel de riesgo |
| `experiment-board.json` | `:experiments` | Tablero de hipótesis legible por máquina |
| `report.html` | `:report` | Dashboard visual autocontenido, sin dependencias externas |

---

## Reglas de trabajo

| Regla | Descripción |
|---|---|
| **Cero invención** | Ningún artefacto puede afirmar algo que no esté respaldado por una entrevista real |
| **Trazabilidad** | Cada persona, dolor y requisito cita el archivo fuente (p. ej. `recepcionista.md`) |
| **Primera persona** | Una persona solo existe si hay una entrevista en primera persona de ese rol |
| **Aislamiento** | Los artefactos de un discovery nunca se mezclan con otro |
| **Idioma** | Español, salvo términos técnicos (user story, MVP, stakeholder) |

---

## Gates automáticos

Dos hooks de validación bloquean la escritura cuando la evidencia no es suficiente.

### Gate de readiness

Se activa antes de generar `mvp-canvas.md` o `user-stories.md`. Verifica que:

- Existe `evidence-map.json`
- Hay al menos 2 entrevistas
- Cada persona primaria tiene respaldo de primera mano
- No hay dolores huérfanos (sin fuente de entrevista)

### Gate de hipótesis

Se activa antes de generar `hypotheses.md` o `experiment-board.json`. Verifica que:

- Las hipótesis son falsables: tienen métrica, umbral numérico y regla de decisión
- El umbral contiene un número concreto (no "muchos" ni "la mayoría")
- La regla de decisión contempla el escenario de fallo
- La métrica no es de vanidad (descargas, likes, líneas de código, story points)

---

## Discovery de ejemplo

`discoveries/citasalud/` contiene un discovery completo de un sistema de citas médicas:
tres entrevistas en primera persona (recepcionista, doctora, paciente), nueve requisitos
trazados, seis user stories, cinco hipótesis falsables y un dashboard HTML generado.
Úsalo como referencia o como demostración del flujo completo.

---

## Proyecto académico

Unidad 1 de **Ingeniería de Software** — Maestría en Software, Universidad Politécnica Salesiana (UPS).