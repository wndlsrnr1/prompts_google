# Meeting Minutes MVP Implementation Plan

**Goal:** Build the MVP core for "Action-First Meeting Assistant" focusing on Brainstorming mode using Gemini 3.0 Pro.

**Architecture:** 
- **Backend:** Python/Node.js script to interact with Gemini API.
- **AI Model:** Gemini 3.0 Pro (via REST API) with JSON Schema enforcement.
- **Data Flow:** STT Transcript -> Pre-processor (Timestamp/Speaker) -> Gemini API -> Structured JSON -> UI/Export.

**Tech Stack:** Gemini API (v1beta), Python (or Node.js), JSON Schema.

---

### Task 1: Environment & API Setup
**Goal:** Verify Gemini 3.0 Pro access and basic connectivity.

**Files:**
- Create: `.env` (add GEMINI_API_KEY)
- Create: `src/config.py`

**Step 1: Check API Key**
Ensure `GEMINI_API_KEY` is present in environment.

**Step 2: Create Basic Client**
Implement a simple function to hit the `models/gemini-1.5-pro-latest` (or 3.0) endpoint.

**Step 3: Test Connectivity**
Run a "Hello World" prompt to confirm authentication works.

---

### Task 2: JSON Schema & Prompt Engineering
**Goal:** Implement the strict JSON schema designed during brainstorming.

**Files:**
- Create: `src/schemas/meeting_schema.json`
- Create: `src/prompts/brainstorming_prompt.py`

**Step 1: Define JSON Schema**
Write the full JSON schema (including `thinking_process`, `meeting_meta`, `brainstorming_items`, `dynamic_analysis`) into a separate file.

**Step 2: Implement Prompt Builder**
Create a function that injects the scheme into the API request body under `generation_config`.

**Step 3: Test Schema Validation**
Send a dummy transcript and verify the output is valid JSON and contains the `thinking_process` field.

---

### Task 3: STT Pre-processor Impl
**Goal:** Format raw transcript data into the optimal format for the AI.

**Files:**
- Create: `src/utils/stt_formatter.py`
- Create: `tests/test_stt_formatter.py`

**Step 1: Define Input Format**
Assume generic input or specific provider (e.g. "Speaker 1 [00:00:10]: Text").

**Step 2: Implement Transformer**
Write logic to convert input to: `[00:00:10] Speaker 1: Text`.

**Step 3: Verify Output**
Pass sample data and check the formatting string.

---

### Task 4: Dynamic Analysis Engine
**Goal:** Allow users to pass custom query fields at runtime.

**Files:**
- Modify: `src/prompts/brainstorming_prompt.py`

**Step 1: Update Prompt Logic**
Update the system prompt generation to accept a list of `custom_fields` (e.g. `["Budget", "Competitors"]`).

**Step 2: Inject into System Instruction**
Append the custom field definitions to the `system_instruction` text dynamically.

**Step 3: Test Dynamic Query**
Run a test asking for "Budget" issues and verify `dynamic_analysis` array in JSON response is populated correctly.

---

### Task 5: Integration Script (MVP Draft)
**Goal:** Stitch it all together into a runnable CLI script.

**Files:**
- Create: `run_analysis.py`

**Step 1: CLI Arguments**
Accept transcript file path and optional custom fields as args.

**Step 2: Orchestration**
Load Transcript -> Format -> Call API with Schema -> Save JSON.

**Step 3: End-to-End Test**
Run with the detailed sample transcript from the brainstorming session and validate the final JSON artifact.
