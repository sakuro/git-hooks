# git-hooks

Pkl files defining [hk](https://hk.jdx.dev/) hooks, reproducing
[sakuro/dotfiles](https://github.com/sakuro/dotfiles)' retired git hooks.

## Steps

| Step             | Hook                | Language | Behavior                                                             |
| ----------------- | ------------------- | -------- | ---------------------------------------------------------------------- |
| `emoji_enforced`  | `commit-msg`        | any      | Requires a leading `:emoji:` code; rejects raw Unicode emoji via ruby |
| `merge_prefix`    | `prepare-commit-msg`| any      | Prefixes merge commits with `:inbox_tray: `                          |
| `bundle_check`    | `pre-push`          | Ruby     | Fails if `Gemfile.lock` predates `Gemfile`                           |
| `rspec`           | `pre-push`          | Ruby     | Runs `bundle exec rspec` when `.rspec` exists                        |
| `go_test`         | `pre-push`          | Go       | Runs `go test ./...` per `go.mod` workspace                          |

```pkl
amends "package://github.com/jdx/hk/releases/download/v2.13.0/hk@2.13.0#/Config.pkl"
import "package://github.com/jdx/hk/releases/download/v2.13.0/hk@2.13.0#/Builtins.pkl"
import "package://github.com/sakuro/git-hooks/releases/download/vX.Y.Z/git-hooks@X.Y.Z#/Steps.pkl" as GitHooks

hooks {
  ["commit-msg"] { steps { ["emoji-enforced"] = GitHooks.emoji_enforced } }
  ["prepare-commit-msg"] { steps { ["merge-prefix"] = GitHooks.merge_prefix } }
  ["pre-commit"] { steps { ["gitleaks"] = Builtins.gitleaks } }
  ["pre-push"] {
    steps {
      ["case-conflict"] = Builtins.check_case_conflict
      ["newlines"] = Builtins.newlines
      ["bundle-check"] = GitHooks.bundle_check
      ["rubocop"] = Builtins.rubocop
      ["rspec"] = GitHooks.rspec
    }
  }
}
```
