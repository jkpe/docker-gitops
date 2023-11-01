# docker-compose gitops

1. commit a docker-compose
2. setup github action workflow
3. renovate looks for new releases and creates PRs
4. merge that PR and github actions triggers a ssh via tailscale, copies the new docker-compose.yml and docker-compose up -d
