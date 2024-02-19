# Guacamole-action

This GitHub Action runs [guacamole](https://github.com/padok-team/guacamole) against infrastructure-as-code to identify code smells and bad practices

## Example of usage

```yaml
on: [push]

jobs:
  guacamole-quality-scan:
    runs-on: ubuntu-latest
    name: guacamole-static-check
    steps:
      - name: Checkout repo
        uses: actions/checkout@master
      - name: Run guacamole action
        id: guacamole
        uses: padok-team/guacamole-action@v1.2.0
```
