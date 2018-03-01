Build-user control
Branch-GEODRIVE
Update the filepath in ControlCenter
Authors Jeffrey Watts, Tony Romero Jr.
------------------------------------------------------------------

This branch is designed to direct the ASEP to a point within a square centered on the target
whose edges are 00.005 NESW
It remains to be seen whether this will actually work.

The strategy is that every 125 iterations of the control loop the current lat and long  will
be appended onto an array of GPS coordinates and the count reset.
That array is then passed into the decision block within which it is further passed into a 
logic block where a 4 bit string is produced which describes what it shoud do next.

The logic block is based on the 16 states which have been defined for the robots current
and past behavior. These 16 states are then reduced to four actions that it can take next.

The string can be 0000 1000 0100 0010 0001 and yes it could just use 2 bits but that would be boring
0000 is destination reached so it stops the robot.
1000 is heading in the right direction so it just keeps doing what it was doing.
0100 is the robot needs to turn left so it passes 50 and 100 to the L and R motors.
0010 is the robot needs to turn right so it passes 100 and 50 to the L and R motors.
0001 is the robot needs to turn around so currently it just goes backwards.
The backwards could be eleminated in an alternate control strategy but that is a job for another time.

From there the control loop continues to iterate until the next 125 iterations are up.


NOTE to self figure out how to get from lat long to m