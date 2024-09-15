# Vue Features Repo

This repo compiles many popular web development features developed in different UI frameworks so I can copy paste into future projects.

## Branches

It has a `main` branch with the basics of a Vue project. If anything about vue must be upgraded, it must be done here.

It has a list of other branches for every UI framework like `ui/tailwind`, `ui/shadcn`, `ui/vuetify`, etc.. 

Based on the framework branches, it has a list of branches with features.

```
main
ui/tailwind
ui/shadcn
ui/vuetify
ui/...
ui/...
feature/lazy-loading
feature/fetch
feature/auto-focus
feature/...
feature/...
```

## How to use

### add UI framework branch

If a new framework needs to be added, create a new branch with the command:

```bash
git checkout main
git checkout -b ui/bootstrap
```

### feature branches

```bash
git checkout -b feature/lazy-loading-tailwind ui/tailwind
```

In this example, the new branch will be created based on the `ui/tailwind branch`.

### updates on the base branch

If the base branch needs to be updated, for example by upgrading vue, the following command can be used:

```bash
git checkout main
# Apply changes, commit them
git checkout ui/tailwind
git merge main
```