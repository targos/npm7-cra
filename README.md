# Some issues with npm@7

## Setup

```console
git clone https://github.com/targos/npm7-cra.git
cd npm7-cra
```

## Steps to reproduce

### Issue 1: `npm ci` changes `package.json`

```console
npm ci
git status
```

Now the `package.json` file has uncommitted changes (reordered elements in `dependencies`).

Note that this is new and did not happen with `7.0.0-beta.10`.

### Issue 2: `npm ci` prints an error without context

```console
npm ci
```

Prints: `npm WARN Error: Unsupported engine` (first line of the output).

### Issue 3: `npm i` always pretends it "added 4 packages"

```console
npm ci
npm i
npm i
npm i
```

Everytime `npm i` is executed, the output is:

```console

added 4 packages, and audited 1729 packages in 2s

69 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

### Issue 4: `npm i react@17` never ends

```console
npm ci
npm i react@17
```

With npm@7, the command never ends and cannot even be killed with CTRL+C.
With npm@6, it ends with an error (because there is no matching version).
