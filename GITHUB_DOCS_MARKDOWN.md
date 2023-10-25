# Setting up the Development Environment on all OS types:

## WSL

Step 1 is to install WSL2 (Ubuntu 22.04) on your windows machine. [Instructions can be found here](https://learn.microsoft.com/en-us/windows/wsl/install)

## Docker

Next install docker, for windows and macOS, install docker desktop on your machine. For linux users, install docker through the command line using the convience script found on this [webpage](docs.docker.com/engine/install/ubuntu)

## VSCode Configuration

Ensure VSCode is installed on your machine. Once it has been installed, three extentions must be downloaded in order to use the container; Docker, Dev Containers, and Remote Development.

## Cloning Repo and Configuring Environment

Now, clone the dev env repo on your machine (in WSL if using windows) using the following instruction: 
 
	git clone https://github.com/Queens-Aerospace/dev_env.git

After that repo has cloned, open it using

	code .

Now, you should see all of the files in the repo in VSCode. Now we will set up your development environment. First press ctrl+shift+P. You should then see a search bar open up. In that search bar, search for Dev Containers: Rebuild and Reopen in Container, and select this option. The dev container will now begin to build, this wil take anywhere between 15-40 mins the first time it build.
Once it is built, you should see the same things VSCode as you did before, however now you are in the development container. Now, we will configure your branch. Make a new terminal within VSCode and type the following commands. These ensure you have access to all repos you need, and will give you a branch on our repo. 

	cd src
	git submodule update --init --recursive

You should now be able to see the contents of any repos highlighted in the ros2.repos file and navigate to them. Now, you need a branch on our repo. 
 
	cd drone_workspace 
	git checkout -b <your_name>

You should have gotten a terminal output confirming that your branch is created and that you have been switched to that branch. For troubleshooting, consult the official readme: https://github.com/Queens-Aerospace/dev_env, Gabe or Conor, Chat, Google, etc.

## Next Steps

Now that you are on your branch, start expirementing with ROS2 through the [video series](https://www.youtube.com/playlist?list=PLLSegLrePWgJudpPUof4-nVFHGkB62Izy) and [ROS2 PX4 integration](https://docs.px4.io/main/en/ros/). Happy bashing!

