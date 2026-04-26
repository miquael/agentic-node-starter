# Data Schema & Structures

> Template guide — replace with your project's actual data models and API contracts. This file helps AI agents understand the data layer without reading code.

---

## How to Use This File

- Define each model with its fields, types, and constraints
- Note key relationships between models
- List API contracts that serve or consume these models
- Keep it current as your schema evolves — stale schema docs mislead agents

---

## Models

> Add one section per core data model. Example structure below.

### [ModelName]

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | `string` | yes | Unique identifier |
| `createdAt` | `Date` | yes | Creation timestamp |
| `updatedAt` | `Date` | yes | Last update timestamp |

### Relationships

> Describe how models relate to each other (one-to-many, many-to-many, etc.)

---

## API Contracts

> List your API routes and their purpose. Expand as needed.

| Route | Method | Description |
|---|---|---|
| `/api/v1/[resource]` | `GET` | Fetch all resources |
| `/api/v1/[resource]/:id` | `GET` | Fetch single resource |
| `/api/v1/[resource]` | `POST` | Create resource |
| `/api/v1/[resource]/:id` | `PUT` | Update resource |
| `/api/v1/[resource]/:id` | `DELETE` | Delete resource |
