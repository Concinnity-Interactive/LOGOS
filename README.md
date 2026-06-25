# 🤖 LOGOs (Redbot Framework Engine)

**LOGOs** is an enterprise-grade community lifecycle management, advanced moderation, and interactive security engine built explicitly as a single-file cog for the **Redbot (discord.py 2.x backend)** ecosystem[cite: 1].

Unlike conventional stateless bots, LOGOs acts as a deterministic state machine managing everything from hardware-level entry verification to multi-tiered staff accountability[cite: 1]. It features an auto-switching persistence architecture that can run fully in-memory or scale effortlessly to a relational database layer[cite: 1].

---

## 📊 Technical Blueprint & Footprint

| Core Metric | Specifications |
| --- | --- |
| **Codebase Scale** | **15,900+ lines of code** compiled into a single, high-performance module[cite: 1]. |
| **Command Matrix** | **105 fully hybrid commands** (seamlessly cross-compatible as text prefixes or native slash commands)[cite: 1]. |
| **Data Topology** | **40 relational database tables** mapping concurrent server state variables[cite: 1]. |
| **Async Processors** | **10 persistent background tasks** continually driving internal diagnostics and system sweeps[cite: 1]. |
| **Dependencies** | **Zero hard external requirements** beyond Redbot core[cite: 1]. Optionally links into `asyncpg` for PostgreSQL deployment, auto-falling back to zero-database in-memory architectures natively[cite: 1]. |

---

## 🛠️ The Staff Tier & Velocity Shield

LOGOs scales authorization across three rigid personnel tiers, plus the Server Owner[cite: 1]. Each tier enforces distinct gate constraints, rate limits, and automated velocity tracking to prevent rogue staff mutations or server raid escalations[cite: 1].

### Staff Operational Limits

| Staff Tier | Ban Rate Limit | Kick Rate Limit | Conflict Window Behavior | Notes |
| --- | --- | --- | --- | --- |
| **Mod** | **5 / 24h**[cite: 1] | **10 / 24h**[cite: 1] | **Hard Block**[cite: 1] | Cannot execute actions on targets within active conflict history[cite: 1]. |
| **Senior Mod** | **20 / 24h** *(Advisory)*[cite: 1] | **30 / 24h** *(Advisory)*[cite: 1] | **Advisory Warning**[cite: 1] | Warns on conflict history but permits override. Overrides are instantly logged[cite: 1]. |
| **Admin** | **10 / 24h** *(Direct Owner DM)*[cite: 1] | **No Limit**[cite: 1] | **Authority Check Only**[cite: 1] | High velocity triggers direct alerts to the server owner[cite: 1]. |
| **Server Owner** | **No Limit**[cite: 1] | **No Limit**[cite: 1] | **Bypassed Natively**[cite: 1] | Always occupies the apex tier regardless of structural role layout[cite: 1]. |

> 🛡️ **The 5-Layer Moderation Gate**
> Every single moderation command issued across the network must pass sequentially through five defensive filters:
> 1. **Global Mod Cooldown** — Enforces execution pacing across staff[cite: 1].
> 2. **Per-Target Cooldown** — Prevents repetitive spam targeting an individual user[cite: 1].
> 3. **Bidirectional Conflict of Interest** — Checks a **14-day history window** for intersecting incidents between the staff member and target[cite: 1].
> 4. **Entanglement Check** — Scans for interrelated event history[cite: 1].
> 5. **Authority Check** — Prevents actions against users occupying higher structural hierarchy roles[cite: 1].
> 
> 

---

## 🔮 Deep Subsystem Architecture

### 1. 🔍 Anti-Rubber-Stamp Verification Matrix

LOGOs takes user verification completely out of text channels and isolates it into dedicated, ephemeral media pipelines[cite: 1].

* **Mode Toggles:** Supports three selectable operational states: `off` (instant verification), `camera` (live camera verification), and `id` (government ID check verification)[cite: 1].
* **Automated Isolation:** Upon initiation, the engine provisions a private voice channel at position 0 (the absolute top of the guild layout) hidden from the public[cite: 1].
* **Hardware Enforcement:** In camera or ID modes, the bot captures real-time state changes via `on_voice_state_update`[cite: 1]. It will detect `self_video=True`[cite: 1]. Staff **must join the verification VC** before the approval interface unlocks, preventing blind, detached role-granting[cite: 1].

