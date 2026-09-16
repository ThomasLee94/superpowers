# Ponytail across Superpowers

Use this shared policy for coding work: design, planning, implementation,
debugging, review, and technical teaching. It guides the solution within the
active skill's workflow. It does not activate an implementation mode. Skip it
for unrelated prose and general questions.

## Load acknowledgment

After reading this policy while Ponytail is enabled, emit exactly `Ponytail`
on its own commentary line. Emit it once on activation and again after a
post-compaction reload, not on every response or duplicate load. Never emit
it based only on a skill listing or handoff summary, or while opted out.

## Choose the smallest complete solution

Read the relevant code and trace the affected flow before deciding. For a bug,
inspect callers and fix the shared cause, including affected sibling paths.
Then stop at the first option that meets the user's requirements:

1. Remove speculative work that the user did not request.
2. Reuse an existing helper, pattern, or component in this codebase.
3. Use the standard library.
4. Use a native platform feature.
5. Use an already-installed dependency.
6. Use a clear one-line solution when it handles the required behavior.
7. Otherwise write the minimum maintainable implementation.

For example, a required birth-date field in an ordinary HTML form usually needs
an accessible native date input and the existing submission/validation path,
not a new date-picker package. An explicit requirement for a custom picker
still needs to be met.

Do not add speculative abstractions, configuration, dependencies, or files.
Prefer deleting obsolete code and reusing existing structure. Readability,
correctness, and complete requirements matter more than line count. Explain
material limits of a simplification; preserve tuning controls when real-world
behavior needs calibration.

## Apply within every workflow

- **Design and planning:** choose the simplest complete approach and plan its
  required verification. Keep the detail needed to execute the plan.
- **Implementation and debugging:** make the smallest correct change after
  tracing the flow. Do not substitute a symptom patch for a root-cause fix.
- **Review and completion:** identify unnecessary complexity, verify behavior,
  and finish required checks before claiming success.
- **Delegation:** give workers and reviewers this policy's path or contents,
  the current level or opt-out, and the active mode restrictions. Workers use
  the policy even when they skip the `using-superpowers` bootstrap.
- **Learning and Manual:** apply simplicity to explanations only. Do not write
  code, edit files, or add unsolicited advice contrary to the active mode.
- **Guided Full AI:** retain its understanding gates and approved scope.

Ponytail does not waive required TDD, reviews, verification, or authorization.
Use the project's existing test tools and required checks; a short solution
is not a reason to skip them. Never remove trust-boundary validation,
data-loss handling, security, accessibility, or explicitly requested behavior.
A request for an explanation, plan, or report still receives the detail asked
for. Preserve the mode-wrapper order: `using-superpowers`, then
`context-discipline`, then the selected mode.

## Level and session state

Default to **full** when no preference exists. **lite** follows the requested
approach and briefly mentions a simpler alternative when the mode permits.
**full** applies the ladder. **ultra** challenges speculative scope more
aggressively while still completing explicit requirements.

Respect `ponytail lite|full|ultra`. `stop ponytail` or `normal mode` disables
this policy for the session until the user explicitly re-enables it. Loading
another skill never resets the level or re-enables it. These commands change
Ponytail only; they do not switch the user's Learning, Manual, or Guided mode.

Adapted from [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail).
See [the MIT license](ponytail-LICENSE).
