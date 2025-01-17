# GraphQL
 
## About this directory

* `src/graphql/lib` and `src/graphql/scripts` are human-editable.
* `src/graphql/data/**` are generated by [scripts](./scripts).

## Editable files

* `src/graphql/lib/validator.json`
  - JSON schema used in `tests/graphql.js`.
* `src/graphql/lib/non-schema-scalars.json`
  - An array of scalar types that live in [`graphql-ruby`](https://github.com/rmosolgo/graphql-ruby/tree/356d9d369e444423bf06cab3dc767ec75fbc6745/lib/graphql/types) only. These are
  not part of the core GraphQL spec.
* `src/graphql/lib/types.json`
  - High-level GraphQL types and kinds.

## Data files

Generated by `src/graphql/scripts/sync.js`:

* `src/graphql/data/schema-VERSION.json` (separate files per version)
* `src/graphql/data/previews.json`
* `src/graphql/data/upcoming-changes.json`
* `src/graphql/data/changelog.json`

## Rendering docs

When the server starts, `middleware/graphql.js` accesses the static JSON files, fetches the data for the current version, and adds it to the `context` object. The added properties are:

* `context.graphql.schemaForCurrentVersion`
* `context.graphql.previewsForCurrentVersion`
* `context.graphql.upcomingChangesForCurrentVersion`
* `context.graphql.changelog`

Markdown files in `content/graphql` use Liquid to loop over these context properties. The Liquid calls HTML files in the `includes` directory to do most of the rendering.

Note that Markdown files exist in `content/graphql` for every URL available in our GraphQL
documentation. Writers can add content to the Markdown files alongside the Liquid.
