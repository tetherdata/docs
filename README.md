# Tether help docs

Source for [docs.tetherdata.io](https://docs.tetherdata.io), the help site for the Tether app. Built with [Mintlify](https://mintlify.com/docs). Changes merged to `main` deploy automatically.

Tether's in-app agent answers user questions by searching this site, so these pages are also the agent's knowledge of the app. Write for both readers.

## Writing a page

Read [AGENTS.md](AGENTS.md) first. It covers the page structure (a `Where:` line in every how-to section), the current app terms, and how to move or remove a page safely. Screen names and button labels come from the app's code, not from memory.

## Preview and check

```
npm i -g mint
mint dev            # preview at http://localhost:3000
mint broken-links   # must pass before a PR
```

## Keeping the docs current

Each week's release notes name the docs page for each shipped feature, the wording it replaces, and the questions users will ask about it. One docs PR per week brings the pages up to date. Before that PR merges, each of those questions, searched on the docs site, should return the right page in the top three results.

## Help

Questions about Tether: help@tetherdata.io.
