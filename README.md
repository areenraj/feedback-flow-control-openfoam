# Feedback Flow Control using a Custom Boundary Condition in OpenFOAM

*Before we begin, I would like to thank Michael Alletto's tutorial for the case of the non-rotating cylinder. I would also like to thank Jozsef Nagzy and his excellent explanation of the use of overset meshes in OpenFOAM.*

## Introduction
Flow Induced Vibrations (FIV) is an important field of study that deals with the response of structures in various flow configurations with one or more degrees of freedom. It is a phenomena which is especially relevant in the areas of offshore drilling, energy harvesting and even vehicle aerodynamics. 

On the other hand, Flow Control is a field that deals with the introduction of certain devices or the use of particular methods to regulate and, in theory, control the flow in a given test case. Flow control maybe done passively - attachment of splitter plates behind a bluff body to prevent vortex shedding - or it may be done actively - moving flaps in an aircraft.

The test case of an elastically mounted cylinder has been studied extensively by many reseachers in the field. The work of S.P. Singh and Mittal, Williamson and Govardhan etc. have been used to study the flow induced vibrations of such a system. For the laminar test case and zero mass damping, flow synchronization or lock-in is observed for a range of reduced velocities and the response can be divided into three branches - initial, lower and upper. Bourguet and Jacono conducted simulations with a similar cylinder which was rotating with a fixed rotational velocity. The results seemed to indicate a change in the amplitude of vibration for certain values of the non-dimensionalized rotational velocity. This indicates the potential use of addding rotation to a translating cylinder to cause a change in its vibrating response. 

Finally, we arrive at the paper this project is based on. Vicente-Ludlam et al. made the use of the Lattice Boltzmann Method to simulate the test case of a rotating, elastically mounted cylinder with one degree of freedom. Their setup involved a constantly changing rotating velocity which was dependent on either the velocity or the acceleration of the cylinder in question. **In this project we will be analyzing a similar rotation law to setup a feedback control system using a custom coded boundary condition in OpenFOAM**

# Setup
The cylinder is setup in a cross-flow configuration and only allowed to move in the transverse direction. It is attached to a spring and the rotation is given about its center of mass. The simulation is 2D in nature and involves zero mass damping. The rotation-feedback law relates the angula velocity with the transverses velocity of the The following equations are valid for the non-dimensional parameters.

```math
Re = \frac{U_{\inf}D}{\nu}
```
```math
U^* = \frac{U_{\inf}}{f_ND}
```
```math
m^* = \frac{m}{\frac{\pi}{4}\rho D^2 H}
```
```math
k^* = \frac{k}{D}
```
For the following test case the value of the Reynold's Number and Mass Ratio is fixed at 100 and 10 respectively. The domain size is 60DX40D with the cylinder situated at (20D,20D).The reduced velocity is varied by changing the spring constant in dynamicMeshDict. The mesh consists of two regions, the first is the cylinder mesh that will actually execute the motion and the second is the rectangular background mesh with two refinement zones. 

![1-s2 0-S0889974616305096-gr1_lrg](https://github.com/areenraj/feedback-flow-control-openfoam/assets/80944803/85fa6952-359a-4484-ad82-fc12a288a875)
*Image taken from D. Vicente-Ludlam, A. Barrero-Gil, A. Velazquez* - https://doi.org/10.1016/j.jfluidstructs.2017.05.001
![cylinder](https://github.com/areenraj/feedback-flow-control-openfoam/assets/80944803/eec8eb6e-ae6f-482d-8323-94d0385db67e)
*The circular mesh that represents the body and a little bit of the surrounding domain that actually oscillates*
![mesh](https://github.com/areenraj/feedback-flow-control-openfoam/assets/80944803/62722f46-7666-4029-8134-af314dc3917d)
*The stationary domain that the cylinder oscillates in*
 
# Mesh Convergence Study
A mesh convergence study was done using Shiels et al. as the reference paper - https://doi.org/10.1006/jfls.2000.0330. The test case simulated was that of mass ratio 5 and non-dimensionalized spring constant 4.74. Increasing refinement in each mesh case was employed. The finer mesh seems to have achieved convergence in results to the paper and is ready to be used for the simulation. 

|               |Coarse Mesh |Fine Mesh    |Finer Mesh   |Shiels et al|
|---------------|------------|-------------|-------------|------------|
|$C_d$ Mean     |   2.283    |   1.5165    |   1.725     |     1.7    |       
|$C_L$ Amplitude|   0.729    |   0.0515    |   0.038805  |     0.04   |
|$St$           |   0.17175  |   0.15335   |   0.1565    |     0.156  |
|$A^*$          |   0.7239   |   0.3683    |   0.421     |     0.46   |
