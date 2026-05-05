---
title: "Everything I Learned About Harness Engineering and AI Factories in San Francisco (April 2026)"
url: "https://escape.tech/blog/everything-i-learned-about-harness-engineering-and-ai-factories-in-san-francisco-april-2026/"
date: "Fri, 03 Apr 2026 17:46:58 GMT"
author: "Antoine Carossio"
feed_url: "https://escape.tech/blog/rss/"
---
<!--kg-card-begin: html-->
<div class="toc"></div>

<!--kg-card-end: html-->
<img alt="Everything I Learned About Harness Engineering and AI Factories in San Francisco (April 2026)" src="https://escape.tech/blog/content/images/2026/04/antoine-tech-blog-article.png" /><p>I spent the last week of March 2026 in San Francisco talking to CTOs, CPOs, and engineering leaders from companies of every size about how they actually build with AI agents today. I&apos;ve met solo founders of pre-series A startups,  I attended <a href="https://www.ycombinator.com/?ref=escape.tech" rel="noreferrer">Y Combinator</a> DevTool Day on March 27 and <a href="https://allthingsweb.dev/2026-03-31-all-things-web-workos?ref=escape.tech" rel="noreferrer">All Things Dev</a> on March 31, sat down with our advisors, and had dozens of conversations with founders and tool builders working at the frontier.</p><p>This document is what I brought back. It is a field report: what I learned, what I think matters, and where the industry seems to be heading. It is also the reference document my team and I will use to structure how we adopt these practices ourselves.</p><p>The audience are startup Founders, CTOs, CPOs, and senior engineers/product managers who are already past the &quot;what is an LLM&quot; stage and want to know what actually works in production. San Francisco is not the whole market, but it is often a leading indicator, and right now, the signal is strong.</p><p>The terms below are overloaded, so I use them narrowly:</p><ul><li><strong>Model / LLM:</strong> The base intelligence layer: tokens in, tokens out. On its own it does not remember sessions, read your repo, run commands, or verify its work. LLM is a specific technology of models.</li><li><strong>Harness:</strong> Everything around the model: instructions, context, tools, runtime, permissions, review loops, verification.</li><li><strong>Agent:</strong> A harnessed loop that can decide, act, observe, and continue until done or blocked.</li><li><strong>Vibe coding:</strong> A low-structure accept-and-iterate workflow. Useful for exploration and prototypes. Weak for correctness, repeatable delivery, and regulated workflows.</li><li><strong>AI factory:</strong> The org-level system that repeatedly turns intent into shipped work: issue framing, execution, review, deployment, telemetry, feedback. Partly engineering, partly product operations. AI Factory enables Vibe Coding at Scale.</li></ul><h1 id="1-whats-happening-and-what-it-means-%E2%80%94-tech-and-product-hot-takes-from-the-bay-area">1. What&apos;s Happening and What It Means &#x2014; Tech and Product Hot Takes from the Bay Area</h1><p>This section is intentionally opinionated. These are not consensus statements. They are recurring arguments, observed shifts, and directional predictions heard across both conferences and in every conversation I had that week.</p><h2 id="productivity-x10-since-december-2025">Productivity x10 since December 2025</h2><p>This was a common framing, but it should not be presented as an audited universal benchmark.</p><p>The charitable and defensible version is:</p><ul><li>The comparison several aggressive teams make is against December 2025 workflows, not against the pre-AI era.</li><li>In one quarter, models improved, harnesses improved, and orchestration improved at the same time.</li><li>The operating ceiling for one engineer with good agents feels materially different than it did a few months earlier.</li></ul><p>Treat &quot;10x&quot; as a directional claim from fast adopters, not as settled measurement science.</p><h2 id="startups-that-dont-adopt-will-die">Startups that don&apos;t adopt will die</h2><p>This is rhetorical, but the underlying claim is serious.</p><p>What the statement is really pointing at:</p><ul><li>The compounding advantage is not only code generation speed.</li><li>It is shorter build-review-ship-learn loops.</li><li>Teams that delay adoption entirely are not just slower at implementation; they are slower at learning.</li></ul><p>The real decision is not &quot;AI or no AI.&quot; The real decision is how much of the delivery loop remains human-led, and which work becomes agent-native now.</p><h2 id="the-rise-of-the-builder">The rise of the &quot;Builder&quot;</h2><p>The distinction between UI designer, UX researcher, product owner, and developer is collapsing. The recurring claim is that a new profile is emerging: the Builder, someone who owns the problem end-to-end and uses agents to cover the skills they lack.</p><ul><li>A PM with no frontend experience ships a working UI change.</li><li>A designer pushes code, not just mockups.</li><li>A founder prototypes a full feature before involving the team.</li></ul><p>The threshold for producing a first-pass pull request dropped so sharply that role boundaries stopped being the constraint. What matters now is not your job title but whether you can judge the output: does this diff belong in the product, is it correct, and is it coherent with everything else?</p><h2 id="the-bottleneck-is-moving-to-product-strategy">The bottleneck is moving to product strategy</h2><p>When implementation gets cheaper, bad strategy gets more expensive.</p><p>The reason is simple:</p><ul><li>Slow implementation used to absorb weak decisions.</li><li>Fast implementation removes that buffer.</li><li>Teams can now ship low-quality strategy much faster than before.</li></ul><p>This is why product quality now depends more on prioritization discipline, not less.</p><h2 id="the-startup-lifecycle-is-compressing">The startup lifecycle is compressing</h2><p>Agent-driven development compresses the time between:</p><ul><li>hypothesis</li><li>first product</li><li>early traction</li><li>version-two confusion</li></ul><p>You reach &quot;the first vision is basically built, now what?&quot; much faster.</p><p>That creates a new failure mode:</p><ul><li>the company has engineering leverage</li><li>but it does not yet have strategic clarity for what to do with it</li></ul><p>The result is feature volume without product direction.</p><h2 id="the-ide-is-dead">The IDE is dead</h2><p>Also rhetorical.</p><p>The stronger version is:</p><ul><li>The center of gravity is moving from the editor to the agent console.</li><li>Editors still matter.</li><li>But for multi-step work, the critical surface is now orchestration, visibility, review, status, and control over parallel sessions.</li></ul><p>The terminal wins whenever the work looks more like operating a system than typing code line by line.</p><h2 id="there-is-no-excuse-not-to-run-24-hours-a-day"><strong>There is no excuse not to run 24 hours a day</strong></h2><p>This follows directly from the previous point. If the compounding advantage is loop speed, then leaving agents idle overnight is a deliberate choice to slow that loop.</p><p>The argument is not about developer working hours. It is about asset utilization. Agents are infrastructure. Leaving them idle from 7pm to 9am is the equivalent of shutting down your CI pipeline every evening and restarting it in the morning.</p><p>The technical capability is no longer in question. Rakuten engineers ran Claude Code autonomously for seven hours on a 12.5-million-line codebase, achieving 99.9% accuracy. OpenAI published a Codex stress test that ran for 25 hours uninterrupted. These are logged runs, not demos.</p><p>What the strongest teams described:</p><ul><li>Engineers push work at end of day. Agents pick up test writing, code review, refactoring, and security scans overnight.</li><li>By morning, the codebase has been tested, reviewed, and flagged. The engineer&apos;s first task is triage, not implementation.</li><li>Nothing merges without human approval. The overnight cycle produces candidates, not commits.</li></ul><h2 id="do-we-need-fewer-pms-or-more">Do we need fewer PMs or more?</h2><p>This is still the wrong framing. Three product people for fifteen engineers is more than enough: possibly too many. The old ratio of 1 PM per 5-7 engineers assumed the PM was the translation layer between business intent and technical execution. When agents eliminate most of that translation cost, the PM&apos;s value shifts entirely upstream.</p><p>What changes is not mainly the headcount math. It is the job shape.</p><p>Work that shrinks:</p><ul><li>detailed ticket translation</li><li>backlog grooming as a communication bridge</li><li>implementation-level handholding</li></ul><p>Work that grows:</p><ul><li>market understanding</li><li>synthesis of customer signal</li><li>prioritization under much faster engineering throughput</li><li>deciding what not to build</li></ul><p>The PM role moves upstream. Less project management. More judgment.</p><h2 id="tasks-for-me-or-for-the-agent">Tasks for me or for the agent?</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Usually better delegated to agents</th>
<th>Usually still human-led</th>
</tr>
</thead>
<tbody>
<tr>
<td>Correctness sweeps</td>
<td>Where to start</td>
</tr>
<tr>
<td>Testing</td>
<td>Architecture</td>
</tr>
<tr>
<td>Error handling</td>
<td>Design direction and consistency</td>
</tr>
<tr>
<td>Debugging after reproduction</td>
<td>Abstraction boundaries</td>
</tr>
<tr>
<td>Boilerplate</td>
<td>Data model and API shape</td>
</tr>
<tr>
<td>Translation</td>
<td>Refactoring intent</td>
</tr>
<tr>
<td>Thoroughness</td>
<td>Product judgment</td>
</tr>
<tr>
<td>Repetitive implementation</td>
<td>Priority tradeoffs</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<p>The practical question is not &quot;can the model do this?&quot; It is &quot;what is the cost of a silent mistake here, and how cheaply can I detect it?&quot;</p><h2 id="model-choice-claude-46-vs-gpt-54-you-should-use-both">Model choice: Claude 4.6 vs GPT-5.4? You should use both</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Claude Opus 4.6</th>
<th>GPT-5.4 in Codex</th>
</tr>
</thead>
<tbody>
<tr>
<td>Better first-pass writing tone</td>
<td>Better implementation reliability</td>
</tr>
<tr>
<td>Better exploratory docs and explanation</td>
<td>Better verification, testing and final passes</td>
</tr>
<tr>
<td>Strong for frontend and UI taste</td>
<td>Strong for correctness-sensitive backend work</td>
</tr>
<tr>
<td>Strong for interactive computer use</td>
<td>Strong for long, tool-heavy execution in Codex</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<p>This is a heuristic, not a law. The real point is to stop treating model choice as a religion and start treating it as task routing.</p><p>The strongest proof point: on March 30, 2026, OpenAI open-sourced <code>codex-plugin-cc</code>: an official plugin that lets you invoke Codex directly from Claude Code. OpenAI shipping a plugin inside a competitor&apos;s tool confirms the moat is the harness, not the model. They&apos;d rather have Codex running inside Claude Code (collecting API charges per review) than have users not use Codex at all. The ecosystem is converging on interoperability, not lock-in.</p><p>The category is still moving fast. Overbuilding orchestration too early is an easy way to create your own internal product to maintain.</p><h1 id="2-harness-engineering-pillars">2. Harness Engineering Pillars</h1><p>Harness engineering is not &quot;writing a better prompt.&quot; It is the design of the system around the model so output quality depends less on raw model brilliance and more on structure.</p><h2 id="minimal-ai-factory-architecture">Minimal AI Factory Architecture</h2><p>If you strip the category down to its minimum useful shape, an AI factory has seven layers:</p><ol><li><strong>Intent capture:</strong> Product request, bug, support signal, roadmap item, or internal need.</li><li><strong>Spec or issue framing:</strong> A bounded instruction with constraints, acceptance criteria, and links to context.</li><li><strong>Context and instruction layer:</strong> Repo guidance, scoped rules, skills, docs, APIs, and environment facts.</li><li><strong>Execution layer:</strong> One or more agents editing code, calling tools, and running commands.</li><li><strong>Verification layer:</strong> Tests, static analysis, review agents, CI, and human sign-off.</li><li><strong>Isolation and permission layer:</strong> Worktrees, sandboxes, runtime isolation, secret boundaries, and approval flows.</li><li><strong>Feedback layer:</strong> Production telemetry, customer signal, review outcomes, and repeated failures fed back into rules, prompts, or process.</li></ol><p>If one of these layers is weak, the whole system regresses:</p><ul><li>No issue framing: fast implementation of vague intent.</li><li>No context discipline: expensive wandering.</li><li>No verification: vibe coding at scale.</li><li>No isolation: parallelism without control.</li><li>No feedback loop: repeated mistakes with better marketing.</li></ul><h2 id="instructions-rules-plugins-and-skills">Instructions, rules, plugins and skills</h2><p>The important instruction artifacts are:</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Artifact</th>
<th>Primary use</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>AGENTS.md</code></td>
<td>Shared project instructions across agent tools, auto-imported by Codex.</td>
<td>Standard format used by all providers but Anthropic</td>
</tr>
<tr>
<td><code>CLAUDE.md</code></td>
<td>Same as <code>AGENTS.md</code> auto-imported by Claude.</td>
<td>Can symlink <code>AGENTS.md</code></td>
</tr>
<tr>
<td><code>SKILL.md</code></td>
<td>Narrow, on-demand workflow or capability</td>
<td>Use for reusable task methods, not global policy</td>
</tr>
<tr>
<td><code>.cursor/rules/*.md</code></td>
<td>Cursor-specific structured rules</td>
<td>Useful when you need metadata or path scoping</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<p><strong>Plugin vs. Skill:</strong></p><p>A skill is a single <code>SKILL.md</code> file invoked via slash command (<code>/deploy</code>). A plugin is a directory with a <code>.claude-plugin/plugin.json</code> manifest that bundles multiple skills, hooks, agents, and MCP configs into a distributable package (<code>/plugin-name:command</code>). Use skills for personal workflows. Use plugins when sharing across teams.</p><p>&#x2139;&#xfe0f; Avoiding duplication between Claude Code and Codex: If you use both tools on the same repo, pick one source of truth:</p><ul><li><strong>Symlink (simplest):</strong> <code>ln -sf AGENTS.md CLAUDE.md</code>. Both filenames point to the same content. Zero drift.</li><li><strong>Reference:</strong> Put <code>@AGENTS.md</code> inside your <a href="http://claude.md/?ref=escape.tech">CLAUDE.md</a>. Claude Code reads the referenced file inline. Add Claude-specific instructions below.</li><li><strong>Pointer:</strong> Keep all shared instructions in <a href="http://agents.md/?ref=escape.tech">AGENTS.md</a>. Make <a href="http://claude.md/?ref=escape.tech">CLAUDE.md</a> a one-liner: <code>READ AGENTS.md FIRST</code>. Add overrides below.</li></ul><p>Concrete architecture: multi-tool project</p><pre><code>my-project/
&#x251c;&#x2500;&#x2500; AGENTS.md                          # Source of truth (shared instructions)
&#x251c;&#x2500;&#x2500; CLAUDE.md -&gt; AGENTS.md             # Symlink for Claude Code
&#x251c;&#x2500;&#x2500; .claude/
&#x2502;   &#x251c;&#x2500;&#x2500; CLAUDE.md                      # Claude-specific overrides (optional)
&#x2502;   &#x251c;&#x2500;&#x2500; rules/
&#x2502;   &#x2502;   &#x251c;&#x2500;&#x2500; testing.md                 # &quot;Always run pytest before committing&quot;
&#x2502;   &#x2502;   &#x2514;&#x2500;&#x2500; frontend.md               # &quot;Use Tailwind, no inline styles&quot;
&#x2502;   &#x2514;&#x2500;&#x2500; skills/
&#x2502;       &#x251c;&#x2500;&#x2500; deploy/
&#x2502;       &#x2502;   &#x2514;&#x2500;&#x2500; SKILL.md              # /deploy: push to prod workflow
&#x2502;       &#x2514;&#x2500;&#x2500; review/
&#x2502;           &#x2514;&#x2500;&#x2500; SKILL.md              # /review: pre-landing PR checks
&#x251c;&#x2500;&#x2500; .cursor/
&#x2502;   &#x2514;&#x2500;&#x2500; rules/
&#x2502;       &#x251c;&#x2500;&#x2500; base.md                    # Cursor-specific conventions
&#x2502;       &#x2514;&#x2500;&#x2500; api.md                     # Path-gated to src/api/**
&#x2514;&#x2500;&#x2500; src/
    &#x2514;&#x2500;&#x2500; api/
        &#x2514;&#x2500;&#x2500; AGENTS.md                  # Directory-scoped: &quot;All endpoints need auth&quot;
</code></pre><p>What happens at session start:</p><ul><li><strong>Claude Code</strong> loads: <code>CLAUDE.md</code> (-&gt; <a href="http://agents.md/?ref=escape.tech">AGENTS.md</a> via symlink) + <code>.claude/CLAUDE.md</code> + <code>.claude/rules/*.md</code> + skill names from <code>.claude/skills/</code>. When you type <code>/deploy</code>, the full <code>deploy/SKILL.md</code> loads into context.</li><li><strong>Codex</strong> loads: <code>AGENTS.md</code> at root. When working in <code>src/api/</code>, also loads <code>src/api/AGENTS.md</code>. The <code>.claude/</code> directory is ignored.</li><li><strong>Cursor</strong> loads: <code>.cursor/rules/*.md</code> + <code>AGENTS.md</code> at root. The <code>.claude/</code> directory is ignored.</li></ul><h2 id="keep-root-context-lean">Keep root context lean</h2><p>The best recent corrective on context-file enthusiasm came from ETH Zurich: detailed repository context often increases cost and can reduce task success when it adds unnecessary requirements.</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Use the root file for</th>
<th>Do not use the root file for</th>
</tr>
</thead>
<tbody>
<tr>
<td>Build, test, and lint commands</td>
<td>Generic clean-code slogans</td>
</tr>
<tr>
<td>Dangerous areas and non-obvious constraints</td>
<td>Style rules your formatter already enforces</td>
</tr>
<tr>
<td>Generated-code boundaries</td>
<td>README duplication</td>
</tr>
<tr>
<td>Migration or deployment cautions</td>
<td>Long architecture tutorials the agent can read elsewhere</td>
</tr>
<tr>
<td>Review and verification expectations</td>
<td></td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<p>What matters in practice:</p><ul><li>Keep one shared source of truth for durable project instructions.</li><li>Put tool-specific behavior only where it belongs.</li><li>Put local or path-specific constraints in narrower scopes, not in the root file.</li><li>Prefer on-demand skills for workflows that are occasionally needed, not always needed.</li></ul><h2 id="verification-beats-advice">Verification beats advice</h2><p>The rule of thumb is simple: if an error class recurs, stop describing it and start preventing it.</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Failure mode</th>
<th>Better fix</th>
</tr>
</thead>
<tbody>
<tr>
<td>Agent stops too early</td>
<td>Explicit build-verify-fix loop</td>
</tr>
<tr>
<td>Agent forgets tests</td>
<td>Pre-completion verification hook plus CI</td>
</tr>
<tr>
<td>Agent edits the wrong area</td>
<td>Scoped instructions and path-specific rules</td>
</tr>
<tr>
<td>Agent repeats the same bug class</td>
<td>Linter, static rule, or regression test</td>
</tr>
<tr>
<td>Agent misses architectural context</td>
<td>Better issue framing and smaller task boundaries</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<p>Example: LangChain published one of the clearest public examples of this pattern in February 2026: their coding agent moved from 52.8% to 66.5% on Terminal Bench 2.0 by changing the harness, not the model.</p><h2 id="review-loops-and-context-drift">Review loops and context drift</h2><p>Over time, agent-generated code drifts:</p><ul><li>Conventions soften</li><li>Dead code accumulates</li><li>Review comments repeat</li><li>Context files become stale</li></ul><p>Useful mitigations:</p><ul><li>Automated review on every meaningful PR</li><li>A second model for high-stakes review when possible</li><li>Periodic cleanup of root instruction files</li><li>Tracing and postmortems on agent failures</li><li>Converting recurring review comments into deterministic checks</li></ul><h2 id="example-coding-standards-in-agentsmd">Example: coding standards in <a href="http://agents.md/?ref=escape.tech">AGENTS.md</a></h2><h2 id="id"></h2><figure class="kg-card kg-code-card"><pre><code class="language-markdown"># Global Coding Standards

1. **YAGNI**: Don&apos;t build it until you need it
2. **DRY**: Extract patterns after second duplication, not before
3. **Fail Fast**: Explicit errors beat silent failures
4. **Simple First**: Write the obvious solution, optimize only if needed
5. **Delete Aggressively**: Less code = fewer bugs
6. **Semantic Naming**: Always name variables, parameters, and API endpoints with verbose, self-documenting names that optimize for comprehension by both humans and LLMs, not brevity (e.g., `wait_until_obs_is_saved=true` vs `wait=true`)
</code></pre><figcaption><p><span style="white-space: pre-wrap;">Source: </span><a href="https://allthingsweb.dev/2026-03-31-all-things-web-workos?ref=escape.tech" rel="noreferrer"><i><em class="italic" style="white-space: pre-wrap;">All Things Web @ WorkOS</em></i></a><i><em class="italic" style="white-space: pre-wrap;">, 31st of March 2026</em></i></p></figcaption></figure><p></p><h1 id="3-engineering-and-product-playbook-for-founders-and-teams">3. Engineering and Product Playbook for Founders and teams</h1><p>As mentioned in the hot takes, adopting Harness Engineering rapidly is a matter of life or death for companies, whatever their size is. As stated by Y Combinator, the trend show come from the top, the Founders, specifically those owning the Technical and the Product Roles, summarized as the CTO and CPO in the rest of the document. With that framing, the CTO controls how fast the org can ship. The CPO controls whether what ships is worth shipping. When agents make the CTO side 10x faster, every CPO mistake compounds 10x faster too.</p><h2 id="first-30-days">First 30 days</h2><p>Don&apos;t standardize on day one. Run agents on real work for two weeks and log every revert, rework, and rejection. Then build guardrails around the failure modes you actually saw: not hypothetical ones.</p><ul><li><strong>CTO:</strong> pick one harness (Claude Code or Codex, not both), add a minimal instruction file, require CI + automated review on all agent PRs, set a per-session cost alert.</li><li><strong>CPO:</strong> rewrite issue templates around intent and success criteria (agents execute literally), define an explicit &quot;do not build&quot; list for the quarter, pull customer signal into written artifacts.</li><li><strong>Together:</strong> review merged agent-assisted PRs weekly. Update process from real failures, not theory.</li></ul><h2 id="autonomy-tiers">Autonomy tiers</h2><p>Not all PRs need the same scrutiny. Start everything at full review. Promote downward only with evidence.</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tier</th>
<th>Examples</th>
<th>Required before merge</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Full autonomy</strong></td>
<td>Typo fixes, test additions, dependency bumps, boilerplate</td>
<td>CI + automated review</td>
</tr>
<tr>
<td><strong>Light review</strong></td>
<td>Feature work within established patterns, bug fixes with clear repro</td>
<td>CI + automated review + human skim (&lt; 5 min)</td>
</tr>
<tr>
<td><strong>Full review</strong></td>
<td>New endpoints, data model changes, auth/payment flows</td>
<td>CI + automated review + thorough human review</td>
</tr>
<tr>
<td><strong>Human-led</strong></td>
<td>Schema migrations, infra changes, security-critical paths</td>
<td>Human writes or co-writes. Agent assists.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="cadence">Cadence</h2><ul><li><strong>Weekly:</strong> review agent-authored regressions. Convert the top recurring mistake into a deterministic rule. Check whether issues were specific enough for agents to act without churn.</li><li><strong>Monthly:</strong> reclassify work across autonomy tiers. Remove dead rules and stale instructions. Audit feature velocity vs. feature impact: are we shipping noise?</li><li><strong>Quarterly:</strong> revisit the stack, permission model, cost structure, and PM staffing ratio.</li></ul><h2 id="metrics">Metrics</h2><ul><li>Lead time from issue to merged PR</li><li>Agent autonomy rate (% of tasks without human intervention)</li><li>Reopen and rollback rate on agent-authored changes</li><li>Wasted work rate (features reverted or unused within 30 days)</li><li>Issue clarity (% of issues agents can act on without clarification)</li><li>Monthly agent API cost per engineer</li><li>Cycle time from customer signal to shipped outcome</li></ul><p></p><h1 id="4-agent-factory-tooling">4. Agent Factory Tooling</h1><p>The point is not to install everything below. The point is to identify the bottleneck you actually have.</p><h2 id="the-winning-stack-pattern">The winning stack pattern</h2><p>This is the stack pattern I would describe as convergent, not mandatory:</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Layer</th>
<th>Standard choice</th>
<th>Why it keeps showing up</th>
</tr>
</thead>
<tbody>
<tr>
<td>Source of truth</td>
<td>GitHub</td>
<td>Claude Code authors ~4% of all public commits (~135K/day). Every agent tool produces PRs against GitHub repos. The entire agent factory pattern assumes Git and GitHub as the substrate.</td>
</tr>
<tr>
<td>Planning</td>
<td>Linear</td>
<td>Declared &quot;<a href="https://linear.app/next?ref=escape.tech">issue tracking is dead</a>&quot; (March 2026). Coding agents installed in 75% of enterprise workspaces. Deeplinks send issue context directly into Claude Code, Cursor, or Copilot as prefilled prompts. Agent work volume up 5x in three months.</td>
</tr>
<tr>
<td>Trigger and coordination</td>
<td>Slack</td>
<td>Non-engineers describe a problem or request in Slack; an MCP integration routes it to an agent that opens a PR. The barrier drops from &quot;file a ticket&quot; to &quot;describe it in a message.&quot;</td>
</tr>
<tr>
<td>Thinking and notes</td>
<td>Obsidian</td>
<td>Local markdown files that agents can read via MCP. Where intent gets structured before it becomes an issue or a prompt.</td>
</tr>
<tr>
<td>Runtime</td>
<td>Cloudflare Agents</td>
<td>Agents SDK, Durable Objects for state, Workflows for long-running tasks. Workers AI runs frontier models on-platform with 77% cost reduction on 7B token/day workloads vs. external API calls.</td>
</tr>
<tr>
<td>Observability</td>
<td>Sentry</td>
<td>Error tracking plus LLM-specific monitoring: agent runs, tool calls, token usage, conversation replay. Also maintains Claude Code agent skills (iterate-pr, code review): sits on both sides of the workflow.</td>
</tr>
<tr>
<td>Business signal</td>
<td>HubSpot</td>
<td>Customer feedback, support tickets, and sales conversations flow into the planning layer, giving agents business context for what to build next.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="terminal-orchestration">Terminal &amp; orchestration</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tool</th>
<th>Bottleneck it solves</th>
<th>Why it matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://cmux.com/?ref=escape.tech">cmux</a> / <a href="https://github.com/manaflow-ai/cmux?ref=escape.tech">repo</a></td>
<td>5+ agent sessions with no status visibility: constant tab-switching</td>
<td>macOS-native terminal with GPU-accelerated rendering (libghostty), per-agent green/yellow/red status indicators, git branch + PR status per workspace. Works with Claude Code, Codex, Gemini CLI.</td>
</tr>
<tr>
<td><a href="https://superset.sh/?ref=escape.tech">Superset</a> / <a href="https://github.com/superset-sh/superset?ref=escape.tech">repo</a></td>
<td>Parallel agents stepping on each other&apos;s files and git state</td>
<td>Git worktree isolation per agent. Each agent gets its own sandbox with no shared mutable state. Launched March 2026.</td>
</tr>
<tr>
<td><a href="https://github.com/garrytan/gstack?ref=escape.tech">Conductor</a></td>
<td>Running agents sequentially: throughput capped at 1x</td>
<td>Orchestration layer from gstack. Runs multiple Claude Code sessions in parallel, each in its own isolated workspace. Garry Tan regularly runs 10-15 parallel sprints.</td>
</tr>
<tr>
<td><a href="https://github.com/Bendzae/claude-manager?ref=escape.tech">Claude Manager</a></td>
<td>Losing track of which Claude session is running, waiting, or finished</td>
<td>Rust TUI that organizes sessions by project/task hierarchy. Live status indicators, diff preview without attaching, worktree lifecycle management. First published March 2026.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="spec-planning">Spec &amp; planning</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tool</th>
<th>Bottleneck it solves</th>
<th>Why it matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://openspec.dev/?ref=escape.tech">OpenSpec</a></td>
<td>Agents coding before the problem is well-defined: expensive iterations on work that doesn&apos;t match intent</td>
<td>Three-phase state machine (proposal, apply, archive). Agent must produce a ~250-line spec before writing code. Supports Claude Code, Cursor, Copilot, and 20+ tools. 27K+ stars, YC-backed.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="quality-review">Quality &amp; review</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tool</th>
<th>Bottleneck it solves</th>
<th>Why it matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/openai/codex-plugin-cc?ref=escape.tech">Codex plugin for Claude Code</a></td>
<td>Want a second opinion from a different model without leaving Claude Code</td>
<td>OpenAI&apos;s official plugin (open-sourced March 30, 2026). Adds <code>/codex:review</code> and <code>/codex:adversarial-review</code>. Uses the same harness as Codex itself. Runs in background using your ChatGPT subscription.</td>
</tr>
<tr>
<td><a href="https://docs.coderabbit.ai/?ref=escape.tech">CodeRabbit</a></td>
<td>PR reviews are slow (waiting for humans) or shallow (humans skim large diffs)</td>
<td>Always-on AI review on every PR. 13M+ PRs reviewed, 2-3M connected repos, 75M defects found. GitHub/GitLab/Azure DevOps/Bitbucket. Free tier available, SOC 2 Type II.</td>
</tr>
<tr>
<td><a href="https://taskless.io/?ref=escape.tech">Taskless</a></td>
<td>Agent keeps making the same class of mistake: you fix it once but nothing prevents it from reappearing</td>
<td>Converts code review corrections into deterministic syntax-tree rules (tree-sitter). Tag @taskless on a PR or file an issue; it creates a pass/fail rule that runs on every PR, in every IDE, on every run. Same result every time: not AI opinions, not prompt engineering. 25+ languages, zero instrumentation.</td>
</tr>
<tr>
<td><a href="https://github.com/getsentry/skills/tree/main/plugins/sentry-skills/skills/iterate-pr?ref=escape.tech">Sentry iterate-pr</a></td>
<td>Manual PR-fix-CI loops: developer re-runs checks, reads logs, applies fix, resubmits</td>
<td>Encodes the fix-CI-resubmit loop as a reusable skill. Agent detects failures, applies fixes, and re-runs checks without human intervention. Good reference for encoding any mechanical review iteration as a skill.</td>
</tr>
<tr>
<td><a href="https://github.com/garrytan/gstack?ref=escape.tech">gstack</a></td>
<td>No structured review/QA patterns beyond basic linting</td>
<td>Pattern library, not a package: role-based review, directory freezes, visual QA, pre-landing checks. Steal the patterns that match your failure mode, ignore the rest.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="context-memory">Context &amp; memory</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>
</th><th>Bottleneck it solves</th>
<th>Why it matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/thedotmack/claude-mem?ref=escape.tech">Claude-Mem</a></td>
<td>Sessions are stateless: everything the agent learned is lost when the session ends</td>
<td>Auto-captures session activity, compresses it with AI (agent-sdk), injects relevant context into future sessions. Adds dynamic, session-derived memory on top of static <a href="http://claude.md/?ref=escape.tech">CLAUDE.md</a> files. 44K+ stars.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="runtime-isolation">Runtime isolation</h2>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tool</th>
<th>Bottleneck it solves</th>
<th>Why it matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://coasts.dev/?ref=escape.tech">Coasts</a> / <a href="https://github.com/coast-guard/coasts?ref=escape.tech">repo</a></td>
<td>Two agents both running <code>localhost:3000</code>: port collisions block parallel testing</td>
<td>Each worktree gets its own containerized runtime with dynamic port assignment. Agnostic to AI providers. Single config file.</td>
</tr>
<tr>
<td>Docker-in-Docker / Docker Sandboxes</td>
<td>Need N isolated full-stack copies (app, database, workers) per agent</td>
<td>Docker Compose with per-agent port mappings. Docker Desktop 4.60+ supports Sandboxes in dedicated microVMs with network isolation. Heavier than Coasts but gives full stack isolation.</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h2 id="other-tools-worth-watching">Other tools worth watching</h2><p>Not all of these belong in a default stack. They are still worth tracking because they attack real bottlenecks.</p>
<!--kg-card-begin: html-->
<table>
<thead>
<tr>
<th>Tool</th>
<th>What it does</th>
<th>Why it&apos;s interesting</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://ghost.build/?ref=escape.tech">Ghost</a></td>
<td>Instant, ephemeral Postgres databases: agents spin them up like git branches. MCP/CLI only, no UI.</td>
<td>Standard SQL, no proprietary SDK. 100 hrs/month free. Pairs with Memory Engine, TigerFS, and Ox (sandboxed execution), all Postgres-native.</td>
</tr>
<tr>
<td><a href="https://fp.dev/?ref=escape.tech">fp</a></td>
<td>CLI-first, local-first issue tracking for Claude Code. <code>/fp-plan</code>, <code>/fp-execute</code>, <code>/fp-review</code>.</td>
<td>Local code review interface that sends inline comments back to the agent. No external service required. Mac desktop app.</td>
</tr>
<tr>
<td><a href="https://gitbutler.com/?ref=escape.tech">GitButler</a></td>
<td>Parallel branches in a single working directory via virtual branching: no worktree directories.</td>
<td>Assign file changes to different branches visually. All branches start from the same state, guaranteed to merge cleanly. Lighter than worktree-based isolation.</td>
</tr>
<tr>
<td><a href="https://finalrun.app/?ref=escape.tech">FinalRun</a></td>
<td>Vision-based mobile testing on real iOS/Android devices. Test cases written in plain English.</td>
<td>76.7% on Android World Benchmark (116 tasks): ahead of DeepSeek, Alibaba, ByteDance agents. ~99% flaky-free. 2-person startup.</td>
</tr>
<tr>
<td><a href="https://www.superbuilder.sh/?ref=escape.tech">SuperBuilder</a></td>
<td>Mac-native command center for Claude Code with per-message cost tracking, rate-limit queuing, and Branch Battle.</td>
<td>Free, BYOK. Tracks cost per thread/project, queues tasks through rate limits, compares two approaches side by side.</td>
</tr>
<tr>
<td><a href="https://agentsmesh.ai/?ref=escape.tech">AgentsMesh</a></td>
<td>Remote AgentPods for running multiple coding agents (Claude Code, Codex, Gemini CLI, Aider, OpenCode).</td>
<td>Self-hosted runners, gRPC + mTLS control plane, Kanban with ticket-to-pod binding. One dev built 965K lines in 52 days using it.</td>
</tr>
<tr>
<td><a href="https://github.com/timescale/ghostgres?ref=escape.tech">Ghostgres</a></td>
<td>Experimental Postgres fork from Timescale: &quot;there are no dumb queries, only dumb databases.&quot;</td>
<td>Early-stage (32 stars), but Timescale&apos;s broader push includes pgai (embeddings + NL-to-SQL in Postgres) and Ox (agent sandbox TUI).</td>
</tr>
</tbody>
</table>
<!--kg-card-end: html-->
<h1 id="-1"></h1><h1 id="5-references">5. References</h1><ul><li>Y Combinator DevTool Day (March 27): <a href="https://www.ycombinator.com/?ref=escape.tech">https://www.ycombinator.com/</a></li><li>All Things Dev (March 31): <a href="https://allthingsweb.dev/2026-03-31-all-things-web-workos?ref=escape.tech">https://allthingsweb.dev/2026-03-31-all-things-web-workos</a></li><li>Anthropic: Manage Claude&apos;s memory: <a href="https://docs.anthropic.com/en/docs/claude-code/memory?ref=escape.tech">https://docs.anthropic.com/en/docs/claude-code/memory</a></li><li>Anthropic: Claude Opus 4.6: <a href="https://www.anthropic.com/news/claude-opus-4-6?ref=escape.tech">https://www.anthropic.com/news/claude-opus-4-6</a></li><li>Anthropic: Claude Sonnet 4.6: <a href="https://www.anthropic.com/news/claude-sonnet-4-6?ref=escape.tech">https://www.anthropic.com/news/claude-sonnet-4-6</a></li><li>OpenAI: Introducing Codex: <a href="https://openai.com/index/introducing-codex/?ref=escape.tech">https://openai.com/index/introducing-codex/</a></li><li>OpenAI: Introducing GPT-5.4: <a href="https://openai.com/index/introducing-gpt-5-4/?ref=escape.tech">https://openai.com/index/introducing-gpt-5-4/</a></li><li><a href="http://agents.md/?ref=escape.tech">AGENTS.md</a> standard: <a href="https://agents.md/?ref=escape.tech">https://agents.md/</a></li><li>Cursor docs on rules and <a href="http://agents.md/?ref=escape.tech">AGENTS.md</a>: <a href="https://docs.cursor.com/en/context?ref=escape.tech">https://docs.cursor.com/en/context</a></li><li>ETH Zurich / SRI Lab: Evaluating <a href="http://agents.md/?ref=escape.tech">AGENTS.md</a>: <a href="https://www.sri.inf.ethz.ch/publications/gloaguen2026agentsmd?ref=escape.tech">https://www.sri.inf.ethz.ch/publications/gloaguen2026agentsmd</a></li><li>LangChain: Improving Deep Agents with harness engineering: <a href="https://blog.langchain.com/improving-deep-agents-with-harness-engineering/?ref=escape.tech">https://blog.langchain.com/improving-deep-agents-with-harness-engineering/</a></li><li>Linear changelog, deeplinks to coding tools: <a href="https://linear.app/changelog/2026-02-26-deeplink-to-ai-coding-tools?ref=escape.tech">https://linear.app/changelog/2026-02-26-deeplink-to-ai-coding-tools</a></li><li>Cloudflare Agents docs: <a href="https://developers.cloudflare.com/agents/?ref=escape.tech">https://developers.cloudflare.com/agents/</a></li></ul>
