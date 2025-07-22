### Thrivory Inc.
_Internal Document_

# Coding Challenge for Software Engineering: Justification & Evaluation Criteria

**Disclaimer:** A lot of my ideas, beliefs are based on my experience in healthcare, working with startups, what worked (and didn't) at Devoted Health, and on my understanding of Thrivory. As I understand Thrivory more, some of these ideas will be refined.

Thrivory's ideal candidate, and hence the approach to finding it, will also evolve as Thrivory grows as a company. For example, later in Thrivory's life-cycle, it may make sense to hire strong technical people even if they don't have the strongest product sense, but that day is not today.

A few things that I'll like to evolve if I had more time:
  - Preferably, change the dateset to be more relevant to Thrivory's business (e.g. outpatient, private insurance claims instead of inpatient medicare claims).
  - Find a way to incorporate more Restful API design.
  - Provide candidate with a bunch of API tests that they use.
  - Have more extensive internal API tests that we can use to test the candidate's code.

Just like any other product, this coding assignment is a living thing, it needs to be tested in the wild and iterated upon.

## The Role & The Ideal Candidate

This is an early engineer role — possibly the first or second hire. It's full-stack-ish, ambiguous, and fast-moving. This role:

* spans both healthcare and fintech domains.
* is remote, async-friendly, and highly autonomous.
* involves figuring out what to build directly with stakeholders, not just how.
* requires dealing with ambiguity and messy real-world constraints.
* is hands-on — you'll write a lot of code and ship actual things.
* will have an impact on the company culture.

### What does the ideal candidate look like?

The ideal candidate is one that will maximize Thrivory's chance of success. I posit that the following are the traits we optimize for, prioritized by importance for our early-stage needs:

1. **Strong first principles:** Candidates strong at breaking down problems and core engineering fundamentals (data modeling, API design, code structure).

2. **Thrive in ambiguity & uncertainty:** Startups are messy with undefined requirements that change rapidly. Ideal engineers welcome this environment and consistently find a way through.

3. **Strong communication & proactive problem-solving:** Excellent communicators who proactively find answers, and explain technical decisions clearly to stakeholders.

4. **Fast builders with modern tooling:** Engineers who ship quality products quickly using modern tools (AI copilots, pragmatic tech choices). Domain comfort in healthcare/fintech is valuable.

5. **Product-driven autonomous decision-making:** Engineers who prioritize building the right thing while making countless solo decisions guided by mission and product sense.

6. **Positive team contributor:** Engineers who are genuinely enjoyable to work with and can uplift team morale and productivity.

**How these traits map to our evaluation:**

* **First principles** → Code structure, data modeling, API design quality
* **Ambiguity tolerance** → How they handle underspecified requirements in the coding challenge
* **Communication & problem-solving** → README documentation, inline comments, technical conversations, follow-up interviews
* **Fast building** → Completion within time constraints, smart use of AI tools, pragmatic scope decisions
* **Product-driven autonomous decision-making** → Understanding user needs, making autonomous decisions based on user needs.
* **Team contribution** → Behavioral interviews, communication style during technical discussions

### Assessment Methods

We use multiple evaluation approaches to maximize our chances of identifying the ideal candidate:

1. **Resume screening:** Startup experience (ambiguity tolerance), healthcare/fintech experience (domain knowledge), experience at companies known for technical excellence (strong first principles).
2. **Behavioral interviews:** Mission alignment, communication skills, cultural fit
3. **Technical conversations:** First principles thinking, product sense, AI tool comfort
4. **Coding challenge:** Realistic scenarios testing core traits. 

_Note: I recommend a process that includes two technical evaluations: 1) This coding Assessment + Follow-up, 2) A more high-level, verbal technical/system conversation._

## Coding Challenge

### Logistics

The coding challenge is shared with the candidate via a private repo. The candidate is expected to complete the challenge within 48 hours.

In order to send the challenge to the candidate:
1. Get the candidate's github username.
2. Create a fork of the existing repo `github.com/thrivory-interviews/take-home-swe`, and name the new repo to `github.com/thrivory-interviews/take-home-swe-<candidate-name>`. 
    
    Make sure the repo is priviate.
3. Add the candidate's username as a collaborator to the repo.
4. This should automatically sent an invitation to the candidate, or you can manually send the new repo link to the candidate.

### Justification

We want something that's realistic, slightly messy, and relevant to what we're doing at Thrivory. In particular, we want something that:

1. Stays within healthcare domain.
2. User/product focused: solve issues vs. just build something.
3. Ambiguous: require candidates to make major decisions, not just about the tech but about the product as well.
4. First principles: Requires clean data structures / models for simplicity and good performance. 
5. High scope (AI co-pilot dependent): should be completable within expected time primarily through smart use of AI copilots.
6. Evolving the code: We want the challenge to test the candidate on evolving an existing code, since majority of the actual work is to build/tinker on top existing codebases.

The challenge I have constructed, though not perfect, attempts to check most of the above boxes. Here are some notes on key aspects of the challenge:

**Context - Users wanting instant estimates:** Sets the "Why are we building" to a product exploration problem. Understanding this _why_ would guide candidates to make some clever decisions.

