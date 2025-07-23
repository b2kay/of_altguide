# of_altguide
Alternative User Guide for OpenFOAM
## Flow Models
### inviscid
1. potential flows
  1. laplace equation for velocity potential
2. Euler Equations
### viscous laminar
- T stress tensor
- D 
### turbulent flow
- RANS equations
- DNS
-  turbulence viscosity is a property of flow
-  LES
  
## Test Case
- the boundary conditions applicable to the prediction of various flow regimes in the same solution domain, like inlet, outlet, symmetry plane and wall boundaries; 
- the major flow features found in ducts with a varying cross section, like flow acceleration and deceleration, flow separation and recirculation, boundary layers and sheer layers, and energy loss due to friction and geometry changes;
- how expected flow features affect the design of the computational grid. 
 
the flow in a channel with a semicircular obstacle on one wall
- The height of the channel is ten centimeters, and the semi-circular obstacle with a radius of five centimeters blocks half of the cross-sectional area.
- The channel extends to 0.5 to 0.8 meters upstream and 0.8 to 1.8 meters downstream of obstacle, depending on flow regime (shortest for inviscid and longest for turbulent flow).
- a sketch in the xy-plane is created and then extruded in the third direction by two millimeters.
-  Velocity inlet is applied at the inlet boundary. All variables except for pressure are prescribed.
-  Pressure outlet is applied at the outlet boundary far downstream of obstacle. A constant pressure is specified at the boundary, while velocities are extrapolated from inside.
-  No-slip wall condition is applied at all wall boundaries. Velocity is set equal to wall velocity, which is here zero, while pressure is extrapolated to the boundary from inside.
-  symmetry plane conditions are applied at the front and rear plane of the solution domain. The normal velocity components is set to zero at the boundary, while the zero gradient condition is applied to all other variables in the direction normal to the boundary, thus leading to an effectively two-dimensional flow in this thin slice.

important flow features phenomena 
- It has boundary layers along no-slip walls.
- It has flow separation (due to the presence of an adverse pressure gradient along the wall) and recirculation.
- It has sheer layers with high velocity gradient between fast and slow moving fluid away from wall.
- it has flow acceleration and deceleration due to the change of the flow cross-sectional area.
- The plot on the left shows a typical distribution of velocity vectors in the boundary layer when the grid resolves the boundary layer all the way to the wall. This is called the low-Re approach. It has nothing to do with Reynolds number of the bulk flow.

Local grid refinements depend on expected flow features.

Boundary layers at walls require grid refinement in wall-normal direction. If the boundary layer should be fully resolved, about 20 prism layers are needed. If wall functions are used, five to 10 prism layers may be sufficient. 
Flow separation from a smooth surface requires a fine grid around the separation line to capture its position accurately. 
Recirculation zones are very important; most often they're undesirable. Therefore, the grid needs to be refined where they are expected to accurately capture their allocation and size. 
Shear layers require a locally refined grid because they can cause instabilities, transition to turbulence, and vortex shedding. 
the grid needs to be fine in zones of rapid variation of variables (pressure, velocity, etc.) compared to zones of moderate variation. 

grid features for the computation of inviscid flow. 
The top figure shows the coarse grid for the complete solution domain. 
The lower plot shows a zoom into the grid around the obstacle.
Grids were refined using the refinement factor of two. This means the grid spacing is halved in both x and y directions. 
The solution is expected to be symmetric around the obstacle and therefore the grid is also refined in a symmetrical manner. 
The grid is made finer near the obstacle wall because the highest gradients are expected there. 
At the inlet, a constant velocity of 1 meter per second is specified. 
Density of fluid is set to 1 kilogram per cubic meter and viscosity is set to 0.

