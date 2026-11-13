# Theme, high contrast component

## Purpose and facilities
`theme-high-contrast` is the theme interface (`ae/theme`) with high-contrast looks, for people who need stronger contrast or play in bright rooms. It has the same shape, functions and settings as `theme`, so a recipe can put it in any slot whose class is the theme class. Its `themes.json` holds `night` (black room, white text, yellow buttons, dark green table) and `lounge` (dark brown room, white text, light blue buttons, dark brown table); every text, button and status colour is opaque and has a contrast ratio of at least 4.5:1 (WCAG 2.1 AA for body text) against every surface it is drawn on. One `themes.json` renders to CSS variables for the web, Swift constants for Apple and Kotlin constants for Android.

Facilities: `theme` (High-contrast design tokens and animated background for web, Apple and Android clients).

## User inputs
`themeName` selects a theme from `themes.json` (`night` or `lounge`); an unknown name falls back to the default. `primaryColour` and `tableColour` are optional colours that replace the theme's primary and table colours; empty means the theme's own. A replacement colour is not checked for contrast.

- `themeName` (string, slug; optional; default `night`)
- `primaryColour` (string, label; optional)
- `tableColour` (string, label; optional)

## Artefacts and dependencies
`component.json` maps every `implementation/` source into `components/theme-high-contrast/`:

- `implementation/android/src/main/java/ae/theme/BackgroundMath.kt` -> `components/theme-high-contrast/android/src/main/java/ae/theme/BackgroundMath.kt`
- `implementation/android/src/main/java/ae/theme/ThemeBackground.kt` -> `components/theme-high-contrast/android/src/main/java/ae/theme/ThemeBackground.kt`
- `implementation/android/src/main/java/ae/theme/ThemeTokens.kt` -> `components/theme-high-contrast/android/src/main/java/ae/theme/ThemeTokens.kt`
- `implementation/android/src/main/java/ae/theme/ThemeTypes.kt` -> `components/theme-high-contrast/android/src/main/java/ae/theme/ThemeTypes.kt`
- `implementation/apple/Sources/BackgroundMath.swift` -> `components/theme-high-contrast/apple/Sources/BackgroundMath.swift`
- `implementation/apple/Sources/ThemeBackgroundView.swift` -> `components/theme-high-contrast/apple/Sources/ThemeBackgroundView.swift`
- `implementation/apple/Sources/ThemeTokens.swift` -> `components/theme-high-contrast/apple/Sources/ThemeTokens.swift`
- `implementation/apple/Sources/ThemeTypes.swift` -> `components/theme-high-contrast/apple/Sources/ThemeTypes.swift`
- `implementation/server/index.ts` -> `components/theme-high-contrast/server/index.ts`
- `implementation/web/background.ts` -> `components/theme-high-contrast/web/background.ts`
- `implementation/web/build-tokens.ts` -> `components/theme-high-contrast/web/build-tokens.ts`
- `implementation/web/index.ts` -> `components/theme-high-contrast/web/index.ts`
- `implementation/web/package.json` -> `components/theme-high-contrast/web/package.json`
- `implementation/web/theme.css` -> `components/theme-high-contrast/web/theme.css`
- `implementation/web/themes.json` -> `components/theme-high-contrast/web/themes.json`
- `implementation/web/tokens.schema.json` -> `components/theme-high-contrast/web/tokens.schema.json`
- `implementation/web/tokens.ts` -> `components/theme-high-contrast/web/tokens.ts`

Dependencies: none.
`tools.lock.json` pins verification tools: node 26.5.0, python3 3.12.8, swiftc 6.4.2, kotlinc 2.2.0, java 26.0.1. Licence: `Apache-2.0` (`LICENCE`, `NOTICE`).

## Provided interfaces
- `interfaces/theme.json` defines `theme` (ae/theme) version 1.0.0.

## Required interfaces
None.

## Integration
Web: import `resolveTheme` and `applyTheme` from the entry module `web/index.ts`, apply the result to `document.documentElement`, link `web/theme.css` for the shipped themes (`:root` is the default theme, `[data-theme=name]` the others), and construct `Background` from `web/index.ts` on a full-screen canvas with `setScene` for pictures. Apple: compile `ThemeTypes.swift`, `ThemeTokens.swift`, `BackgroundMath.swift` anywhere, and `ThemeBackgroundView.swift` in UIKit targets (iOS, tvOS, Mac Catalyst); read colours as `ThemeSet.named(name).resolved(primary:table:)` and `Color(themeColour)`. Android: add the three Kotlin files and `ThemeBackground.kt` to a Compose module; `ThemeSet.named(name).resolved(...)`. To change a look, edit `themes.json` and run `node web/build-tokens.ts themes.json --css DIR --swift DIR --kotlin DIR` to regenerate the three outputs; `tokens.schema.json` documents the shape and `validateTokens` enforces it. Other components (`controls`, `table-layout`, `card-graphics`, `chip-graphics`) read colours from these tokens.

## Visual definition and connected examples
`visual/definition.json` maps its ports to the provided and required interfaces. `visual/examples/connected.json` connects the component to an illustrative application consumer. Both image formats and a text description are retained under `visual/output/`.

## Infrastructure
None. Pure data, local rendering and on-device drawing. No accounts, network or deployment.

## Verification
Node tests check the token shape against the schema, that the OpenRPC interface's token schemas agree with `tokens.schema.json` and that every method it lists is an exported web function, overrides, CSS variable rendering, that the committed generated CSS, Swift and Kotlin equal what the renderers produce, the background placement maths, and that every theme meets WCAG AA contrast (4.5:1) for text, muted text, buttons and status colours on the background, surface and table. The Apple check compiles the Swift and compares colours and frames with the TypeScript fixtures; the Android check is written for kotlinc and does not run where kotlinc is missing.

- `node --test tests/web.test.ts` (web, required-local; tools: node 26.5.0)
- `python3 tests/native.py apple` (apple, platform; tools: python3 3.12.8, swiftc 6.4.2)
- `python3 tests/native.py android` (android, platform; tools: python3 3.12.8, kotlinc 2.2.0, java 26.0.1)

## Scenarios and presentation
A recipe that names the `theme` slot gets the high-contrast looks with `aepm design ... --substitute theme=ourapps-ae/theme-high-contrast@0.1.0`; every client then draws the same high-contrast colours. A recipe's look answer keeps choosing between `night` and `lounge`.

## Updates and removal
Patch updates replace files only. Regenerate the CSS, Swift and Kotlin outputs after any change to `themes.json`. The component keeps no data; removal deletes its files and the generated outputs.
