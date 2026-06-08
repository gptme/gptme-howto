# How-To: Debug a Failing Python Test

Reproduce a test failure, trace the root cause, and fix it — all in one session.

## Start with the failing test

```
pytest tests/test_payment.py::test_refund_calculates_correct_amount is failing.
Run it, show me the traceback, and find the bug.
```

gptme runs pytest, reads the traceback, then reads the relevant source files.

---

## Full debug session example

```
This test is failing:

    def test_calculate_discount():
        result = calculate_discount(100, 0.2)
        assert result == 80

Run pytest on it, trace through the logic, and fix the bug.
```

gptme will:
```
> shell pytest tests/test_pricing.py::test_calculate_discount -xvs
# output: AssertionError: assert 120 == 80

> read src/pricing.py
# finds: return price + price * discount  (wrong: should subtract)

> patch src/pricing.py
<<<<<<< ORIGINAL
    return price + price * discount
=======
    return price - price * discount
>>>>>>> UPDATED

> shell pytest tests/test_pricing.py::test_calculate_discount -xvs
# output: 1 passed
```

---

## Debug with print tracing

```
The function `process_batch` in src/worker.py sometimes returns empty results.
Add strategic print statements, run the failing test with -s, and show me what's happening.
```

---

## Debug a flaky test

```
tests/test_api.py::test_concurrent_requests fails about 1 in 5 runs.
Run it 5 times and show me the pattern in the failures.
```

```python
# gptme can run this inline:
import subprocess
results = [subprocess.run(['pytest', 'tests/test_api.py::test_concurrent_requests', '-x'],
           capture_output=True, text=True) for _ in range(5)]
for i, r in enumerate(results):
    print(f"Run {i+1}: {'PASS' if r.returncode == 0 else 'FAIL'}")
    if r.returncode != 0:
        print(r.stdout[-500:])
```

---

## Debug by reading the stack

```
I'm getting this error in production:
    KeyError: 'user_id' in process_request() at line 47 of src/handlers.py

Read the handler, find all callers, and tell me which one could pass a dict without user_id.
```

---

## Fix and verify

```
Fix the bug, run the full test suite for the payment module, and confirm nothing else broke.
```

---

## Tips

- **Share the exact error**: paste the full traceback, not just the last line.
- **Run with `-xvs`**: stops at first failure, shows print output.
- **Ask to explain first**: "explain why this test would fail before fixing it".
