### Thrivory Inc.

# Coding Challenge for Software Engineering

## Overview

Hello! We're so glad that you're considering joining Thrivory. We've designed this take home assignment to 1) give you a sense of the type of technical problems you may face at Thrivory, and 2) get a sense of how you handle such problems.

Thrivory is a healthcare fintech platform that accelerates insurance reimbursements for medical practices. As part of our mission, we build tools that forecast expected amounts for submitted claims.

In this challenge, you will build a simplified tool that can be used to **roughly** estimate the payment amounts for a particular inpatient stay. More details of the assignment are provided later in this document.

_Note: At Thrivory, we do not deal with inpatient claims at this moment. However, the overall problem we solve is similar._

### Split into Two Scenarios

The exercise is divided into two scenarios. You are expected to complete Scenario 1 first, and Scenario 2 second. 

**Important:** Please read Scenario 2 only after completing Scenario 1 to maintain the intended challenge progression. It'll be more fun that way (but we leave it up to you).

### Time & Effort Expectations

You are expected, and encouraged to complete the assignment in the most efficient way possible. This includes making good use of AI copilots and reducing the scope where necessary.

We suggest that you spend ~1hr reading and understanding the assignment, the provided dataset and the key. The implementation part of the assignment is expected to take ~3-5 hrs (2-3 hrs for Scenario 1 and 1-2 hrs for Scenario 2).

You are free to reduce the scope if you find yourself spending too much time on the assignment.

### **Submission**

You are being provided access to a GitHub repository, and are expected to keep your code in it.

Please provide a `doc.md` file, giving explicit instructions on how to run your code. Please also include any other relevant information you want us to know while we review your submission.

You are free to break down your work however you want (and in whatever number of commits). However, we request that you provide a clear distinction on when you finish Scenario 1, by tagging the final commit of it with `v1.0.1` (using GitHub tags).

### **Evaluation**

This exercise is intentionally subjective. You will be evaluated holistically on your submission, the decisions and trade-offs that you make in the process, and the code quality and design.

You're not expected to polish UI, handle every edge case, or build perfect features. The real world is messy. Clarity, structure, and reasoning matter more than perfect results. Partial completions are acceptable, if well-justified in your `doc.md` (e.g., prioritizing the API over a polished UI). We value creative, pragmatic solutions over perfection.

## Scenario 1: Build an estimator tool

_Note: Please aim to spend 2-3 hours on this._

Recently, Thrivory has gotten some market signals that hospitals want to get a sense of the expected payments they would receive for their inpatient admissions.

Although hospitals are not Thrivory's current core clientele, we want build something quick to test out this theory.

We have access to some data, which we believe could be used.

  1. Dataset – a sampled, real-world inpatient claims data from CMS (Centers for Medicare and Medicaid Services) from 2008.
  2. Key – the accompanying data dictionary that describes each column of the dataset.

      _These will be provided to you in the GitHub repo. If you have any questions about the dataset or challenge, feel free to contact us. Some extra information about the dataset that you may find useful: DRG codes represent diagnoses related to the hospital stay._

      _Note: The dataset is Medicare-focused, which differs from Thrivory's outpatient clinic emphasis—feel free to make assumptions or adjustments as needed. There are similarities to how you'd adapt for an outpatient scenario._

You are asked to build a tool that potential users can use to get an estimate of the payment amounts for inpatient stays. The tool should have:

* A frontend component (that users can interact with)
* An API (that the frontend, or another system can interact with). The API should:
  * Accept: **DRG Code** and **Length of Stay (in days)**
    * Endpoint: `GET /api/estimate?drg=<value>&days=<value>`
  * Return: **Estimated payment** and **Confidence level**, in the format:
    ```json
    {
      "estimated_payment": <integer value>,
      "confidence_level": <"low" | "medium" | "high">
    }
    ```
  * Example:
    * Request: `HTTP GET /api/estimate?drg=470&days=3`
    * Response:
      ```json
      {
        "estimated_payment": 11250,
        "confidence_level": "high"
      }
      ```
  * Consider how to handle edge cases like invalid DRG codes or missing data.

It is expected that the API will rely on the provided dataset to make its estimations. However, you are free to decide how to use it (or to ignore it -- we all have free will). There are multiple ways to calculate a **rough** payment estimate, and we leave it up to you to choose a method that makes most sense to you.

For determining the confidence level, you are free to use any common sense approach.

---

## Scenario 2: Make life easier for Alice

_Note: Please aim to spend 1-2 hours on this._

Users are liking your tool and using it often -- Good job! However, some users have been saying that they have to repeatedly fill in the same information every time (to get the same result). For example, a user, Alice, gave feedback saying:

   "Our small-specialized hospital only deals with cardiac patients, and we almost always need estimates for DRG code 231, with inpatient stays of around 5 to 10 days. It'll be helpful if we could get those answers fast".

You are asked to make life easier for users like Alice. Extend your existing backend API and/or frontend to support batch estimates. Add an endpoint:

```
GET /api/estimate/batch?drg=<code>&days_from=<value>&days_to=<value>
```

* Returns estimates for the DRG code across the specified day range.

#### **Example Response Format:**

```json
[
  {
    "days": 5,
    "estimated_payment": 12000,
    "confidence_level": "medium"
  },
  {
    "days": 6,
    "estimated_payment": 12500,
    "confidence_level": "high"
  }
  // ... more for the range
]
```

Optionally, integrate this into the frontend to make it usable.

---

Good luck! We're excited to see how you think and build.

*For questions about this challenge or the hiring process, please reach out to the Thrivory recruiting team.*