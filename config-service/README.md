#Netflix OSS Example - Config Service

##Introduction

This sevice will keep the configuration to be read by the micro-services. The objective is to have one centralized place to store the configuration.

##Quick Start

To compile:

```ShllSession
mvn clean package
```

To execute:

```ShellSession
java -jar target/config-service.jar
```

##Configuration

###bootstrap.yml

This is the first file read by the application when is run. This file contains the name of the application and where to find the configuration files.

The configuration files are stored in the following [git repository] (https://github.com/Oreste-Luci/netflix-oss-example-config-repo).

###application.yml

This file contains configurations for the port in which it should run, the eureka server to use, and the Actuator management path.

##Testing

Once the server is running it can be queried by:

```ShellSession
http://localhost:8888/{name}/{env}/{label}
```

Where:

* **name** is the application name
* **env** is the profile name (default by default)
* **label** is the branch name (master by default). This is optional and can be omitted.

For example:

```ShellSession
curl http://localhost:8888/serviceA/default/master | jq '.'
```

It should return something like this:

```json
{
  "name": "default",
  "label": "",
  "propertySources": [
    {
      "name": "https://github.com/Oreste-Luci/netflix-oss-example-config-repo/serviceA.properties",
      "source": {
        "default.message": "From default file"
      }
    }
  ]
}
```

If we know query for local we should get something like this:

```json
{
  "name": "local",
  "label": "",
  "propertySources": [
    {
      "name": "https://github.com/Oreste-Luci/netflix-oss-example-config-repo/serviceA-local.properties",
      "source": {
        "default.message": "From local file"
      }
    },
    {
      "name": "https://github.com/Oreste-Luci/netflix-oss-example-config-repo/serviceA.properties",
      "source": {
        "default.message": "From default file"
      }
    }
  ]
}
```
