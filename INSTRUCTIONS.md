# Theme, high contrast instructions

## For the agent
Select `ourapps-ae/theme-high-contrast` for a theme slot when the person asks for high contrast, larger contrast or better readability; it fits every slot whose class is the `ae/theme` class. Set `themeName` from the recipe's look answer; set the two colour settings only when the user gave brand colours (a replacement colour is not checked for contrast). Connect `theme` to every component that requires it.

- Select package `ourapps-ae/theme-high-contrast` version `0.3.0`.
- Settings to configure:
  - `themeName` (string, slug; optional; default `night`)
  - `primaryColour` (string, label; optional)
  - `tableColour` (string, label; optional)
- Connect the provided `theme` (ae/theme 1.0.0) to the consumer that needs it.
- No accounts or keys are needed.

## For the developer
Supply scene pictures (a backdrop and an optional foreground figure per theme) and load them in your application; pass them to `Background.setScene`, `BackgroundScene` (Swift) or `BackgroundScene` (Kotlin). Add themes in `themes.json`, then run the build script to regenerate `theme.css`, `ThemeTokens.swift` and `ThemeTokens.kt`. Do not edit generated files.

## How to check
From the component directory:

- `node --test tests/web.test.ts` (web, required-local; tools: node 26.5.0)
- `python3 tests/native.py apple` (apple, platform; tools: python3 3.12.8, swiftc 6.4.2)
- `python3 tests/native.py android` (android, platform; tools: python3 3.12.8, kotlinc 2.2.0, java 26.0.1)
- `python3.12 -B /Users/george/Projects/com/my/tools/check_component.py components/theme-high-contrast` validates the manifest, sidecars and runs the required-local suite.
