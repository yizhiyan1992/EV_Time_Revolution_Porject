# EV_Time_Revolution_Porject

## Table of content

- [Project Description](#Project-Description)
- [Progress](#Progress)
- [MATSim Guide](#MATSim-Guide)
- [OSM data](#OSM-Data)
- [References](#References)
- [FAQs](#FAQs)

---

## Project Description

### Basic steps

- Population generation for EV owners and regular vehicle owners
- Daily activities sampling for each agent (people). A 24-hour time series activities.
- Build network for MATSim (including EV charging scenarios)
- Traffic assignments. Mapping out the activity events with specific geographical locations.

---

## Progress

- Week 1</br> add later
- Week 2</br> add later
- Week 3</br> add later
- Week 4</br>
  Discuss with Dr. Chen for the third program

  1. There are two approaches for sampling: pure markov chain and markov chain with duration sampling (the later one considers the probablity of duration for each activity). Either one would be good to perform. Former one is simpler.
  2. In the previous program, 12 activities are chosen. For our project, we need to redefine the activites that associate with the EV public charging (such as going to the restaurants). [to-do]
  3. Once the Markov chain is modeled, we will sample people with different activities using the MC. However, before we use them as inputs for MATSim, we need to map the activities with concrete places. [to-do]

  Keep reading the MATSim docs. (details see MATSim Guide)

  Quick look on OSM data.

- Week 5<br>

1. Compare using OSM data and UDOT .shp file for building the network.
2. Keep reviewing the MATSim guidance pdf
3. Literature review: how to generate EV household distribution?

---

## MATSim Guide

### Building blocks for the required files

1. config.xml
   containing the configuration options for MATSim
2. network.xml
   describe the road network
3. population.xml
   providing the information about travel demand (agent and daily plans)

#### Network.xml:

It contains nodes and links two types of object.

For each node, attributes include:

- ID
- x and y (coordinate)

For each link, attributes include:

- id
- length
- flow capacity
- freespeed
- the number of lanes
- modes {'car','bike','taxi'}

Note that each link is uni-directional.

Examples:

```xml
<network name= "example network">
<nodes>
<node id= "1" x= "0.0" y= "0.0" />
</nodes>

<links>
<link id= "1" from= "1" to= "2" length = "3000.00" capacity = "3600"
freespeed = "27.78" permlanes = "2"
</links>
</network>
```

#### population.xml

## OSM Data

OSM stands for OpenStreetMap. OSM data is free and public available data: [OpenStreetMap](https://www.openstreetmap.org/)

How to download OSM data:

- export data from [API](https://www.openstreetmap.org/). Can only download a small portion of the dataset given a bounding box.
- Full dataset dowload (100G)
- Large dataset download [HERE](https://download.geofabrik.de/). (two formats: **.osm.pbf** and **.osm.bz2**)

How to work with .osm.bpf data?
**PYROSM** is python API to manipulate the .osm.pbf data.
A tutorial on how to use PYROSM can be found [HERE](https://pyrosm.readthedocs.io/en/latest/basics.html). Besides, **osmnx** and **networkx** are the lower level API under the hood of PYROSM. They support extracting osm data using **overpassing API** internally as well.

A tutorial of using **PYROSM** to extract road network [HERE](https://github.com/yizhiyan1992/EV_Time_Revolution_Porject/blob/main/pyrosm_tutorial.ipynb).

A tutorial of using **osmnx** to extract road network [HERE](https://github.com/yizhiyan1992/EV_Time_Revolution_Porject/blob/main/osmnx_tutorial.ipynb).

> :warning: The **PYROSM** failed to extract road network in large area for unknown reason. Instead, **osmnx** is suggested to apply to extract large road network.

## References

### EV household distribution modeling

- **Potential Early Adopters of Hybrid and Electric
  Vehicles in Spain—Towards a Customer Profile**

  basic idea: The author made a survey of EV purchase intention with ~400 people in different backgroup. For each respondent, socio-ecnomic features (gender, income, age) are considered.Apart from them, range anxiety, price, and morality are also considered.

  The author then applied clustering algorithm to divide the people into two groups (people with stronger purchase will and weak one). The average purchase scores are 5.4 and 4.5 (out of 7), respectively.

  In their clustering analysis, it is found that <u> socio-economic factors play less important role in affecting EV purchase</u>. Instead, anxiety range is the most important factor to distinguish the two clusters.

---

## FAQs
