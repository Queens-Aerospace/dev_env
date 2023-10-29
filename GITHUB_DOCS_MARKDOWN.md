# Setting up the Development Environment on all OS types:

## WSL
If youre on windows:

Step 1 is to install WSL2 (Ubuntu 22.04) on your windows machine. [Instructions can be found here](https://learn.microsoft.com/en-us/windows/wsl/install)

## Docker

Next install docker, for windows and macOS, install docker desktop on your machine. For linux users, install docker through the command line using the convience script found on this [webpage](docs.docker.com/engine/install/ubuntu)

For windows and mac users once docker is downlaoded go into resources and turn off resource save mode.

## VSCode Configuration

Ensure VSCode is installed on your machine. Once it has been installed, three extentions must be downloaded in order to use the container; Docker, Dev Containers, and Remote Development. (Can be found in the read me at the top)

## Cloning Repo and Configuring Environment

Now, clone the dev env repo on your machine (in WSL if using windows) using the following instruction: 
 
	git clone https://github.com/Queens-Aerospace/dev_env.git

After that repo has cloned, open it using

	code .
 
 (the above line of code opens vscode in your current directory so make sure you're in the den_env directory when you run that)

Now, you should see all of the files in the repo in VSCode. Now we will set up your development environment. First press ctrl+shift+P. You should then see a search bar open up. In that search bar, search for Dev Containers: Rebuild and Reopen in Container, and select this option. The dev container will now begin to build, this wil take anywhere between 15-40 mins the first time it build.
Once it is built, you should see the same things VSCode as you did before, however now you are in the development container. Now, we will configure your branch. Make a new terminal within VSCode and type the following commands. These ensure you have access to all repos you need, and will give you a branch on our repo. 

	cd src
	git submodule update --init --recursive

You should now be able to see the contents of any repos highlighted in the ros2.repos file and navigate to them. Now, you need a branch on our repo. 

 	cd src
	cd drone_workspace 
## Creating a Branch
(this only works if youre a collaborator on the repo so send us your github name)

Go into GitHub on your browser, click on the repo that you're working in (in this example its ros2_drone_workspace) go to branchs (should be right under the repos name, and should say "4 branchs" or however many branches have already been made. 

Then in the top right click new branch and make one with a name of your choice. To go use the branch in vscode in terminal do the following:

Make sure youre in the right dir:

	cd src
 	cd drone_workspace (or whatever you called the repo in the ros2.repos file in src)
  
Then fetch the repo:

 	git fetch

Now when you run:

	git branch
 
 You should see your branch, to switch into it do:

 	git checkout <branch name> (e.g git checkout conor)

now you should b in your own branch you can push and pull to.

## ROS2 workspace

Now that you're in the dev_env you can see that in src/drone_worspace there is a folder called my_drone_ctrl and in there is another folder called my_drone_ctrl if you cd into the second my_drone_ctrl you can run the "my_first_node.py" node by typing into the command line:

	./my_first_node.py

This is an exmple of "hello world in ros2"  and should see a simular output in the terminal. 

If you want to create a node to make the drone take off and follow your commands you will make another file with a simular format as to my_first_node.py

## PX4 Simulation

If you want to run the simulation cd into the PX4-Autopilot directory This file is located in the root directory of the dev_env. To get the the root of dev_env use the code below in the terminal:

	cd

From there:

	cd PX4-Autopilot

Once in this directory you can build the sim with these commands:

DRONE:

 	make px4_sitl gz_x500

VTOL:

	make px4_sitl gz_standard_vtol

## Next Steps

Now that you are on your branch, start expirementing with ROS2 through the [video series](https://www.youtube.com/playlist?list=PLLSegLrePWgJudpPUof4-nVFHGkB62Izy) and [ROS2 PX4 integration](https://docs.px4.io/main/en/ros/). Happy bashing!

