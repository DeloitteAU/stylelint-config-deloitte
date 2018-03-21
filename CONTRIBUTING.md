# Contributing to Stylelint Config Deloitte

> **Please note** while contributions are welcome, these configurations are being published with our use cases in mind and are opinionated by our engineers. We may not accept *feature* pull requests unless they are aligned with our needs.

To get started please [fork](https://github.com/DeloitteDigitalAPAC/stylelint-config-deloitte#fork-destination-box) this code on Github.

At the root; run `npm install`.

## Tests

In order to run tests/lint:

```bash
npm run test
```

## Publishing

Instructions for publishing new releases:

- Check out the `master` branch.
- Do not manually change version numbers in or `package.json` files (they are updated programatically).
- Update the `CHANGELOG.md` file and add the changes to the git staging area. These changes will be included in the automatic commit that increments the version numbers. You don't need to commit them separately.
- Run `npm version <newversion>`, where `<newversion>` is `major`, `minor`, `patch`, [etc](https://docs.npmjs.com/cli/version). This will create a version commit and tag in git. The `--force` flag can added so that your staged changes to `CHANGELOG.md` are included in the version commit.
- Push the commit and tag to Github.
- Run `npm publish`.
