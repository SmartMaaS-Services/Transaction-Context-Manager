<h1 align="center">
  <br>
  <a href="https://dataspace-connector.de/dsc_logo.svg"><img src="https://dataspace-connector.de/dsc_logo.svg" alt="Dataspace Connector Logo" width="200"></a>
  <br>
      Dataspace Connector
  <br>
</h1>


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



## License
Copyright © 2020 Fraunhofer ISST. This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) for details.
