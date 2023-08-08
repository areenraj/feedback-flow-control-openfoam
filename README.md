# Flow Control of a Elastically Mounted Cylinder using a Custom Boundary Condition coded in OpenFOAM

*Before we begin, I would like to thank Michael Alleto's tutorial for the case of the non-rotating cylinder. I would also like to thank Jozsef Nagy and his excellent explanation of the use of overset meshes in OpenFOAM.*

## Introduction
Flow Induced Vibrations (FIV) is an important field of study that deals with the response of structures in various flow configurations with one or more degrees of freedom. It is a phenomena which is especially relevant in the areas of offshore drilling, energy harvesting and even vehicle aerodynamics. 

On the other hand, Flow Control is a field that deals with the introduction of certain devices or the use of particular methods to regulate and, in theory, control the flow in a given test case. Flow control maybe done passively - attachment of splitter plates behind a bluff body to prevent vortex shedding - or it may be done actively - moving flaps in an aircraft.

The test case of an elastically mounted cylinder has been studied extensively by many reseachers in the field. The work of S.P. Singh and Mittal, Williamson and Govardhan etc. have been used to study the flow induced vibrations of such a system. For the laminar test case and zero mass damping, flow synchronization or lock-in is observed for a range of reduced velocities and the response can be divided into three branches - initial, lower and upper. Bourguet and Jacono conducted simulations with a similar cylinder which was rotating with a fixed rotational velocity. The results seemed to indicate a change in the amplitude of vibration for certain values of the non-dimensionalized rotational velocity. This indicates the potential use of addding rotation to a translating cylinder to cause a change in its vibrating response. 

Finally, we arrive at the paper this project is based on. Vicente-Ludlam et al. made the use of the Lattice Boltzmann Method to simulate the test case of a rotating, elastically mounted cylinder with one degree of freedom. Their setup involved a constantly changing rotating velocity which was dependent on either the velocity or the acceleration of the cylinder in question. **In this project we will be analyzing a similar rotation law to setup a feedback control system using a custom coded boundary condition in OpenFOAM**

 
 