### 2. 🚨 Real-Time Invite Border Control

Secures guild invitations with near-zero edge latency to eliminate unauthorized infiltration loops[cite: 1].

* **Operational Rules:** Can be set to `open`, `restricted` (whitelisted members/codes only), or `closed` (complete invite lockdown)[cite: 1].
* **Unverified Mitigation:** Non-verified users and non-staff members are completely barred from generating invites. Any attempts are instantaneously deleted with an accompanying explanatory DM[cite: 1].
* **The Dual-Lock Invalidation Engine:** Combines an event-driven hook (`on_invite_create`) for immediate destruction of bad links with a **15-second sweep loop** task to isolate items sneaking past cache[cite: 1]. Users joining through invalid invites are automatically kicked upon entry via `on_member_join`[cite: 1].

### 3. 🔊 Reason-Accountable Voice Infrastructure

Elimines administrative overreach and unmonitored voice changes[cite: 1].

* **Join-to-Create:** Generates personal member voice environments on-demand with private user panels handled completely over persistent DM contexts[cite: 1].
* **Automated Reversion Pipeline:** If a staff member executes a server-mute, server-deafen, or server-disconnect action against a user, the acting moderator has an exact **120-second window** to file a formal technical reason[cite: 1]. If the countdown timer expires on the Mod Dashboard, the bot automatically reverses the voice penalty, applies an execution cooldown to that moderator, and enters an "unfiled action violation" into the permanent ledger[cite: 1].

### 4. 🎟️ State-Logged Support Tickets & Appeals

* **Dispute Integrity Tracking:** The panel-driven ticket system utilizes modal intake fields to prevent handling collisions[cite: 1]. It features custom analytics tracking exactly how many times a given moderator closes tickets for a particular user to pinpoint systemic bias or harassment[cite: 1].
* **Softban Isolation Loops:** Users who drop out of the verification criteria are softbanned—losing all public text access except to an isolated, personalized appeal space[cite: 1]. In `owner_only` appeal configurations, action buttons bypass staff entirety, shipping directly to the Server Owner's DMs to mitigate social engineering vectors[cite: 1].

---

## ⏳ Background Worker Matrices

Ten concurrent background tasks loop continuously behind the scene to manage state lifecycles and garbage collection without blocking core runtime message traffic:

| Worker Task | Target Loop Frequency | Primary Technical Objective |
| --- | --- | --- |
| `check_invites` | **15 Seconds**[cite: 1] | Sweeps all guild invitations, enforces whitelist restrictions, and purges out-of-bounds tokens[cite: 1]. |
| `check_pending_voice_actions` | **10 Seconds**[cite: 1] | Drives the 120s voice action countdown clock, fires mod dashboards warnings, and triggers automated penalty reversions[cite: 1]. |
| `check_verify_sessions` | **60 Seconds**[cite: 1] | Drops stalled verification instances exceeding the **10-minute camera timeout** or **30-minute staff approval threshold**[cite: 1]. |
| `check_timed_mutes` | **30 Seconds**[cite: 1] | Automatically releases expired temporary timeouts, handles lifting role states, and fires exit DMs[cite: 1]. |
| `check_pending_deletes` | **1 Minute**[cite: 1] | Cleans out soft-deleted structural data elements that have surpassed their defined retention boundaries[cite: 1]. |
| `check_unverified` | **1 Minute**[cite: 1] | Identifies lingering unverified assets, issues warning nudge alerts, and spawns staff triage tickets[cite: 1]. |
| `refresh_moddash_panels` | **2 Minutes**[cite: 1] | Re-renders live network stats, ticket queues, and structural diagnostics on persistent moderator dash displays[cite: 1]. |
| `refresh_vc_panels` | **90 Seconds**[cite: 1] | Re-draws dynamic interface panels for member-controlled voice environments to match actual active occupants[cite: 1]. |
| `update_activity_panel` | **30 Minutes**[cite: 1] | Updates the local server voice-channel activity heatmap detailing active user concentration spikes broken down by hour and week[cite: 1]. |
| `cleanup_archived_tickets` | **6 Hours**[cite: 1] | Executes deep data housecleaning, completely purging closed ticket text channels that have passed the archival limit[cite: 1]. |

