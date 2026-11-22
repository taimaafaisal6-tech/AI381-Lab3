# Model selection



## The question



This model predicts whether a customer is likely to churn (leave the service). A wrong prediction may cause the company to miss a customer who needs retention support or waste resources on unnecessary retention offers.



## Candidates



| Candidate | Why I tried it | AUC | F1 | F1 per slice (lowest) | p95 latency (ms) | Size (KB) | MLflow run ID |

|---|---|---:|---:|---|---:|---:|---|

| Logistic Regression | Simple, fast baseline | 0.798 | 0.4948 | 0.2500 (one-year, two-year) | 14.3 | 4 | f63b7bf5e5b84f97a0d7be7a406a316d |

| Random Forest | Test a tree-based ensemble | 0.759 | 0.4536 | 0.2222 (one-year) | 55.0 | 3160 | 0b2b570454934431bace5cbd9cf4d169 |

| Gradient Boosting | Test boosting performance | 0.748 | 0.4167 | 0.2222 (two-year) | 14.8 | 142 | 2b096b4ecf3e47a6bd5c6b0f08f2f152 |



## The champion



I selected Logistic Regression. It achieved the highest AUC (0.798) and F1 (0.4948), with low p95 latency (14.3 ms) and the smallest model size (4 KB). It also had the best lowest-slice F1 (0.2500). However, its performance on one-year and two-year contracts still needs improvement.



## My promotion rules



- Latency budget (p95): 25 ms, because it allows fast predictions while excluding the slower Random Forest candidate.

- Minimum gain to replace the champion (F1 points): 0.005, because a new model should improve F1 by at least 0.5 percentage points.



## What I would check next



I would investigate the low F1 for one-year and two-year contract customers and check whether these groups have fewer training examples or different churn patterns.

