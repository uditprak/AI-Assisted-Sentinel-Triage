# Evaluation plan

The goal is to show whether the AI note actually helps triage, not just that it runs.

| Check | Method | Target |
| :--- | :--- | :--- |
| Severity agreement | Compare `suggested_severity` with my own triage decision on 20+ incidents | Agreement on most incidents; every disagreement reviewed |
| MITRE mapping | Check the technique ID against the analytics rule's mapping | Correct on brute-force incidents (T1110) |
| Hallucination | Any fact in the summary not present in the input data | Zero tolerated; the prompt is fixed if found |
| Time to first decision | Time from incident creation to my triage decision, with vs without the note | Shorter with the note |
| Failure handling | Send malformed / empty model output | Playbook posts nothing and logs the error |

Results will be added here as a table once the playbook is live.
