# Lab 4 WebSocket -- Project Report

## Description of Changes
### Tests

Completed the onChat test:

- Deleted the `@Disabled` annotation and wired a ComplexClient that connects to `ws://localhost:8080/eliza`.

- Used a range check `assertTrue(count in 3..6)` to tolerate minor timing variations.

- Added concrete assertions to identify a typical Eliza response: the initial greeting equals `"The doctor is in."` and at least one server response contains one of the following tokens (`feel`, `believe`, `enjoy`) and ends/contains a question mark.

### Documentation

Added inline comments in tests explaining:
- Why a snapshot of `list.size` is taken.

- Why checking an interval is preferred over `assertEquals`.

- Why the test assertions are structured as they are.

## Technical Decisions
- **Snapshot the list size:** Reading `list.size` multiple times in a concurrent environment risks race conditions. Assigning it to a local val gives a stable value for assertions and log messages.

- **Range-based assertion instead of exact equality:** The exact number of messages can vary slightly because of timing, network scheduling, or small differences in server behavior. Using a range makes the test robust to these realistic variations while still verifying expected behavior.

- **Use of `session.asyncRemote.sendText(...)`:** Asynchronous sending avoids blocking the `@OnMessage` thread and reduces the chance of synchronous I/O exceptions interfering with message processing.

## Learning Outcomes
- Gained practical experience testing WebSocket endpoints in a Spring Boot environment.

- Learned to write more resilient tests for non-deterministic systems: Why exact-count assertions may fail intermittently and how range checks improve reliability.

- Improved debugging skills by reading stack traces.

## AI Disclosure
### AI Tools Used
- ChatGPT

### AI-Assisted Work
- **Generated with AI assistance:**
    - Explanations on concurrency issues, why to snapshot `list.size`, and why range assertions are preferable here.

- **Percentage of AI-assisted vs. original work:**
    - Approximately 30% AI-assisted: explanations on the issues specified before.

    - Approximately 70% original: running tests locally, adding code to the project and final validation.

- **Modifications made to AI-generated code:**
    - Comments and some phrasing were adapted to reflect the specific project context.

### Original Work
- **Work done without AI assistance:**

    - Completed and ran tests locally to confirm functional behavior and to choose a robust assertion strategy.

    - Integrated final code into the repository, validated `BUILD SUCCESSFUL`, and ensured tests are stable under typical CI timing.

- **Understanding and learning process:**
    - How to design assertions that are tolerant and meaningful for asynchronous WebSocket interactions.