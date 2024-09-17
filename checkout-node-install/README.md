# actions/checkout-node-install

A composite action to checkout, setup NodeJS and install dependencies

## Source Code

```yaml
inputs:
  node-version:
    description: Version of NodeJS to setup
    default: lts

  cache-hash-path:
    description: Path to file to hash and use as cache key
    default: "./package-lock.json"

  registry-url:
    description: Registry URL for publishing packages
    default: https://registry.npmjs.org/

runs:
  using: "composite"
  steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Setup Node.js ${{ inputs.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ inputs.node-version }}
        cache: npm
        cache-dependency-path: ${{ inputs.cache-hash-path }}
        registry-url: ${{ inputs.registry-url }}

    - name: Install dependencies
      shell: bash
      run: npm ci
```

## Usage

```yaml
steps:
  - name: Checkout, Setup NodeJS v20.x and Install dependencies
    uses: manferlo81/actions/checkout-node-install@v1
    with:
      node-version: 20.x
      cache-hash-path: "./package.json"
      registry-url: https://npm.pkg.github.com/
```
