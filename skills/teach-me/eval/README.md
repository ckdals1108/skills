# Teach Me Evaluation Bundle

`cases.json` is the public development evaluation bundle for `teach-me`. It does not score exact phrasing.
The `assertions` in each case represent observable pedagogical behaviors verified in the headless run's final response.

Execute one case at a time in a read-only ephemeral session. Explicitly invoke `$teach-me` and cross-reference the output with the assertions. Sync the project source to the global skills directory before execution to evaluate current changes:

```sh
npx skills add . -g --agent codex --skill teach-me --copy --yes
codex -a never exec --ephemeral --skip-git-repo-check -s read-only -C /tmp \
  'Use $teach-me to ...'
```

To pass, all assertions for a case must be satisfied. Keep failure traces only in temporary directories, modify the skill, and re-verify against the same case. Independent validators test generalization using separate holdout cases not present in the public suite.
