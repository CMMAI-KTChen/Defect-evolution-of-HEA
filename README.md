# HEA mechanisms
In this repositiory, we demonstrate the LAMMPS code used in our MD simulations and the snapshot videos for our simulations.

## Tensile simulation
If you wish to run our code, we use the **`lammps-16Mar18`** version of LAMMPS with mpi execution.
The **`equimolar.data`** file is our data file, you can also generate your preferable atom configuration. Please note that the simulation box size should be identical and the lattice parameter is 3.595 Angstroms. The data is in [100], [010], [001] axial directions. 

The **`tensile_equimolar.in`** is our input file. The simulation process is as follows:
1. Energy minimization
2. Lattice relaxation
3. Monte Carlo simulation
4. Quenching process
5. Boundary condition readjustment
6. Tensile simulation

#### Energy minimization
We use min_style `sd` to initialize the model and `dnax` value of 0.2. This is because we only want to ensure the stability of the model, and the precision would not matter much in this case.
The atomic stress is also defined in this section.

#### Lattice relaxation
Since our boundary condition is currently periodic, we here run `isothermal–isobaric ensemble` (NPT) for initial lattice relaxation. This is also the stage we assign velocity to the system, so a random seed is needed for this step. In our simulations, we changed the random seed in the same composition for maximizing our simulation validity (we usually run 4 or 5 times within one composition, using the same data dile and different random seed). We chose a 1.8 darg for the barostat/thermostat, but you can tune to your preference value.

#### Monte Carlo simulation
The `Monte Carlo` simulation is ultilized here is because we want to simulate the short-range ordering effect and lattice distortion effect of the HEA systems. By minimizing the system energy using Monte Carlo method, we wish the configuration of the system can be more realistic. The simulation steps for swapping is 15000. So if you are performing a composition with one of the elements being set to 0 molar ratio, the swapping steps should be annotated.
We experimented swapping multiple atoms within one step, but the result in convergent and the major difference is the simulation time. Also, the swapping steps is not fine tuned so there may be an optimum number for a given atom number. We only chose a reasonable number of steps because it is time consuming.

#### Quenching process
Again, this part of the code aimed for more realistic local configuration. We heat the system from 300K to 1500K, equilibrium under 1500K, then cool back to 300K, follows by a equilibrium under 300K. `NPT` ensemble is used in this section. In our simulations, 1500K is high enough for the system to melt and rearrange. However, there might be a chance that the final lattice structure remained amorphous, such as Ni0.

#### Boundary condition readjustment


#### Tensile simulation

Animation of all simulation runs are shown in this project. 
Animations were processed through Common Neighbor Analysis(CNA) and a self-developed defect classifying algorithm via OVITO. In CNA processed videos, atoms with fcc crystal structure is colored green, bcc crystal structure is colored blue and hcp crystal structure is colored red. Amorphous atoms are excluded in all videos.
Each animation is recorded till the model rupture or amorphous tip nucleated.

If you have any question about our project, please contact our email address: qqqqhair@caece.net
