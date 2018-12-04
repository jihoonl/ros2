# ROS2

# Build from source on OS X High Sierra

## Install dependencies
```
> xcode-select install
> brew install cmake cppcheck eigen pcre poco python3 tinyxml wget

# install dependencies for Fast-RTPS if you are using it
> brew install asio tinyxml2

# brew install opencv

# rviz dependency
> brew install qt freetype assimp

# Add the Qt directory to the CMAKE_PREFIX_PATH
> export CMAKE_PREFIX_PATH=$CMAKE_PREFIX_PATH:/usr/local/opt/qt

# Python3 modules
python3 -m pip install argcomplete catkin_pkg colcon-common-extensions coverage empy flake8 flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes git+https://github.com/lark-parser/lark.git@0.7b mock nose pep8 pydocstyle pyparsing setuptools vcstool
```

## Building base from upstream source

```
> mkdir -p ~/ros2/base
> cd ~/ros2/base

> wget https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos
> vcs import src < ros2.repos

# Build as release. debug mode wasn't fully working.
> colcon build --merge-install --cmake-args -DCMAKE_BUILD_TYPE=Release --ament-cmake-args -DCMAKE_BUILD_TYPE=Release --catkin-cmake-args -DCMAKE_BUILD_TYPE=Release

> source install/setup.bash

# Then, create not existing local_setup.bash and local_setup.sh for some packages.
```

# Set up overlay workspace

```
> mkdir -p ~/ros2/overlay
> cd ~/ros2/overlay

# Clone existing example as sample
> mkdir src
> cd src
> git clone https://github.com/ros2/examples
> cd ..

> source ~/ros2/base/install/setup.bash
> colcon build
```

# Execute nodes in overlay

```
> source ~/ros2/overlay/install/setup.bash
> ros2 run examples_rclcpp_minimal_publisher publisher_lambda
[INFO] [minimal_publisher]: Publishing: 'Hello, world! 0'
```
