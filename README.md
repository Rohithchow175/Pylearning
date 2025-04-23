# !/ usr / bin / env python3
import rospy
from nav_msgs.msg import Odometry
from geometry_msgs.msg import twist
from tf.transformation import euler_from_quaternion
import numpy as np
import math

class TurtleBot3Controller:
  def __init__(self):
     rospy.init_node('turtlebot3_controller', anonymous=True)
     self.x=0.0
     self.y=0.0
     self.theta=0.0
     
     self.x_goal=2.0
     self.y_goal=2.0
     
     self.k_l = 0.5
     self.k_a = 2.0
     self.k_b=-1.0
     
     rospy.Subscriber('/odom',Odometry,  self.odom_callback)
     self.cmd_pub = rospy.Publisher('/cmd_vel', Twist, queue_size=10)
     self.rate = rospy.Rate(10)
   def odom_callback(self, msg):
        orientation_q = msg.pose.pose.orientation
        _, _, self.theta = euler_from_quaternion([
            orientation_q.x,
            orientation_q.y,
            orientation_q.z,
            orientation_q.w
        ])
   def odom_callback(self, msg):
      self.x=msg.pose.pose.position.x
      self.y=mas.pose.pose.position.y
      
      orientation_q=msg.pose.pose.orientation
      orientation_list = [orientation_q.x, orientation_q.y, orientation_q.z, orientation_q.w]   
    (_, _, yaw) = euler_from_quaternion(orientation_list)
       self.theta = yaw
      
      
# Pylearning
