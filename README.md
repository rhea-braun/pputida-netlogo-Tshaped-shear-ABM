# A NetLogo ABM of the chemotactic response of Pseudomonas putida toward naphthalene at a NAPL-water interface under shear flow
**pputida-netlogo-Tshaped-shear-ABM**


A Netlogo agent based model to describe the chemotaxis and motility of Pseudomonas putida in a T-shaped micro fluidic device




## WHAT IS IT?

This model is an agent-based simulation of **bacterial chemotaxis under shear flow** in a microfluidic environment for a paper by Gao, Braun, Wu, and Ford (2026) [1]. It represents individual motile bacteria swimming, tumbling, and responding to chemoattractant gradients while being advected by fluid flow.

The model is designed to investigate how **fluid velocity and shear interfere with bacterial chemotaxis**, reducing directed migration toward a chemical source. It mirrors a T-shaped microfluidic device used in experiments, importing chemoattractant concentration fields generated in COMSOL and applying Poiseuille flow profiles in the vertical (z) direction.

The model supports comparison between populations with varying motility and chemotaxis parameters, exploration of rheotaxis and shear-dependent motility, and extraction of spatial bacterial density profiles for comparison with experimental data and continuum-scale simulations.



## HOW IT WORKS

The model uses individual bacteria as agents (turtles) moving on a two-dimensional grid of patches that store chemoeffector concentration.

### Agents (Bacteria)

Each bacterium:

* Has a swimming speed drawn from a normal distribution
* Alternates between runs and tumbles
* Senses temporal changes in local chemoattractant concentration based on its experience moving in the chemoeffector field
* Experiences fluid advection and shear based on its vertical (z) position in a poisseule flow

### Chemotaxis

* Tumbling probability is calculated each tick using a chemotaxis model adapted from Rivero et al. [2]
* Bacteria reduce their tumbling frequency when moving up a chemoattractant gradient.
* Chemorepellent behavior can also be modeled via parameter changes.

### Motion Rules

At each tick:

1. The bacterium evaluates its tumbling probability (`Ptau`)
2. It either:

   * **Tumbles**, choosing a new direction from an experimentally derived angle distribution, or
   * **Runs**, moving forward with slight directional noise
3. Fluid flow advects bacteria downstream according to a Poiseuille velocity profile
4. Optional behaviors such as rheotaxis and shear-modulated swimming speed are applied

### Environment

* Chemoattractant gradients are imported from COMSOL simulations (attached files required)
* Fluid velocity varies with vertical position (z), and shear can be simulated
* Boundary conditions maintain constant bacterial concentration via spawning, recycling, or culling




## HOW TO USE IT

 **Set parameters** using sliders and switches in the Interface tab:

   * Number of bacteria (red and green)
   * Swimming speed, tumbling probability, chemotactic sensitivity
   * Flow rate and zoom factor
   * Behavioral switches (chemotaxis, rheotaxis, shear effects)

 Click **SETUP** to:

   * Import chemoattractant fields
   * Initialize bacteria with randomized properties
   * Reset timers and counters

 Click **GO** to:

   * Run the simulation forward in time
   * Observe bacterial trajectories, clustering, and downstream transport

 Optional:

   * Enable recording to export frames
   * Run batch simulations to automatically sweep parameters and save outputs

### Interface Elements (typical)

* **Sliders**: `flowrate`, `velocity-red`, `P0-red`, `sigma-red`, `bacnumber-red`, `zoomfactor`
* **Switches**: `rheotaxis?`, `shear-function?`, `simple-source?`, `recycling?`, `record?`
* **Buttons**: `setup`, `go`, batch run buttons
* **Visuals**: Blue chemoattractant gradient, red/green bacteria, optional trajectory lines




## THINGS TO NOTICE

* How increasing flow rate stretches bacterial trajectories downstream
* Loss of chemotactic accumulation at increasing flow rate / shear
* Differences between runs in static versus flowing conditions
* Clustering of bacteria near chemoattractant sources at low flow
* How shear modifies swimming speed when the shear function is enabled




## THINGS TO TRY

* Increase flow rate while keeping chemotaxis parameters constant
* Turn rheotaxis on and off and compare spatial distributions
* Disable chemotaxis (set sigma to zero or use buffer) and observe transport-only behavior
* Compare results with and without shear-dependent swimming, customizing shear function
* Run multiple replicates using batch mode and compare variability




## EXTENDING THE MODEL

Possible extensions include:

* Implementing receptor saturation or adaptation dynamics
* Allowing bacteria to modify the chemical field (consumption or degradation)
* Including explicit wall adhesion or near-wall swimming behavior
* Modeling multiple chemical species or competing gradients
* Extending to three-dimensional spatial motion




## NETLOGO FEATURES

This model makes use of several advanced NetLogo features:

* **Breeds** to represent different bacterial populations
* **Agent-owned variables** to store flow, shear, and chemotaxis parameters
* **File I/O** to import COMSOL data and export simulation results
* **Custom agent shapes** to visually resemble bacteria
* Use of **can-move?** for boundary detection and reflection

Workarounds were used to represent three-dimensional effects (z-dependent flow and shear) within a two-dimensional simulation.


## CREDITS AND REFERENCES

This model was developed as part of a study on bacterial chemotaxis under shear flow using agent-based modeling in NetLogo.

Key references:

1. Gao, B., Braun, R. M., Wu, D., and Ford, R.M., 2026. Pseudomonas putida swimming reversal frequency and chemotactic response toward naphthalene at a NAPL-water interface decreased under increasing shear flow (in preparation)
2. Rivero, M.A., Tranquillo, R.T., Buettner, H.M., Lauffenburger, D.A., 1989. Transport models for chemotactic cell populations based on individual cell behavior. Chem. Eng. Sci. 44, 2881–2897. https://doi.org/10.1016/0009-2509(89)85098-5
3. Duffy, K. J.; Ford, R. M. Turn Angle and Run Time Distributions Characterize Swimming
Behavior for Pseudomonas Putida. J. Bacteriol. 1997, 179 (4), 1428–1430.
https://doi.org/10.1128/jb.179.4.1428-1430.1997.
4. Harwood, C. S.; Fosnaugh, K.; Dispensa, M. Flagellation of Pseudomonas Putida and
Analysis of Its Motile Behavior. J. Bacteriol. 1989, 171 (7), 4063–4066.
https://doi.org/10.1128/jb.171.7.4063-4066.1989.
5. Marx, R.B., Aitken, M.D., 2000. Bacterial chemotaxis enhances naphthalene degradation in a heterogeneous aqueous system. Environ. Sci. Technol. 34, 3379–3383. https://doi.org/10.1021/es000904k
6. Marx, R.B., Aitken, M.D., 1999. Quantification of chemotaxis to naphthalene by Pseudomonas putida G7. Appl. Environ. Microbiol. 65, 2847–2852.
https://doi.org/10.1128/aem.65.7.2847-2852.1999

Chemoattractant fields were generated using COMSOL Multiphysics and imported into NetLogo.

The NetLogo code for this model is provided as supplementary material accompanying the publication.

 
