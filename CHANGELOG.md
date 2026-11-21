# Changelog

## 0.1.0

- Establish a Lucy 2.0.7 Pure-Lucy package layout.
- Add a project-root `lucy.toml` for project-local package discovery.
- Expose the public API through `packages/lucyds/src/init.lucy`.
- Keep implementation modules private to the package's internal layout.
- Add a regression test suite, usage example, API reference, and package notes.
- Replace the length-only hash bucket calculation with a polynomial hash.
- Validate HashTable capacity and cover resize/update behavior in tests.
