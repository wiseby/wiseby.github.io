---
layout: post
title: "Setting up linting and formatting tools for Angular development"
categories: ["Angular"]
---

[Prettier Setup](https://medium.com/@victormejia/setting-up-prettier-in-an-angular-cli-project-2f50c3b9a537)
[Linting Setup]()

I had already a existing project I wanted to add automated linting and formatting to. I installed the following packages according to the guides I followed:

```sh
npm install eslint

npm install @typescript-eslint/eslint-plugin eslint-plugin-prettier

npm install prettier prettier-eslint eslint-config-prettier
```

I was using node v13.12.0 so I had to upgrade. Using nvm I only needed to run this command:
Taken from [StackOverflow](https://stackoverflow.com/questions/34810526/how-to-properly-upgrade-node-using-nvm)

```
nvm install stable --reinstall-packages-from=current
```

Now my version is the latest stable v15.14.0

install vscode Extension for [eslint](https://github.com/Microsoft/vscode-eslint)

I got so comfortable when all these tools worked the magic without me needing to lift a finger. These tools have been enabled by default for my projects at work and I see why that is!
All commits where fixed with the same configurations with the help of pre-commit hooks!
