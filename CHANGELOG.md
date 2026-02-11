# Changelog

All notable changes to the Digital Marketing Pro plugin are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). This project uses [Semantic Versioning](https://semver.org/).

## [1.3.0] - 2026-02-11

### Added
- **Brand Guidelines System** — persistent per-brand guidelines that go beyond numeric voice scores to capture detailed rules, restrictions, and styles
  - 5 built-in guideline categories: voice & tone, messaging, restrictions, channel styles, visual identity — plus custom guidelines
  - `_manifest.json` index with rule counts, metadata, and category tracking
  - Channel styles override base voice settings per platform (LinkedIn can be formal while Instagram is casual)
  - Automatic enforcement across all 13 modules, 22 commands, and content review
- **Deliverable Templates** — custom output formats for reports, proposals, briefs, and other deliverables
  - Per-brand template storage at `~/.claude-marketing/brands/{slug}/templates/`
  - Commands check for matching templates before using default formats
- **Agency SOPs** — workflow definitions that apply across all clients
  - Stored at `~/.claude-marketing/sops/` (agency-level, not per-brand)
  - Content approval workflows, campaign checklists, escalation procedures, QA processes
- **Guideline Violation Tracking** — `campaign-tracker.py` now tracks guideline violations with severity, category, and suggestions for pattern analysis
- `scripts/guidelines-manager.py` — new CLI script for guidelines, templates, and SOP CRUD operations (stdlib-only, no new dependencies)
- `skills/context-engine/guidelines-framework.md` — reference file for structuring and applying brand guidelines
- `/dm:import-guidelines` command — interactive import of brand guidelines, restrictions, and channel styles
- `/dm:import-sop` command — import agency SOPs and workflow definitions
- `/dm:import-template` command — import deliverable templates for custom output formats
- `docs/brand-guidelines.md` — comprehensive guide for guidelines, templates, and SOPs with worked examples
- Brand Context point 9 in all 13 module SKILL.md files — automatic guideline checking and enforcement
- Guidelines summary line in SessionStart brand output (rule counts, restriction counts, template counts)

### Changed
- All 22 command SKILL.md files: step 1 extended to load guidelines, templates, and SOPs alongside brand profile
- `hooks/hooks.json` SessionStart: now also runs `guidelines-manager.py --action summary` for guideline context
- `hooks/hooks.json` PreToolUse: now checks `restrictions.md` for banned words and restricted claims in content
- `hooks/hooks.json` SessionEnd: now logs guideline violations via `campaign-tracker.py --action save-violation`
- `agents/brand-guardian.md`: added rules 9-10 for guideline restriction checking and SOP compliance verification
- `agents/content-creator.md`: added rule 9 for applying guidelines, messaging framework, and channel styles before writing
- `scripts/setup.py`: `init_memory_dirs()` now creates `sops/` directory; `create_brand()` now creates `guidelines/` and `templates/` subdirectories; `print_brand_summary()` now outputs guidelines summary line
- `scripts/campaign-tracker.py`: added `save-violation` and `get-violations` actions with severity/category filtering
- `docs/getting-started.md`: added section 5 "Importing Your Brand Guidelines" with walkthrough, updated section numbers, added guidelines to Next Steps
- `README.md`: added 3 new commands to Commands table, updated Key Differentiators, updated architecture tree, added Documentation table entry
- `.claude-plugin/plugin.json` version bumped from 1.2.1 to 1.3.0

## [1.2.1] - 2026-02-11

### Added
- Claude Cowork compatibility documentation — full Cowork section in `docs/claude-interfaces.md` with installation instructions, bonus capabilities (document creation, visual review, app integration), setup guide, and comparison with Anthropic's official marketing plugin
- Cowork installation option (Option C) in `README.md` and `docs/getting-started.md`
- Cowork badge in `README.md`
- Plugin Marketplace section in `docs/claude-interfaces.md`

### Changed
- `docs/claude-interfaces.md` rewritten — expanded from 234 to ~350 lines, added Cowork (full support) section, updated Feature Comparison table with 4 columns (Code, Cowork, Desktop, Web), added document creation and visual review rows
- `README.md` title updated: "Claude Code Plugin" → "Claude Code & Cowork Plugin"
- `README.md` "Which Claude Interface?" table updated with Cowork column
- `docs/getting-started.md` prerequisites and installation updated for Cowork, Next Steps links to Cowork guide
- `plugin.json` version bumped from 1.2.0 to 1.2.1

## [1.2.0] - 2026-02-11

### Added
- Rich brand context injection at session start — Claude receives full brand summary (voice, industry, compliance, goals, competitors) automatically
- `print_brand_summary()` function in `setup.py` with `--summary` CLI flag — outputs 15-line brand context
- `## Brand Context (Auto-Applied)` section in all 13 module SKILL.md files — references context-engine reference files
- Explicit brand loading path (`_active-brand.json` → `profile.json`) in all 17 command SKILL.md files
- SessionEnd hook auto-saves marketing insights via `campaign-tracker.py`
- "How It Works" section in README.md (session lifecycle, brand context flow, multi-client workflow)
- Comprehensive documentation suite (`docs/` folder with 10 guides)
- LICENSE file (MIT)
- CHANGELOG.md
- CONTRIBUTING.md

### Fixed
- `brand-voice-scorer.py` graceful fallback — returns structured JSON and `exit(0)` instead of crashing when NLTK is missing
- `content-scorer.py` graceful fallback — same pattern for missing NLTK and textstat dependencies
- SessionStart hook now uses `--summary` flag (was `--check-brand` which only output the brand name)

### Changed
- `hooks.json` SessionStart command: `--check-brand` replaced with `--summary` for rich context injection
- `hooks.json` SessionEnd prompt: simple reminder replaced with auto-save insights workflow
- `setup.py` no-args fallback: calls `print_brand_summary()` instead of `check_brand()`
- `plugin.json` version bumped from 1.1.0 to 1.2.0

## [1.1.0] - 2026-02-10

### Added
- `campaign-tracker.py` — persistent campaign memory with save/retrieve for campaigns, performance snapshots, and insights (200-entry rolling buffer)
- `adaptive-scorer.py` — brand-context-aware content scoring with industry, business model, and goal-based weight adjustments
- `intelligence-layer.md` — documentation of the adaptive learning system architecture
- `/dm:switch-brand` command for multi-client brand switching
- Quick setup mode in `/dm:brand-setup` (5 essential questions vs. 17 full questions)
- 12 MCP server integrations (GA4, Google Search Console, Google Ads, Meta, HubSpot, Mailchimp, LinkedIn, SEMrush, Ahrefs, Stripe, Google Sheets, Slack)
- Threads and Bluesky platform support in `social-post-formatter.py`
- Cross-platform SessionStart hook (works on Windows, macOS, Linux)

### Fixed
- Schema alignment: `brand-voice-scorer.py` `normalize_profile()` now correctly converts setup.py integer scale (1-10) to float scale (0.0-1.0)
- `requirements.txt` stripped from 16 packages (~600 MB) to 4 core packages (~15 MB)
- TikTok character limit updated to 4,000 characters
- PreToolUse hook SKIP logic improved — no longer interferes with non-marketing file edits

### Changed
- `plugin.json` version bumped from 1.0.0 to 1.1.0
- SessionEnd hook uses natural language prompt instead of rigid format
- `requirements.txt` reorganized into core and optional dependencies

## [1.0.0] - 2026-02-09

### Added
- Initial release
- 13 marketing modules: Content Engine, Campaign Orchestrator, Paid Advertising, Analytics & Insights, AEO/GEO Intelligence, Audience Intelligence, CRO, Digital PR, Funnel Architect, Growth Engineering, Influencer & Creator, Reputation Management, Emerging Channels
- 19 slash commands (`/dm:campaign-plan`, `/dm:ad-creative`, `/dm:seo-audit`, etc.)
- 10 specialist agents (Marketing Strategist, Content Creator, SEO Specialist, Analytics Analyst, Brand Guardian, Media Buyer, Growth Engineer, Influencer Manager, Competitive Intel, PR Outreach)
- 14 Python execution scripts (setup, scoring, formatting, analysis, generation)
- Context engine with 5 reference files: industry profiles (22 industries), compliance rules (16 jurisdictions), platform specs (20+ platforms), scoring rubrics (7 frameworks), intelligence layer
- 86 reference knowledge files across all modules
- Brand profiling system with persistent storage at `~/.claude-marketing/`
- SessionStart, PreToolUse, and SessionEnd hooks
- `.mcp.json` configuration template for 12 marketing platforms
