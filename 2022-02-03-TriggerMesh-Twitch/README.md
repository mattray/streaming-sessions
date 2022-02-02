# TriggerMesh Twitch

Rough outline:
 * Install Knative on K3s
 * Install [TriggerMesh](https://docs.triggermesh.io/guides/installation/)
 * [gtflp](https://github.com/JeffNeff/gtflp) for viewing events with [config](config/gtflp-release.yaml)
 * [IBM MQ server](config/mq-server.yaml)
   * You should be able to access the MQ Server at https://localhost:9443/ibmmq/console/ accept the certificate, and login with the user `admin` and password `passw0rd`.
 * [MQ source](config/mq-source.yaml)