the grid features for laminar flow.
Grids were refined using the refinement factor of two, that is the grid spacing is halved in both x and y directions. 
Because flow separation and recirculation are expected and boundary layers develop along walls, the grid has prism layers along all walls.
It is locally refined downstream of obstacles in a larger region to capture the recirculation zone.
At inlet a parabolic velocity profile is prescribed, with the analytical solution for fully developed channel flow, with mean value of velocity equal to 1.3333 meters per second. 
Fluid density is 1 kilogram per cubic meter and viscosity is 0.001 Pascal seconds. 
This gives Reynolds number of 133.33. Finally, let's check grid features for turbulent flow computation. 
Grids were refined using the refinement factor of two, which means that the grid spacing is halved in both x and y direction. Six prism layers are created at all walls, with the stretching factor of 1.2. 
Because the recirculation zone is longer in the case of turbulent flow than in the case of laminar flow, the size of the solution domain and the grid refinement zones are also made longer. The channel extends 0.8 meters upstream and 1.8 meters downstream of obstacle. 
At inlet a constant velocity of 10 meters per second is prescribed. 
Fluid is water with density of 1000 kilogram per cubic meter and dynamic viscosity of 0.001 Pascal seconds. This leads to the Reynolds number of 1 million. 

The ideal grid is the one on which the discretization errors are uniformly distributed. This means that inevitably a non-uniform grid is required in almost all practical applications. 
The grid needs to be locally refined with smaller spacing where the variables vary more strongly or where specific critical features need to be captured accurately, like flow separation location.

### Simulation of inviscid flow. 
This lesson is about simulation of inviscid flows in ducts with a variable cross-section geometry.
The main objectives of this lesson are: to apply a CFD tool, here Simcenter STAR-CCM+, to simulate inviscid flow in the selected test case; to analyze the obtained solutions; to understand the flow physics, like relation between velocity and pressure variation; to evaluate the accuracy of solutions by comparing results obtained with different grids; and to explain the influence of the order of the discretization scheme on the accuracy of the solution for the given computational grid. The physics models selected for this simulation are: constant density fluid, inviscid flow, segregated flow solver for which we need to choose the convection scheme (which is here selected as second-order), and the steady-state flow. The following boundary conditions were imposed at the solution domain boundaries. Symmetry for front and back planes. You can see here the names of boundaries as given in the CAD tool during creation of CAD model of solution domain. No-slip wall condition for the top boundary, bottom boundary, and semi-cylindrical obstacle. Then inlet at the left boundary and outlet condition at the outlet boundary. These two plots show the distribution of pressure and the stream-wise velocity component computed on the fine grid. Pressure distribution is symmetric, hence zero net force on obstacle in flow direction is obtained. The velocity field should also be symmetric. Disturbances on the downstream side are due to numerical errors. Streamlines are smooth and almost perfectly symmetric around the obstacle. They are colored by the velocity magnitude. A comparison with pressure and velocity contours shown before reveals: where the lowest velocities are found, which is at the corners upstream and downstream of the obstacle, pressure has the highest values; where the highest velocity is obtained, which is at the top of the obstacle, pressure has the lowest value. This plot shows the variation of the streamwise velocity component along the top and bottom channel walls. The obstacle blocks 50% of the channel cross-section, so the mean velocity above the obstacle doubles. However, velocity is not uniform above the obstacle. At the top wall the maximum velocity is about 1.8 times higher than at the inlet, while at the top of the obstacle, it is about 2.6 times higher. Velocity goes to zero at both upstream and downstream corners. As the grid is refined the solution becomes perfectly symmetric. Downstream of the obstacle, velocity should ideally be equal at both walls. This is the case upstream of obstacle. Due to the discretization errors, there is a small difference. In reality, velocity would be zero at walls, but in an inviscid fluid, the velocity is constant across the channel. This plot shows the variation of pressure along the top and bottom channel walls, computed on the fine grid. As the velocity along the top wall increases, the pressure reduces, and vice versa. Due to the presence of an obstacle on the bottom wall, pressure first increases at the front stagnation point before decreasing rapidly toward the obstacle top. The variation on the downstream side should be fully symmetric, which is for the finest grid almost true. The pressure is much lower at the top of the obstacle than at the opposite wall, because the velocity is the highest at the obstacle top. Sufficiently far away from the obstacle, pressure is equal at both walls and the same upstream and downstream of obstacle - there is no pressure loss. Because the pressure is symmetric around the obstacle, the net force on obstacle in x-direction is equal to zero, which is of course not realistic. These plots show the variation of the tangential velocity along the top and bottom channel walls, computed on the three grids: coarse, medium, and fine. On the coarse grid, there is a significant difference in velocity at the two walls downstream of the obstacle. They should be equal in an inviscid flow. As the grid is refined, the error becomes smaller and the velocities are almost equal at the fine grid. In these computations, the second-order discretization was used for all terms in the Euler equations. These two plots show the variation of the tangential velocity along the top and bottom channel walls, computed on the fine grid using the first order discretization method for convection terms, which is the first order upwind scheme, and second-order discretization, which is the linear upwind scheme. The first-order upwind scheme introduces numerical diffusion, which leads to a very large error in the solution downstream of the obstacle. Even on the fine grid, the velocities on top and bottom wall differ by about 18%, while the difference is smaller than 1%, when the second-order scheme is used. The first order discretization methods should be avoided when solving the Euler or Navier-Stokes equations. These two plots show the velocity contours computed on the fine grid using the first order discretization for convection terms, and second-order discretization. The solutions are almost the same on the upstream side of the obstacle. The differences become apparent above the obstacle top and are especially large on the downstream side. The solution obtained with the second order scheme is perfectly symmetric around obstacle at the top wall, as required for an inviscid flow, while the solution obtained at the first-order method is obviously over diffusive on the downstream side. Near bottom wall, the contours from the second order scheme exhibit oscillations, while in the solution obtained with the first-order method, the errors spread all the way to the outlet. The conclusions from this lesson can be summarized as follows. Inviscid flows can be computed using Simcenter STAR-CCM+ by setting fluid viscosity to zero or by using the inviscid flow model. Euler equations are then solved instead of the Navier-Stokes equations. Inviscid flows are not fully realistic and simulations of such flows are seldom used in practice, except when specially tuned to a particular application, like for example, in some design tools for propellers. For some inviscid flows, there are analytical solutions. They can be used to assess the discretization errors in numerical solution methods. Even where analytical solutions are not available, like in the present case, the knowledge about the properties of inviscid flows is useful for the analysis of discretization methods. Thank you for your attention.

