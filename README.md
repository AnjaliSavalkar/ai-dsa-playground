# AI-DSA-Playground: Internship Project

This repository contains three project tracks for six students (three teams of two). Each track combines classic data structures and algorithms with modern, AI-flavored applications, using only CPU-friendly tools and Python.

Each team builds:

- A clean, testable backend (FastAPI, Python).
- A simple but usable frontend (Streamlit).
- A small “intelligent” layer (light ML-style logic, no heavy model training).
- Proper engineering workflow (Git, tests, linting, pull requests).

All teams must use Git actively, committing after completing each meaningful function or feature, and later forking and opening a pull request to the mentor’s repo.

***

## 1. Learning Goals (For All Teams)

By working through these tasks, you will learn:

- **Practical DSA application**  
  How arrays, hash maps, heaps, queues, graphs, sliding windows, and greedy algorithms power real systems (recommenders, schedulers, monitors) rather than just solving isolated LeetCode questions.

- **Backend and API design**  
  How to structure a FastAPI service with clear endpoints, request/response models, and separation between business logic and I/O.

- **Frontend development with Python**  
  How to build a usable, interactive UI using Streamlit that talks to your backend APIs.

- **Lightweight “AI touch” without GPUs**  
  How to add intelligence using:
  - Rule-based logic,
  - Simple statistical/ML-style updates (moving averages, difficulty adjustment),
  - TF-IDF or other CPU-friendly text vectorization.

- **Software craftsmanship**  
  - Writing unit tests (pytest) for core logic.
  - Handling exceptions gracefully and logging important events.
  - Using linters/formatters (Black, isort, Flake8/ruff).
  - Organizing code into modules and layers.

- **Git and collaboration**  
  - Working in small teams with branches and frequent commits.
  - Writing meaningful commit messages.
  - Forking the main repo and submitting pull requests.

### Real-life analogy

Think of each project as a **mini product team in a startup**:

- Team A builds the **“search and discovery”** feature, like the recommendation section of LeetCode, Netflix, or YouTube.
- Team B builds the **“personalized learning planner”**, similar to how Duolingo or Coursera picks what you should practice next.
- Team C builds the **“observability and monitoring dashboard”**, like internal tools used at companies to watch API health and detect abuse.

You are not just “solving coding problems”; you are building small versions of real systems used in AI-powered products today.

***

## 2. Common Technical Constraints & Expectations

- **Language & stack**
  - Python 3.x
  - FastAPI backend
  - Streamlit frontend
  - CPU-only laptops (no GPU, no heavy model training)

- **Architecture**
  - Core logic (algorithms & data structures) must live in separate modules, written as pure functions/classes (no direct I/O), making them easy to test.
  - FastAPI routes use the core logic but do not contain it.
  - Streamlit app calls the FastAPI APIs (local or via HTTP).

- **Quality requirements**
  - Unit tests with `pytest` for core logic.
  - Structured exception handling (no raw stack traces to users).
  - Logging using Python’s `logging` module.
  - Linting/formatting tools: Black, isort, and Flake8 (or ruff).
  - Basic type hints for functions and data models where reasonable.

- **Git workflow**
  - Each team maintains its own forked repo.
  - Commit **after each function or meaningful feature**:
    - Example: after implementing `compute_similarity`, after adding `/recommend` route, after adding a Streamlit page section, etc.
  - Use feature branches if possible (`feature/recommender`, `feature/scheduler`, etc.).
  - When done, open a **pull request** to the mentor’s main repo.

***

## 3. Team A – Smart Problem Recommender & Pattern Explainer

**Title:** LeetCode Problem Recommender with Pattern Hints

### Problem statement

You are building a helper tool for coding interview preparation. When a user inputs a LeetCode problem title or short description, your system should:

1. Suggest similar problems.
2. Highlight common patterns (e.g., “two pointers”, “sliding window”, “binary search”, “BFS/DFS”).
3. Provide a short explanation for why each problem was recommended.

### What you will learn (Team A)

- **Data structures & algorithms**
  - String processing and tokenization.
  - Use of hash maps (dictionaries) for frequency counts.
  - Similarity search using vectors (cosine similarity).
- **Light “AI” without training**
  - TF-IDF vectorization (e.g., scikit-learn) on CPU.
  - Rule-based pattern classification using keyword rules.

**Real-life analogy:**  
You are building a small version of the “People also watched…” or “Related problems” section on platforms like LeetCode, Netflix, or YouTube. When you click on one video/problem, the system finds similar items using efficient search over text and metadata.

### Functional requirements

