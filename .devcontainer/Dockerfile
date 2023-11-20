# Use the base ROS 2 image with the specified tag
FROM althack/ros2:humble-full

# Update packages and install git
RUN apt-get update && \
    apt-get install -y git python3-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone PX4-Autopilot repository and build
RUN git clone --recursive https://github.com/PX4/PX4-Autopilot.git /home/ros/PX4-Autopilot && \
    bash /home/ros/PX4-Autopilot/Tools/setup/ubuntu.sh && \
    cd /home/ros/PX4-Autopilot/ && \
    make px4_sitl

# Install Python dependencies
RUN pip3 install -U empy pyros-genmsg setuptools

# Clone and build Micro-XRCE-DDS-Agent
RUN git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git /home/ros/Micro-XRCE-DDS-Agent && \
    cd /home/ros/Micro-XRCE-DDS-Agent && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    make install && \
    ldconfig /usr/local/lib/

# Clone PX4 repositories
RUN mkdir -p /home/ros/ws_sensor_combined/src/ && \
   git clone https://github.com/PX4/px4_msgs.git /home/ros/ws_sensor_combined/src/px4_msgs && \
   git clone https://github.com/PX4/px4_ros_com.git /home/ros/ws_sensor_combined/src/px4_ros_com

#Build the workspace using colcon
RUN cd /home/ros/ws_sensor_combined && \
    /bin/bash -c "source /opt/ros/humble/setup.sh && colcon build"

RUN sudo chown -R ros:ros /home/ros/PX4-Autopilot

# Add an environment variable for the workspace
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> /home/ros/.bashrc
RUN echo "source /home/ros/ws_sensor_combined/install/setup.bash" >> /home/ros/.bashrc

# Download and install QGroundControl
RUN wget https://s3-us-west-2.amazonaws.com/qgroundcontrol/latest/QGroundControl.AppImage -O /home/ros/QGroundControl.AppImage && \
    chmod +x /home/ros/QGroundControl.AppImage

# Set environment variable to allow running GUI applications
ENV DISPLAY=:0

# Install FUSE for QGroundControl AppImage
RUN apt-get update && \
    apt-get install -y fuse && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

#update bashversion in order to be able to use ohmybash
RUN apt-get install -y bash
#add ohmybash and set it as the bash https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh
RUN bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
RUN sed -i 's/OSH_THEME=.*/OSH_THEME="powerline"/g' /home/ros/.bashrc

# Command to run QGroundControl as the 'ros' user
#"/home/ros/QGroundControl.AppImage"

USER root

#install figlet
RUN apt-get update && \
    apt-get install -y figlet && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
USER ros

#install figlet fonts & add as
RUN git clone https://github.com/xero/figlet-fonts.git /home/ros/figlet-fonts
RUN sudo mv /home/ros/figlet-fonts/3d.flf /usr/share/figlet/
RUN sudo mv /home/ros/figlet-fonts/Crazy.flf /usr/share/figlet/
RUN sudo mv "/home/ros/figlet-fonts/Big Money-se.flf" /usr/share/figlet/
# Copy big_money_plane_V.flf from the host to the container's figlet-fonts directory
COPY big_money_plane_V.flf /home/ros/figlet-fonts/

# Move the font file to the appropriate directory
RUN sudo mv /home/ros/figlet-fonts/big_money_plane_V.flf /usr/share/figlet/



RUN echo "figlet -f 3d -c Welcome to" >> /home/ros/.bashrc
RUN echo "figlet -f big_money_plane_V QADT V" >> /home/ros/.bashrc 
