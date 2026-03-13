# Roblox Luau Execution Action 🎮

[![GitHub Release](https://img.shields.io/github/v/release/thegamerbay/roblox-luau-execution-action?style=flat-square)](https://github.com/thegamerbay/roblox-luau-execution-action/releases)
[![Lint Code and Workflows](https://github.com/thegamerbay/roblox-luau-execution-action/actions/workflows/lint.yml/badge.svg)](https://github.com/thegamerbay/roblox-luau-execution-action/actions/workflows/lint.yml)
[![Update Major Tag](https://github.com/thegamerbay/roblox-luau-execution-action/actions/workflows/release.yml/badge.svg)](https://github.com/thegamerbay/roblox-luau-execution-action/actions/workflows/release.yml)
[![License](https://img.shields.io/github/license/thegamerbay/roblox-luau-execution-action?style=flat-square)](https://github.com/thegamerbay/roblox-luau-execution-action/blob/main/LICENSE)

A composite GitHub Action that seamlessly integrates with the **Roblox Open Cloud API**. It uploads a built `.rbxl` place file to your Universe and executes a Luau test script (like TestEZ) directly on Roblox servers.

## 🚀 Features
* **Zero Dependencies:** Runs on pure Python standard libraries, meaning execution starts instantly without waiting for `pip install`.
* **Automated Polling:** Automatically creates the task, polls the Roblox servers, and fetches the execution logs.
* **Native Integration:** Prints logs natively in GitHub Actions groups and correctly sets the exit code so your CI fails if your tests fail.

## 🛠 Usage

To use this action in your CI/CD pipeline, add the following step after building your `.rbxl` file (e.g., with Rojo).

```yaml
- name: Upload & Run Tests via Open Cloud
  uses: thegamerbay/roblox-luau-execution-action@v1
  with:
    api_key: ${{ secrets.ROBLOX_API_KEY }}
    universe_id: ${{ vars.ROBLOX_TEST_UNIVERSE_ID }}
    place_id: ${{ vars.ROBLOX_TEST_PLACE_ID }}
    place_file: 'dist.rbxl'
    script_file: 'tasks/runTests.luau'
```

## 📥 Inputs

| Input | Required | Default | Description |
| --- | --- | --- | --- |
| `api_key` | Yes |  | Your Roblox Open Cloud API Key with `universe.places:write` and `universe.place.luau-execution-session:write` permissions. |
| `universe_id` | Yes |  | Target Roblox Universe ID. |
| `place_id` | Yes |  | Target Roblox Place ID. |
| `place_file` | Yes |  | Path to your compiled place file (e.g., `dist.rbxl`). |
| `script_file` | Yes |  | Path to the Luau script to run on the server. |
| `publish` | No | `false` | Set to `true` to Publish the place instead of just Saving it. |

## 📤 Outputs

| Output | Description |
| --- | --- |
| `task_status` | The final state of the task (e.g., `COMPLETE`, `FAILED`). |
| `task_logs` | The raw string of logs returned by the execution task. |

## 📄 License

This project is licensed under the MIT License.
