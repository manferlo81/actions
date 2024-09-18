# actions/create-release

A composite action to create a GitHub release

## Index

* [Usage](#usage)
* [Source Code](#source-code)
* [Inputs](#inputs)
* [Permissions](#permissions)

## Usage

```yaml
steps:
  - name: Create a GitHub release
    uses: manferlo81/actions/create-release@v0.0.1
    with:
      tag_name: v1.2.3
      latest: false
```

## Source Code

```yaml
name: Create GitHub Release
description: Creates a GitHub Release

inputs:
  tag-name:
    description: Tag name
    required: true

  latest:
    description: Whether or not to make this the latest release
    required: false
    default: "true"

runs:
  using: "composite"
  steps:
    - name: Create Release
      uses: softprops/action-gh-release@v2
      with:
        generate_release_notes: true
        make_latest: ${{ inputs.latest != 'false' }}
        name: ${{ inputs.tag-name }}
```

## Inputs

| Input       | Description                                    | Default value |
| ----------- | ---------------------------------------------- | ------------- |
| `tag-name`  | Tag name                                       | `REQUIRED`    |
| `latest`    | Whether or not to make this the latest release.<br />Anything other than `"false"` will be threated as `"true"`. | `"true"`        |

## Permissions

This action requires the `contents` permission to be set to `write` in order to be able to create a GitHub Release.

```yaml
permissions:
  contents: write
```

## License

[MIT](../LICENSE) &copy; 2024 [Manuel Fernández](https://github.com/manferlo81) (@manferlo81)
