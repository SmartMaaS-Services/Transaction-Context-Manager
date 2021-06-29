<h1 align="center">
  <br>
  <a href="https://github.com/SmartMaaS-Services/Transaction-Context-Manager/blob/main/docs/images/Header.jpeg"><img src="https://github.com/SmartMaaS-Services/Transaction-Context-Manager/blob/main/docs/images/Header.jpeg" alt="SmartMaaS Header" width="500"></a>
  <br>
      Dataspace Connector
  <br>
</h1>

<img src="docs/images/Header.jpeg">

<p align="center">
  <a href="mailto:info@dataspace-connector.de">Contact</a> •
  <a href="#contributing">Contribute</a> •
  <a href="https://international-data-spaces-association.github.io/DataspaceConnector/">Docs</a> •
  <a href="https://github.com/International-Data-Spaces-Association/DataspaceConnector/issues">Issues</a> •
  <a href="#license">License</a>
</p>


***

<h3 align="center" >
  <a href="https://international-data-spaces-association.github.io/DataspaceConnector/">
    Manual & Documentation
  </a>
</h3>

<details>
<summary><strong>Table of Contents</strong></summary>

- [Smart-Platform-Services (Slim Starter)](#smart-platform-services-slim-starter)
	- [Content](#content)
	- [Prerequisites](#prerequisites)
		- [Technical requirements](#technical-requirements)
		- [Maxmind license](#maxmind-license)
		- [PayPal account](#paypal-account)
	- [Deployment](#deployment)
		- [Preperation of VM](#preperation-of-vm)
		- [Clone the project files](#clone-the-project-files)
		- [Setup script #1](#setup-script-1)
		- [Setup first Umbrella users](#setup-first-umbrella-users)
		- [Setup script #2](#setup-script-2)
	- [Configuration](#configuration)
		- [Configure Keyrock (Identity Manager)](#configure-keyrock-identity-manager)
			- [Change admin user credentials](#change-admin-user-credentials)
			- [Create a standard user](#create-a-standard-user)
			- [Organizations and applications](#organizations-and-applications)
			- [Roles and permissions](#roles-and-permissions)
				- [Standard roles](#standard-roles)
				- [Custom roles](#custom-roles)
				- [Create role](#create-role)
				- [Create permission](#create-permission)
				- [Assign permission to role](#assign-permission-to-role)
				- [Assign role to user](#assign-role-to-user)

</details>


```
<key>|<value>|<key>|<value>|<key>|<value> etc..
```

-   `i` (device ID): Device ID (unique for the API Key).
-   `k` (API Key): API Key for the service the device is registered on.
-   `t` (timestamp): Timestamp of the measure. Will override the automatic IoT Agent timestamp (optional).
-   `d` (Data): Ultralight 2.0 payload.

The `i` and `k` parameters are mandatory.

> <b><i>NOTE:</i></b> This project is a forked and revised "slim starter" version of the original project which can be found here: https://github.com/SmartMaaS-Services/dev.smartmaas.services.

### Setup script #2 ###

Run the second script which will create Umbrella Website backends, Keyrock applications and roles. It also configures and deploys the remaining services of the platform. The following options are supported:

<pre>
<i>Mandatory options:</i>  
<b>--domain</b>             domain name (MUST be the same value as in first setup script!) 
<b>--api-key</b>            API Key of the first created Umbrella user  
<b>--token</b>              Admin API Token of the first created Umbrella admin  
<b>--stack</b>              stack name for the Docker Swarm - can be chosen freely and will be used as name prefix for Docker container and networks (MUST be the same value as in first setup script!) 

<i>Optional options:</i>  
<b>--bae-paypal-id</b>      PayPal client ID to be used when using PayPal as payment gateway in BAE Marketplace  
<b>--bae-paypal-secret</b>  PayPal client secret  
<b>--version</b>            prints out the script's version  
<b>--help</b>               prints out usage information and these options
</pre>

> <i>NOTE:</i> Options `--domain` and `--stack` must have assigned the same values as in first setup script. Omitting the `--bae-paypal*` options will disable marketplace payments. Also don't forget about the single quotes ('') here.


#### GET data ####

Now to query the created entity with the same user, we send a GET request to the Orion v2, again specifying the `Fiware-Service` and the `Authorization` header as before:

```js
curl --location --request GET 'https://context.example.org/v2/entities?id=DHT22_8892' \
--header 'Fiware-Service: exampleinc' \
--header 'Authorization: Bearer 4543a954065073f235e776861e3d96bd8a8b49e3'
```

On success, the server should reply with a `200 OK` and contain the requested entity object in the HTTP body:

```js
[
    {
        "id": "DHT22_8892",
        "type": "WeatherObserved",
        "dateObserved": {
            "type": "DateTime",
            "value": "2021-03-30T08:43:04.00Z",
            "metadata": {}
        },
        "location": {
            "type": "geo:json",
            "value": {
                "type": "Point",
                "coordinates": [
                    10.118,
                    54.332
                ]
            },
            "metadata": {}
        },
        "refDevice": {
            "type": "Relationship",
            "value": "Device_4482",
            "metadata": {}
        },
        "relativeHumidity": {
            "type": "Number",
            "value": 0.999,
            "metadata": {}
        },
        "stationName": {
            "type": "Text",
            "value": "DHT22_8892",
            "metadata": {}
        },
        "temperature": {
            "type": "Number",
            "value": 7.6,
            "metadata": {}
        }
    }
]
```



Example:
```bash
./scripts/setup-part2.sh --domain 'example.org' --api-key 'GKix62HPfoCtGyAV2CXTte4JvWrjvFJZwVl7e9EO' --token 'tUWTKOqbFDvgnA2oZgsxHQDk6j1G5se86aTYBrcS' --bae-paypal-id 'mOh69Fg852kXlY7vhkki62jTFlu7Nwbt' --bae-paypal-secret 'JpOrhdL7HXN6SP5Ve9uYup26iHeaSpYG' --stack 'swarm-test-stack'
```

### Maxmind license ###

APInf Umbrella needs a Maxmind License in order to use GeoIP location information. Please request your own free license key at [Maxmind](https://www.maxmind.com/en/request-service-trial?service_geoip=1).

> <i>NOTE:</i> This step is very important, because the APInf Umbrella installation will not work - to be exact, the docker service would not even start up without a valid Maxmind license!
  
<p align="center">
	<img src="docs/img/setup/maxmind/maxmind_request_service_trial.png" alt="Image of sign-up page for free Maxmind service trial" width="80%">
</p>




```yaml
tutorial:
    image: fiware/tutorials.ngsi-ld
    hostname: iot-sensors
    container_name: fiware-tutorial
    networks:
        - default
    expose:
        - "3000"
        - "3001"
    ports:
        - "3000:3000"
        - "3001:3001"
    environment:
        - "DEBUG=tutorial:*"
        - "PORT=3000"
        - "IOTA_HTTP_HOST=iot-agent"
        - "IOTA_HTTP_PORT=7896"
        - "DUMMY_DEVICES_PORT=3001" # Port used by the dummy IOT devices to receive commands
        - "DUMMY_DEVICES_API_KEY=4jggokgpepnvsb2uv4s40d59ov"
```

The `tutorial` container is driven by environment variables as shown:

| Key                   | Value                        | Description                                                                                                                                                                        |
| --------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEBUG                 | `tutorial:*`                 | Debug flag used for logging                                                                                                                                                        |
| WEB_APP_PORT          | `3000`                       | Port used by web-app which displays the dummy device data                                                                                                                          |
| IOTA_HTTP_HOST        | `iot-agent`                  | The hostname of the missing IoT Agent - used in a later tutorial                                                                                                                   |
| IOTA_HTTP_PORT        | `7896`                       | The port that the missing IoT Agent will be listening on. `7896` is a common default for UltraLight over HTTP                                                                      |
| DUMMY_DEVICES_PORT    | `3001`                       | Port used by the dummy IoT devices to receive commands                                                                                                                             |
| DUMMY_DEVICES_API_KEY | `4jggokgpepnvsb2uv4s40d59ov` | Random security key used for UltraLight interactions - this will be used in a later tutorial to ensure the integrity of interactions between the devices and the missing IoT Agent |

The other `tutorial` container configuration values described in the YAML file are not used in this tutorial.

## How to Deploy?

The most easy way to deploy Draco is running the container available on DockerHub.

Start a container for this image by typing in a terminal:

     $ docker run --name draco -p 8080:8080 -p 5050:5050 -d ging/fiware-draco

However if you want to have a custom installation please go to the **Installation and Administration Guide** at
[readthedocs.org](docs/installation_and_administration_guide/README.md)


## What is Draco?

This project is part of [FIWARE](http://fiware.org), as part of the Core Context Management Chapter .

Draco is a is an easy to use, powerful, and reliable system to process and distribute data. Internally, Draco is based
on [Apache NiFi](https://nifi.apache.org/docs.html), NiFi is a dataflow system based on the concepts of flow-based
programming. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation
logic. It was built to automate the flow of data between systems. While the term 'dataflow' is used in a variety of
contexts, we use it here to mean the automated and managed flow of information between systems.

| :books: [Documentation](https://fiware-draco.rtfd.io) | :mortar_board: [Academy](https://fiware-academy.readthedocs.io/en/latest/core/draco) | :whale: [Docker Hub](https://hub.docker.com/r/ging/fiware-draco) | :dart: [Roadmap](docs/roadmap.md) |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------- | --------------------------------- |

```console
docker-compose -v
docker version
```

#### :one: Request:

## Docker

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/FIWARE/tutorials.IoT-Sensors/NGSI-LD/docker-compose.yml) is used configure
the required services for the application. This means all container services can be brought up in a single command.
Docker Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux users will need
to follow the instructions found [here](https://docs.docker.com/compose/install/)


## Why use Draco?

Draco is designed to run specific set of processors and templates for persistence context data to multiple sinks.

Current stable release is able to persist the following sources of data in the following third-party storages:

-   NGSI-like context data in:
    -   [MySQL](https://www.mysql.com/), the well-known relational database manager.
    -   [MongoDB](https://www.mongodb.org/), the NoSQL document-oriented database.
    -   [PostgreSQL](http://www.postgresql.org/), the well-known relational database manager.
    -   [Cassandra](http://cassandra.apache.org/), Distributed database.
    -   [Carto](https://carto.com/), for geospatial Data
    -   [HDFS](https://hadoop.apache.org), High Distributed filesystem.
    -   [DynamoDB](https://aws.amazon.com/es/dynamodb/), A cloud key-value Amazon DB. 



***

## Quick Start

# IoT Sensors[<img src="https://img.shields.io/badge/NGSI-LD-d6604d.svg" width="90"  align="left" />](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.04.01_60/gs_cim009v010401p.pdf)[<img src="https://fiware.github.io/tutorials.IoT-Sensors/img/fiware.png" align="left" width="162">](https://www.fiware.org/)<br/>

[![FIWARE IoT Agents](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/iot-agents.svg)](https://github.com/FIWARE/catalogue/blob/master/iot-agents/README.md)
[![License: MIT](https://img.shields.io/github/license/fiware/tutorials.IoT-Sensors.svg)](https://opensource.org/licenses/MIT)
[![Support badge](https://img.shields.io/badge/tag-fiware-orange.svg?logo=stackoverflow)](https://stackoverflow.com/questions/tagged/fiware)
[![UltraLight 2.0](https://img.shields.io/badge/Payload-Ultralight-27ae60.svg)](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
<br/> [![Documentation](https://img.shields.io/readthedocs/fiware-tutorials.svg)](https://fiware-tutorials.rtfd.io)

This tutorial is an introduction to IoT devices and the usage of the
[UltraLight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
Protocol for constrained devices. The tutorial introduces a series of dummy agricultural IoT devices which are displayed
within the browser and allows a user to interact with them. A complete understanding of all the terms and concepts
defined in this tutorial is necessary before proceeding to connect the IoT devices to an NGSI-LD context broker via a
real IoT Agent.

The tutorial uses [cUrl](https://ec.haxx.se/) commands throughout, but is also available as
[Postman documentation](https://fiware.github.io/tutorials.IoT-Sensors/ngsi-ld.html)

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/1805fa92c4d6abaa374f)

-   このチュートリアルは[日本語](README.ja.md)でもご覧いただけます。

## Contents

<details>
<summary><strong>Details</strong></summary>

-   [What are IoT devices?](#what-are-iot-devices)
-   [What is Ultralight 2.0?](#what-is-ultralight-20)
    -   [Southbound Traffic (Commands)](#southbound-traffic-commands)
        -   [Push Command using HTTP POST](#push-command-using-http-post)
    -   [Northbound Traffic (Measurements)](#northbound-traffic-measurements)
        -   [Measurement using HTTP GET](#measurement-using-http-get)
        -   [Measurement using HTTP POST](#measurement-using-http-post)
-   [Architecture](#architecture)
-   [Prerequisites](#prerequisites)
    -   [Docker](#docker)
    -   [Cygwin](#cygwin)
-   [Start Up](#start-up)
-   [Communicating with IoT Devices](#communicating-with-iot-devices)
    -   [Irrigation System Commands](#irrigation-system-commands)
        -   [Turn on the Irrigation System](#turn-on-the-irrigation-system)
        -   [Turn off the Irrigation System](#turn-off-the-irrigation-system)
    -   [Tractor Commands](#tractor-commands)
    -   [FMIS System Commands](#fmis-system-commands)
        -   [Activate a Tractor](#activate-a-tractor)
        -   [Deactivate a Tractor](#deactivate-a-tractor)
    -   [Filling Station Commands](#filling-station-commands)
        -   [Remove Hay from the Barn](#remove-hay-from-the-barn)
    -   [Sending Measures](#sending-measures)

</details>


## Usage: Overview

The best way to start with Draco is following the **Quick Start Guide** found at readthedocs.org and it provides a good
documentation summary ([Draco](docs/quick_start_guide.md)).

Nevertheless, both the **Installation and Administration Guide** also found at
[readthedocs.org](docs/installation_and_administration_guide/README.md) cover more advanced topics.

The **Processors Catalogue** completes the available documentation for Draco
([Draco](docs/processors_catalogue/README.md)).

## Training courses

### Academy Courses

Some lessons on Draco Fundamentals will be offered soon in the
[FIWARE Academy](https://fiware-academy.readthedocs.io/en/latest) .

### Examples

Several examples are provided to facilitate getting started with GE. They are hosted in the official documentation at
[Read the Docs](https://fiware-draco.readthedocs.io/en/latest/quick_start_guide/index.html).

## Testing

In order to test the code:

    $mvn clean test -Dtest=Test* cobertura:cobertura coveralls:report -Padd-dependencies-for-IDEA

## Quality Assurance

This project is part of FIWARE and has been rated as follows:

-   **Version Tested:** TBD
-   **Documentation:** TBD
-   **Responsiveness:** TBD
-   **FIWARE Testing:** TBD

## Roadmap

The list of features that are planned for the subsequent release are available in the
[ROADMAP](https://github.com/ging/fiware-draco/blob/develop/docs/roadmap.md) file.

## Maintainers

[@anmunoz](https://github.com/anmunoz).


Next Steps
Want to learn how to add more complexity to your application by adding advanced features? You can find out by reading the other tutorials in this series

License
MIT © 2020 FIWARE Foundation e.V.

![](https://fiware.github.io/tutorials.IoT-Sensors/img/device-measures.png)

Once the door is locked, no further customers may enter. The Motion Sensor will report no further movement detected, the Smart Door cannot be opened manually and the Smart Lamp will slowly return to the ambient lighting level.

## Licensing

Draco Except as otherwise noted this software is licensed under the Apache License, Version 2.0 Licensed under the
Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may
obtain a copy of the License at `http://www.apache.org/licenses/LICENSE-2.0` Unless required by applicable law or agreed
to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and
limitations under the License.

## Reporting issues and contact information

Any doubt you may have, please refer to the
[Draco Core Team](docs/installation_and_administration_guide/issues_and_contact.md).

## Contribution ##

Pull requests are welcome. Please make sure to update tests as appropriate.
Git conventions are being followed and changes go to development only from feature/bugfix branches.

## License ##

Smart-Platform-Services is licensed under Affero General Public License (GPL) version 3.

© 2020-2021 FIWARE Foundation


## License
Copyright © 2020 Fraunhofer ISST. This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) for details.
