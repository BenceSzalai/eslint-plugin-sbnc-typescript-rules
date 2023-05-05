# ESLint Plugin: SBNC Typescript Rules

This plugin includes some specialised ESLint rules to be used in TypeScript projects.

The current version of the rules are based on the [v8.39.0](https://github.com/eslint/eslint/releases/tag/v8.39.0) version of ESLint and are NOT tested to be compatible with ESLint v7 or earlier.

## Installation

You'll first need to install [ESLint](https://eslint.org/):

```sh
npm i eslint --save-dev
```

You'll also need to have typescript-eslint set up:
```sh
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint typescript
```

Next, install `eslint-plugin-sbnc-typescript-rules`:

```sh
npm install eslint-plugin-sbnc-typescript-rules --save-dev
```

## Usage

Add `sbnc-typescript-rules` to the plugins section of your `.eslintrc` configuration file. You can omit the `eslint-plugin-` prefix:

```json
{
    "plugins": [
        "sbnc-typescript-rules"
    ]
}
```


Then configure the rules you want to use under the rules section. Since these rules are a superset of the built-in rules with the same names those need to be disabled for the replacements to work as intended.

```json
{
    "rules": {
      "@typescript-eslint/type-annotation-spacing"   : "off",
      "sbnc-typescript-rules/type-annotation-spacing": "warn"
    }
}
```

## Supported Rules

This Plugin contains one rule. It is an extended versions of the existing rule under the same name provided with typescript-eslint. This rule should behave exactly the same as the original counterpart if the rule configuration is the same. However, it allows some additional configuration options to further fine-tune the behaviour.

For detailed information and examples about the rule refer to the respective documentation under the `docs/rules` folder:
* [docs/rules/type-annotation-spacing.md](https://github.com/BenceSzalai/eslint-plugin-sbnc-typescript-rules/blob/main/docs/rules/type-annotation-spacing.md)

### type-annotation-spacing

This rule provides extra options to allow turning off some parts of the rule enforcement.

The two new options are: `ignoreBefore` and `ignoreAfter`. These can be used to turn off the enforcement of spaces before or after the type annotation.

This can be useful in use with conjunction of the `key-spacing` rule to allow aligning the type annotations on the colons. An example configuration may look like this:

```json
{
  "rules": {
    "key-spacing": [ "warn", { "align": "colon" } ],
    "sbnc-typescript-rules/type-annotation-spacing": [ "warn", { "overrides": { "property": { "ignoreBefore": true } } } ]
  }
}
```

This configuration would allow the following code, which would otherwise be considered invalid and cause a conflict between `key-spacing` and `@typescript-eslint/type-annotation-spacing`:

```typescript
type Foo = {
  barShortName                        : string
  barVeryLongNameThatPushesTheColonOut: string
}
```


## Additional info

The plugin scaffolding was created based on the [@darraghor/eslint-plugin-nestjs-typed](https://github.com/darraghoriordan/eslint-plugin-nestjs-typed) plugin.

***

Bence Szalai - https://sbnc.eu/

For similar extended rules of the base ESLint rules check out my other plugin: [eslint-plugin-sbnc-rules](https://github.com/BenceSzalai/eslint-plugin-sbnc-rules).
