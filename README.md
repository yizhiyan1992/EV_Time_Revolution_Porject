# EV_Time_Revolution_Porject

## Table of content

- [Project Description](#Project-Description)
- [Progress](#Progress)
- [MATSim Guide](#MATSim-Guide)
- [References](#References)
- [FAQs](#FAQs)

---

## Project Description

---

## Progress

- Week 4</br>
  Discuss with Dr. Chen for the third program

  1. There are two approaches for sampling: pure markov chain and markov chain with duration sampling (the later one considers the probablity of duration for each activity). Either one would be good to perform. Former one is simpler.
  2. In the previous program, 12 activities are chosen. For our project, we need to redefine the activites that associate with the EV public charging (such as going to the restaurants). [to-do]
  3. Once the Markov chain is modeled, we will sample people with different activities using the MC. However, before we use them as inputs for MATSim, we need to map the activities with concrete places. [to-do]

  Keep reading the MATSim docs. (details see MATSim Guide)

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

## References

---

## FAQs
