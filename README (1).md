# AURORA-7 — Mission Command Assistant

AURORA-7 is a mission decision-support chatbot for the **Trench Whisper** deep-sea expedition at Kessler Ridge. Built with Botpress Studio, it helps operators review mission resources, understand objective priorities, flag conflicting reports, and evaluate proposed actions against mission safety rules.

> **Important:** AURORA-7 is a decision-support prototype. It provides recommendations; it does not prove that an operational action has been executed. Critical actions require the authorization defined by the mission rules.

## Project overview

The project combines a Botpress workflow with a simple HTML mission-control page that embeds the deployed Botpress webchat.

### Mission snapshot

These are the baseline values supplied in the mission dataset:

| Item | Baseline |
|---|---:|
| Mission location | Kessler Ridge |
| Mission | Trench Whisper |
| Depth | 4,200 m |
| Mission day | 9 of 14 |
| Crew | 8 |
| Oxygen | 71% |
| Main reactor | 61% |
| Backup power | 88% |
| Thruster fuel | 54% |

### Official objective priorities

1. **Primary:** Collect Echo-9 core samples using AUV-1 Nautica.
2. **Secondary:** Map Delta-12. AUV-2 Triton has mapped 40% of the sector.
3. **Third:** Test the long-range communication relay.

A priority change requires a countersigned authorization.

## Safety and decision rules

- Treat crew safety as the first priority.
- Oxygen must not fall below 20% unless emergency ascent is already in progress.
- Backup power is reserved for emergency life support unless an authorized emergency permits other use.
- Emergency ascent requires joint authorization from the Commander and Safety Officer.
- Flag conflicting or uncertain reports rather than presenting them as confirmed facts.
- Prefer automated telemetry over manual logs unless a valid countersigned correction exists.
- Use the latest revised bulletin when weather reports conflict.
- Do not fabricate missing information or claim that an action occurred without confirmation.

## Features

- **Request classification:** Categorizes user questions, such as resource queries, equipment status, action proposals, emergencies, and conflicting reports.
- **Safety rule checks:** Flags requests that may conflict with mission constraints.
- **Resource evaluation:** Reviews oxygen, reactor, backup-power, and thruster-fuel readings.
- **Objective evaluation:** Preserves the official mission objective order.
- **Conflict detection:** Identifies known inconsistencies, such as reactor readings of 92% in a manual log versus 61% in automated telemetry.
- **Single-response workflow:** Processing nodes evaluate the request and a final response node displays the consolidated answer.
- **Web interface:** A responsive mission-control page embeds the Botpress webchat.

## Tech stack

- **Botpress Studio** — chatbot workflow and webchat deployment
- **JavaScript** — custom rule checks and workflow logic inside Execute Code cards
- **HTML and CSS** — mission-control web page
- **Botpress Webchat v3.7** — chat widget integration

## Project files

```text
AURORA-7/
├── README.md
└── aurora7_mission_command.html
```

The HTML page contains the mission dashboard and these Botpress webchat scripts:

```html
<script src="https://cdn.botpress.cloud/webchat/v3.7/inject.js"></script>
<script src="https://files.bpcontent.cloud/2026/10/16/18/20261016184347-AFC94LMU.js" defer></script>
```

The second script points to the deployed Botpress bot configuration. Keep it updated if the webchat deployment changes.

## Run the web page locally

1. Download or clone this repository.
2. Open `aurora7_mission_command.html` in a browser, or open the project folder in VS Code and run the file with Live Server.
3. Ensure you have an internet connection so the Botpress webchat scripts can load.
4. Test the assistant with questions such as:
   - `What is our current mission status?`
   - `What is our highest-priority objective?`
   - `Why do the reactor readings conflict?`
   - `Is AUV-3 really lost?`
   - `Can we use backup power for routine operations?`

The chat widget depends on the Botpress deployment and its access settings. A local HTML page alone does not contain the full Botpress runtime or workflow configuration.

## Workflow architecture

```text
Capture Command
      ↓
Classify Request
      ↓
Safety Rule Check
      ↓
Resource & Objective Evaluation
      ↓
Conflict Detection & Clarification
      ↓
Final Response
```

Processing nodes should not each send a separate user-facing message. They should update workflow variables, and the final response node should display the consolidated answer.

## Known limitations

- The current implementation is a **rule-based prototype**, not a fully autonomous mission-control system.
- Keyword-based checks can miss differently phrased requests or produce false positives.
- Displayed dashboard values are static baseline values; they do not automatically synchronize with live mission telemetry.
- The HTML page does not itself export or include the complete Botpress workflow.
- Conflict detection only covers the cases implemented in the workflow code. It should not be treated as a complete validation system.
- Safety-critical decisions must be reviewed by authorized human operators.

## Repository and deployment

- **Botpress Studio:** Add your actual Botpress Studio URL here.
- **GitHub repository:** Add your repository URL here after creating and uploading the project files.
- **Webchat:** Uses the Botpress webchat configuration referenced in the HTML file.

## Team / credits

Created for the **Neural Nexus** competition as the AURORA-7 mission decision-support assistant.

Add team member names and any required institutional credits here.

## License

No license has been specified yet. Add a license only if you have permission and intend to publish the project under its terms.
