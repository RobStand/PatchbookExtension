# Customizing the extension
The Patchbook markup language is very simple, and the extension adds colorization in a very straightforward way.

Each feature of the markup language has an entry in the `PatchBook.YAML-tmLanguage` file. For example, here are a couple of patterns:

```
- comment: VOICE
  name: keyword.patch
  match: (\bVOICE\b)

- comment: Label
  name: string.patch
  match: ([^\(]+(?=\)))
```

Each pattern has a `comment`, a `name`, and a `match`. The `comment` is just a note about what the pattern is for. The `name` is a scope used in a `tmTheme` file. For example, `string.patch` is the `string` scope, which will have a different color depending on which theme the user loads. And `match` is the regex to match the syntax from the markup language.

## Color scheme
The color theme is based on the typical/standard themes included in VS Code. Scopes in the themes are reused for simplicity. For example, input and output label are colorized as `strings`. 

Currently the extension doesn't recognize the difference between input modules & labels and output modules & labels so it colorizes them the same way. Rather than one wonky regex that excludes what we don't want, the better way to do it is to use `captures` in the syntax definition. I would like to add `captures` to make the separation between inputs and outputs more clear. That is on the roadmap for sure. 

## Updating the syntax rules
If you want to update the syntax rules to change a scope or add a better set of regexes, you will need to edit the `PatchBook.YAML-tmLanguage` file. I use PackageDev in Sublime Text 3 to generate the `PatchBook.tmLanguage` file. Any change you make to `PatchBook.tmLanguage` is subject to being overwritten if/when PackageDev generates a new version.

If you contribute a PR with changes to the syntax highlighting rules and/or scopes, make sure you put those changes in `PatchBook.YAML-tmLanguage` and generate the `PatchBook.tmLanguage` file. These will need to match in order for the PR to be accepted.

## Additional file types
I chose the `.patch` and `.patchml` file types for their simplicity and the likelihood they are not already used in programming languages. If you want to use a different file type, add it to the `PatchBook.YAML-tmLanguage` file in the `fileTypes` array:

```
fileTypes: [patch, patchml]
```

## Learning resources
When building the extension, I relied heavily on the [Sublime Text docs](http://docs.sublimetext.info/en/latest/extensibility/syntaxdefs.html) to understand the YAML file and the [VS Code docs](https://code.visualstudio.com/docs/extensions/themes-snippets-colorizers#_adding-a-new-language-colorizer) to figure out how to build the colorizer in the first place.

This [blog post](https://www.apeth.com/nonblog/stories/textmatebundle.html) about scopes is really helpful for identifying the commonly-used scopes and choosing which ones to reuse.