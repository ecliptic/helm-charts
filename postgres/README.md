# PostgreSQL

A [Helm](https://helm.sh/) chart to bootstrap a single node PostgreSQL deployment on a Kubernetes cluster using the official [Docker image](https://hub.docker.com/_/postgres/).

## Installing the Chart

To install the chart with the release name `my-release`:

```sh
$ helm install --name my-release .
```

The command deploys PostgreSQL on the Kubernetes cluster in the default configuration. The configuration section below lists the parameters that can be configured during installation.

By default a random password will be generated for the user. If you'd like to set your own password change the postgresPassword in the values.yaml.

You can retrieve the password by running the following command:

```sh
printf $(printf '\%o' `kubectl get secret [YOUR_RELEASE_NAME]-postgres -o jsonpath="{.data.postgres-password[*]}"`)
```

## Uninstalling the Chart

To delete the `my-release` deployment:

```sh
$ helm delete my-release
```

To purge it so you can re-use the name:

```sh
$ helm delete --purge my-release
```

## Configuration

| Parameter                  | Description                        | Default                                                    |
| -----------------------    | ---------------------------------- | ---------------------------------------------------------- |
| `imageTag`                 | `postgres` image tag.                 | Most recent release                                        |
| `postgresUser`                | Username of new user to create.    | `nil`                                                      |
| `postgresPassword`            | Password for the new user.         | `nil`                                                      |
| `postgresDatabase`            | Name for new database to create.   | `nil`                                                      |
| `persistence.enabled`      | Create a volume to store data      | true                                                       |
| `persistence.size`         | Size of persistent volume claim    | 8Gi RW                                                     |
| `persistence.storageClass` | Type of persistent volume claim    | generic                                                    |
| `persistence.accessMode`   | ReadWriteOnce or ReadOnly          | ReadWriteOnce                                              |

Some of the parameters above map to the env variables defined in the [PostgreSQL DockerHub image](https://hub.docker.com/_/postgres/).
