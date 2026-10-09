Copyright (C) 2026 Andrew Nelson

# Sheikah Lens

**A private, gameplay aware Special Agent for *The Legend of Zelda: Breath of the Wild*.**

This is the fairy Link always wanted.

Sheikah Lens integrates an intelligent gameplay assistant directly with Cemu. The player can ask a question, share the current game view, or request situational analysis without leaving Hyrule. The Special Agent receives each deliberate request through an independently developed backend, draws on an expansive proprietary Hyrule intelligence library, and returns its response through a compact in game overlay. The result is direct access to a powerful in game AI model capable of complex, multistep reasoning across the current screen, canonical game knowledge, and the player's own campaign history.

Lens is a contextual gameplay intelligence system rather than a generic chat overlay. It can investigate a puzzle, identify what is visible on screen, recall campaign history, explain a mechanic, and recommend a next step. Its guidance follows a discovery first philosophy: preserve exploration, offer useful hints before explicit solutions, and distinguish verified facts from interpretation.

## The experience

| Capability | In play |
| --- | --- |
| **Special Agent** | A dedicated, highly capable AI reasoning agent maintains context for the running Lens session and can solve complex, multistage gameplay questions. |
| **Manual Look** | Capture the current Cemu view on demand and send that exact image with a request. |
| **In game questions** | Type into the slim overlay input bar, optionally attach the current view, and continue playing while the response is prepared. |
| **Campaign knowledge** | Search a source governed Hyrule intelligence library and the current campaign record with exact domain precision. |
| **Persistent evidence** | Retain ordered requests, source images, complete replies, timing data, and campaign tool activity for review. |
| **Adjustable overlay** | Move and resize the panel, select an appearance preset, tune colors and opacity, and decide whether the player's own messages appear. |
| **Experimental dictation** | Push to talk capture and request routing are implemented; transcription quality is still being replaced and validated. |

The current runtime is deliberately controlled by the player. Lens does not take periodic screenshots or initiate hidden background conversations. Every active request begins with an explicit player action.

## An independent Special Agent

The primary Lens route is not a macro wrapped around a desktop chat. It is a self contained application pipeline that owns the Special Agent's session, request queue, evidence, tools, and reply delivery.

At launch, Lens starts a private backend process and creates one ephemeral agent session for that run. The selected model, reasoning level, instruction set, tool definitions, and application build identity are fixed for the session. Typed questions, deliberate screenshots, and accepted speech transcripts enter one FIFO request stream, preserving the exact association between words, images, tool activity, and replies.

The backend is designed around strong ownership and failure boundaries:

- One Lens process owns the active queue and agent session.
- Intentional requests reserve their position before image capture or transcription completes.
- Each turn is matched to its exact session and request identity.
- Uncertain submissions are held for review instead of being resent automatically.
- Canceled work cannot be revived by a late callback.
- Complete responses are saved before the overlay publishes them.
- Restarting Lens creates a new session and never replays an old queue.

This architecture keeps normal interaction inside the game experience. It does not require selecting, activating, or routing each request through a separate desktop conversation.

## The Hyrule intelligence library

The information system behind the Special Agent is one of Sheikah Lens's defining technical achievements: a comprehensive, proprietary AI retrieval library engineered specifically for *Breath of the Wild*. It transforms an enormous body of game knowledge and campaign evidence into a governed intelligence system the agent can query with record level precision.

This is far more than a bundled walkthrough, a folder of notes, or a general purpose search index. The library is organized around explicit source authority, canonical identifiers, typed domains, provenance controls, relationship traversal, exact placement data, and a discovery first spoiler boundary. Its retrieval router selects the smallest authoritative record set for each question, giving the Special Agent encyclopedic reach without flooding a turn with irrelevant material.

Its coverage spans:

- quests, prerequisites, triggers, characters, rewards, and relationship chains;
- shrines, towers, settlements, facilities, named places, and fixed world placements;
- combat systems, weather, cooking formulas, mechanics, and equipment statistics;
- weapons, bows, shields, armor upgrades, shops, inventory, materials, and drops;
- creatures, enemies, objects, actor identities, and enemy health;
- story events, memories, Divine Beast progression, and campaign specific history.

The result is a knowledge layer capable of moving from a visible object to its mechanics, drops, uses, vendors, related characters, quest dependencies, and known world placements, or from a campaign question to the exact supporting event, without confusing those different forms of evidence. Retrieval remains narrow by design: the Special Agent requests the exact domain and record needed, improving relevance, limiting accidental spoilers, and preserving the distinction between canonical facts, observed campaign evidence, and strategic recommendations generated for the current situation.

