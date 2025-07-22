### Thrivory Inc.
_Internal Document_

# Coding Challenge for Software Engineering: Baseline Solution & Implementation Guidance

This document describes expected solution patterns, technical approaches, and quality indicators to help evaluators understand what good implementations look like.

_Note: Ideally, if I have more time, I'll create a sample implementation of the solution, and use that as a baseline to test the candidate's code._ This part feels rather subjective, as of now, which is okay as a starting point.

## Scenario 1: Expected Implementation Patterns

### Data storage approaches
Most candidates will choose in-memory storage for simplicity. Expected trade-offs they should consider:

- In memory: 
    - Much less complexity, quick iterations in development _but_ 
    - cold start **(need to load the data on startup every time)**, querying data is slow (since no natural indexing, candidates can build indexes/lookups, which lead to more complexity).
- Persistence storage: 
    - Indexing out of the box, so faster lookups.
    - Complexity around managing models/db-layer, which can slow the iteration cycle.

**Good candidates** will choose in-memory design and demonstrate awareness of performance implications.
    
### Data modeling
**Good candidates** will:
    
* Implement mapping tables/lookups for different column values/keys (e.g., DRG column keys and DRG Codes, number of days column key and the actual days, etc.). These mappings are provided in the data key file.
* Implement a data model representing the actual dataset. 

### Dataset handling
**Look for candidates who:**
    
* Use AI tools effectively for CSV parsing and data loading
* Include basic validation to ensure data loads correctly
* Handle parsing errors gracefully (e.g., invalid data types, missing required fields, malformed CSV rows)

### Payment estimation approaches
Expect varied approaches based on candidate judgment. Common patterns from simple to complex: 

Given a DRG code and number of days, the candidate could:
1. Find an existing row with that combo, and return the average of the quantile that particular row falls into (e.g., if DRG code 123, number of days 10, and the row falls into the 3rd quintile, return the average of the 3rd quintile).
2. Find existing rows with that particular DRG code (ignoring the number of days), and return the common average of all the quintiles, so if quantile averages are 10, 20, 30, 40, 50, return (10 + 20 + 30 + 40 + 50) / 5 = 30.
3. Find existing rows with that particular DRG code (ignoring the number of days), and return the average middle quintile, so if quantile averages are 10, 20, 30, 40, 50, return 30.
4. Attempt to build an ML model (**an overkill**)
    * DRG Codes are enums, so will probably have to binary encode them
    * Could build regression model (number of days → payment estimate) 
    * Could build a decision tree model (number of days → payment estimate)

**Strong candidates** will choose simple approaches (options 1-2) and justify their decision-making process.

### Calculating the confidence level
Most good candidates will base confidence level on the sample size for DRG codes (available in data dictionary). For example, if the quintile averages for DRG code 123 are based on 5 claims, the confidence level should be "low"; if they're based on 1000 claims, the confidence level could be "high".

### API implementation
**Look for exact adherence to provided specification:**
```
GET /api/estimate?drg=<value>&days=<value>
```
Responding with the following format (exactly the same as the provided API spec):

```json
{
    "estimated_payment": <integer value>,
    "confidence_level": <"low" | "medium" | "high">
}
```

**Quality indicators:**
- Exact response format compliance
- Graceful error handling for invalid inputs (missing DRG codes, invalid parameters, proper HTTP status codes like 400 for bad requests, 404 for missing data)
- Proper HTTP status codes

_Note: Sample test cases from the dataset should be created to validate API implementations (not included due to time constraints)._

### Frontend patterns
**Good candidates** will implement a simple form with two inputs (DRG, days) that calls the API correctly.

**Quality indicators:**
- Input validation and user-friendly error messages
- Clean, functional UI (framework choice irrelevant)
- Evidence of AI copilot usage for rapid development
- Use of Vanilla HTML/CSS/JS or full-stack framework integration with the API.

## Scenario 2: Code Evolution Patterns

**Challenge:** Extend existing codebase to support batch estimates across day ranges.

**Common implementation approaches:**
1. **Simple wrapper:** Loop through existing single-day API internally
2. **Code evolution:** Modify core estimation logic to handle ranges natively

**API compliance:** Must match specification exactly:

```
GET /api/estimate/batch?drg=<value>&days_from=<value>&days_to=<value>
```

**Expected response format:**
```json
[
    {
        "days": <integer value>,
        "estimated_payment": <integer value>,
        "confidence_level": <"low" | "medium" | "high">
    }
]
```

_Note: Sample test cases from the dataset should be created to validate API implementations (not included due to time constraints)._

**Quality indicators:**
- Successfully extends existing codebase without breaking Scenario 1 functionality (original `/api/estimate` endpoint continues to work as expected)
- Clean integration approach (wrapper vs native implementation)
- Handles edge cases (invalid ranges, single-day ranges)
- Maintains performance for reasonable day ranges

---