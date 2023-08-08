# Amplitude Reduction Flow Control using Postion Feedback Rotation Law

This repo contains the files for the test case of flow around cylinder using OpenFOAM. The case has the following parameters:-
- Re = 7500
- Inlet Velocity = 0.25 m/s
- Diameter of Cylinder = 0.03 m

For the purposes of this case, the use of the following schemes has been made:-
- For time derivatives, the steady state scheme has been utilized.
- For gradient schemes, the conventional Gaussian scheme with linear interpolation has been used.
- For advective divergence schemes, bounded schemes are used because of the steady state test case.

The flow is modeled by the incompressible, steady state solver simpleFOAM and the results are plotted using MATLAB
 
 
