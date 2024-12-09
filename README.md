# Turborepo Bugreport

This is a bug report to demonstrate that the ``update`` command on @turbo/codemod does not work with Yarn 4+

Below is the output from the console commands:

```console
Microsoft Windows [Version 10.0.19045.5131]
(c) Microsoft Corporation. All rights reserved.

D:\repos\Bugs\TurboCodemodYarnFour>npx create-turbo@canary -e with-shell-commands 
? Where would you like to create your Turborepo? .
? Which package manager do you want to use? yarn

>>> Creating a new Turborepo with:

Application packages
 - apps\app-a: An application that uses other Internal Packages
rds.                                                                                                                     rds.
Library packages
 - packages\pkg-a
 - packages\pkg-b
 - packages\tooling-config: A package used by every other package.

>>> Success! Your new Turborepo is ready.

To get started:
- Enable Remote Caching (recommended): npx turbo login
   - Learn more: https://turbo.build/repo/remote-cache

- Run commands with Turborepo:
- Run a command twice to hit cache

D:\repos\Bugs\TurboCodemodYarnFour>yarn set version 4.5.3
(node:18780) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)
➤ YN0000: You don't seem to have Corepack enabled; we'll have to rely on yarnPath instead
➤ YN0000: Downloading https://repo.yarnpkg.com/4.5.3/packages/yarnpkg-cli/bin/yarn.js
➤ YN0000: Saving the new release in .yarn/releases/yarn-4.5.3.cjs
➤ YN0000: Done with warnings in 0s 696ms

D:\repos\Bugs\TurboCodemodYarnFour>npx @turbo/codemod@canary update
? Where is the root of the repo to migrate? .
No codemods required to migrate from 2.3.4-canary.2 to 2.3.3 

Upgrading turbo from 2.3.4-canary.2 to 2.3.3 (no codemods required) 

Upgrading turbo with yarn add turbo@latest --dev -W 

Migration failed
Unable to upgrade turbo: Error: Command failed: yarn add turbo@latest --dev -W

D:\repos\Bugs\TurboCodemodYarnFour>yarn add turbo@latest --dev -W 
Unknown Syntax Error: Command not found; did you mean one of:

  0. yarn add [--json] [-F,--fixed] [-E,--exact] [-T,--tilde] [-C,--caret] [-D,--dev] [-P,--peer] [-O,--optional] [--prefer-dev] [-i,--interactive] [--cached] [--mode #0] ...
  1. yarn add [--json] [-F,--fixed] [-E,--exact] [-T,--tilde] [-C,--caret] [-D,--dev] [-P,--peer] [-O,--optional] [--prefer-dev] [-i,--interactive] [--cached] [--mode #0] ...

While running add turbo@latest --dev -W

D:\repos\Bugs\TurboCodemodYarnFour>
```

From my guesses the ``-W`` flag is the villain here! It doesn't seem to exist on Yarn 4+
