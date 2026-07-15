# HKPUG Opik 14-Day Challenge

Improve one support-answer prompt over as many as eight scored attempts. Each
attempt returns encrypted feedback that your team can inspect in Opik before
revising the next prompt.

[Six-case mini workshop](https://pythonhk.github.io/20260711-opik-14-days-challenge/tutorial/) |
[First submission guide](https://pythonhk.github.io/20260711-opik-14-days-challenge/start/) |
[Submission feedback guide](https://pythonhk.github.io/20260711-opik-14-days-challenge/submission-feedback/) |
[Live leaderboard](https://pythonhk.github.io/20260711-opik-14-days-challenge/leaderboard/)

## Rules

- A team may submit twice per Hong Kong calendar day and eight times in total.
- The official score is 75% discovery and 25% holdout.
- A submission pull request must change only `submission/submission.zip`.
- Keep your team private key and plaintext prompt out of Git.

## Challenge setting

Your team is improving HarbourCloud's support copilot. The same submitted
system prompt is tested across 50 policy-heavy support cases: 40 discovery
cases and 10 hidden holdout cases. DeepSeek V4 Flash produces each answer with
temperature 0 and seed 0. Deterministic checks and Qwen 3.7 Plus then score the
output contract, citations, evidence coverage, escalation, relevance,
instruction following, and faithfulness.

## First submission

New to Opik? Complete the
[six-case mini workshop](https://pythonhk.github.io/20260711-opik-14-days-challenge/tutorial/)
first. It includes a public local-Opik dataset, the original 24 workshop
questions, Python case files, and revealable answers.

Download `hkpug-opik-helper` for your platform from the
[latest release](https://github.com/pythonhk/20260711-opik-14-days-challenge/releases/latest).
The [first submission tutorial](https://pythonhk.github.io/20260711-opik-14-days-challenge/start/)
has installation steps for macOS, Linux, and Windows.

Start with the example prompt, then edit `submission/prompt.txt`:

```sh
cp starter/prompt.example.txt submission/prompt.txt
```

Check the team credentials supplied at registration:

```sh
hkpug-opik-helper doctor \
  --team-id your-team-id \
  --private-key /path/to/team-private-key.pem \
  --team-cert /path/to/team-certificate.pem
```

Create and inspect the one-file submission:

```sh
hkpug-opik-helper pack \
  --team-id your-team-id \
  --private-key /path/to/team-private-key.pem
hkpug-opik-helper inspect \
  --team-cert /path/to/team-certificate.pem
```

Commit `submission/submission.zip`, push your branch, and open a pull request to
`main`:

```sh
git add submission/submission.zip
git commit -m "submission: add scored attempt"
git push
```

## Review feedback

After scoring, use the workflow link in the pull request comment to download the
team-encrypted artifact ZIP. Extract `submission-feedback.cms`, decrypt it, and
load the traces into a running local Opik instance:

```sh
hkpug-opik-helper decrypt \
  --private-key /path/to/team-private-key.pem \
  --team-cert /path/to/team-certificate.pem
hkpug-opik-helper load
```

Follow the [submission feedback guide](https://pythonhk.github.io/20260711-opik-14-days-challenge/submission-feedback/)
for setup and review guidance. The practice cases are in [`public`](public), and
the supplied prompts are in [`starter`](starter).
