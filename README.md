# RoboFieldLocalisation

Using the video as found in https://youtu.be/DYQFtrk6B18.

### Goal
- Find an approximate location for the robot in the field (Note: Because of field symmetry there are likely to be more possible locations)

### How?
####(step 1)
Find robot's position in respect of the visible lines from the robot's vision (circle in the video):
- Find the lines
- Retrieve a random set of points on the visible lines (pts)
- Compensate lens distortion for each pt in pts
- Calculate values comparable to the real world distance and angle for each pt in pts

####(step 2). 
Localization in total field:
- Use n particles (prs), uniformly distributed over the field
- Move each pr in prs in an random direction (in each iteration)
- Take, for each particle a random set of points (pts) on lines within x radius from the particle
- Calculate values comparable to the real world distance and angle for each pt in pts
- Calculate (for this iteration) the difference between the set of (distance, angle) to the set (distance, angle) retrieved from the robot's vision (in step 1)
- The latest calculated value is the value we're optimizing on. If small enough, slow the particle (and TODO: change direction towards the local optimum). If large, speed up.
- Any particles going out of bounds will be removed and placed randomly near an existing particle or anywhere on the field.
- Particles in the field will also randomly be replaced every once in a while. This prevents only finding local optima

### Issues:
- Parameters: How many particles, how often do we replace? What is the difference between distances in the video and on the field.
- The optimization parameter in step 2. How do we calculate this? Using distances and angles we should get near. But do we have enough random point selections to get close?
- The optimization parameter heavily depends on the first issue. The difference between distances in the field and seen from the robot
- The resulting lines as seen from the robot are distortion free. Not yet perspective free. This should make a large difference.

### Sample image 
Sample image of what it looks like. At a given early moment in the process
