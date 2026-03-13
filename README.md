# MyPelo Deploy Runner

> CI/CD runner for [MyPelo](https://mypelo-web.pages.dev) — builds and deploys user projects to Cloudflare Pages / Workers via GitHub Actions.

## How It Works

1. User connects GitHub + Cloudflare on MyPelo
2. User selects a GitHub repo to deploy
3. MyPelo dispatches a workflow here via GitHub API
4. This runner:
   - Clones the user's repo
   - Runs `npm install` + `npm run build`
   - Deploys to user's Cloudflare account using their API token
5. Deployment status is sent back to MyPelo via webhook

## Workflow Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `repo_url` | ✅ | GitHub repo URL (`https://github.com/user/repo`) |
| `repo_branch` | - | Branch to deploy (default: `main`) |
| `cf_api_token` | ✅ | User's Cloudflare API Token |
| `cf_account_id` | ✅ | User's Cloudflare Account ID |
| `project_name` | ✅ | CF Pages or Worker project name |
| `project_type` | ✅ | `pages` or `worker` |
| `build_command` | - | Build command (default: `npm run build`) |
| `output_dir` | - | Build output dir (default: `dist`) |
| `callback_url` | - | MyPelo webhook URL for status updates |
| `deployment_id` | - | MyPelo deployment ID |

## Security

- CF API tokens are passed as runtime inputs, never stored in this repo
- The runner only has read access to user repos (via `MYPELO_GITHUB_TOKEN` secret)
- All deployments use the user's own Cloudflare credentials

## License

MIT
