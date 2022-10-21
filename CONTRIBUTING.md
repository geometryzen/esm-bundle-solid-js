# How to Contribute

We'd love to accept your patches and contributions to this project. There are just a few guidelines you need to follow.

## Code reviews

All submissions, including submissions by project members, require review. We
use GitHub pull requests for this purpose. Consult
[GitHub Help](https://help.github.com/articles/about-pull-requests/) for more
information on using pull requests.

## Community Guidelines

This project follows [Contributor Covenant](https://www.contributor-covenant.org/)
as it's Code of Conduct, and we expect all project participants to adhere to it.

## Maintaining dist/index.d.ts

This file is pseudo-manually maintained. rollup.config.mjs is configured to build dist/generated.index.d.ts using the solid-js types in node_modules. It does this by using the rollup-plugin-dts which requires that module specifiers have a .d.ts extension. For some reason, the type definitions created by solid-js in node_modules have a d.ts extension but internally the module references have a .js extension. The workaround is to change the internal module references from .js to .d.ts. Do this recursively until the generated.index.d.ts file has the 'csstype' as the only import. The manual step is to copy the contents over from dist/generated.index.d.ts to dist/index.d.ts.

It is an open issue to determine whether the output of solid-js is incorrect or whether the rollup-plugin-dts should be more lenient in its inputs.