Lesson 4: Simulation of Laminar Flow.
This lesson is about simulation of laminar flows in ducts with a variable cross-section geometry. 
The main objectives of this lesson are: to apply a CFD tool, here Simcenter STAR-CCM+, to simulate the laminar flow at the Reynold's number = 133.3 in the selected test case; to analyze the obtained solutions to understand the flow physics; to evaluate the accuracy of solutions by comparing results obtained with different grids; to explain the influence of the order of discretization scheme on the accuracy of solution; and to recall the difference in flow features compared to the inviscid flow from Lesson 3. The following physics models were selected for this simulation: steady state flow, constant density fluid (with the density of 1 kilogram per cubic meter), laminar flow, segregated flow solver (which means sequential solution of equations for velocity components and pressure correction), or coupled solver (which means a coupled solution of all equations). Both first order and second order upwind schemes for convection fluxes were tested. The following conditions were imposed at boundaries of the solution domain: symmetry for front and back planes, to impose two-dimensional solution (the solution domain is a 2 millimeters thin slice with one layer of cells); no-slip wall for top and bottom channel wall and the semi-cylindrical obstacle; velocity inlet at the left boundary (the parabolic velocity profile of a fully developed laminar flow in a plane channel was specified, which is the analytical solution of the Navier-Stokes equations for fully developed flow conditions); and outlet condition at the right boundary (which means zero-gradient in flow direction, with imposed the same flow rate at the outlet as at inlet). The maximum velocity in the parabolic inlet velocity profile was 2 meters per second, which means mean velocity of 1.33 meters per second, which leads to the Reynolds number of 133.33. These two plots show the distribution of computed pressure and the streamwise velocity component. Note that pressure distribution is not symmetric. Hence, there is a non-zero net force on the obstacle in flow direction. In an inviscid flow, the pressure distribution is symmetric and the net force is zero. The velocity distribution is also highly asymmetric, with a reverse flow direction in part of the week. For the same mean velocity, the maximum velocity in a laminar flow is higher than in an inviscid flow. Even in a straight channel without any obstacle, the maximum velocity in a laminar flow is higher than in an inviscid flow, where the velocity is constant across the channel. In the parabolic profile of a laminar flow, the maximum velocity at the symmetry plane is 1.5 times higher than the mean velocity. Note also the existence of boundary layers at walls and sheer layer between the core flow and the recirculation zone. These plots show the visualization of the flow by streamlines and line integral convolution. Note that there is a very strong recirculation behind obstacle and the weak one in front of it. Flow separation points are denoted here by S and reattachment points by R. This plot shows the variation of the shear stress along the top and bottom walls computed on the fine grid. The shear stress at the top wall here, denoted by the red line, increases as the flow approaches the narrowest cross-section above the obstacle, where it's about five times higher than in the straight channel. Thereafter, it reduces below the level of the undisturbed channel flow, and then recovers again to attain, at the end, the same value as in front of the obstacle. The shear stress at the bottom wall, here denoted by the blue line, decreases gradually as the flow approaches the obstacle. It becomes 0 at the first separation point, is 0 then again at the front stagnation point and increases then rapidly along the obstacle to reach its maximum shortly before the top of the obstacle, where it is about ten times higher than in the straight channel. The shear stress reduces then rapidly as the flow goes around the top of the obstacle, becomes 0 where the flow separates from the obstacle, is 0 then again shortly before the rear stagnation point (because there is a tiny recirculation here in the corner). It increases again within the recirculation zone, becomes 0 at the reattachment point, and then increases gradually to reach the value of the fully developed channel flow. A signed tangential shear stress vector component is changing sign at separation and reattachment locations. If it was plotted instead of the shear stress magnitude, the blue line would look like this. It would cross the 0 line here, where the separation takes place at the obstacle wall, come back and cross the 0 line where the reattachment of the tiny recirculation of the obstacle is, cross the 0 again, where the separation at the bottom wall begins, stay on this side within the recirculation zone, and then cross the 0 line again at the reattachment point. This plot shows the variation of pressure along the top and bottom channel walls, computed on the fine grid. As the velocity near top wall increases, the pressure reduces, and vice versa. Due to the presence of the obstacle on the bottom wall, the pressure first increases at the front stagnation point before decreasing rapidly towards the top of the obstacle. On the downstream side of the obstacle, the pressure recovers, but not as much as in an inviscid flow. A local pressure loss occurs due to the geometry change and fluid viscosity. The steady pressure drop in a straight channel is also visible from the slope of the pressure profile. The additional pressure loss due to the obstacle is visible as the distance between lines corresponding to the linear pressure drop of the fully developed flow upstream and downstream of the obstacle. Without an obstacle, the straight line from the upstream side would simply extend all the way to the outlet. Note that the fully developed flow has not yet been reached at the outlet - a longer channel would be needed for that purpose. These two plots show the comparison of pressure variation along the bottom wall and of streamwise velocity component profile along the line at x = 0.14 meters, computed on three systematically refined grids using 2nd-order upwind discretization. The three lines are hardly distinguishable from each other, indicating that the grids are fine enough and that the solutions of medium and fine grid are very accurate. These plots show the comparison of pressure variation along the bottom wall and of streamwise velocity component profile along the line at x = 0.14 meters, computed on three systematically refined grids using the 1st-order upwind discretization scheme for convection fluxes. Downstream of the obstacle, differences between solutions from different grids are significant. The difference between fine and medium grid solution is half the difference between medium and coarse grid solution, as expected of a 1st-order discretization method. Here, the errors on the fine grid are not very large, but it is problem-dependent. In flows dominated by recirculation, the errors may be much larger, as will be shown in another lesson. 1st-order method should not be used in practical applications because the 2nd-order scheme provides a much more accurate solution at the same computing cost. The conclusions from this lesson can be summarized as follows. Laminar flows are found in many applications, whenever is the Reynolds number smaller than the critical value for the particular geometry and flow conditions. An accurate prediction of laminar flow can be obtained by solving the Navier-Stokes equations on a moderately fine grid using 2nd-order discretization methods. A laminar flow differs significantly from an inviscid flow. It exhibits flow separation, recirculation, boundary and sheer layers, and the pressure loss in flow direction. First-order discretization methods for convection fluxes should be avoided because they require much finer grids to reach the same level of accuracy as the 2nd-order methods. Thank you for your attention!
en

