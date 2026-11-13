# Local workflow

Local only: repository `ourapps-ae/theme-high-contrast` has no commits, pushes, remote changes or publishing without George's say-so. Licence: `Apache-2.0` (`identity.licence`; `LICENCE` holds the licence text, `NOTICE` the copyright notice).
Do not edit `mcinpoker/`, `skull/`, `aepm/`, `OurPoker/proof/` or `OurPoker/recipe/`.
Regenerate: `python3.12 -B /Users/george/Projects/com/my/tools/scaffold_component.py components/theme-high-contrast --spec components/theme-high-contrast/authoring/spec.json --render`.
Check: `python3.12 -B /Users/george/Projects/com/my/tools/check_component.py components/theme-high-contrast`. Suite commands (from the package root): `node --test tests/web.test.ts`; `python3 tests/native.py apple`; `python3 tests/native.py android`.
Always run Python with `-B`; never write bytecode into the repository.
