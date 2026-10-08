# 3D engine evaluation — 2026-10-09

Captured verbatim from the design-phase agent response below. This is a working recommendation for the controller to act on next, not an owner-approved architecture decision or a claim that the chosen approach has been benchmarked on real hardware.

---

## Recommendation: Filament `RenderableManager` geometry via `filamat-android`, same version as the already-pinned engine

**Single approach:** keep `com.google.android.filament:filament-android` as the only 3D engine, and add exactly one same-family dependency, `com.google.android.filament:filamat-android`, so `MaterialBuilder` can compile a real in-process `Material` that `RenderableManager` attaches to procedural geometry. This is the only way to get a visible, native-rendered object without a `matc` CLI, a Gradle plugin, NDK/CMake, or a `settings.gradle.kts` change — all of which this phase's constraints rule out.

**Exact coordinates:**
- `com.google.android.filament:filament-android:1.56.0` — unchanged, already pinned in `gradle/libs.versions.toml` and verified there against Maven Central's `maven-metadata.xml` (comment dated 2026-10-08).
- `com.google.android.filament:filamat-android:1.56.0` — verified version, cited from `docs/reference/FILAMAT_ANDROID.md` (verified 2026-10-08 against Maven Central's `maven-metadata.xml` HTTP 200, with a resolving POM/AAR and one compatible runtime dependency, `androidx.annotation:annotation:1.9.0`). I am using that file's recorded verification rather than re-deriving it from memory, per the task's instruction and because I have no network access this phase. It happens to match `filament-android`'s version, but that match is corroborated evidence, not an assumption.

Add this as a single new version-catalog entry reusing the existing `filament` version ref (or a new `filamat` ref pointing to the same `"1.56.0"` string), plus one `implementation(libs.filamat.android)` line — no plugin block, no NDK, no `settings.gradle.kts` edit.

### Against the evaluation criteria
- **Performance:** a single procedural cube with one unlit material is a trivial draw load for a mid-range device's frame-time budget; the real cost is `filamat-android` bundling a native shader cross-compiler (glslang/spirv-cross/spirv-opt per ABI), adding APK size and a one-time compile cost at first `MaterialBuilder` use, not per-frame. No frame-time/thermal/battery measurement exists yet on real hardware — that remains an open follow-up, not something this phase can close. Longer-term, precompiling the `.filamat` bytes in a dev-time/CI step and shipping only the compiled blob would drop `filamat-android` from the release dependency graph entirely, but that needs shell/build access this phase doesn't have.
- **Accessibility:** unaffected by this dependency. `EngineHarness.kt` already keeps the Filament `AndroidView` semantics-cleared and puts the real `testTag("engine-canvas")` and tap action on the surrounding Compose `Box`, so TalkBack and the controller's tap automation reach a real composable, never the raw render surface. The existing Compose `Canvas` cube remains the required non-native/reduce-motion fallback path (it must keep existing, not be deleted) — it just must stop being the thing presented as satisfying this milestone.
- **Asset licensing:** nothing to flag. Geometry is a hand-authored procedural cube and the material is authored in-process via `MaterialBuilder`; no third-party model is imported.
- **Automated verification:** no new mechanism needed. `agent/visual_qa.py`'s `engine` journey already taps `engine-canvas` and mechanically checks an `engine-render-status` semantics node for the literal text `"native"` (failing the gate on anything else) — exactly the honest signal `docs/reference/FILAMAT_ANDROID.md` specifies implementing this dependency should finally make true.
- **Integration cost:** stays within the stated ceiling — one engine, one small same-family runtime dependency, no plugin/native-toolchain/settings change.

### Main trade-off
Accepting `filamat-android`'s native-compiler weight and first-use compile latency now, instead of building separate asset-pipeline infrastructure, in order to get an actual `RenderableManager`-backed object this milestone rather than a permanent skybox-plus-Canvas-cube substitute — which is exactly the gap Codex's prior review (`agent/runs/20261008-232956/engine-1-review.json`) blocked on.

### Confidence and scope
This is a working recommendation for the next bounded milestone, not a benchmarked or owner-approved architecture decision. I have not run anything on real hardware; frame-time, thermal, and battery figures are still unmeasured. The version I'm citing is verified in `docs/reference/FILAMAT_ANDROID.md`, not re-derived from memory, per that file's own instruction that it should be treated as a stable, safe-to-cite reference across runs.
