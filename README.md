# turbo-prune-reproducer

## preparation

These are the steps I used to prepare the repo using luxon as an example:
- Setup example repo (`npx create-turbo@latest -e with-shell-commands`)
- Install luxon 3.7.2 into app-a (will be hoisted to root node_modules)
- Install luxon 3.7.0 into app-b (will be kept in app node_modules)
- Uninstall luxon 3.7.2 from app-a
- Lockfile will still contain luxon with a local path (`apps/app-b/node_modules/luxon`)

## run prune

Run prune for 2.8.12 and 2.8.13+:
`turbo prune app-b --docker`

Then check the lockfile in `out/package-lock.json`.

### turbo 2.8.12
`apps/app-b/node_modules/luxon`
201 lines

### turbo 2.8.13
`node_modules/luxon`
143 lines

### turbo 2.8.20
`node_modules/luxon`
143 lines


-> difference in size seems to only come from empty attributes that are no longer added with newer version
