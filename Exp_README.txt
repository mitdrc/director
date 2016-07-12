README for Experiment/Trajectory Modules
----------------------------------------
Author: Arjun Balasingam, 12 July 2016

Running scripts:
- Start Director and open Python console.
- Currently, the following scripts work:
    pointTrajectory(point,hand): plans a trajectory to goal position `point`, with 'right' or 'left' hand
    randPointTrajectory(): invokes pointTrajectory() after selecting a random (reachable) point from space
    collectRandPoints(n): generates `n` random point trajectories*
    
    wipingTrajectory(center, orientation, hand): plans a wiping trajectory around `center` with surface `orientation` given by [<theta>,0,90], with hand 'left' or 'right'
    randWipingTrajectory(): plans a wiping trajectory at center=[0.5,-0.5,1.0] with 'right' hand and a randomly selected orientation where theta~U(110,180)
    collectWipingTrajectory(): generates `n` random point trajectories*

* These dataset collection scripts do NOT invoke the LCM logger. There is some commented-out code (`w.onClick()`, etc.) that invokes the LCMLogger from the script, but this doesn't seem to record all trajectories. Not sure why, but my workaround was to invoke the LCMLogger at the start of the data collection and kill the process at the very end. So all data for a single call to this function will reside in a single LCM file. Invoking the Logger from the script itself is more optimal, so we have separate files for each run of the experiment, making it easier to concatenate data vectors before feeding into the model. The current solution requires that we parse the large .mat file to get individual trials.

Adding more experiments/trajectories, etc.:
- Here I'll discuss the software organization, in case more trajectories may need to be generated:
    - The `mappingDemo` module handles the trajectory planning:
        - To create a new trajectory, (1) write a spawn affordance function (if needed) similar to spawnCircleTargetAffordance()
        - and (2) write a planTrajectory function that enumerates your goal positions (look at planPointTrajectory() and planWipingTrajectory())
    - I then defined functions (above) in startup.py that use the mappingDemo module. These functions can be called directly from the Director's Python console.