- **Data ingestion**
  - Collect a small set of LeetCode-like problems:
    - Title
    - Short description
    - Tags/topics
    - Difficulty level
  - You may scrape a small subset (respecting website terms) or manually curate a JSON/CSV file.

- **Core logic (Python)**
  - Preprocess text:
    - Lowercase, remove punctuation, tokenize.
  - Vectorize:
    - Use bag-of-words or TF-IDF to convert descriptions into vectors.
  - Compute similarity:
    - Implement cosine similarity to find top‑k similar problems given a query.
  - Pattern mapping:
    - Use keyword rules to infer patterns:
      - Examples: “subarray”, “window” → sliding window; “two pointers” → two pointers; “BFS”, “queue” → BFS.

- **Backend (FastAPI)**
  - Endpoint `/recommend`:
    - Input: JSON with `query` (text), optional `k` (number of results).
    - Output: list of recommended problems, each with:
      - Title, difficulty, inferred patterns, similarity score, brief “why” explanation.

- **Frontend (Streamlit)**
  - Text input for the user’s query.
  - Button to “Get recommendations”.
  - Display:
    - Recommended problems in a list or table.
    - Patterns as tags/badges.
    - A one-line explanation: e.g., “Shares sliding window and hash map pattern with your query.”
  - Basic UX:
    - Show loading indicators, handle empty results gracefully.

- **Engineering practices**
  - Unit tests:
    - For text preprocessing, similarity computation, and pattern mapping.
  - Exception handling:
    - Handle empty queries, missing data files, invalid inputs.
  - Logging:
    - Log received queries and number of recommendations returned.
  - Linting & formatting:
    - Configure Black, isort, and Flake8/ruff.
  - Documentation:
    - `README` section explaining how to run the backend and frontend.

***

## 4. Team B – Personalized Practice Planner with Difficulty Adaptation

**Title:** AI-Flavored Practice Scheduler for LeetCode Problems

### Problem statement

You are building a practice planner that creates a daily LeetCode study plan for a user. The system should:

1. Generate a list of problems that fit within a daily time budget.
2. Balance topics (arrays, trees, DP, graphs, etc.).
3. Adapt problem difficulty over time based on user feedback (“too easy”, “too hard”, “just right”).

No heavy AI models; just smart use of data structures, algorithms, and simple adaptation rules.

### What you will learn (Team B)

- **Data structures & algorithms**
  - Priority queues (heaps) for problem selection.
  - Greedy scheduling under constraints (time budget, topic diversity).
  - Map-based tracking of topics and difficulties.
- **Light “AI” adaptation**
  - Simple difficulty update rules, like:
    - Adjusting difficulty score using feedback.
    - Maintaining a moving average of perceived difficulty.

**Real-life analogy:**  
You are building a mini version of a **personalized learning engine** like Duolingo or LeetCode Premium, which picks the next set of tasks for a user based on their performance and limited available time.

### Functional requirements

- **Data model**
  - Each problem has:
    - ID, title, topic(s), estimated duration (minutes), base difficulty (1–10).

- **Core scheduling logic**
  - Inputs:
    - Daily time budget.
    - Target difficulty range (e.g., 3–7).
  - Use:
    - A priority queue (heap) prioritizing problems that best match difficulty and underrepresented topics.
    - A greedy algorithm to fill the time budget.
  - Topic balancing:
    - Track how many problems of each topic are selected; penalize overrepresented topics to maintain variety.

- **Difficulty adaptation**
  - After a session, user gives feedback for each problem:
    - `too_easy`, `too_hard`, or `just_right`.
  - Update difficulty scores:
    - For example, +1 for `too_easy`, –1 for `too_hard`, minimal change for `just_right` (or a weighted average based on historic feedback).
  - Store updated scores in a simple JSON/SQLite store.

- **Backend (FastAPI)**
  - `/generate_plan`:
    - Input: time budget, difficulty range.
    - Output: list of selected problems with their topic, difficulty, estimated time.
  - `/feedback`:
    - Input: list of `{problem_id, feedback}`.
    - Output: updated difficulty scores or a success message.

- **Frontend (Streamlit)**
  - Form:
    - Inputs for daily time budget and difficulty range.
  - View:
    - Generated plan: problems, topics, difficulty, duration.
  - Feedback section:
    - After solving, user marks each problem’s feedback.
  - Optional:
    - Simple chart showing how the user’s difficulty profile or average difficulty changed over past sessions.

- **Engineering practices**
  - Unit tests:
    - For scheduling logic (under constraints) and difficulty updates.
  - Exception handling:
    - Handle too small time budget, invalid difficulty ranges, or empty dataset.
  - Logging:
    - Log generated plans and feedback updates (not sensitive data).
  - Linting & documentation as in Team A.

