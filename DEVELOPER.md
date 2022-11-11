# Developer Notes

## Forcing install and update

This may be required because of conflicting rollup dependencies.

```
npm install --force
npm update --force
```

## Maintaining src/index.ts

This file exports everything from _solid-js_ but also exports resources from the sub-packages. This is because there appears to be some hidden state that is shared between sub packages. For the runtime we obtain all resources from this SolidJS proxy, but types are obtained from all the proxy packages. This ensures that the developer experience is the same as the SolidJS documentation.

## Generating dist/index.d.ts

The build creates _generated.index.d.ts_ in the _dist_ folder. Following an update to SolidJS, this file may/will not contain the bundled definitions. This is because the SolidJS type definition files in node_modules import files with _js_ extensions. The current workaround is to manually fixup the _js_ extensions to _d.ts_ (simply omitting the extension does not work). This is done recursively from the input specified in _rollup.config.mjs_ until the _generated.index.d.ts_ file contains the fully bundled type definitions. Once the contents of _generated.index.d.ts_ are correct, they can be used to manually replace the contents of _index.d.ts_ in the _dist_ folder.

The only import that should remain is

```
import * as csstype from 'csstype';
```