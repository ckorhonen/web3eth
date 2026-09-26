# Repository guide

## Layout and commands

This Ruby gem exposes Ethereum RPC, ABI, contract, and Etherscan helpers in `lib/web3ethereum/`; the entrypoint is `lib/web3ethereum.rb`. Tests live in `spec/`. Dependencies come from `Gemfile` and `web3eth.gemspec`.

The gem declares Ruby >= 2.4; `.github/workflows/main.yml` uses Ruby 3.0.1 and Bundler 2.2.15. Use that CI combination when reproducing failures. Install with `bundle install` (`bin/setup` runs it with shell tracing). `bundle exec rake` runs RSpec and RuboCop; use `bundle exec rspec spec/path_spec.rb` for a focused test or `bundle exec rubocop` for lint. `bundle exec rake build` packages the gem locally; `rake release` tags, pushes, and publishes, so it is not a validation command.

`spec/spec_helper.rb` currently requires `web3eth`, while the library entrypoint is `web3ethereum.rb`; the sample spec references `Web3eth` and contains `expect(false).to eq(true)`. These are source-visible baseline problems, not evidence that tests passed or a reason to silently change unrelated code.

## Working and verification

Inspect `git status --short` and preserve unrelated edits. Complete authorized local changes through relevant tests/lint and repair regressions without asking about routine reversible steps. Add meaningful coverage for changed RPC serialization or ABI behavior; use fixtures/stubs instead of live Ethereum transactions. Keep public API compatibility and README examples aligned. For prose-only changes, inspect links/commands and run `git diff --check`.

Do not expose RPC/API credentials, send transactions, change remote node settings, or publish the gem without explicit task authorization. If dependencies, baseline tests, or required decisions block validation, name the exact failure and continue independent work. Report changed paths, executed checks and their outcomes, and what remains unverified; source inspection is not a successful test run.
