# Welcome to Node App Tech Docs

This is Martin's first Tech Docs test for Backstage.

There is also a [nested doc](./pages/nested_doc.md) to show hierarchy, structure, and linking.

I created this project by using the default NodeJS template. The template does not include tech docs by default so I made some tweaks to enable it in the project.

Once getting the config right in the `catalog-info.yaml` and the `docs/mkdocs.yaml` files, my locally running Backstage instance was able to fetch and generate the docs and store them on my local disk.

My TechDocs configuration YAML looks like this:

```yaml
techdocs:
  builder: 'local' # Alternatives - 'external'
  generator:
    # runIn: 'docker' # Alternatives - 'local'
    runIn: 'local' # Alternatives - 'docker'
  publisher:
    type: 'local' # Alternatives - 'googleGcs' or 'awsS3'. Read documentation for using alternatives.
    local:
      # (Optional). Set this to specify where the generated documentation is stored.
      publishDirectory: '/Users/<path-to-my-project-root>/__generated_docs__/'
```

## Other Notes

I am using my Backstage Starter project which has configurations enabled for Postgres and Github Auth and integrations.

### Things I Had To Do

Tech Docs require Node be run with `--no-node-snapshot` option:

```sh
# Set in the terminal where yarn dev command will run
export NODE_OPTIONS=--no-node-snapshot
```

Install Github Scaffolder Module for the Backend:

```sh
yarn --cwd packages/backend add @backstage/plugin-scaffolder-backend-module-github
```

Add the Backend package in `packages/backend/index.ts`:

```sh
backend.add(import('@backstage/plugin-scaffolder-backend-module-github'));
```

Some errors I saw along the way:  
"Failed to create the User repository shadygrove/backstage-node, Resource not accessible by personal access token"  
"Forbidden: Write access to repository not granted."
