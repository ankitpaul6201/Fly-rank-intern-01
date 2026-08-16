# 📑 Submission 7 — Phase: Setup & AI Fluency (FL-02: Frame It As Cases)

**Task Reference:** `Setup — Frame It As Cases (AI Fluency Week 2)`  
**Phase:** Setup / AI Fluency | **Estimated Hours:** 4  
**Deliverable File:** [`submissions/submission_07_framed_cases.md`](submissions/submission_07_framed_cases.md)

---

## 🎙️ 1. Voice Card & Standing Instructions

**Voice Card (5 words):**  
`sharp, empirical, plain, direct, evidence-first`

**Standing Instructions configured in Claude Project / AI Assistant:**
```text
VOICE CARD:
Use a tone that is sharp, empirical, plain, direct, and evidence-first.

RULES:
- Never use generic corporate AI fluff or buzzwords (e.g. "results-driven", "spearheaded", "cutting-edge", "game-changing", "seamlessly").
- Ground every claim in concrete metrics, human decisions, and real dataset numbers.
- Write in short, active sentences using natural human voice.
- Keep the focus on the decision improved, the trade-off made, and the operational outcome achieved.
```

---

## 💬 2. The AI Interview Process (Unfiltered Q&A)

To extract real decisions and outcomes without borrowing generic AI templates, I conducted a one-question-at-a-time interview with Claude acting as a rigorous technical interviewer.

### Q1: What specific problem were you trying to solve in FlyRank, and who was suffering because it wasn't solved?
> **Answer:** Content teams at mature websites manage tens of thousands of URLs. Over time, search rankings decay quietly. Editors cannot manually inspect 30,000 pages every week. The product already had hand-written rules, but those rules flagged thousands of pages indiscriminately without showing which 20 pages an editor should update *this week*. Wasting hours on healthy pages had a huge opportunity cost, while missing decaying top-traffic pages meant permanent search traffic loss.

### Q2: What exact decisions did you make when framing and building the solution?
> **Answer:** I decided to frame it as a ranking and scoring problem rather than binary classification, because editors need a prioritized top-K queue matching their weekly capacity. I also decided that target labels must come strictly from observed search console performance in later time windows, rather than relying on circular internal flags like health scores. In code, I verified the 22,006 active demand slice, modeled position-dependent CTR deficits, and used client-holdout splits to prevent domain leakage.

### Q3: What were the actual measured results?
> **Answer:** The multi-signal ML scoring model achieved 88% Precision at 50, delivering a 10 percentage point improvement over fixed static rules and a 3x precision lift over naive baselines. This meant that 44 out of 50 top-ranked recommendations were genuine decay opportunities that content managers could confidently refresh.

---

## 📁 3. Framed Portfolio Case Studies (Three Beats)

---

### Case Study 1: FlyRank — Search Content Decay Opportunity Scoring

#### Beat 1: The Problem
Mature websites with tens of thousands of published pages face silent search traffic decay. Editorial teams have limited weekly capacity and can only audit 20 to 50 URLs per sprint. Existing hand-written rules flagged over 13,000 pages indiscriminately, leaving editors with a massive unprioritized backlog. Auditing healthy pages wasted limited editorial budget, while missing decaying top-traffic pages caused permanent traffic loss.

#### Beat 2: What I Did & Decided
I framed the challenge as a ranking and continuous opportunity scoring problem rather than binary classification. Instead of predicting circular internal flags, I built observed target labels from downstream search console impression telemetry. I sliced the inventory to 22,006 active demand pages with at least 100 90-day impressions, verified row grain integrity, and engineered features capturing non-linear position-CTR deficits. To ensure honest evaluation, I evaluated models using client-holdout splits so no domain appeared in both training and test sets.

#### Beat 3: What Came Of It (The Outcome)
The multi-signal opportunity scoring model achieved an 88% Precision at 50, outperforming fixed hand-written rules by 10 percentage points and delivering a 3x precision improvement over baseline heuristics. This gave content managers a reliable weekly queue where 44 out of 50 top-ranked recommendations represented high-yield refresh opportunities.

