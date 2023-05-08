# Ch6_Delta_Robot

#This code is intended to control the deta robot to perform a pick and place task in CoppeliaSim.

import sim
import numpy
import time
import math

# Connect to CoppeliaSim
sim.simxFinish(-1)
clientID = sim.simxStart('127.0.0.1',19999,True,True,5000,5)
if clientID!=-1:
    print('Connected to remote API server')
else:
    print('Failed to connect to remote API server')


joint1 = sim.simxGetObjectHandle(clientID, 'drivingJoint1', sim.simx_opmode_blocking)
joint2 = sim.simxGetObjectHandle(clientID, 'drivingJoint2', sim.simx_opmode_blocking)
joint3 = sim.simxGetObjectHandle(clientID, 'drivingJoint3', sim.simx_opmode_blocking)

# Set joint control mode to position control
sim.simxSetObjectIntParameter(clientID, joint1, sim.sim_jointintparam_ctrl_enabled, 1, sim.simx_opmode_oneshot)
sim.simxSetObjectIntParameter(clientID, joint2, sim.sim_jointintparam_ctrl_enabled, 1, sim.simx_opmode_oneshot)
sim.simxSetObjectIntParameter(clientID, joint3, sim.sim_jointintparam_ctrl_enabled, 1, sim.simx_opmode_oneshot)

# Set target joint positions, setting variables arbitrarily to induce movement.
target_pos1 = 0.1
target_pos2 = 0.2
target_pos3 = 0.3

# Move the robot
sim.simxSetJointTargetPosition(clientID, joint1, target_pos1, sim.simx_opmode_oneshot)
sim.simxSetJointTargetPosition(clientID, joint2, target_pos2, sim.simx_opmode_oneshot)
sim.simxSetJointTargetPosition(clientID, joint3, target_pos3, sim.simx_opmode_oneshot)

# Disconnect from CoppeliaSim
sim.simxFinish(clientID)


#I have been unable to induce any motion of the ABB IRB 360 Flexpicker robot. My anticipated simulation was to
#have the robot use the inverse kinematics equations outlined in my chapter and perform a "pick" motion (the sphere in the sim)
#then return to a different location and perform a "place" motion, as most pick and place tasks do. Unfortunately I was unable to 
#get this working in time for the deadline, but I will still be pursuing this as it is something that interests me in manufacturing. 
