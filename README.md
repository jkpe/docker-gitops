# docker-compose gitops

1. commit a docker-compose
2. setup github action workflow
3. renovate looks for new releases and creates PRs
4. merge that PR and github actions triggers a ssh via tailscale, copies the new docker-compose.yml and docker-compose up -d

### Updating Tailscale as a dependancy

#### Renovate

If you already use [Renovate](https://docs.renovatebot.com/) to keep dependancies up to date you can use the [regex manager](https://docs.renovatebot.com/modules/manager/regex/) to keep the version of Tailscale used in your GitHub Action up to date by defining it as a dependency.

Here is an example of `renovate.json` that will look for the version string and compare it against the latest [tailscale/tailscale](https://github.com/tailscale/tailscale) GitHub Release.

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "config:recommended"
  ],
  "customManagers": [
    {
      "customType": "regex",
      "fileMatch": ["^(workflow-templates|\.(?:github|gitea|forgejo)/workflows)/[^/]+\.ya?ml$"],
      "matchStrings": ["uses: tailscale\\/github-action@v2(?:\\s+.*\\n)*?.*version: (?<currentValue>.*?)\\n"],
      "depNameTemplate": "tailscale/tailscale",
      "datasourceTemplate": "github-releases"
    }
  ]
}
```