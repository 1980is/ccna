# Automation #
-   Python + Jinja2.
-   Python + Netmiko. Allows us to connect to our devices using SSH. It sends CLI commands over SSH. A newer way is to us APIs to connect and manage the devices but that’s only supported on newer devices.
-   Zero Touch Provisioning.
-   Look at the tool Postman for APIs.
-   **CRUD** = Create, Read, Update, Delete.

## Rest API ##

-   A restful API has six rules.
    -   Client-Server
    -   Stateless
    -   Cacheable
    -   Uniform interface
    -   Layered
    -   Code-On-Demand
-   When we enable the R est API on our router, it becomes the server and we are the client.

## Data Serialization Languages ##

- Data serialization is the process of converting structured data to a standardized format that allows sharing or storage of the data in a form that allows recover of its original structure.
- It allows transfer of the data between different systems, applications and programming languages. 
-  Types of DSL languages.
    -   xml
    -   json //need to know for the CCNA.
    -   yaml

## Ansible ##

-   It’s an agent-less solution.
-   Is based on Python.
-   Uses a push model.

## Puppet

-   It requires an agent.
-   Nexus switches run Linux so it’s possible to manage them using Puppet.
-   It’s based on Ruby.
-   Has a pull model.
-   Needs a Puppet Master Linux server.
-   Free edition manages 10 devices.

## Chef

-   It is written in Ruby.
-   Loved by developers.
-   It needs an agent.
-   It uses a central server called Recipes.
-   It is pull based.
-   It doesn’t work with Cisco devices currently.
 