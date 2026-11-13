# Source mapping

Made from `ourapps-ae/theme` 0.4.2, which was extracted from McInPoker revision `19905b75dbea89fbfd424d67fe26c81aaed0e018` (its SOURCE.md has the line ranges).

- `implementation/web/themes.json`: new palette. `night` and `lounge` keep theme's spacing, radii, type scale and background motion; every colour is opaque and every text, button and status colour has at least 4.5:1 contrast on the background, surface and table (`tests/web.test.ts`).
- `implementation/web/theme.css`, `implementation/apple/Sources/ThemeTokens.swift`, `implementation/android/src/main/java/ae/theme/ThemeTokens.kt`: generated from `themes.json` by `node implementation/web/build-tokens.ts implementation/web/themes.json`.
- `tests/fixtures/background.json`: generated from `themes.json` by `node tests/make-fixtures.ts`.
- `interfaces/theme.json`: a byte copy of theme's `ae/theme` 1.0.0 document.
- Every other file under `implementation/`, `tests/` and `examples/` is theme 0.4.2's, unchanged; the expected colours in `tests/web.test.ts` are this palette's, and the contrast test is new.
