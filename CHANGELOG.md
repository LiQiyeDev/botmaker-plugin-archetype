# Changelog

All notable changes to `botmaker-plugin-archetype`.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this module uses
[semantic versioning](https://semver.org/). `release.sh` refuses to cut a version with no section here.

## [0.0.1] — 2026-09-02

First release. `0.x` to match the platform the skeleton is generated against; the archetype itself pins
nothing and is forced by no other module's release, because what it ships is text.

### Added

- **The module** — the tenth BotMaker repository, and the first one aimed at somebody who does not work on
  BotMaker. Until now the only plugin was the SDK, written by hand inside the umbrella, which is exactly why
  the pom requirements were undocumented and untested.
- **A skeleton that builds and passes its tests with no edits** — a `pom.xml` with the three scopes that are
  easy to get wrong, the `META-INF/services` declaration, `ExampleApi` (one offered method and one
  `@Hidden`), `ExamplePlugin` (a palette, one registered `ValueType` with a codec, one slot editor chosen by
  the *call*) and `ExamplePluginTest` (seven tests, including the contexts the editor must **decline** —
  the half a plugin author never tests by hand).
- **The skeleton's codec writes its literal with `Source.string`** (2026-08-28), where it used to carry a
  private `quote(…)` escaping the backslash and the quote and nothing else. The example a beginner copies is
  the one they will copy into a real plugin, and a hand-rolled escaper is exactly the mistake the toolkit
  now owns: a pasted tab in a value becomes a compile error in somebody's bot.
- **Four required properties, each with a working default** — `pluginId`, `pluginName`, `studioApiVersion`,
  `toolkitVersion`. An archetype that stops to ask a question a beginner cannot answer is worse than one
  that guesses: a guess is visible in the generated files and can be edited.
- **`main-SNAPSHOT` as the default BotMaker version.** A real JitPack coordinate that never goes stale,
  rather than a released tag baked in here — which would owe an edit on every contract release and age
  silently between them. The generated README says to pin a tag before publishing.

### Deliberately absent

- **A `.gitignore` in the skeleton.** `archetype:jar` drops `**/.gitignore` through the archiver's default
  excludes, with no warning; every workaround ends with the generated project holding a file named something
  else. The generated README asks for one instead.
- **A second copy of the templates in the CLI.** `botmaker new` will shell to this archetype. The pom scopes
  are the thing that must not drift between two copies.
- **An integration test that builds what it generates.** That would resolve `main-SNAPSHOT` from the network
  inside `mvn install` at the umbrella root. The manual command is in `README.md` and runs against the local
  reactor.
