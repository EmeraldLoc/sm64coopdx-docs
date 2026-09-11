# Contributing to Documentation

## Setting Up

It's recommended to use a markdown editor that can use [`markdownlint`](https://github.com/DavidAnson/markdownlint). [Visual Studio Code](https://code.visualstudio.com) does a excellent job at this with the [markdownlint extension](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint). Another great option is using [Obsidian](https://obsidian.md/download) and [installing the `markdownlint` extension](https://community.obsidian.md/plugins/markdownlint).

## Markdown Standards

We follow the rules laid out by [`markdownlint`](https://github.com/DavidAnson/markdownlint#rules--aliases) with the following exceptions:

- `MD013` may be ignored. It is recommended to enable word wrapping when writing documentation
- `MD024` may be ignored if the duplicate header does not have the same parent
- `MD035 no-bare-urls` can be ignored
- `MD041 first-line-heading/first-line-h1` may be ignored if first line heading is a back button, or an image. It is disabled project wide due to the common nature of back buttons
- `MD-059 descriptive-link-text` can be ignored

View the [configuration file](../.markdownlint.json) to see every single rule ignored.

## Our Standards

- Every single document should contain a back button going back to what linked to it. The back button is a `h2` header hyperlink that uses the :rewind: (`:rewind:`) emoji along with where it goes back to. As an example:

```md
## [:rewind: Modding](../modding.md)
```

- Title and header capitalization uses title case. Specifically, we use the [APA style](https://apastyle.apa.org/style-grammar-guidelines/capitalization/title-case)
- In a bullet like this, do not end off the final sentence with a `.`. For example, this sentence is the last, so there will not be a period, but the previous sentence was not the last so it had a period
- Refrain from using inline HTML in manually written documentation
- Tables should have pipes separated with a space:

```md
Do:

| Name | Description |
|------|-------------|
| mario | he's so cool! |

Don't do:

|Name|Description|
|----|-----------|
|mario|he's so cool!|
```

## Contributing

When contributing to the documentation, follow the normal [contribution guidelines](../CONTRIBUTING.md).

Always target the `dev` branch with documentation. We hope to improve on this system in the future so things can be pushed immediately if the documentation isn't on a dev-specific feature, but as it stands this is the current way we do things.
