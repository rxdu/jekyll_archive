---
layout: page
comments: false
sharing: false
footer: true
---

Control and Motion Planning for Quadrotors in Simulation
======

Currently the code repository for this project includes the following:

* quadrotor simulations: AscTec Hummingbird, 3DR Solo,Bitcraze Crazyflie 2
* quaternion-based attitude and position controller
* space partitioning data structures (square grid, quadtree, 3d cube array)
* class templates for graph construction and A* search, [GitHub Repo](https://github.com/rxdu/astar_search)
* basic visualization of graph/search and workspace decomposition
* minimum-snap polynomial trajectory optimization
* integration with OMPL for sample-based planning (RRT*)
* integration with Octomap for efficient 3D environment representation
* integration with LCM for inter-process communication
* integration with ROS for advanced data visualization
* integration with g3log for simulation data logging
* a QT-based application for log data plotting

Quadrotor Simulation:

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/5VGGHFQIzGk?list=PLCTIfKO4vA6axJpi3eWmM4-nV6Wxn19DI" frameborder="0" allowfullscreen></iframe>
</center>

Trajectory Generation and Tracking

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/9c3ewYJLf5Y?list=PLCTIfKO4vA6YOlP94UzpYJAZOJMoX653J" frameborder="0" allowfullscreen></iframe>
</center>

2D Workspace Decomposition and A* Search
<center><img src="/img/projects/new_map_path_cmp1.jpg" width="600"/></center>
<center><img src="/img/projects/new_map_path_cmp2.jpg" width="600"/></center>

Plotting of Log Data
<center><img src="/img/projects/log_analyzer.png" width="600"/></center>
