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


## License
Copyright © 2020 Fraunhofer ISST. This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) for details.
