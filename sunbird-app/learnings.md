# Project Learnings

## 1) Validation Strategy and Trust Boundaries
- Apply strict runtime validation at system edges where untrusted input enters.
- Avoid repeating heavy validation internally when data already crossed a trusted boundary.
- Re-validate whenever data crosses into a new independent system.

## 2) Choosing Between `TypedDict`, `dataclass`, and Runtime Schemas
### `TypedDict` (best for transport payloads)
- Good for static/editor-time checks of dictionary shape.
- Lightweight and low-friction for DTO-style data passed across layers.
- Does **not** enforce structure at runtime.

### Runtime validation (for external boundaries)
- Use runtime schema tools (e.g., Pydantic) when exchanging data with external systems.
- Runtime checks are necessary when correctness and explicit failures are required in production.

### `dataclass` (best for evolving domain objects)
- Better when objects represent domain concepts rather than raw payloads.
- Improves readability (`obj.field` vs `dict["field"]`) and maintainability in multi-step transformations.
- Useful when behavior, invariants, or helper methods are likely to be added over time.

### Practical decision rule
- Transport-only payload: prefer `TypedDict`.
- Data with behavior/lifecycle: prefer `dataclass`.
- External contracts: add runtime schema validation.

## 3) Performance Prioritization
- Optimize the slowest stage first to improve end-user experience meaningfully.
- In this pipeline, Text-to-Speech (TTS) was the dominant bottleneck, so optimization effort should focus there before smaller stages like summarization.

## 4) Streaming Reality with the Current Sunbird APIs
- Current Sunbird endpoints used in this project are request/response REST calls, not token-streaming APIs.
- Because the server returns final results only, true partial hypothesis streaming for translation/summarization is not available from the client side.
- TTS returns an `audio_url` after synthesis completes, so generation-time audio streaming is not possible before that URL exists.

## 5) UX Improvements That *Are* Feasible
- Step-level progress updates are viable (show completion of each pipeline stage as it finishes).
- “Fake typing” for text output is viable after full text is received (e.g., stream words progressively in the UI for better perceived responsiveness).

## 6) Lightweight Implementation Insight
- Parsing audio directly in memory (`wave.open(io.BytesIO(audio_bytes))`) is an effective approach under tight runtime constraints.
- This avoids temporary disk writes and heavy dependencies (such as ffmpeg) for simple processing needs.
