# VTL Community

## Towards a community of VTL developers

### Vision

Several organizations are developing tools related to VTL. Coordinating these developments would bring more clarity for VTL users and avoid duplicating work.

In order to establish such a collaboration, it is proposed to set up a community based on the open source principles and methods.

### Members

The first members of the community are: Banca d'Italia, the European Central Bank and Insee (French Statistical Office). The community welcomes additional members.

### Objectives

The general objectives are interoperability and promotion of the VTL tools developed by the community members.

The following specific subjects have already been identified:

* design a standard REST API for VTL engines

* document the interoperability mechanism based on an abstract engine

* develop a test common framework, or even a conformance benchmark

* create communication material (guides, success stories, business cases) for the promotion of VTL tools

### Open discussion points

#### Enlarging the group
* For the next meeting, add "usual suspects" in Eurostat, OECD, Antonio Olleros

#### Marketing towards business users
* SQL or Python instead of VTL if you speak to a IT savvy audience
* Nothing if you speak to a statistican non-IT savvy audience
* In ECB, users cannot use Spark in production. VTL could help them to utilise Spark through VTL on big datasets
* In BdI, users can use Spark but applications cannot
* Norway: no tight dependency between VTL and Spark

#### Governance: (linked to the above)
* Gap: current SDMX TWG TF is not very active and responsive for VTL fixes and enhancements
* INSEE: approach of "active metadata" for business users - we can elaborate in the next meeting

#### Issues on structural metadata:
What to do when the data files do not have structural information? E.g. a CSV file does not tell to VTL which columns are dimensions, attributes, measures.

_Hadrien:_ assumption in their implementation is that every column is a measure. Once you use a group-by, the concepts in the group-by clause are treated as identifiers

* Option 1: create SDMX DSD to cover the files, the connector is ready and standardised
* Option 2: use another metadata standard (DPM? DDI?) and write a connector for VTL
* Option 3: lightweight way to define VTL data models --> e.g. separate metadata JSON or CSV file with column name/number and D/A/M to give strcutre to the VTL scripts
  * SSB and ECB each have a JSON strcuture to define metadata. We can agree on a target structure spec as a future VTL-native alternative to SDMX for cases where SDMX is not available 
  * Issue: data type defintions, e.g. date string patterns. VTL differs from XML and Java and probably we should use VTL syntax
  * __Action:__ draft a JSON structure based on the two existing:
  https://github.com/FranckCo/VTL-Community/issues/1

#### Testing: there is an issue on creating data within VTL for testing
Could we work on a test suite?

#### Engines
Is there an opportuntiy to merge Trevas with the BdI engine? Currently architecture and coverage are slightly different.
BdI engine is stronger in memory and user dashboard for testing, Trevas is stronger in terms of Spark deployment for large jobs / scalability.
Idea: Spark can run locally in memory as well

### Known related repos
* Trevas Java engine done by INSEE: https://github.com/InseeFr/Trevas
* Trevas JS JavaScript engine done by INSEE: https://github.com/InseeFr/Trevas-JS
* Banca d'Italia SDMX Connectors: https://github.com/amattioc/SDMX
* Meaningful Data open source library for SDMX available in PyPi and on https://github.com/Meaningful-Data/sdmxthon 