Lesson 5: Simulation of Turbulent Flow. This lesson is about the simulation of turbulent flows in ducts with a variable cross-section geometry. The main objectives of this lesson are: to apply a CFD tool, here Simcenter STAR-CCM+, to simulate the turbulent flow at the Reynolds number of one million in the selected test case; to analyze the obtained solutions to understand the flow physics (like flow separation and recirculation in front of and behind the obstacle, losses due to fluid viscosity and turbulence, etc.); to evaluate the accuracy of solutions by comparing the results obtained with different grids; to explain the influence of the order of discretization scheme on the accuracy of the solution for the given computational grid; and to recall the difference in flow features compared to laminar flow from Lesson 4. The following physics models were selected for this simulation: a constant density fluid (water, with the density of 1,000 kilogram per cubic meter, and dynamic viscosity of 0.001 Pa per second); turbulent flow, with k-omega turbulence model and wall functions; segregated flow solver or coupled solver; steady-state flow. Both first-order and second-order discretization schemes for convection fluxes are tested. The following conditions were imposed at boundaries of the solution domain: symmetry for front and back planes, to impose two-dimensional solution; no-slip wall for the top and bottom channel walls and for the semi-cylindrical obstacle; velocity inlet at the left boundary, where a constant velocity is specified; pressure outlet at the right boundary, where constant zero pressure relative to the reference level is specified. These plots show the distribution of pressure and the streamwise velocity component, computed on the fine grid using the k-omega turbulence model. Note that the pressure minimum and the velocity maximum are upstream of the highest point on the obstacle and that isobars are not orthogonal at the obstacle wall. These plots show the visualization of flow using streamlines and line integral convolution, computed on the fine grid using the k-omega turbulence model. Note the strong recirculation behind the obstacle, enclosing another week recirculation at the rear stagnation point. A recirculation zone is also present in front of the obstacle due to the adverse pressure gradient there. It encloses another micro recirculation at the front stagnation point. The front recirculation zone would not be present if the bottom wall was replaced by a symmetry plane. For the creation of a recirculation zone, both adverse pressure gradient and a wall in flow direction need to be present. The separation and reattachment points are here marked by S and R, respectively. These plots show the distribution of turbulent kinetic energy and turbulent viscosity ratio, computed on the fine grid using the k-omega turbulence model. Note that the turbulent kinetic energy is low where velocity gradients are low, and has a maximum value above the center of the recirculation zone. The maximum turbulent viscosity is 13,537 times higher than fluid viscosity. This plot shows the variation of shear stress magnitude along the top and bottom walls, computed on the fine grid using the k-omega turbulence model. Near inlet boundary, wall shear stress is higher than in a fully developed flow because a constant velocity was specified at the inlet, resulting in very high-velocity gradients in the direction normal to walls. The shear stress of the top wall increases as the flow approaches the narrowest section above the obstacle, where it is about five times higher than in the straight channel. Thereafter it reduces steadily towards the solution for the fully developed channel flow. At the bottom wall, the shear stress reduces as the flow approaches the obstacle. It is zero at the separation point of the front recirculation zone, is very small within the recirculation zone, and is zero again at the front stagnation point. It then increases rapidly as the flow accelerates over the front of the obstacle and reaches the maximum value shortly before the top of the obstacle, where it is about 10 times higher than in a straight channel. It then reduces rapidly on the rear side of the obstacle to zero at the separation point, is small within the tiny recirculation zone near the rear stagnation point, increases within the recirculation zone, becomes zero again at the reattachment point, and then increases gradually toward the fully developed state. When a fully developed state is reached, the shear stresses at the top and bottom wall will become equal. The channel in this simulation was not long enough to reach the fully developed state. This plot shows the variation of pressure along the top and bottom channel walls, computed on the fine grid using the k-omega turbulence model. As the velocity near top wall increases, the pressure reduces, and vice versa. Due to the presence of an obstacle on the bottom wall, pressure first increases at the front stagnation point before decreasing rapidly towards the obstacle top. The minimum pressure is found shortly before the top of the obstacle. On the downstream side of the obstacle, the pressure recovers, but not as much as in laminar flow. The local pressure loss due to the obstacle is much larger than the loss due to friction in a straight channel. In the case of laminar flow, they were comparable (see Lesson 4). These plots show the comparison of pressure variation along the bottom wall and the shear stress along the bottom wall, computed on three systematically refined grids using the k-omega turbulence model and second-order upwind discretization for convection fluxes for all variables. Differences between solutions on different grids are much larger than in the case of laminar flow. High shear stress at the inlet is due to the specified constant velocity there. As the grid is refined, the gradient of the first near wall cell appears larger, because the velocity is zero at the wall, which is why the shear stress increases here as the grid is refined. The pressure is set to zero at the outlet, this is why pressure at the inlet increases when the grid is refined. These plots show the comparison of profiles of the streamwise velocity component and turbulent kinetic energy along a vertical line at x equal to 0.14 m, computed on three systematically refined grids using the k-omega turbulence model and second-order upwind discretization for convection fluxes for all variables. Differences between solutions obtained on different grids are much larger than in the case of laminar flow. Although the Grid 3 is relatively fine, the solution will still change appreciably with another grid refinement. The difference between profiles obtained on Grids 2 and 3 (medium and fine) is much smaller than the difference between profiles obtained on Grids 1 and 2 (course and medium), indicating the convergence toward the grid-independent solution. These plots show the comparison of solutions on the medium grid using different combinations of discretization schemes for convection fluxes for the profile of U-velocity at x=0.14 m and for the shear stress on the bottom wall. Black line indicates solutions when the first-order scheme is used for all equations. The red line indicates that the second-order scheme is used in all equations, and blue line indicates that the first-order scheme is used for k and omega, and the second-order scheme for momentum equations. Discretization of convection fluxes in momentum equations has the greatest effect on the solution accuracy. The difference between solutions obtained using the first and the second-order method is very large. Because the source terms in the equations for k and omega are functions of velocity gradients, it is important that the velocity field is accurately predicted. The difference between solutions obtained when convection is discretized with second order in all equations, and when convection is discretized with first-order in equations for k and omega only, is very small. The blue and the red line are very close to each other. The conclusions from this lesson can be summarized as follows: The turbulent viscosity varies four orders of magnitude within the solution domain. Turbulent kinetic energy is generated in boundary layers near walls, and, to a much higher degree, in shear layers and obstacle wake. The grid dependence of solution is much stronger when the flow is turbulent than when it is laminar. The order of discretization for convection terms is most important for momentum equations and less important for turbulence model equations, because the latter are dominated by source terms, which depend strongly on velocity gradients. Thank you for your attention!
en
​


