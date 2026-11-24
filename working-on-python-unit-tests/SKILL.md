---
name: working-on-python-unit-tests
description: How to work on Python unit tests. Use when creating, editing, or refactoring Python test files, including incidental test changes made as part of a broader task.
---

# Working on Python Unit Tests

Use when creating, updating, editing, or refactoring Python tests.

Follow these instructions strictly.

---

## Pre-flight Checklist

- Read nearby tests and follow their established structure, naming, and patterns.

---

## Rationale

- Behavior-focused tests are more resilient to implementation changes and verify what users of the code can observe.
- Testing behavior at its owning layer avoids redundant coverage and makes failures easier to diagnose.
- A clear Arrange–Act–Assert structure keeps each test's setup, behavior, and verification easy to understand.
- Parametrizing only cases with the same structure keeps variations easy to compare without hiding meaningful differences.
- Splitting oversized test modules by concern keeps tests navigable while preserving meaningful ownership.

---

## Strict Rules

You must:

- Use classes only for meaningful shared state or setup boundaries.
- Test observable behavior through supported interfaces, not local implementation helpers.
- Follow Arrange–Act–Assert (AAA):
  - Arrange: declare fixtures, prepare inputs and test data, and establish required context.
  - Act: perform the focused operation or sequence of steps needed to exercise one behavior under test.
  - Assert: verify the observable result or effect.
- Separate the Act from Arrange and Assert with a blank line; do not add blank lines within the Act.
- Assign returned values before asserting; do not put the call under test directly in an assertion.
- Prefer existing fixtures, helpers, and assertion utilities over duplicating test code.
- For multiline strings, use indented triple-quoted strings rather than `\n` escapes; use `dedent()` when indentation must be removed.
- Use test framework helpers when asserting floating-point values:
  - stdlib unittest: `self.assertAlmostEqual()`
  - pytest: `pytest.approx`
- Prefer `assert` to narrow types, instead of using `Any`, `object`, or `cast()`.
- In tests that intentionally pass a value of the wrong type or an invalid value, prefer targeted `# type: ignore[...]` suppressions over `cast()`.
- Ensure that tests don't issue Python warnings. You can use framework tools/options to ignore `FutureWarning`.

You must not:

- Add brittle tests.
- Assert on exact strings, log messages, or exception messages; unless they're part of the contract.
- Test local implementation code.

---

### Test Parametrization

- Use framework helpers for parametrization when multiple cases exercise the same behavior with the same Arrange–Act–Assert structure:
  - stdlib unittest: `self.subTest()`
  - pytest: `pytest.mark.parametrize`
- Parameters may vary data and expected values, but never setup, execution, parsing, assertions, or control flow; otherwise, use separate tests.
- Expected values must be prefixed with `expected_`.
- Expected booleans are allowed only when they vary data, not assertion logic; otherwise, use separate tests.
- Do not use union types in parametrized parameters; split the test to handle each type separately.

---

## Ownership Boundary

Test each behavior at the layer that owns it. Do not duplicate lower-layer behavior in higher-layer tests unless the higher layer adds distinct behavior.

---

## Test File Size

Keep each test module below 1,000 physical lines.

Split a test module by layer or concern before a change would bring it to 1,000 lines. Do not split by arbitrary line ranges. Preserve test coverage, parametrization, and test ownership.

Name test files hierarchically to reflect their scope:

- Use `test_<scope>.py` for a layer, behavior, or concern.
- When splitting that scope, use `test_<scope>_<subscope>.py`, where the added part names a narrower layer, behavior, or concern within the parent scope.
- If a file still needs splitting, continue adding narrower scope components, such as `test_<scope>_<subscope>_<detail>.py`.

Keep the hierarchy meaningful: each added filename component must describe a narrower part of the preceding scope, not an arbitrary grouping.

Split only to stay below line limit, do not create unnecessary hierarchy levels.

For example, `test_api.py` might be split into `test_api_authentication.py` and `test_api_pagination.py`. If authentication needs further splitting, use names such as `test_api_authentication_tokens.py` and `test_api_authentication_permissions.py`.

---

## Completion Criteria

- Review changed tests against the applicable criteria below and nearby project conventions.
- Report any unmet criteria and any criteria that could not be assessed.
- Tests are not brittle.
- Tests follow AAA pattern.
- Test the public behavior relevant to the change at the layer that owns it.
- Local implementation details are not tested.
- Only observable behaviour is tested.
- Exact strings are not asserted if they're not part of the contract.
- Floating-point values compared with framework helpers.
- Tests parametrization is not used for a single case.
- Changed test modules are below 1,000 physical lines.