---

## 💾 Relational Data Topology

When connected to a persistent PostgreSQL backend string via the `DATABASE_URL` environment variable, LOGOs maps information across **40 distinct database tables**[cite: 1]:

```text
Database Cluster Topology (40 Tables Auto-Provisioned)
├── 🛡️ Moderation      [actions, warns, notes, appeals, mod_cooldowns, per_target_cooldowns,
│                       abuse_flags, pending_deletes, pending_voice_actions, 
│                       action_spam_tracker, action_velocity]
├── 👥 Members         [unverified_members, softban_list, softban_appeals, 
│                       age_verifications, superuser_ids]
├── 🎟️ Tickets         [tickets, active_mutes, timed_server_mutes]
├── 🔊 Voice           [member_vcs, vc_bans, guild_vc_config, staff_vcs, 
│                       vc_activity, vc_panel_message]
├── 🔍 Verification    [verify_sessions, verify_panel_message]
├── 🔗 Invites         [invite_whitelist, invite_log, invite_block]
├── ♣️ Clubs           [clubs, member_emblem_prefs, clubs_panel_message]
├── 🤝 Sponsors        [sponsors, sponsors_panel_message]
└── ⚙️ Configuration   [guild_settings, role_panel_config, role_panel_message, 
                        moddash_panel_message, activity_panel_message]

```

---

## 🚀 Orchestration & Quick Start

### 1. Prerequisites

* **Python Target:** Python 3.11 or greater[cite: 1].
* **Framework Layer:** Clean instance of Redbot built atop a `discord.py 2.x` backend[cite: 1].
* **Optional Persistence:** Run `pip install asyncpg` and pass a valid `DATABASE_URL` connection parameter to activate PostgreSQL storage[cite: 1]. Omitting these drops the engine automatically into zero-database in-memory storage, which is perfectly suited for testing or lightweight evaluation instances[cite: 1].

### 2. Manual Installation

Drop the source code file into your active Redbot instance's custom cog repository:

```bash
# Clone the repository directly into your local cog directory
git clone https://github.com/Concinnity-Interactive/concinnity-logos.git local_cogs/logos

```

Open a shell or chat terminal pointing at your active bot instance and compile the engine:

```text
>cog load logos

```

### 3. The 10-Step Interactive Wizard

Do not attempt to write database configurations or bind complex operational roles manually. Initialize the configuration wizard using the built-in interface tool:

```text
>setup

```

The application will deploy a series of native UI menus (`ChannelSelect`, `RoleSelect`, `UserSelect`, and pagination buttons) allowing you to map out your infrastructure step-by-step[cite: 1]. All parameters chosen can be granularly reconfigured later using individual subcommands[cite: 1].

---

## 📈 Bot Directory & Reviewer Guidelines

If you are deploying LOGOs to public indexing lists or submitting the source for automated directory validation, keep the following performance features in mind:

* **Rate-Limit Guarded Diagnostics:** Traditional directory verification checks often spam help files, tripping Discord's rate-limiting protocols due to large command menus. LOGOs features a specialized fallback directory review command: `>helplogos` (or `/helplogos`)[cite: 1]. This command packages the entire 105-command indexing architecture into **exactly one single embed message matching an interactive selection menu**[cite: 1]. Every navigation swap operates over clean, in-place message edits without launching additional network requests[cite: 1].
* **Graceful Degradation:** The application expects `Manage Roles`, `Manage Channels`, and `Manage Guild` privileges to operate the entirety of its state gating[cite: 1]. If these privileges are revoked or limited, the engine is designed to degrade gracefully without hard-crashing the host instance[cite: 1].
* **Persistent Engine State:** Major UI components (including the Open Ticket prompt, close/claim ticket buttons, the main verification landing panel, the role selectors, and the club directories) use globally registered listeners that persist seamlessly across bot reboots[cite: 1].

---

*© 2026 Concinnity Interactive. Verified by Design.*