---

### Case Study 2: CP Vault — Developer Productivity & Code Persistence

#### Beat 1: The Problem
Competitive programmers and algorithm developers write hundreds of solutions across multiple online judge platforms. Solution code is frequently scattered across browser tabs, temporary local files, or external judges, making past implementation patterns hard to query or reuse during timed contests.

#### Beat 2: What I Did & Decided
I built CP Vault as a structured chrome extension and local workspace integration. I decided against storing code in unindexed flat files; instead, I built a local categorization schema indexing submissions by problem tags, space-time complexity, and verification status. I implemented automated local file syncing so developers retain total ownership of their codebase offline.

#### Beat 3: What Came Of It (The Outcome)
CP Vault provided instant sub-second search across personal algorithm implementations, reducing code retrieval friction during contest preparation and serving as a persistent knowledge base across hundreds of competitive programming problems.

---

### Case Study 3: Campus Buddy — Full-Stack Educational Workflow Platform

#### Beat 1: The Problem
University students balance fragmented academic schedules, course resources, and campus updates across disconnected portals, leading to missed deadlines and poor administrative visibility.

#### Beat 2: What I Did & Decided
I designed and developed Campus Buddy as a unified full-stack web and mobile application. I prioritized offline-first data caching and clean responsive interface components, allowing students to access class timetables, attendance tracking, and resource hubs instantly without waiting on slow university server queries.

#### Beat 3: What Came Of It (The Outcome)
Delivered a high-performance campus dashboard that consolidated academic workflows into a single interface, reducing daily app load latency and providing students with real-time schedule notifications.

---

## 👤 4. Bio & Conversion CTA Copy

### Bio Copy (3 Lines)
I build applied, readable machine learning decision-support systems and full-stack tools.  
My focus is transforming noisy telemetry logs into clear, evidence-backed priority queues for human experts.  
I value clean data contracts, client-holdout validation, and measurable operational impact over generic complexity.

### Call to Action (CTA Copy)
**Let's talk engineering.**  
If you are evaluating applied ML decision-support systems or need someone who builds clean, evidence-backed tools, schedule a 15-minute technical discovery chat or explore my code on GitHub.

* **Primary Action:** [Schedule a 15-Min Technical Chat](https://github.com/ankitpaul6201/Fly-rank-intern-01)  
* **Code Repository:** [Explore FlyRank Capstone Code](https://github.com/ankitpaul6201/Fly-rank-intern-01)

---

## 🔄 5. Before vs. After Comparison (Generic AI vs. Edited Voice)

### Generic AI Line (Before)
> *"Leveraged cutting-edge machine learning algorithms and advanced feature engineering techniques to seamlessly predict content decay trends, empowering results-driven editorial teams to optimize search engine performance and maximize ROI."*

### Edited Human Line (After)
> *"I framed content decay as a ranking problem on 22,006 active search pages. The model achieved 88% Precision at 50, giving editors a reliable weekly queue where 44 out of 50 recommendations target genuine traffic recovery opportunities."*

### Why the Edit Wins:
* **Removes Fluff:** Eliminates empty buzzwords like "cutting-edge", "seamlessly", "results-driven", and "maximize ROI".
* **Anchors in Real Metrics:** Replaces vague claims ("optimize performance") with exact numbers (22,006 pages, 88% Precision@50, 44 out of 50 queue accuracy).
* **Sounds Like a Real Engineer:** Speaks directly to the technical decision and operational outcome without promotional hyperbole.

---

## 💡 6. What I Learned

1. **AI as an Interviewer, Not a Writer:** Using AI to interview me about real decisions extracted authentic project narrative rather than generic resume fluff.
2. **The 3-Beat Case Structure:** Structuring every project around *The Problem*, *What I Did & Decided*, and *What Came Of It* keeps case studies clear, tight, and focused on business value.
3. **Voice Discipline:** A strict voice card ("sharp, empirical, plain, direct, evidence-first") provides clear boundary rules for editing AI drafts.