***

## 5. Team C – Real-Time Usage Monitor & Anomaly Detector for AI API

**Title:** Streaming Log Monitor for AI API Anomalies

### Problem statement

You are building a monitoring tool for an AI API (like a text-generation endpoint). The system processes a stream of log events and must:

1. Maintain rolling metrics (e.g., requests per minute, average latency, error rate).
2. Detect anomalies (usage spikes, latency spikes, error spikes, per-user abuse).
3. Display metrics and anomalies in a dashboard.

This imitates real production monitoring systems used to keep AI services healthy.

### What you will learn (Team C)

- **Data structures & algorithms**
  - Sliding window using queues/deques.
  - Hash maps for aggregating metrics per user.
  - Basic statistics (mean, standard deviation) on streaming data.
- **Operational “AI” systems**
  - How real AI APIs are monitored for reliability and abuse.
  - How streaming aggregation pipelines work conceptually.

**Real-life analogy:**  
You are building a tiny version of tools like **Datadog, Prometheus dashboards, or custom internal monitoring** panels used in companies to observe whether an AI service is being overloaded or misused.

### Functional requirements

- **Log event model**
  - Each event contains:
    - `timestamp`, `user_id`, `latency_ms`, `tokens_used`, `is_error` (boolean).

- **Core metrics & sliding window**
  - Maintain metrics over a rolling time window (e.g., last 5–10 minutes):
    - Requests per minute.
    - Error rate.
    - Average latency.
    - Per-user usage and error counts.
  - Use:
    - A deque to store recent events.
    - Dictionaries for aggregate counts and sums.

- **Anomaly detection**
  - Compute baseline metrics over the window (means, standard deviations).
  - Declare anomalies if:
    - A metric exceeds mean + `k * std` (configurable threshold).
  - Classify anomaly types:
    - High error rate, high latency, or unusual per-user token usage.
  - Assign severity levels (e.g., INFO, WARNING, CRITICAL) based on deviation.

- **Backend (FastAPI)**
  - `/ingest`:
    - Accepts new log events (in simulation, you can generate them in batches).
  - `/metrics`:
    - Returns current metrics and list of active anomalies.

- **Frontend (Streamlit)**
  - Simulate a stream:
    - Periodically send synthetic log events to the backend.
  - Display:
    - Current metrics in cards (latency, error rate, requests per minute).
    - A list/table of anomalies with type and severity.
  - Visuals:
    - Simple charts for latency and error rate over time.
    - Filter by `user_id` to inspect suspicious users.

- **Engineering practices**
  - Unit tests:
    - For sliding window maintenance, metric calculations, and anomaly detection logic.
  - Exception handling:
    - Handle out-of-order timestamps, malformed events, and invalid values.
  - Logging:
    - Log detected anomalies and threshold configurations.
  - Linting & documentation as before.

***

## 6. Suggested Repository Structure

## 📁 Your Folder Structure (ALREADY CREATED)
```
team-a-recommender/
├── backend/app/main.py     ← Add your API routes here
├── backend/app/core/       ← Put DSA algorithms here
├── frontend/app.py         ← Build UI here
└── tests/                  ← Unit tests
```

## 🚀 Start Coding (2 minutes)

```bash
pip install -r requirements.txt

# Backend (Terminal 1)
cd team-a-recommender/backend
uvicorn app.main:app --reload

# Frontend (Terminal 2)  
cd team-a-recommender/frontend
streamlit run app.py
```
## 🎯 What Each Team Builds

**Team A**: Input "two sum" → Output similar problems + patterns  
**Team B**: Input "60min daily" → Output balanced practice plan  
**Team C**: Input API logs → Output metrics + anomaly alerts

## ✅ Success = 
- [ ] Backend runs (`localhost:8000`)
- [ ] Frontend works (`localhost:8501`) 
- [ ] 5+ unit tests pass (`pytest`)
- [ ] Docstrings on all functions
- [ ] Clean code (`black .`)
***

## 7. Git & Collaboration Instructions

For all teams:

1. **Fork the main repo** `ai-dsa-playground` to your own GitHub account.
2. **Clone your fork** to your local machine.
3. **Create branches** for features (recommended):
   - `feature/similarity`, `feature/frontend`, `feature/anomalies`, etc.
4. **Commit frequently**:
   - After each function or piece of logic is completed and tested.
   - Example commits:
     - “Implement TF-IDF similarity computation”
     - “Add practice plan generator with heap-based scheduling”
     - “Implement sliding window and metrics aggregation”
   - Write clear, meaningful commit messages.
