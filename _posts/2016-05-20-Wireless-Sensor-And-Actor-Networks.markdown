---
title:  "Wireless Sensor And Actor Networks"
date:   2016-05-20 05:58:00
description: Overview of WSANs
---

WSNs consists of sensor nodes which can only sense the physical and environmental conditions but Wireless Sensor and Actor Networks (WSANs) along with sensor nodes consists of actor nodes that can act upon the physical environment. The term ‘actor’ is different from the notion of an ‘actuator’ in the sense that beside being able to act upon the environment using one or more actuators, it is also a network entity that performs network related functionalities like receiving, transmitting, processing and relaying data.   In order to provide effective sensing and acting a distributed local coordination mechanism is necessary among sensors and actors. Some of the key differences between them could be as follows:

1. Actor nodes present in WSANs typically have stronger computational abilities and high energy budget as compared to low power and inexpensive sensor nodes with limited computing and communication abilities.
2. Power concern is a major issue in WSN whereas real time communication may be a major concern in WSAN depending upon the application.
3. The cost of deploying a Wireless Sensor and Actor Network may be more than that of a similar Wireless Sensor Network.
4. The number of sensor nodes deployed may be in the order of hundreds or thousands but actor nodes dos not need such a dense deployment.
5. Unlike WSNs where the central entity (i.e. sink) performs the functions of data collection and coordination, in case of WSANs sensor-actor and actor-actor coordination is required.


### Characteristics of WSANs

In WSANs the sensor nodes collect data from the environment and the actor nodes performs action based on the sensed data. The sink node monitors the overall network and communicates with the task manager node and sensor and actor nodes. Depending on the type of application a Wireless Sensor and Actor Network can have two types of architecture:

1. Semi-Automated Architecture:  Sensors sensing a phenomenon route back the data to the sink which may issue some command to the actors. Because the sink (central controller) collects the data and coordinates the acting process this is called as a semi-automated architecture. 
2. Automated Architecture: Sensors transmit their reading to the actor nodes which process all incoming data and initiate appropriate actions. So because of non-existence of a central controller this is called as an automated architecture.

![Types of Architecture](../../assets/images/wsan.PNG)

Some of the advantages of the Automated Architecture could be as follows:

1. Low Latency:  Because of sensor-actor coordination the latency in case of WSANs in minimized.
2. Long Network Lifetime: In a Semi-Automated Architecture the sensor nodes in close vicinity of the sink are always stressed because all the event information routed back to the sink pass through them. So these nodes may die off quickly and can make the entire network useless.

   Similarly, in case of Automated Architecture the nodes in close vicinity of the actors may have high load of relaying data but for each event different actors may be triggered and accordingly relaying sensor nodes will also be different. Hence the relay load gets evenly distributed between all nodes. Because of sensor actor coordination around the event area, the sensors that are far away from the area do not function as relaying nodes which saves energy and bandwidth in case of WSANs.


