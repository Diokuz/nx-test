## Project level task

1. Run `npx nx foo-task foo` → files are copied
1. Change `packages/foo/src/index.ts`
1. Run `npx nx foo-task foo` → cache miss
1. Change `packages/foo/src/__stories__/stories.ts`
1. Run `npx nx foo-task foo` → cache hit

Thats Ok! Because I excluded `__stories__` folder from task inputs.

## Workspace level task

1. Run `npx nx task-workspace` → files are copied
1. Change `packages/foo/src/index.ts`
1. Run `npx nx task-workspace` → cache miss
1. Change `packages/foo/src/__stories__/stories.ts`
1. Run `npx nx task-workspace` → cache miss!

Why cache miss?

File `packages/foo/src/__stories__/stories.ts` excluded two different ways:

```json
{
  "targetDefaults": {
    "task-workspace": {
      "inputs": [
        ...
        "{workspaceRoot}/packages/**/[!_]*/*.ts",
        "!{workspaceRoot}/**/__stories__/*.ts"
      ],
```
