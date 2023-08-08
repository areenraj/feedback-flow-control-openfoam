# Feedback Flow Control using a Custom Boundary Condition in OpenFOAM

*Before we begin, I would like to thank Michael Alletto's tutorial for the case of the non-rotating cylinder. I would also like to thank Jozsef Nagzy and his excellent explanation of the use of overset meshes in OpenFOAM.*

## Introduction
Flow Induced Vibrations (FIV) is an important field of study that deals with the response of structures in various flow configurations with one or more degrees of freedom. It is a phenomena which is especially relevant in the areas of offshore drilling, energy harvesting and even vehicle aerodynamics. 

On the other hand, Flow Control is a field that deals with the introduction of certain devices or the use of particular methods to regulate and, in theory, control the flow in a given test case. Flow control maybe done passively - attachment of splitter plates behind a bluff body to prevent vortex shedding - or it may be done actively - moving flaps in an aircraft.

The test case of an elastically mounted cylinder has been studied extensively by many reseachers in the field. The work of S.P. Singh and Mittal, Williamson and Govardhan etc. have been used to study the flow induced vibrations of such a system. For the laminar test case and zero mass damping, flow synchronization or lock-in is observed for a range of reduced velocities and the response can be divided into three branches - initial, lower and upper. Bourguet and Jacono conducted simulations with a similar cylinder which was rotating with a fixed rotational velocity. The results seemed to indicate a change in the amplitude of vibration for certain values of the non-dimensionalized rotational velocity. This indicates the potential use of addding rotation to a translating cylinder to cause a change in its vibrating response. 

Finally, we arrive at the paper this project is based on. Vicente-Ludlam et al. made the use of the Lattice Boltzmann Method to simulate the test case of a rotating, elastically mounted cylinder with one degree of freedom. Their setup involved a constantly changing rotating velocity which was dependent on either the velocity or the acceleration of the cylinder in question. **In this project we will be analyzing a similar rotation law to setup a feedback control system using a custom coded boundary condition in OpenFOAM**

# Setup
The cylinder is setup in a cross-flow configuration and only allowed to move in the transverse direction. It is attached to a spring and the rotation is given about its center of mass. The simulation is 2D in nature and involves zero mass damping. The following equations are valid for the non-dimensional parameters.

```math
Re = \frac{U_{\inf}D}{\nu}
```
```math
U^* = \frac{U_{\inf}}{f_ND}
```
```math
m^* = \frac{m}{\frac{\pi}{4}\rho D^2 H}
```
For the following test case the value of the Reynold's Number and Mass Ratio is fixed at 100 and 10 respectively. The domain size is 60DX40D with the cylinder situated at (20D,20D).The reduced velocity is varied by changing the spring constant in dynamicMeshDict. The mesh consists of two regions, the first is the cylinder mesh that will actually execute the motion and the second is the rectangular background mesh with two refinement zones. 

![cylinder](https://github.com/areenraj/feedback-flow-control-openfoam/assets/80944803/eec8eb6e-ae6f-482d-8323-94d0385db67e)
![mesh](https://github.com/areenraj/feedback-flow-control-openfoam/assets/80944803/62722f46-7666-4029-8134-af314dc3917d)
 
 
