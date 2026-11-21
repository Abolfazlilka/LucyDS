# Lucy 2.0.7 compatibility notes

This package follows the Pure-Lucy layout documented in the Lucy 2.0.7 source:

```text
packages/lucyds/
  lucy.toml
  src/
    init.lucy
```

The repository root also contains `lucy.toml`. Lucy 2.0.7 walks upward from
the executing source file to find the nearest project root, then adds that
root's `packages/` directory to module lookup.

`src/init.lucy` imports sibling modules using selective imports, for example:

```lucy
from linked_list import LinkedList
```

This works because Lucy resolves a module relative to the directory of the
currently importing source file. The `init.lucy` entry module then exposes its
public bindings through `import lucyds`.

The package manifest mirrors the package metadata example in Lucy 2.0.7.
The runtime's project-local package discovery uses the source layout; it does
not currently enforce all manifest fields as a package-manager schema.

No C++ extension is used because all included features are implemented in Lucy.