### Reasoning over evidence

The library supplies authoritative evidence; the in game model supplies synthesis. Together they allow the Special Agent to interpret a screenshot, connect entities across multiple knowledge domains, trace quest and prerequisite chains, compare equipment or cooking options, reason through puzzles, reconstruct relevant campaign history, identify uncertainty, and recommend actions appropriate to the current context.

Because the reasoning model receives the exact supporting records alongside current campaign context and visual evidence, it can perform tasks that a static guide, isolated search result, or generic vision chatbot could not reliably handle alone. The model can work through a problem step by step while Lens keeps provenance, campaign authority, and spoiler boundaries explicit.

The knowledge system separates three complementary layers:

| Layer | Role |
| --- | --- |
| **Canonical reference corpus** | Read only factual knowledge governed by explicit sources about the game world and its systems. |
| **Campaign state** | A compact, rebuildable view of the current playthrough used for continuity and context. |
| **Campaign event ledger** | Append only evidence authority for discoveries, progress, rewards, and corrections. |

Inspectable current evidence and direct player statements outrank stored state. Missing information remains unknown rather than being guessed. Strategy is derived at answer time and is never misrepresented as a database fact.

## Campaign continuity with bounded authority

The Special Agent can maintain campaign continuity, but it cannot freely edit the knowledge system. Lens exposes only three guarded operations:

- retrieve a compact, verified campaign context;
- look up an exact record within an explicit domain;
- submit a structured campaign event through the existing transaction helper.

The canonical factual corpus remains read only. Confirmed campaign updates use an event first transaction, deterministic state rebuild, replay verification, and retained evidence from before and after the change. Tool identity, arguments, results, ledger fingerprints, and attributed events are captured with the originating turn.

This boundary gives the Special Agent enough authority to remember genuine progress without granting broad write access to the reference database or application source.

## Request flow

