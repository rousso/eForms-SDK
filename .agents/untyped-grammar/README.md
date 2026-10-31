# Untyped grammar: where the plan lives

The grammar change on this branch (`feature/untyped-grammar`, from `efx-2`) is one half of the work that moves EFX-2 type checking out of the grammar and into the toolkit. The plan, the rules of engagement and the progress record live in the toolkit fork:

- repository `rousso/efx-toolkit-java`, branch `feature/untyped-grammar`
- `.agents/untyped-grammar/plan.md` (approved by Yannis Rousochatzakis on 2026-10-31)
- `.agents/untyped-grammar/progress.md` (single record of progress; it names the matching commit of this branch at every gate)

Only `efx-grammar/Efx.g4`, `efx-grammar/README.md` and `CHANGELOG.md` change on this branch; `EfxLexer.g4` does not. Nothing here is pushed to `efx-2` or to any OP-TED repository.
