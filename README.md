# pnpm-issue-1618-demo

A demo of [pnpm issue 1618](https://github.com/pnpm/pnpm/issues/1618) (peerDependencies not checked when installing subpackage in monorepo)

## Instructions for testing

```
git clone https://github.com/earksiinni/pnpm-issue-1618-demo.git
cd pnpm-issue-1618-demo
pnpm i --strict-peer-dependencies @pnpm-test/a
```

Observe the output (no errors or warnings but error about peerDependencies is expected)

```
$> pnpm i --strict-peer-dependencies @pnpm-test/a
Scope: current workspace package
Already up-to-date

dependencies:
+ @pnpm-test/a 0.0.1 <- packages/pnpm-test-a

Performing headless installation
$>
```

## Package structure

- `@pnpm-test/root`: Root package for monorepo, no dependencies
- `@pnpm-test/a`: Subpackage A, has exactly one dependency (peer dependency on `@pnpm-test/b`)
- `@pnpm-test/b`: Subpackage B, no dependencies

## File structure

```
package.json (@pnpm-test/root, no dependencies)
pnpm-workspace.yaml (points to '.' and 'packages/**')
packages
  pnpm-test-a
    package.json (@pnpm-test/a, peer dependency on @pnpm-test/b)
  pnpm-test-b
    package.json (@pnpm-test/b, no dependencies)
```
