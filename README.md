# jfr-plugin-installation-action

This is a brief introduction of `jfr-plugin-installation-action`.
It can help users install extra plugins in the host machine.
If you want to learn more about the usage of this action,
you can check the [central documentation page](https://jenkinsci.github.io/jfr-action-doc).

## Inputs

| Name | Type | Default Value | Description |
| ----------- | ----------- | ----------- | ----------- |
| `pluginstxt` | String | plugins.txt | The relative path to plugins list file. |

## Example

Please note this action doesn't run the Jenkins pipeline.
You need to use `jfr-runtime-action` instead.
You can call this action by using `jenkinsci/jfr-plugin-installation-action@master`.
The users need to use `jfr-setup-action` in advance.

```yaml
name: CI
on: [push]
jobs:
  jfr-runtime-action-pipeline:
    strategy:
      matrix:
        os: [ ubuntu-latest, macOS-latest, windows-latest ]
    runs-on: ${{matrix.os}}
    name: jfr-runtime-action-pipeline
    steps:
      - uses: actions/checkout@v2
      - name : Setup Jenkins
        uses:
          jenkinsci/jfr-runtime-action@master
      - name: Jenkins plugins download
        uses:
          jenkinsci/jfr-plugin-installation-action@master
        with:
          pluginstxt: plugins.txt
      - name: Run Jenkins pipeline
        uses:
          jenkinsci/jfr-runtime-action@master
        with:
          command: run
          jenkinsfile: Jenkinsfile
```
