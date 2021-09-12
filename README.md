<h2 align="center">
  <a href="https://smart-maas.eu/en/"><img src="https://github.com/SmartMaaS-Services/Transaction-Context-Manager/blob/main/docs/images/Header.jpeg" alt="Smart MaaS" width="500"></a>
  <br>
      SMART MOBILITY SERVICE PLATFORM
  <br>
  <a href="https://smart-maas.eu/en/"><img src="https://github.com/SmartMaaS-Services/Transaction-Context-Manager/blob/main/docs/images/Logos-Smart-MaaS.png" alt="Smart MaaS" width="250"></a>
  <br>
</h2>

<p align="center">
  <a href="mailto:info@smart-maas.eu">Contact</a> •
  <a href="https://github.com/SmartMaaS-Services/Transaction-Context-Manager/issues">Issues </a> •
  <a href="https://smart-maas.eu/en/">Project Page</a>
</p>


***

<h1 align="center">
  <a>
    Transaction Context Manager
  </a>
</h1>

It is a generic building block to process data from a big variety of datasources and processing frameworks on a transaction basis. It offers a new interaction pattern that offers new ways of data processing, brokering and marketing.

The Smart MaaS demo applications are alreay published and available in the file https://github.com/SmartMaaS-Services/Transaction-Context-Manager/blob/main/Transaction-Context-Manager.xml here in the repo. It is a Apache Nifi template that is ready for usage and it contains integrates parts of 
- the Flixbus API for buying tickets for Flixbus and Flixtrain
- the TripGo API for obtaining individual routing
- the KillBill API for handling payments and provide clearing and subscription capabilites
- the EsriGIS datasource for charging stations in Germany

You can simply import the template into Nifi, but for full operation you need the following (you can use parts to start working with some APIs):
- A Nifi instance 
- A Orion-LD instance
- Both instances must be available to connect to each other
- Auth Token for connecting to the Context broker
- Credentials to connect to the Flixbus API
- Credentials to connect to the TripGo API
- A running instance of Killbill with its credentials 
