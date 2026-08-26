# Flint AI Inventory Scan

A [GitHub Action](https://github.com/features/actions) for using [Flint AI](https://www.flintai.dev/). This action performs static analysis on your code to detect AI assets (such as models, agents, and MCP servers), creating an inventory. This inventory is then sent to your Flint AI instance, where it's enriched with additional information and analyzed for issues. You can view the results in the Flint AI web interface. Refer to the [Flint AI user guide](https://docs.flintai.dev/) for details.



## Configuration
You can configure the Action as shown in the following example::


```yaml
name: Example workflow for Python using Flint AI Inventory Scan
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@master
      - name: Run Flint AI Inventory detection
        uses: sandbox-quantum/flintai-codescan-action@main
        with:
          flintai_instance: https://app.flintai.dev
          flintai_token: ${{ secrets.FLINTAI_TOKEN }}
          llm_model: anthropic:claude-opus-4-8
          llm_api_key: ${{ secrets.LLM_API_KEY }}
```

## Properties
Properties are passed to GitHub Action via explicit `with` input variables. For security, we strongly recommend using [GitHub secrets](https://docs.github.com/en/enterprise-cloud@latest/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets) for the sensitive input variables `flintai_token` and `llm_api_key`.


| Property            | Required | Description                                                                                                                              |
| ------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `flintai_instance`  | yes      | URL of your Flint AI instance, e.g. `https://app.flintai.dev` (other environments: `https://dev.flintai.dev`, `https://staging.flintai.dev`).      |
| `flintai_token`     | yes      | API key for your Flint AI instance                                                                                                       |
| `llm_model`         | yes      | LLM to use, in the form `<provider>:<model>`. Supported providers: `anthropic`, `openai`, `gemini`/`google` (e.g. `anthropic:claude-opus-4-8`). |
| `llm_api_key`       | yes      | API key for the provider selected in `llm_model`. The action forwards it to the scanner under the provider-native name (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, or `GOOGLE_API_KEY`). |

## About
Scans the repository contents for AI usage and reports findings back to Flint AI.

[Learn more](https://www.flintai.dev/).
