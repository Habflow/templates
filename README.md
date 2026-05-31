# templates

This repository contains the bundled workflow templates for HabboFlow.

---

## Directory structure

Templates are organised in **one level of category subdirectories**. Each subdirectory name is the category slug. Each YAML filename (without extension) is the template slug.

```
templates/
└── <category>/
    └── <slug>.yaml
```

The template `id` used by the system is `<category>/<slug>`.

**Example:**

```
templates/
└── room-management/
    └── greet-on-enter.yaml   →  id: "room-management/greet-on-enter"
```

---

## Metadata block

Every template YAML **must** include an `extensions.x-habflow.template` block with the following fields:

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | string | yes | Human-readable template name |
| `description` | string | yes | Short description shown in the template browser |
| `icon` | string | yes | [Tabler icon](https://tabler.io/icons) name (e.g. `door-open`) |
| `author.habboName` | string | yes | Habbo username of the template author |
| `author.habboHotel` | string | yes | Habbo hotel domain (e.g. `com`, `es`, `de`) |

The rest of the file must be a valid `.habflow` automation definition. The `extensions.x-habflow.template` block is stripped when the definition is loaded for use.

### Example

```yaml
dsl: "1.0.0"
namespace: room-management
name: greet-on-enter
version: "1.0.0"

trigger:
  type: manual

nodes:
  - id: write-greeting
    kind: habbo-write-variable
    config:
      kind: habbo-write-variable
      roomId: "{{roomId}}"
      variableName: lastGreeting
      value: "Welcome to the room!"
    next: []

extensions:
  x-habflow:
    template:
      title: Greet on Enter
      description: >
        Stores a welcome message in a room-scoped variable each time the
        automation runs.
      icon: door-open
      author:
        habboName: HabboFlow
        habboHotel: com
```

---

## Adding a template

1. Pick or create a category subdirectory (lowercase, hyphen-separated slug).
2. Create `<slug>.yaml` inside it.
3. Add a valid automation definition.
4. Add the `extensions.x-habflow.template` block with all required fields.
5. Verify: a missing `title` field causes the template to be silently skipped by the repository.