# WD Intro to OF9

To list all the environment variables related to 
OpenFOAM®, type in the terminal:
$> env | grep –i “OpenFOAM”

To list all the aliases related to OpenFOAM®, type in the 
terminal:
$> alias | grep -i “FOAM”

find $WM_PROJECT_DIR -type f -name "*.name"

grep -rin "LES" $FOAM_SOLVERS


icoFOAM laminar incompressible unstead

'''
foamLog log.icoFOAM
gnuplot
  set logscale y
  plot [][] "logs/p_0" using 1:2 with lines, plot ....
  exit
'''

The fact that the initial residuals are dropping to the same value of the final residuals  (monotonic convergence), is a clear indication of a steady behavior.


​pyFoamPlotRunner.py [options] <foamApplication>

pyFoamPlotWatcher.py log.icoFoam

If you want to stop the simulation and save the solution, in the controlDict dictionary made 
the following modification,
stopAt writeNow;
This will stop your simulation and will save the current time-step or iteration.


foamListTimes -rm -processor
foamCleanTurorials

FYI, solving for the velocity is relatively inexpensive, whereas solving for the pressure is expensive

All the incompressible solvers implemented in OpenFOAM®  (icoFoam, simpleFoam, pisoFoam, and pimpleFoam), use the modified pressure, 

