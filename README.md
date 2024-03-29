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

- Week 6<br>

1. EV adoption distribution: how to decide which households have EVs?

**build logistic regression (binary model)**

- add red

**clustering based on questionaire**

- Potential Early Adopters of Hybrid and Electric Vehicles in Spain—Towards a Customer Profile

  basic idea: The author made a survey of EV purchase intention with ~400 people in different backgroup. For each respondent, socio-ecnomic features (gender, income, age) are considered.Apart from them, range anxiety, price, and morality are also considered.

  The author then applied clustering algorithm to divide the people into two groups (people with stronger purchase will and weak one). The average purchase scores are 5.4 and 4.5 (out of 7), respectively.

**Assume a fixed EV penetration rate**

- Distribution and scale studies of public charging stations considering EVs' optimal charging choose-2016
  : assume the total number of vehicle is 80,000, and 10% of them are EVs.

**Assume a fixed EV penetration rate and build a propbability model**

- Simulation-optimization model for location of a public eletric vehicle charging infrastruture-2013, part E:

  - apply variables including household num of vehicles, household income, education level, gender, driving age, price of gas and electrivity to infer the probability of EV adoption for each household (0.21-0.39)
  - assume 1% peneration of EV over all vehicles, and then scale such probability.

  We can use this approach based on WFRC data.

  What useful socio-economic features WFRC data have?

  household size , the number of household, and average income (based on TAZ level?).

  concern: we dont have other important features such as the num of vehicles for each household, gender, educational level, age etc.

- Week 7<br>

ATUS data:
Target: re-define the activities for EV use purpose.

Solutions:

- use activity code to classify the types of activity that relate to EV public charging behavior.
- use the location as the reference to define the activities that relate to EV public charging behavior.

Idea: classify the activities based on the location instead of the activity codes. Since the activitiy code is very detailed level of activity, and there are lots of activity we do not really need.

- Place:
  1. home
- transferring status:
  1. car (driving)
- locations where user could potentially use EVs:

  1. workplace
  2. other people's home
  3. restaurant or bar
  4. place of worship
  5. grocery store
  6. other store/mall
  7. school
  8. outdoors
  9. library
  10. gym
  11. other place

- locations that are not related to EV use:

  1. car (passenger)
  2. walking
  3. bus
  4. subway
  5. bicyle
  6. boat
  7. taxi
  8. airplane
  9. other transportation mode
  10. bank
  11. post office
  12. unspecific place

- Week 8<br>
  - genrate synthetical vehicle distribution
  - discuss with Dr. Chen: can we use ATUS data to generate the vehicle trajectory based on daily activities?
    - possible solution:
      - when we use MC to generate activity data, the activity "driving" bridges different types of activities. For instance, "home" ---> "driving" ---> "work".
      - driving activity has specific time. we use POI data to find one office building that has similar travel time with driving activity.
      - problem: this is basically drawing a circle. Random effect is very large.

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

---

## FAQs
