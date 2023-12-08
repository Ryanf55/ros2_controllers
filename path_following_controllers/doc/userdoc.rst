:github_url: https://github.com/ros-controls/ros2_controllers/blob/{REPOS_FILE_BRANCH}/path_following_controllers/doc/userdoc.rst

.. _path_following_controllers_userdoc:

path_following_controllers
===========================

Controller for executing following 2D or 3D paths. 
Input paths commonly are generated obeying Dubins path constrains.
Trajectories are specified as a TODO,
which the controller attempts to TODO.
Waypoints consist of TODO.

Nonlinear Path Following Guidance(NPFL)
---------------------------------------

NPFL is an implementation of the controller described in `Low-Altitude Control and Local Re-Planning Strategies for SmallFixed-Wing UAVs<https://tstastny.github.io/pdf/tstastny_phd_thesis_wcover.pdf>`_.
While `originally implemented in the PX4 Autopilot<https://github.com/PX4/PX4-Autopilot/pull/18810>`_, it has been ported to ROS 2.
This allows NPFL to be used on ROS-enabled vehicles with other autopilots that do not support NPFL.

