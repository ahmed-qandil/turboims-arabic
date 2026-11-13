# Modifications vs upstream Turbo IMS v3.0 (Turbo1123/TurboIMS, based on vvb2060/Ims)

1. Full Arabic localization: added `app/src/main/res/values-ar/strings.xml` translating all 67 strings. App name stays English "Turbo IMS".
2. Locales trimmed (standing rule: Arabic + English only): deleted `values-zh` (it was also incomplete - 47 of 68 strings). Only default English `values` + `values-ar` remain.
3. Language switch rewired to Arabic: the header button toggled English<->中文; `LocaleHelper` now defaults to Arabic on Arabic systems (English otherwise) and toggles English<->العربية. Button label shows the other language's name ("العربية" in English UI, "English" in Arabic UI). First-launch behavior still follows the system language - no defaults changed.
4. De-junked (standing clean rule): removed the "for Pixel" subtitle from the main screen header (branding, misleading on non-Pixel), removed the entire 2-second SplashActivity (layout, hardcoded "v3.0" text, logo drawable, manifest entry) - MainActivity is now the launcher activity, so the app opens straight to its single screen.
5. Update/About/disclaimer stripping: upstream has none - verified no update checks, no links, no About screen. Nothing to remove.
6. TalkBack/accessibility: the 7 feature switches were unlabeled (title and description are separate TextViews), so a screen reader announced only "switch, on/off". Each switch now has a contentDescription from its feature title string, spoken in Arabic. The hardcoded English toast "Unable to open network settings" moved to a string resource and is translated. All other controls are text buttons/labels and read correctly.
7. Release config: removed the upstream debug-key signing of release builds so `assembleRelease` emits an UNSIGNED APK for the owner to sign himself. Version set to v3.0-ar1 (versionCode 6).
8. No default of any user-toggleable setting changed (all 7 feature toggles remain default-on, as upstream).
9. No device gating exists upstream (verified: zero manufacturer/model checks) - the app uses generic CarrierConfigManager APIs and works on any phone with Shizuku; nothing device-specific was added or removed.

Upstream credits: Turbo IMS by Turbo1123 (github.com/Turbo1123/TurboIMS), an enhanced fork of IMS by vvb2060 (github.com/vvb2060/Ims). Neither repository ships a LICENSE file. Source of this modified version is published in this repository.
