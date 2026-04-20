# Entrance + TimeProfile Binding — Software Schematic

TypeScript application integrating the iLOQ S50 Management API.
Scope: **one-button window** that assigns an `Entrance` to a key/token,
**always bound to a `TimeProfile`**. Assignment without a TimeProfile
is not representable in the type system and rejected at runtime.

This document is **design-only**. No implementation code.

---

## 1. Component Layout

```
+-----------------------------------------------------------+
|                     Window (1-button UI)                  |
|                                                           |
|   [  Grant Entrance  ]   <- single action button          |
|                                                           |
|   status line: idle | working | ok | error                |
+--------------------------|--------------------------------+
                           |
                           v
+-----------------------------------------------------------+
|                   AssignmentController                    |
|   - onClick() -> buildAssignment() -> submit()            |
|   - guards: entrance chosen, timeProfile chosen           |
+--------------------------|--------------------------------+
                           |
                           v
+-----------------------------------------------------------+
|                   AssignmentService                       |
|   - assign(entrance, timeProfile): Promise<Result>        |
|   - enforces Entrance <-> TimeProfile pairing invariant   |
+--------------------------|--------------------------------+
                           |
                           v
+-----------------------------------------------------------+
|                      iLOQClient                           |
|   - login / session token                                 |
|   - getEntrances(), getTimeProfiles()                     |
|   - setEntrancesWithTimeProfiles(keyId, pairs[])          |
+--------------------------|--------------------------------+
                           |
                           v
                   iLOQ S50 Management API
```

---

## 2. Domain Model (types — declaration shape)

```
Entrance
  id:   EntranceId   (opaque string, iLOQ GUID)
  name: string
  realEstateId: string

TimeProfile
  id:   TimeProfileId (opaque string, iLOQ GUID)
  name: string
  slots: ReadonlyArray<TimeSlot>

# The only way to pair the two. No "Entrance without TimeProfile".
BoundEntrance
  entrance:    Entrance
  timeProfile: TimeProfile   # REQUIRED, non-nullable

AssignmentRequest
  keyId:  KeyId
  bound:  NonEmptyArray<BoundEntrance>
```

**Invariant (compile-time):** `BoundEntrance.timeProfile` is non-optional.
There is no constructor, factory, or code path that produces an
`Entrance` reaching `AssignmentService` without an accompanying
`TimeProfile`.

**Invariant (runtime):** `AssignmentService.assign` rejects any payload
whose `bound` array contains an element missing `timeProfile`, before
the iLOQ call is issued.

---

## 3. One-Button Window — UX Flow

```
 launch window
      |
      v
 fetch entrances + timeProfiles from iLOQ  (parallel)
      |
      v
 pre-select:
   - entrance    = configured default (or single available)
   - timeProfile = configured default (or single available)
      |
      v
 enable [Grant Entrance] button iff BOTH are selected
      |
      v
 user clicks button
      |
      v
 controller builds BoundEntrance { entrance, timeProfile }
      |
      v
 service.assign(...)  -> iLOQ API
      |
 +----+--------+
 |             |
 v             v
 ok          error
 status      status + retry enabled
```

Notes:
- The window has **one actionable control**: the button.
- Selections are resolved from config / sensible defaults, not user menus.
- Button is disabled until both sides of the pair are known.

---

## 4. iLOQ API Mapping

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

## 5. Failure Modes

| Case                                  | Handling                          |
|---------------------------------------|-----------------------------------|
| entrance list empty                   | button stays disabled, status err |
| timeProfile list empty                | button stays disabled, status err |
| auth / network failure                | status err, button re-enabled     |
| server rejects pairing                | status err with server message    |
| caller attempts bypass (no profile)   | type error at compile; throw at runtime |

---

## 6. What this schematic deliberately excludes

- Multi-select UI, grids, search.
- Entrance management without a time profile — not supported by design.
- Key creation, person management, hardware programming flows.
- Persistence beyond the in-memory session token.
