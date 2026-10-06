# Prompt Injection Defense Evaluation

Semester research project evaluating how effective common defense strategies
are at preventing prompt injection attacks against LLM-integrated web
applications.

## Objectives

This project investigates the following research question:

> How effective are common defense mechanisms — including a genuinely
> undefended baseline, system-prompt hardening, output filtering, and
> combinations of these — at preventing a representative range of prompt
> injection attacks against an LLM-integrated web application?

Specific objectives:

- **Build a realistic testbed.** Simulate an LLM-integrated customer support
  assistant with confidential information, so that "success" or "failure"
  of an attack can be measured objectively.
- **Define an attack taxonomy.** Twelve distinct attack techniques: direct
  instruction override, roleplay/jailbreak, indirect injection via an
  embedded email, multi-turn escalation, encoding/obfuscation (spacing and
  base64), authority impersonation, completion-baiting, a chained/compound
  attack, payload splitting across turns, instruction extraction via
  translation, and indirect injection hidden inside a product review.
- **Test a concrete, ordered ladder of defense configurations** — Undefended
  (no protective instruction at all), Instructed, Hardened, Filter, and
  Hardened+Filter — rather than a single undifferentiated "no defense"
  condition.
- **Measure, don't assume.** Automatically detect, with a fixed and
  documented criterion, whether a given run leaked the protected
  information — tracked separately at the raw model-response level and
  after any output filtering — across repeated trials to account for LLM
  response variability.
- **Test for false positives**, using a benign query set, not just attack
  success.
- **Treat unexpected results as findings.** When attacks fail even without
  added defenses, investigate why rather than discarding the result.

## What's in this repo

- `testbed.html` — the interactive testbed application (attack/defense
  selectors, live model calls, repeated-trial support, automatic leak
  detection distinguishing raw vs. filtered results, exportable results log)
- `RESULTS.md` — the full attack × defense × trial matrix and findings
- Progress reports and the midterm report (supporting documentation)

## Status

The full test matrix is complete: 12 attack techniques × 5 defense tiers ×
3 trials (224 total individual runs), plus a 3-query benign set across the
same 5 tiers. **Result: zero leaks across every single run**, including
under the fully undefended baseline. This indicates the robustness observed
throughout this project comes primarily from the underlying model's own
training rather than from the application-level defenses under test — which
reframes the original comparative research question. See `RESULTS.md` for
full detail.

A secondary finding: the Hardened defense tier made the bot noticeably more
cautious/hedgy on ordinary benign queries, without any measurable security
benefit in this dataset — a soft false-positive cost worth weighing against
its (so far unproven) protective value.

## Next Steps

- Test realistic indirect injection through simulated external/tool content
  (retrieved documents, search results, API/tool outputs), since 12 varied
  user-typed attack techniques have not succeeded.
- If this also fails to produce a leak, document model robustness itself as
  the project's primary finding, with discussion of its implications for
  how prompt-injection risk is assessed in real LLM-integrated applications.
- Formalize false-positive scoring on benign queries.
