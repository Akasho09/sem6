## What is modular programming? 
Modular programming is a general programming concept where developers separate program functions into independent pieces

## Maturity Levels of CMM, CMM vs ISO 9001, Cyclomatic Complexity
### ✅ Maturity Levels of CMM:  
> IRDMO

Level 1 – Initial: Ad hoc and chaotic
Level 2 – Repeatable: Basic project management processes
Level 3 – Defined: Processes are standardized
Level 4 – Managed: Quantitative metrics used
Level 5 – Optimizing: Continuous process improvement


## Fault vs failure 
| **Aspect**         | **Fault** (also called *defect* or *bug*)             | **Failure**                                           |
| ------------------ | ----------------------------------------------------- | ----------------------------------------------------- |
| **Definition**     | A flaw, mistake, or error in the system or code       | The system's inability to perform a required function |
| **Cause**          | Caused by incorrect logic, bad code, or design errors | Caused when a fault is executed during operation      |
| **When It Occurs** | Exists in the system even if not triggered            | Happens during execution when a fault is activated    |
| **Visibility**     | May not be visible to users (latent fault)            | Always visible to users or external observers         |
| **Relation**       | A fault *can lead to* a failure                       | A failure is *the result of* a fault being triggered  |


- Fault Example:
A developer writes if (x = 5) instead of if (x == 5) in a login function.
This is a fault (a code-level error), but the system may still run without issues until the condition is evaluated.

- Failure Example:
When a user tries to log in and the system lets them in without checking the correct condition due to the above fault — this is a failure (the system did not behave as expected).