In OpenFOAM®, most of the solvers are implicit, which means they are unconditionally  stable. In other words, they are not constrained to the CFL number condition.
• However, the fact that you are using a numerical method that is unconditionally stable, does  not mean that you can choose a time-step of any size.
• The time-step must be chosen in such a way that it resolves the time-dependent features, and it maintains the solver stability.
• For the moment and for the sake of simplicity, let us try to keep the CFL number below 5.0 and  preferably close to 1.0 (for good accuracy).
• Other properties of the numerical method that you should observe are: conservationess, boundedness, transportiveness, and accuracy. We are going to address these properties and the CFL number when we deal with the FVM theory.


Run the case with Re = 10 and Re = 1000. Feel free to change any variable to achieve the Re value (velocity, 
viscosity or length). Do you see an unsteady behavior in any of the cases? What about the computing time, 
what simulation is faster?
• At larger Re the computation should be slower.
• Also, the physics becomes strongly unsteady so the use of steady solvers is not recommended.
• At Re = 10, the simulation might diverge, this is purely numerical.  
• This result might be very surprising because increasing the viscosity have the effect of stabilizing 
the solution due to dissipation effects. This is purely numerical and is related to the corrections in 
the piso loop.
• The case setup by default will use the momentumCorrector correction.  This correction is 
recommended for strongly convective flows.  But for low Re flows or creeping flows, this correction 
may add instabilities (due to poor approximations), so it is better to turn this option off by setting,
• momentumPredictor off;
• This correction is recommended for highly convective flows, which is not the case for Re = 10.
• If you want to keep this option in this case, you will need to increase the number of correctors 
nCorrector in order to get a stable solution.

