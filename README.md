# HSR_Object_Recognition
User manual 
Package Name: hsrb_darknet_tutorials 
Files:
launch/default_model_demo.launch
Description: This is a file that should be on the HSR Robot and it is in charge of running YOLO. It subscribes to the colour image on HSR Robot and runs YOLO on the received image. It then publishes the converted image with the detected object  as well as an array of the detected object centre and the boundary height and width.
Arguments: None 
Note: The first thing you need to do before doing anything is to run yolo on the GPU if you don't you get an error. If you get the error the only thing you can do is to restart the HSR and try again. You also need be logged into the level 3 research network whose password is crispyink133.
How to run:
			$ ssh -x ubuntu@unsw-hsrb-tk1.local
Passwod :  dt3gpu
$ cd workspace/indigo_workspace/
$ source devel/setup.bash 
$ export ROS_MASTER_URI=http://unsw-hsrb.local:11311/
$ export ROS_HOSTNAME=unsw-hsrb-tk1.local
$ roslaunch hsrb_darknet_tutorials default_model_demo.launch

Package Name: myvis
Files:
src/ToPickFinal.cpp
Description: ToPickFinal.cpp is a publisher that read in the command line and prints that value as the object to pick. It will only take in the first value as the string to publish  so if the object's name contain multiple word you will need to put it in single quotation.
Arguments: <Object_to_pick>
How to run:
$ cd workspace
$ hsrb_mode
$ source devel/setup.bash 
$ rosrun myvis ToPickFinal.py ‘bottle’

src/visionfinal.cpp
Description: This code subscribes to the array of centres and the boundary height and width from YOLO. It uses this data to calculate the xyz global and local positions and to publishes Objects.msg for both the local and global frame.
Arguments: None
How to run:
$ cd workspace
$ hsrb_mode
$ source devel/setup.bash 
$ rosrun myvis visionfinal.py

msg/tables.msg
Description: The data being transferred over ROS which contains an array of table
msg/table.msg
Description: The data being transferred over ROS which contains the centre of the table in xyz position and the min and max xyz for the table.
msg/Object.msg
Description: The data being transferred over ROS which contains the centre of the Object in xyz position and the camera x and y position. The camera x and y position are also used to store height and width when ObjectPCL is publishing an object.
msg/Objects.msg
Description: The data being transferred over ROS which contains an array of Object

Package Name: opencvcode
Files:
src/table.cpp
Description:  This code subscribes to the point cloud and finds all the tables. It then publishes the point cloud it see one by one. It should also publish an array of all the tables but that has been implemented yet. This file is on the HSR Robot.
Arguments: None
How to run:
$ ssh -X hsr-user@unsw-hsrb.local
Password : dt3lap
$ cd workspace/indigo_workspace/
$ source devel/setup.bash 
$ rosrun opencvcode table

src/pointcloud_sub.cpp
Description: This code subscribes to the point cloud and as well as the ToPickFinal Object to pick. The first thing the code does is finds all Object 
Arguments: None
How to run:
$ ssh -X hsr-user@unsw-hsrb.local
Password : dt3lap
$ cd workspace/indigo_workspace/
$ source devel/setup.bash 
$ rosrun opencvcode ObjectPCL



