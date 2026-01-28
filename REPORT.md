# TP4 - Model Promotion Pipeline Report

**Name:** Rakotomalala Gentley
**Date:** 28 jan

---

## Task 1: Run Candidate -> Staging Workflow

**Workflow triggered:** Candidate to Staging

**Results:**

| Metric | Value |
|--------|-------|
| Model Version | 3 |
| Accuracy | 0.8975 |
| Gate Passed? | No |

**Screenshot of workflow logs:**


![79304.png
](20260128161035.png)


A new candidate model (version 3) was successfully trained and registered in MLflow with an accuracy of 0.8975.
The automated quality gate required a minimum accuracy of 0.90, which the model did not reach.
As a result, the gate failed and the pipeline stopped before promotion, ensuring that production was not impacted by a sub-standard model.


## Task 2: Explain What "Staging" Proves

**Question:** What does staging test that offline evaluation does not?

**Answer:**
Staging proves that the model works in real conditions, not just on offline metrics.
It checks that the model can be loaded from the registry, that the API runs correctly, and that basic tests pass before touching production.
Unlike offline evaluation, staging can catch issues related to deployment, configuration, or integration, even if the accuracy looks good.

This is why a model can look fine during training but still be blocked before production.


---

## Task 3: Promote to Production

**Model version promoted:**

**Screenshot of promotion log:**

![[Insert screenshot here]
](20260128163557.png)
---

## Task 4: Prove Production Uses Registry Stage

**Commands run:**

```bash
curl http://localhost:8000/health   # Staging
curl http://localhost:8001/health   # Production
```

**Results:**

- Staging response (`localhost:8000`):
```json

```

- Production response (`localhost:8001`):
```json

```

---

## Discussion Questions

### 1. Why is it dangerous to deploy "whatever just merged to main" as the model?



### 2. What does the registry stage give you that a Git tag does not?



### 3. If staging passes but production fails, what could be the causes?



### 4. Where should DVC fit in a serious pipeline?

- Training data snapshot:
- Evaluation dataset snapshot:
- Drift reference dataset:

### 5. What should be added to the gate beyond accuracy?

- Latency:
- Schema checks:
- Fairness constraints:
- Adversarial/robustness tests:

---

## Optional: Extensions

- [ ] ngrok integration for public-facing endpoint
