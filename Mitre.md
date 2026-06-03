# MITRE ATT&CK

## Overview
MITRE ATT&CK is a globally-accessible knowledge base of adversary tactics, techniques, and procedures (TTPs) based on real-world observations. It provides a structured matrix that organizations use to model adversary behavior, prioritize detections, plan mitigations, and evaluate controls.

## Matrices
- Enterprise, Mobile, ICS, and PRE-ATT&CK matrices organize techniques under high-level tactics (e.g., Initial Access, Execution, Persistence, Exfiltration).
- Techniques can have sub-techniques and are identified by stable IDs (e.g., `T1059` for Command and Scripting Interpreter).

## ATT&CK Navigator
The ATT&CK Navigator is an interactive tool for visualizing and annotating matrices, mapping detections, and building threat emulation plans.

## Use Cases
- Threat intelligence: map observed behaviors to known techniques.
- Detection engineering: prioritize telemetry and create detection logic for specific techniques.
- Red/Purple teams: emulate adversary behavior to validate defenses.
- Risk assessment & threat modeling: identify coverage gaps and defensive priorities.

## Related resources and tools
Common attack-emulation and automation tools that align with ATT&CK include Atomic Red Team, Caldera, ATTACK_range, and other frameworks that translate ATT&CK technique IDs into repeatable tests.

## Att3k
`Att3k` is an attack-emulation project/toolset that focuses on automating and mapping adversary behaviors to ATT&CK techniques for red-team and purple-team exercises. It is used to reproduce specific techniques in test environments to validate detections and controls. (If you want, I can add a link to the specific Att3k repository you prefer.)

## D3FEND
`D3FEND` (by MITRE) is a complementary knowledge graph that documents defensive techniques, countermeasures, and the mappings between defensive actions and ATT&CK techniques. It helps defenders understand mitigation patterns, detection opportunities, and how controls interrelate with adversary behaviors.

## References
- MITRE ATT&CK: https://attack.mitre.org/
- MITRE D3FEND: https://d3fend.mitre.org/

