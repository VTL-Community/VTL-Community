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
* specify mechanisms for acessing and understanding external data (e.g. CSV files)
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
* Github: create Github organisation VTL-Community and move repo there
  --> add folder for files such as presentations, training material... as long as it is not commercial

Discussed in meeting 07/09/2021:
* Official SDMX VTL-TF is responsilbe for official VTL releases and documentation
* This community can gather interested developers, users, and experts to share experice and code, discuss issues and change request and communicate to the VTL-TF
* we should find a slot for a regular community meeting --> first Tuesday of the month 3pm-5pm central European time
  --> next meeting 5th Oct: wrap-up of communication during SDMX global conf
  --> presentation of Antonio or work done by his company 
* information about the community will be shared through the SDMX global conference (Antonio, Katrin)

#### Issue management:
* We can encourage users and developers to post issues on the community issues tab
* Once issues are discussed and closed, we can add solutions and example to the Q&A page

#### Testing: there is an issue on creating data within VTL for testing
Could we work on a test suite?

#### Engines
Is there an opportuntiy to merge Trevas with the BdI engine? Currently architecture and coverage are slightly different.
BdI engine is stronger in memory and user dashboard for testing, Trevas is stronger in terms of Spark deployment for large jobs / scalability.
Idea: Spark can run locally in memory as well

### Known related repos
* Trevas Java engine done by INSEE: https://github.com/InseeFr/Trevas
* Trevas JS JavaScript engine done by INSEE: https://github.com/InseeFr/Trevas-JS
* ISTAT OSS VTL Framework https://github.com/VTLFrameworkDevelopment/VTLFramework
* Banca d'Italia VTL Engine & Editor: https://github.com/vpinna80/VTL 
* Meaningful Data open source library for SDMX available in PyPi and on https://github.com/Meaningful-Data/sdmxthon 
