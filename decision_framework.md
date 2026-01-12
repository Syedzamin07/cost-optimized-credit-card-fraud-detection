This document defines the business problem and decision logic for a cost-sensitive fraud detection system. All technical and modeling decisions in this project are aligned with these business realities.

**Who is losing money?**

→ A bank

**Why are they losing money?**

→ Fraudulent credit card transactions that must be reimbursed to customers

**What decision must be made?**

→ Whether to allow or block each transaction in real time

**What mistakes cost what?**

→ Missed fraud (False Negative): $100 (assumed average fraud loss)

→ Blocked customer (False Positive): $5 (assumed operational + customer friction cost)

**What does “success” mean?**

→ Reducing expected financial loss compared to a naive baseline decision rule