Run the tutorial with Re = 100, a mesh with  120 x 120 x 1 cells, and using the default setup (original 
controlDict, fvSchemes and fvSolution). Did the simulation converge? Did it crash?  Any comments.
• With the same mesh and time step, the simulation should crash.
• The simulation crashes because the CFL number becomes larger.
• In module 6, we are going to see how to add more stability to the solver.
• Also, the simulation might not crash, but you will realize that it is much much slower or maybe too inaccurate.
• Usually, by reducing the time-step we stabilize the simulation but a cost of a longer wall clock time.
• By increasing the number of corrections, you can get more stability
• You can also reduce the under-relaxation factors. 
• But be careful, if you use values too low, you can lose time accuracy.


Change the base type of the boundary patch movingWall to patch. (the boundary file). Do you get the same 
results? Can you comment on this?
• You should get the same results.
• The main difference between wall and patch is related to turbulence modeling. 
• With the base type wall, you can use wall functions (turbulence modeling).

Run the simulation using Gauss upwind instead of Gauss linear for the term div(phi,U) (fvSchemes).  Do 
you get the same quantitative results?
• No, you should not get the same results.
• Upwind is first accurate; therefore, is too diffusive.
• Your final solution should always be at least second order accurate.

nstead of using the boundary condition totalPressure and pressureInletOutletVelocity for the patch top, try 
use zeroGradient.  Do you get the same results? Any comments?
(Hint: this combination of boundary conditions might give you an error, if so, read carefully the screen 
and try to find a fix, you can start by looking at the file fvSolution)
• The results should be the same.
• However, you will need to set a reference pressure in the domain.  
• This is done in the dictionary fvSolution.

Run the simulation in a close domain. Does the volume integral of alpha.water remains the same? Why the 
value is not constant when the domain is open?
• In a perfect world, the volume integral should conserve.
• But due to numerical diffusion, we can lose information.
• Remember, numerical methods produces certain amount of garbage, and we need to live with that.

Use the utility postprocess to measure the average pressure on the obstacle.                                                    
(Hint: use the utility postProcess with patchAverage, take a look at module 5)
• If you do not know how to use the postprocess application, you can jump to module 5 (section 3).
• You can use postprocess as follows,
• postProcess -func 'patchAverage(U,patch=outlet)' 

Run a numerical experiment for cAlpha equal to 0, 1, and 2.  Do you see any difference in the solution? What 
about computing time?
• The recommend value is 1.
• If you use 0, the free surface might not be well resolved (too much diffusion).
• If you use 2, the solution might diverge (too compressible).

ncrease the number of nOuterCorrector to 2 and study the output screen. What difference do you see?
• By increasing the number of correction, the solution is more accurate and stable.
• However, at the cost of an increased computational time.
• You will see on the screen two loops per iteration.


Turn off the MULES corrector (MULESCorr). Do you see any difference on the solution or computing time? 
• If you switch off the MULES corrector and you keep the CFL number above 1, the solution might diverge.
• With the MULES corrector off, the computing time might be lower.
• It is strongly recommended to always enable the MULES corrector (switch on).

Module 3 - Meshing

Mesh quality metrics
- Orthogonality
- Skewness
- Aspect Ratio

- 

SHM

- no more than 4 layers, refine backgrond mesh to improve

-  surfaceFeature convert: convert from vtk to eMesh

-  meshQualityDict
- maxNonOrtho 75;
- maxBoundarySkewness 20;
- maxinternalSkewness 4;
- 


 


