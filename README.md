# docker-compose gitops

1. commit a docker-compose
2. setup stack in portainter on relevant host
3. renovate looks for new releases and creates PRs
4. merge and github actions triggers a webhook for portainer to pull the new docker-compose
