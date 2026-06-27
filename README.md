# FlintAI AI-SPM Inventory Scan

A [GitHub Action](https://github.com/features/actions) for using [FlintAI](https://www.flintai.dev/) AI-SPM functionality. This action performs static analysis on your code to detect AI assets (such as models, agents, and MCP servers), creating an inventory. This inventory is then sent to your FlintAI instance, where it's enriched with additional information and analyzed for issues. You can view the results in the FlintAI web interface. Refer to the [FlintAI AI-SPM user guide](https://docs.flintai.dev/) for details.



## Configuration
You can configure the Action as shown in the following example::


```yaml
name: Example workflow for Python using FlintAI AI-SPM Inventory Scan
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@master
      - name: Run AI-SPM Inventory detection
        uses: sandbox-quantum/aispm-inventory-action@main
        with:
          flint_instance: https://some_url
          flint_token: ${{ secrets.FLINT_TOKEN }}
```

## Properties
Properties are passed to GitHub Action via explicit `with` input variables. For security, we strongly recommend using [GitHub secrets](https://docs.github.com/en/enterprise-cloud@latest/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets) for the sensitive input variable `flint_token`.


| Property          | Required | Description                                                                           |
| ----------------- | -------- | ------------------------------------------------------------------------------------- |
| `flint_instance`  | yes      | URL of your FlintAI instance                                                          |
| `flint_token`     | yes      | API key for your FlintAI instance                                                     |

## About
Scans the repository contents for AI usage and reports findings back to FlintAI.

[Learn more](https://www.flintai.dev/).