![The Lens data flow](https://github.com/Cobblecat/The-Lens/blob/main/Data%20Flow.png)

Capture, input ownership, cancellation, and the visible overlay remain local to the workstation. The Special Agent handles finite conversational turns through its private backend session. No extra hosting layer is required for the current single workstation design.

## Using Independent Lens

This is the primary development route.

1. Start *Breath of the Wild* in Cemu.
2. Open **Launch Independent Lens.vbs**.
3. Wait for Lens to connect using the existing Codex sign in.
4. Use the controls shown in Lens settings or in the optional overlay guide.

| Control | Behavior |
| --- | --- |
| **Manual Look** | Captures the verified Cemu window once and sends the image to the Special Agent. |
| **Text bar** | Sends exact typed words, with the current view attached when that option is enabled. |
| **Hold to Dictate** | Records while held and submits an accepted transcript; transcription remains experimental. |
| **Attach current view** | Adds a fresh Cemu capture to a typed or spoken request. Manual Look always includes an image. |

The text bar clears only after the request has been safely recorded and any requested screenshot succeeds. Pressing Escape returns keyboard focus to the game while preserving an unfinished draft.

Independent Lens maintains its own conversation. Requests and replies are not forwarded to whichever conversation happens to be visible in the desktop application. Quitting Lens closes its backend and speech helper while preserving the completed session archive.

## Desktop paired route

The original desktop paired route remains available through **Launch Lens.vbs**. It binds a Lens record queue to a deliberately selected desktop task and preserves the same ordered photo, text, and reply records. This route is retained for compatibility and development comparison; **Launch Independent Lens.vbs** starts the self contained Special Agent instead.

Pairing does not switch modes. To change routes, quit Lens and open the appropriate launcher. An existing draft or uncertain request should be reviewed before changing sessions.

## Overlay and presentation

Quiet Glass is the current interface baseline. It prioritizes the newest completed reply while keeping controls and status secondary.

- Drag the top strip to move Lens.
- Drag the lower right grip to resize it.
- Use **Overlay → Show hotkey guide** to reclaim space when the guide is not needed.
- Use **Overlay → Show my messages** to show or hide the player's recent submitted messages.
- Use **Overlay → Show Lens in screenshots** when an external screen capture should include the Lens interface.
- Adjust the appearance preset, colors, text, and entire window opacity in Settings.

Lens captures only the verified Cemu window for agent input, so the overlay is excluded from Manual Look images. External screenshots can include the overlay when the presentation option is enabled and the chosen capture method covers both windows.

## Evidence, observability, and evaluation

Independent Lens retains a detailed local record of its operation:

- exact prompts and accepted transcripts;
- input image hashes, dimensions, and durable source files;
- full responses and the text actually displayed in the overlay;
- queue, dispatch, provider, and display timing;
- model, reasoning, policy, instruction, tool schema, and build identity;
- every campaign tool attempt, result, ledger fingerprint, and attributed event;
- clean shutdown checkpoints and append only study indexes.

This evidence supports regression analysis, delayed human review, reproducible model comparisons, and campaign integrity audits. A session's model assignment remains fixed, and changes to the inference build create a distinct evaluation cohort. Historical observations are not silently mixed with newly instrumented results.

Session records are private local data ignored by Git. They are not a substitute for a separately managed, checksummed backup.

## Current status

The manual baseline controlled by the player is implemented and validated end to end:

- verified Cemu window capture;
- independent image and text turns through the Lens owned backend;
- ordered typed, photo, and speech request handling;
- complete reply delivery to the overlay;
- durable records and strict monitoring evidence;
- guarded campaign retrieval and persistence tools;
- move, resize, focus, settings, and presentation behavior.

Voice acquisition and request routing work, but the current Windows speech recognizer has not met transcription quality requirements on clear retained recordings. Dictation remains experimental until a replacement is selected and validated.

The former Watch feature has been removed completely. There is no dormant scheduler, periodic capture loop, hidden inactivity trigger, or automatic model cadence. The original eye and ruby light artwork remain only as reusable presentation components.

Scout is a future mission oriented mode, not a renamed Watch feature. It will require explicit activation, a defined objective, bounded duration and budget, visible state, player request preemption, rejection of stale results, and no automatic restart resumption. It will be evaluated against the same player controlled baseline; an inconclusive result favors the manual experience.

## Recent field captures

![Link gliding across the Hebra mountains](docs/showcase/hebra-glide.png)

*A Manual Look during a glide across Hebra's snowbound peaks.*

<details>
<summary>More from the latest Independent session field tests</summary>

![Link using Magnesis to complete a cliffside block puzzle](docs/showcase/magnesis-puzzle.png)

*A live Magnesis puzzle captured at the decisive move.*

![A Korok appearing after the cliffside puzzle is solved](docs/showcase/korok-discovery.png)

*The resulting Korok discovery, retained as exact campaign evidence.*

![Rin Oyaa Shrine activating at night in the snow](docs/showcase/rin-oyaa-shrine.png)

*Rin Oyaa Shrine activating after a search through the Hebra snowfields.*

</details>

These are unedited Cemu captures retained by Lens during recent Independent sessions. They show the exact game views supplied as evidence to the Special Agent. Because gameplay input deliberately excludes the overlay, they do not simulate a composite interface screenshot.

## Privacy and repository boundaries

Sheikah Lens is a private Windows development project. The repository contains the application, explicit tests, and development documentation. It does not include:

- the proprietary Zelda retrieval database or campaign ledgers;
- private session records, prompts, replies, screenshots, or audio evidence;
- credentials or Codex account data;
- the local Python environment, Cemu installation, or runtime logs specific to the machine.

The current build assumes the Lens repository is located inside its local Zelda data workspace and that Cemu is installed on the same workstation. It is not yet packaged as a portable installer.

## Local development

The runtime uses Python 3.12 and the existing **.venv**. Run only the explicit tests relevant to a change. Do not use automatic test discovery: importing **test_clipboard.py** changes the real system clipboard.

~~~powershell
.\.venv\Scripts\python.exe -m unittest test_frame_difference test_manual_baseline test_lens test_session_pause test_paste_menu test_session_records test_owned_backend test_owned_engine -v
~~~

The primary implementation is organized around:

- **capture.py**: verified Cemu window capture;
- **engine.py** and **owned_engine.py**: local request coordination, FIFO ordering, cancellation, and overlay publication;
- **codex_transport.py** and **owned_backend.py**: the private Special Agent session and finite turn protocol;
- **campaign_gateway.py** and **campaign_permissions.py**: bounded retrieval and campaign persistence;
- **session_records.py** and **model_study.py**: durable evidence, timing, checkpoints, retention, and evaluation;
- **overlay.py** and **settings_ui.py**: in game presentation and configuration;
- **speech.py** and **speech_host.ps1**: the current experimental dictation adapter.

See [HANDOFF.md](HANDOFF.md) for current engineering priorities, [SCOUT_PRODUCT_DECISION.md](SCOUT_PRODUCT_DECISION.md) for the governing Scout boundary, and [CURRENT_DATA_FLOW_AND_VPS.md](docs/CURRENT_DATA_FLOW_AND_VPS.md) for the implemented architecture and hosting analysis.
