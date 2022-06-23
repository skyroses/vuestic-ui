# Release script

This document is about `release` script.

The script is meant to automate release procedure. So far it doesn't cover full release flow, but gets rid of some tedious procedures.

Here's what script does:

* perform checks if we can release (no uncommitted changes, correct branch);
* update version strings in files;
* add and push commit and tag;
* build vuestic-ui;
* publish vuestic-ui to npm.

There are a couple of cli arguments you can pass to script to modify its behaviour:

```sh
npx tsx build/release-script.ts

  # for testing - doesn't push changes anywhere and performs a cleanup
  --dry-run 
  
  # release type - monthly | weekly | development | experimental, default: experimental
  --release-type=experimental
```

### Repo root commands
You have the following commands from repo root to simplify script usage:

```bash
release:montly
release:weekly
release:next
release:experimental
```

### Release types

|                     | **monthly** | **weekly** |            **next**            |            **experimental**            |
|---------------------|:-----------:|:----------:|:------------------------------:|:--------------------------------------:|
| **git tag**         |      +      |     +      |               -                |                   -                    |
| **dist tag**        |  `latest`   |  `latest`  |             `next`             |             `experimental`             |
| **dist version**    |   `1.2.0`   |  `1.2.1`   | `1.2.1-next-de4db33f-20220608` | `1.2.1-experimental-de4db33f-20220608` |
| **commits version** |      +      |     +      |               -                |                   -                    |
| **branch**          |  `master`   | `develop`  |           `develop`            |                  any                   |

* **monthly** - large release - we should advertize it and include fancy features;
* **weekly** - once-in-a-week release, includes all current features;
* **next** - release for each commit in `develop` branch;
* **exprimental** - release for developer to showcase the build.

### Further development

Let's keep this script well documented and smooth to use. We want painless releases.