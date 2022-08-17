# spin-plugins
Spin plugins must specify which versions of Spin they are compatible with specifying a [comparator](https://docs.rs/semver/1.0.13/semver/struct.Comparator.html) along with the version of Spin. The result is a string that matches the following regular expression: `^[=><~^*]?[=]?v?(0|[1-9]\d*)(\.(0|[1-9]\d*))?(\.(0|[1-9]\d*))?(-(0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(\.(0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*)?(\+[0-9a-zA-Z-]+(\.[0-9a-zA-Z-]+)*)?$`.
## Validating Plugin Schemas
A plugin schema can be validated locally using any JSON schema validator. The spin plugins GitHub workflow that must succeed before a plugin is merged uses [ajv](https://ajv.js.org/), which can also be run locally as follows:
1. Install [`ajv-cli`](https://www.npmjs.com/package/ajv-cli)
1. Get the current schema used by spin and validate all json plugin manifests against it:
    ```sh
    export CURRENT_JSON_SCHEMA=$(cat json-schema/current.txt)
    ajv -s json-schema/spin-plugin-manifest-schema-$CURRENT_JSON_SCHEMA.json -d "plugins/*.json" --spec=draft2019
    ```