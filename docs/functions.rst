Functions
---------

.. py:mod: 
.. py:mod:: py_mod

.. function:: imap(x, in_min, in_max, out_min, out_max)
  
   Maps an integer value in the range **[in_min, in_max]** to interval **[out_min, out_max]**
   Analogous to arduino map function that uses long int numeric types.  If the input parameters 
   are non-integer numerics, they will be converted to a Python **int** type at whatever resolution
   is available by the Python implementation being used.

  :param x: input numeric value to map
  :param in_min: lower bound of input range
  :param in_max: upper bound of input range
  :param out_min: lower bound of output range
  :param out_max: upper bound of output range

  :return: bounded value
  :rtype: int

  Note: The input is *not* bounded.
  Use the **constrain(...)** function to bound it first if required
 
  A typical use of this function with robotic control would be to take a
  value in decimal range of **[0,100]** and map into **[0,255]** ie. (**[0,FF]** hex) 
  before sending it to a motor controller.


.. function:: fmap(x, in_min, in_max, out_min, out_max)
  
   Maps a float value in the range **[in_min, in_max]** to interval **[out_min, out_max]**
  
  :param x: input numeric value to map
  :param in_min: lower bound of input range
  :param in_max: upper bound of input range
  :param out_min: lower bound of output range
  :param out_max: upper bound of output range

  :return: bounded value
  :rtype: float


.. function:: constrain(x, xmin, xmax)
  
   Bounds a numeric value to range **[xmin, xmax]**

  :param  x: input numeric value 
  :param  xmin: lower bound
  :param  xmax: upper bound

  :return: bounded value
  :rtype: float


.. function:: rad2deg(rad)

  Converts an angle in radians to degrees

  :param  rad:  input angle in radians

  :return: angle in degrees
  :rtype: float


.. function:: deg2rad(deg)

   Converts an angle in degrees to radians

  :param  deg:  input angle in degrees

  :return: angle in radians
  :rtype: float


.. function::  bound2pi(angle)

  Bounds an angle to (+/-) pi radians

  :param  angle: angle in radians

  :return: bounded angle in radians
  :rtype: float


.. function::  bound2piDeg(angle)

  Bounds an angle to (+/-) 180 degrees

  :param  angle: angle in degrees

  :return: bounded angle in degrees
  :rtype: float


.. function::  boundTo2pi(angle)

  Bounds an angle into one circular rotation of 2 pi radians (360 degrees).
  So even if the input angle is spinning perpertually either counter-clockwise
  in the positive direction or clockwise in the negative direction
  the output angle is contained into only one equivalent full circular 
  rotation of 2 pi radians (360 degrees)

  :param  angle: angle in radians

  :return: bounded angle in radians
  :rtype: float


.. function::  radPerSecToRpm(rps)

   Converts angular velocity in radians per second
   to RPM (revolutions per minute)

  :param  rps:  angular velocity in radians per second

  :return: angular velocity in revolutions per second
  :rtype: float


.. function::  rpmToRadPerSec(rpm)

   Converts angular velocity in RPM (revolutions per minute)
   to radians per second

  :param  rpm:  angular velocity in RPM

  :return: angular velocity radians per second
  :rtype: float


.. function::  degPerSecToRadPerSec(dps)

   Converts angular rotational rate in degrees per second
   to radians per second

  :param  dps:  angular rotational rate in degrees per second 

  :return: angular rotational rate in radians per second
  :rtype: float


.. function::  radPerSecToDegPerSec(rps)

   Converts angular rotational rate in radians per second
   to degrees per second

  :param  rps: angular rotational rate in radians per second 

  :return: angular rotational rate in degrees per second
  :rtype: float


.. function::  mps2kmph(mps)

   Converts meters per second to kmph

  :param  mps: rate in meters per second

  :return: rate in kilometers per hour

  :rtype: float


.. function::  mps2mph(mps)

   Converts meters per second to mph

  :param  mps: rate in meters per second

  :return: rate in miles per hour

  :rtype: float


.. function::  getDistance(x0,y0,x1,y1)

   Usual 2-space euclidian distance

  :param  x0: start pos x
  :param  y0: start pos y
  :param  x1: end pos x
  :param  y1: end pos y

  :return: distance

  :rtype: float


.. function::  getDistanceFromTo(x0,y0,x1,y1)

  Same as **getDistance(...)** just more verbose


.. function::  getPositionAt(x0,y0, d, theta)

  Returns position **(x1,y1)** that is  **d** distance away
  from **(x0,y0)** at relative angle **theta**

  Useful for getting the position of a remote object when using ranging sensors
  For example, IR sensors. The ranging distance is returned from a known sensor mounted at angle
  **theta** relative to robot's **frame forward heading** when the robot is at current position (x0,y0)

  :param  x0: start pos x
  :param  y0: start pos y
  :param  d: distance from some current position (x0,y0) to remote point
  :param  theta: angle (deg) relative to current heading at position (x0,y0) to remote point
 
  :return: (x1,y1): tuple of remote position coordinates 

  :rtype: float

  
  Note that the robots current position **(x0,y0)** and the position of the remote object
  at range **d** returned as **(x1,y1)** are in the *same* coordinate frame. There are 
  no frame transforms between, for instance, the robots frame and a world frame.
  But, the angle **theta**, the direction that a ranging sensor would point at,
  is in the robots frame relative to 0 degrees that is assumed to be the robots front,
  center and forward heading on the robot itself in a right-handed coordinate system. 
  So for instance, theta = 0 degrees is easting, theta = 90 degrees is pointing north
  and theta = -90 is due south. Also, **theta** is not to be confused with   
  typically notated **phi** for robots heading if its pose is **(x0,y0,phi**) in a
  world frame or whatever frame it is configured to operate and move in. 

  To have the remote position coordinates at range returned in the **robot frame** then
  keep (x0,y0) = (0,0). In other words, keep the robots current position, irregardless of
  its mobile position (and heading) in world coordinate space, at its physical frame center!

  To get the romote position coordinates at range from the robot for a particular sensor
  returned in the **world coordinate frame** then have (x0,y0) set to the robots current 
  position in world coordinates and set theta equal to theta the sensor angle on the robot 
  frame, plus phi the robot's heading in the world frame. Eg. theta = phi + theta_sensor. 
  Since the robots heading could be unpredictable, use a **roboutils** function to bound it.
  Eg. theta = bound2piDeg(phi+theta_sensor)
 


.. function::  getPosAt(x0,y0, d, theta)

  Short-hand for **getPositionAt(...)**

 

.. function::  getAngleFromTo(x0,y0,x1,y1,<deg360>)

   Returns angle (in degrees) of line segment from **(x0,y0)** to **(x1,y1)**  

   Uses normal trig conventions for signed angles of rotation:
   positive angle are to left (counter-clockwise)
   negative angles are to right (clockwise)
   

  :param  x0: start pos x
  :param  y0: start pos y
  :param  x1: end pos x
  :param  y1: end pos y
  :param  deg360:  = False (default) to bound angle to 180 degrees
                   = True to  bound in full rotation of 360 degrees
 
  :return: angle in degrees

  :rtype: float






