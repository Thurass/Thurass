# Entrance + TimeProfile Binding — Software Schematic

TypeScript application integrating the iLOQ S50 Management API.
Scope: **one-button window** that assigns an `Entrance` to a key/token,
**always bound to a `TimeProfile`**. Assignment without a TimeProfile
is not representable in the type system and rejected at runtime.

This document is **design-only**. No implementation code.
Diagrams are written in GitHub-flavored Mermaid (```mermaid fenced blocks).

---

## 1. Component Layout

```mermaid
flowchart TB
    UI["Window (1-button UI)<br/>[ Grant Entrance ]<br/>status: idle | working | ok | error"]
    CTRL["AssignmentController<br/>onClick · guards"]
    SVC["AssignmentService<br/>assign(entrance, timeProfile)<br/>enforces pairing invariant"]
    CLIENT["iLOQClient<br/>login · getEntrances<br/>getTimeProfiles · setPairs"]
    API[("iLOQ S50<br/>Management API")]

    UI -->|click| CTRL
    CTRL --> SVC
    SVC --> CLIENT
    CLIENT <-->|HTTPS| API

    classDef ui fill:#e3f2fd,stroke:#1565c0;
    classDef logic fill:#fff3e0,stroke:#e65100;
    classDef ext fill:#ede7f6,stroke:#4527a0;
    class UI ui;
    class CTRL,SVC,CLIENT logic;
    class API ext;
```

---

## 2. Domain Model

```mermaid
classDiagram
    direction LR
    class Entrance {
      +EntranceId id
      +string name
      +string realEstateId
    }
    class TimeProfile {
      +TimeProfileId id
      +string name
      +TimeSlot[] slots
    }
    class BoundEntrance {
      +Entrance entrance
      +TimeProfile timeProfile
    }
    class AssignmentRequest {
      +KeyId keyId
      +BoundEntrance[] bound
    }
    BoundEntrance --> Entrance : required
    BoundEntrance --> TimeProfile : required
    AssignmentRequest "1" --> "many" BoundEntrance
```

**Invariant (compile-time):** `BoundEntrance.timeProfile` is declared
non-optional. No constructor, factory, or code path produces a
`BoundEntrance` without an accompanying `TimeProfile`.

**Invariant (runtime):** `AssignmentService.assign` rejects any payload
whose `bound` array contains an item missing `timeProfile`, before the
iLOQ call is issued.

---

## 3. One-Button Window — UX Flow

```mermaid
flowchart TD
    A([Launch window]) --> B[Fetch entrances + timeProfiles<br/>in parallel]
    B --> C{Both lists<br/>non-empty?}
    C -- no --> X[Status: error<br/>button disabled]
    C -- yes --> D[Resolve defaults:<br/>entrance, timeProfile]
    D --> E{Both selected?}
    E -- no --> X
    E -- yes --> F[[Enable button]]
    F --> G((User clicks<br/>Grant Entrance))
    G --> H[Build BoundEntrance<br/>entrance + timeProfile]
    H --> I[service.assign]
    I --> J{API result}
    J -- ok --> K[Status: ok]
    J -- error --> L[Status: error<br/>re-enable button]
    L --> F

    classDef bad fill:#ffebee,stroke:#c62828;
    classDef good fill:#e8f5e9,stroke:#2e7d32;
    classDef act fill:#fff8e1,stroke:#f9a825;
    class X,L bad;
    class K good;
    class G act;
```

Notes:
- The window has **one actionable control**: the button.
- Selections are resolved from config / sensible defaults, not user menus.
- Button is disabled until both sides of the pair are known.

---

## 4. Assignment Sequence (iLOQ API)

```mermaid
sequenceDiagram
    actor U as User
    participant W as Window
    participant C as AssignmentController
    participant S as AssignmentService
    participant I as iLOQClient
    participant API as iLOQ API

    W->>I: login()
    I->>API: POST /CreateSession
    API-->>I: sessionToken

    par fetch pair sources
        W->>I: getEntrances()
        I->>API: GET /Entrances
        API-->>I: Entrance[]
    and
        W->>I: getTimeProfiles()
        I->>API: GET /TimeProfiles
        API-->>I: TimeProfile[]
    end

    I-->>W: lists ready
    W->>W: enable button

    U->>W: click "Grant Entrance"
    W->>C: onClick()
    C->>C: build BoundEntrance<br/>(entrance, timeProfile)
    C->>S: assign(request)

    alt timeProfile missing
        S-->>C: reject (invariant)
        C-->>W: status: error
    else valid pair
        S->>I: setEntrancesWithTimeProfiles(keyId, pairs)
        I->>API: POST /Keys/{id}/SecurityAccesses
        API-->>I: 200 OK
        I-->>S: ok
        S-->>C: ok
        C-->>W: status: ok
    end
```

---

## 5. Button State Machine

```mermaid
stateDiagram-v2
    [*] --> Loading
    Loading --> Ready: entrances + timeProfiles loaded
    Loading --> Error: fetch failed / empty list
    Ready --> Working: click
    Working --> Ok: API 200
    Working --> Error: API failure / invariant violation
    Ok --> Ready: reset
    Error --> Loading: retry
    Ready --> Ready: selection unchanged
```

---

## 6. iLOQ API Mapping

| Domain op                | iLOQ endpoint (conceptual)                       |
|--------------------------|--------------------------------------------------|
| authenticate             | `POST /api/v2/CreateSession`                     |
| list entrances           | `GET  /api/v2/Entrances`                         |
| list time profiles       | `GET  /api/v2/TimeProfiles`                      |
| assign paired to a key   | `POST /api/v2/Keys/{keyId}/SecurityAccesses`     |

Each payload item sent to `SecurityAccesses` must carry both
`EntranceId` and `TimeProfileId`. The client refuses to serialize an
item that lacks either.

---

## 7. Failure Modes

| Case                                  | Handling                                |
|---------------------------------------|-----------------------------------------|
| entrance list empty                   | button stays disabled, status err       |
| timeProfile list empty                | button stays disabled, status err       |
| auth / network failure                | status err, button re-enabled           |
| server rejects pairing                | status err with server message          |
| caller attempts bypass (no profile)   | type error at compile; throw at runtime |

---

## 8. What this schematic deliberately excludes

- Multi-select UI, grids, search.
- Entrance management without a time profile — not supported by design.
- Key creation, person management, hardware programming flows.
- Persistence beyond the in-memory session token.
