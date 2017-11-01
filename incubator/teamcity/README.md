Helm chart for TeamCity
=======================

## Requirements

TeamCity depends on persistent storage to store server configuration settings,
project definitions and build results. Due to the fact that TeamCity needs to
re-start itself during the initial configuration the teamcity server has to be
configured with a working persistant volume claim. In most cases letting helm
dynamically create a persistent volume to attache to the included PVC should
work fine.

## Installation

```bash
helm install . --name my-release
```

## Exposing TeamCity through the load balacer

```bash
cat > local.yaml <<EOD
service:
  type: LoadBalancer
EOD
helm install . --name my-release --values local.yaml
```

## Customization

If you need to customize the deploy you have to extend the base Docker image.

You can specify an alternative container image or pin the deploy to a specific
TeamCity version by overriding some values:

```bash
cat > local.yaml <<EOD
image:
  repository: my-orga/teamcity-server
  tag: latest
EOD

helm install . --name my-release --values local.yaml
```

## Deploying a kubernetes build agent

## Deploying a DinD buld agent

* Remember to set the `dindagent.teamcityServerURL` after deploying teamcity
  and before deploying the dindagent.