**Two Scenarios (A & B)**: I've split the challenge into two scenarios to allow us to test how candidates handle evolving their codebase. 

_Note: It's tricky to keep the scope of scenario 2 small, while offering enough challenge. I've tried to balance this._

**Dataset: 2008_BSA_Inpatient_Claims_PUF:** Real-world sampled, inpatient medicare claims data. It

* Grounds us in healthcare domain with realistic data complexity
* Mimics actual healthcare ETL projects involving data parsing and loading
* Normalized dataset with a key-reference, which demands a clean data structure
* Perfect use case for AI copilots (structured file parsing)

    _Note: Inpatient Medicare data differs from Thrivory's outpatient focus, but was most accessible to me for this challenge. Consider S3 hosting to add realistic data fetching scenarios._

**Estimator tool:** Users provide payment estimates using DRG codes and length of stay. Intentionally underspecified to test decision-making. Dataset includes quintile averages for direct use, avoiding unnecessary ML complexity. Confidence levels communicate estimate uncertainty to users.

**Scope: API + Frontend**: Full-stack requirement encourages AI copilot usage, especially for form generation.

**Tech Stack**: Intentionally agnostic - premature to optimize for specific technologies.

**Completeness**: Candidates should scope work to time constraints. Evaluation focuses on decisions and reasoning, not completeness. API endpoints remain core requirements.


## Evaluation Criteria & Scorecard

_This evaluation framework assesses the 6 key traits: (1) First principles, (2) Ambiguity tolerance, (3) Communication, (4) Fast building, (5) Product sense, and (6) Team contribution._

### Part 1: Review - Code Submission

This section evaluates the code submission, and should be completed prior to the follow-up interview. 

**1. First Principles Thinking** (8 points)

a. Data Modeling (4 points): Thoughtful, minimal data model with appropriate claims/DRG structures?

    Score: ___ / 4

b. Performance (2 points): API endpoint performance considerations (O(n) vs O(1))?

    Score: ___ / 2

c. Code Structure & Naming (2 points): Clear organization with separation of concerns?

    Score: ___ / 2

**2. Coding Efficiency** (4 points)

a. Working End-to-End Build for Scenario 1 (2 points): Complete implementation with working API and UI?

    Score: ___ / 2

b. Working End-to-End Build for Scenario 2 (2 points): Did they also include a frontend?

    Score: ___ / 2

**3. Navigating Ambiguity** (4 points)

a. Estimation Logic (4 points): Is the payment estimation approach clear, justified, and without unnecessary complexity?

    Score: ___ / 4


**Total Score - Code Submission (16 points)**
Tally up the total score.

    Total Score: ___ / 16


### Part 2: Review - Follow-up Interview

Complete this section after the followup interview.

**1. First Principles Thinking** (4 points)

a. Can they clearly explain why they modeled things the way they did? (e.g., why those specific fields or types, how they grouped data, how they handled estimation logic?)

Is their approach rooted in fundamentals and simplicity?

    Score: ___ / 4

**2. Navigating Ambiguity** (4 points)

a. How did they make decisions in the face of vague or missing requirements? (e.g., estimator strategy, no clear frontend requirements)

    Score: ___ / 4

**3. Efficiency / Speed of Execution** (4 points)

a. How well did they use AI tooling or shortcuts? Did they identify the best areas to offload to copilots (e.g., CSV parsing, UI forms)?

    Score: ___ / 4

**4. Communication & Collaboration** (4 points)

a. Are they collaborative, clear, and someone we'd enjoy working with?

Did they explain things in a thoughtful and non-defensive way? Were they able to narrate decisions like someone who communicates across PM/eng/stakeholder lines?

    Score: ___ / 4

**Total Score - Follow-up Interview (16 points)**
Tally up the total score.

    Score: ___ / 16

### Overall Score
Add the "Code Submission" and "Followup Interview" scores, and divide by 4 for a weighted score out of 8.

    Total Score: ___ / 32
    Weighted Score: ___ / 8

_Note: The weighted scoring divides by 4. to normalize the combined 32-point scale to an 8-point scale for easier interpretation, where each point represents strong performance across multiple evaluation dimensions._

### Scoring Interpretation & Decision Framework

#### Score Ranges:
- **7.0-8.0**: Strong hire - Exceptional candidate who excels across multiple dimensions
- **6.0-7.0**: Hire - Solid candidate with good fundamentals and clear potential  
- **5.0-6.0**: Borderline - Mixed results, consider specific role needs and team gaps
- **Below 5.0**: No hire - Significant gaps in core requirements


**Would you recommend this candidate?** 

□ **Strong Hire** - Exceptional performance, immediate contributor
□ **Hire** - Good fundamentals, strong potential for growth  
□ **Borderline** - Mixed signals, requires further evaluation
□ **No Hire** - Significant gaps in core requirements

**Key Strengths:**
_[Brief summary of candidate's strongest areas]_

**Areas for Development:**
_[Any concerns or growth opportunities]_

**Recommendation Rationale:**
_[2-3 sentences explaining your decision]_

---