5. **Push regularly** to your fork.
6. When your track is complete and passes tests:
   - Open a **pull request** from your fork to the mentor’s main repo.
   - In the PR description, summarize:
     - What you built.
     - How to run backend and frontend.
     - Any known limitations.

This workflow will help you become comfortable with real-world Git usage: branching, committing often, and collaborating through pull requests.

Code documentation is part of writing professional-quality software, not an optional “extra.” It is how future you, your teammates, and other engineers will understand, safely change, and extend your code months or years later.

You can add this section to your shared `README.md` (or treat it as an add-on).

***

## 8. Code Documentation – Why It Matters

In all three projects, clear documentation is required, not optional.

### Why it is important

- **Helps future readers (including you)**  
  Code that “made sense in your head” today will look unfamiliar in a few weeks. Good docs explain the *why* and *how* behind your design, not just the *what*.

- **Reduces bugs and misuse**  
  When function behavior, inputs, outputs, and edge cases are documented, others are less likely to call it incorrectly or make wrong assumptions.

- **Enables collaboration**  
  In a team, you often use each other’s modules. Documentation makes it possible to treat them like well-defined building blocks instead of black boxes.

- **Reflects your professionalism**  
  Recruiters and interviewers looking at your GitHub will judge your craft not just by whether “it works,” but by whether your codebase is understandable and maintainable.

**Real-life analogy:**  
Think of documentation like signboards and instructions in a complex building (hospital, airport). Without them, people constantly get lost, ask directions, and make mistakes. With clear signs and maps, everyone moves efficiently and safely.

***

## 9. What You Should Document in This Project

Each team should focus on three layers of documentation:

1. **High-level project docs**
   - In each team’s `README.md`, briefly document:
     - What the project does.
     - Architecture overview (backend, frontend, core logic).
     - How to run the backend and frontend.
     - How to run tests and linters.
     - Any configuration (env vars, ports).

2. **Module and function docs (docstrings)**
   - Every important module and public function/class should have a docstring that explains:
     - Purpose.
     - Input parameters and types.
     - Return values.
     - Possible exceptions or special behavior.

3. **Inline comments (sparingly)**
   - Use comments to explain *why* something is done in a non-obvious way, not to restate what the code already clearly shows.
   - Example: explain a tricky algorithm step or a performance tradeoff.

***

## 10. How to Write Good Docstrings (Best Practices)

Use a consistent style (e.g., Google-style or NumPy-style). Here’s an example in Python that you can follow:

```python
def compute_similarity(query_vector: np.ndarray, item_matrix: np.ndarray, top_k: int = 5) -> list[int]:
    """
    Compute the top-k most similar items to a query using cosine similarity.

    Args:
        query_vector: 1D numpy array representing the query.
        item_matrix: 2D numpy array where each row is an item vector.
        top_k: Number of top items to return.

    Returns:
        A list of indices of the top_k most similar items, sorted by decreasing similarity.

    Raises:
        ValueError: If top_k is not positive or larger than the number of items.
    """
    ...
```

**Guidelines for your docstrings:**

- Start with a **one-line summary** in plain language.
- Then optionally add more detail about how/when to use it.
- Document **all parameters**, their meaning, and expected types.
- Document **return type** and format.
- Mention **exceptions/edge cases** if important.
- Keep language clear and concise; avoid repeating the code.

***

## 11. Documentation Expectations for Each Team

For **Team A (Recommender)**:
- Add docstrings for:
  - Text preprocessing functions.
  - Vectorization and similarity functions.
  - Pattern classification functions.
- Module-level docstring in `similarity.py` describing the overall approach.

For **Team B (Planner)**:
- Document:
  - Scheduler function(s) explaining how the heap/priority works.
  - Difficulty update logic and how feedback values affect scores.
- In `scheduler.py`, add a short high-level explanation of the algorithm used (e.g., greedy + heap, topic balancing).

For **Team C (Monitor)**:
- Document:
  - Sliding window maintenance functions (what assumptions are made about timestamps).
  - Metric and anomaly detection functions: which metrics are computed, and how thresholds work.
- In `anomalies.py`, clearly describe how severity levels are determined.

***

## 12. Short Checklist for “Good Documentation” in This Repo

Before opening your pull request, each team should check:

- [ ] `README.md` explains what the project does and how to run it.  
- [ ] Main modules (`core/*.py`) have a clear module-level docstring.  
- [ ] All public functions/classes have docstrings with inputs, outputs, and behavior.  
- [ ] Comments explain *why* (not just *what*), and are not redundant with code.  
- [ ] Any configuration (env variables, ports, file paths) is documented.  

If you follow these practices, you will not only learn to “solve problems,” but also to build codebases that real teams can understand, maintain, and extend.