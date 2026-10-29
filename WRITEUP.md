1.	AI: 
•	AI should read the proposal and extract the facts (license, insurance, price, weeks, warranty years, team and plans) with evidence. 
•	AI should also write a small reason that why the proposals meet the evaluation criteria. This reason should include references e.g., if something is missing from mandatory requirements or some information is conflicting.
Rules:
•	The backend system should validate the extracted data, check if the data contains mandatory requirements and the requirements are valid, calculate the weighted scores and rank the eligible proposals. 
•	If mandatory information is missing or uncertain, the proposal is flagged for human review rather than automatically rejected. If the missing information is resolved and all mandatory requirements are met, the proposal proceeds to scoring. If a mandatory requirement is confirmed to have failed, the proposal is marked as ineligible. If the information remains unresolved, it stays flagged and excluded from ranking.
2.	Consistency and Explainability:
•	System should use code for scoring the weights and validating the data in proposal. It should store the facts, evidence, scores, weights, ranking, status and reasons for each evaluation.
•	The system will show the same output for same input. The extraction output will be saved and reused on re-rank instead of calling AI again for the extraction of document. 
•	The reviewer should not trust the ranking blindly. The source of score is extracted values, points earned, weights and mandatory checks. These factors show the exact reason why the proposal is scored or ineligible. AI’s summary is based on these factors.
3.	Human in the Loop: 
•	A person reviews proposals when the extracted information is flagged as missing, uncertain, or conflicting. The reviewer can verify whether the bidder holds a valid license. If the information remains unresolved, the proposal stays flagged and excluded from ranking. If a mandatory requirement is confirmed to have failed, the proposal is marked as ineligible.
•	Reviewers should be able to take the final award decision by inspecting the evidence, correct extraction errors, add notes and record justified overrides. 
•	The ineligible proposals with their extracted data and reason of ineligibility are saved in database so the decision may be challenged by the reviewer.
•	Audit log should record who uploaded proposal, time-stamps, proposal identifiers, extracted and verified information, criteria, prompts, scores, ranking, flags, overrides, reasonings and the final award decisions.
4.	Changing Criteria:
Evaluation criteria are configurable through admin screen not hard-coded. The criteria are stored as versions. Each scoring run records the criteria version used. If an admin changes criteria, existing results are saved as old version e.g, as v1 and new version is saved as e.g, v2. The reviewer can re-score. The extractions would be same; a re-score just re-runs the code with new weights. The admin screen validates changes. A reviewer compares v1 and v2 rankings side by side before deciding. Final award decision is made by human. 
5.	Risks and Safeguards:
•	The main risk is wrong extraction by AI.  It may mislead or do inconsistent scoring. So, every field needs an evidence quote. Code checks the schema. Unsure means null. Low-confidence fields go to human review. 
•	AI may generate made-up facts that are not actually in the proposal, to make proposal stronger. So, to safeguard it, anything that’s not found should be treated as missing. 
•	A proposal may contain hidden instructions to manipulate AI into ranking a bidder first. The proposal will be treated as untrusted input. The design flags instructions-like text and is reviewed by human.
•	Hidden unfairness is also a risk. But the scoring in this design only uses admin criteria for this purpose. Company names are not used in scoring. Price, experience, warranty, team and timeline are the factors. Override also requires a proper reason and are logged.
•	Corrupted, scanned, or unreadable PDFs may prevent accurate extractions of proposal information. For this, the design asks for re-uploading the PDF. Unreadable PDF is flagged for review instead of being scored.
