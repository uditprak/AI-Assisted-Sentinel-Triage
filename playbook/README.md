# Logic App design

| # | Step | Logic Apps action |
| :- | :--- | :--- |
| 1 | Start when a Sentinel incident is created | Microsoft Sentinel: *When incident is created* |
| 2 | Read the IP and account entities | *Entities - Get IPs*, *Entities - Get Accounts* |
| 3 | Run `kql/incident-context.kql` with those values | Azure Monitor Logs: *Run query and list results* |
| 4 | Build the prompt from `prompts/triage-prompt.md` | *Compose* |
| 5 | Call the LLM | *HTTP* POST to Azure OpenAI chat completions (Managed Identity / key from Key Vault) |
| 6 | Validate the JSON | *Parse JSON* with the output schema; on failure, stop and log |
| 7 | Add the triage note to the incident | Microsoft Sentinel: *Add comment to incident* (prefixed "AI-generated triage") |
| 8 | Flag for L2 if suggested severity is higher than current | *Condition* → *Update incident* (add tag `ai-suggests-escalation`) |

The exported workflow JSON will be saved here as `ai-triage-playbook.json` once built, with subscription and connection IDs removed.
