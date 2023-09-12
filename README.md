# Jest project specific config don't allow `testTimeout`

This repo is a minimal reproduction of a bug in Jest 29.7.0, which doesn't allow project specific config to override the `testTimeout` value.

This was discovered while using Jest as part of [island.is Nx monorepo](https://github.com/island-is/island.is) where individual apps have their own `jest.config.(js|ts|json)` files and have different requirements for `testTimeout`.

[Type for `ProjectConfig`](https://github.com/jestjs/jest/blob/v29.7.0/packages/jest-types/src/Config.ts#L434) doesn't define `testTimeout` as allowed property, but when using Jest with monorepo it should be possible to override this value in project specific config.

## Steps to reproduce

1. Clone this repo
2. Run `yarn`
3. Run `yarn test --projects src/packages/sum/jest.config.ts`
