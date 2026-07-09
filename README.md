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
          flintai_instance: https://some_url
          flintai_token: ${{ secrets.FLINTAI_TOKEN }}
          llm_model: anthropic:claude-opus-4-8
          llm_api_key: ${{ secrets.LLM_API_KEY }}
```

## Properties
Properties are passed to GitHub Action via explicit `with` input variables. For security, we strongly recommend using [GitHub secrets](https://docs.github.com/en/enterprise-cloud@latest/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets) for the sensitive input variables `flintai_token` and `llm_api_key`.


| Property            | Required | Description                                                                                                                              |
| ------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `flintai_instance`  | yes      | URL of your FlintAI instance                                                                                                            |
| `flintai_token`     | yes      | API key for your FlintAI instance                                                                                                       |
| `llm_model`         | yes      | LLM to use, in the form `<provider>:<model>`. Supported providers: `anthropic`, `openai`, `gemini`/`google` (e.g. `anthropic:claude-opus-4-8`). |
| `llm_api_key`       | yes      | API key for the provider selected in `llm_model`. The action forwards it to the scanner under the provider-native name (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, or `GOOGLE_API_KEY`). |

## About
Scans the repository contents for AI usage and reports findings back to FlintAI.

[Learn more](https://www.flintai.dev/).
