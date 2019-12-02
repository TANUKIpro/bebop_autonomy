# bebop_autonomy

[ROS](http://ros.org) driver for [Parrot Bebop](http://www.parrot.com/ca/products/bebop-drone/) drone (quadrocopter).

* Documentation: http://bebop-autonomy.readthedocs.io/
* ROS wiki page: http://wiki.ros.org/bebop_autonomy
* Support: [ROS Q&A (tag: bebop_autonomy)](http://answers.ros.org/questions/scope:all/sort:activity-desc/tags:bebop_autonomy/page:1/)
* Code API: http://docs.ros.org/indigo/api/bebop_autonomy/html

## Development Team

* Author: [Mani Monajjemi](http://mani.im) ([Autonomy Lab](http://autonomylab.org), [Simon Fraser University](http://www.sfu.ca)) + [other contributers](http://bebop-autonomy.readthedocs.io/en/latest/contribute.html#list-of-contributers)
* Maintainers:
    * [Sepehr MohaimenianPour](http://sepehr.im/) ([Autonomy Lab](http://autonomylab.org), [Simon Fraser University](http://www.sfu.ca))
    * Thomas Bamford ([Dynamic Systems Lab](http://www.dynsyslab.org), [University of Toronto](https://www.utoronto.ca/))
    * [Tobias Naegeli](https://ait.ethz.ch/people/naegelit/) ([Advanced Interactive Technologies Lab](http://www.ait.ethz.ch/), [ETH Zürich](http://www.ethz.ch/))

## Build Status

[![Build Status (ROS I,J,K) - TravisCI](https://travis-ci.org/AutonomyLab/bebop_autonomy.svg?branch=indigo-devel)](https://travis-ci.org/AutonomyLab/bebop_autonomy) [![Build Status (ROS I,J) - Semaphore](https://semaphoreci.com/api/v1/projects/11786233-d505-4d79-b27c-80c2742243a4/537552/badge.svg)](https://semaphoreci.com/mani_monaj/bebop_autonomy)

Built against [parrot_arsdk](https://github.com/AutonomyLab/parrot_arsdk) 3.12.6p1  

# 使い方  
0. 前提条件  
    * Ubuntu16.04 or Ubuntu14.04  
    * ROS indigo or kinetic  
    * ROSのワークスペースがすでに存在している  

1. bebopと接続する　 
    * bebopにバッテリーを装着し、電源を入れる
    * __catkin_ws__ に __bebop_autonomy__ のリポジトリをクローンしてmakeする  
    `$cd ~/catkin_ws/src`  
    `$git clone　https://github.com/TANUKIpro/bebop_autonomy.git`  
    `$catkin_make ~/catkin_ws`
    * bebopがホストのwifiに接続する。SSIDは __BebopDrone-xxxxx__ とかになってる。  
    パスワードは無い。
    * パスを通す  
    `$source ~/catkin_ws/devel/setpu.bash`  
    * 接続   
    `$roslaunch bebop_driver bebop_node.launch`
    * 接続されると、ドローンのパラメータとかがいろいろ表示される  

2. トピックを確認してみる  
    ```
    $rostopic list  
    /bebop/bebop_driver/parameter_descriptions
    /bebop/bebop_driver/parameter_updates
    /bebop/camera_control
    /bebop/camera_info
    /bebop/cmd_vel
    /bebop/flattrim
    /bebop/flip
    /bebop/image_raw
    /bebop/image_raw/compressed
    /bebop/image_raw/compressed/parameter_descriptions
    /bebop/image_raw/compressed/parameter_updates
    /bebop/land
    /bebop/navigate_home
    /bebop/reset
    /bebop/states/ARDrone3/CameraState/Orientation
    /bebop/states/ARDrone3/GPSState/NumberOfSatelliteChanged
    /bebop/states/ARDrone3/MediaStreamingState/VideoEnableChanged
    /bebop/states/ARDrone3/PilotingState/AltitudeChanged
    /bebop/states/ARDrone3/PilotingState/AttitudeChanged
    /bebop/states/ARDrone3/PilotingState/FlatTrimChanged
    /bebop/states/ARDrone3/PilotingState/FlyingStateChanged
    /bebop/states/ARDrone3/PilotingState/NavigateHomeStateChanged
    /bebop/states/ARDrone3/PilotingState/PositionChanged
    /bebop/states/ARDrone3/PilotingState/SpeedChanged
    /bebop/states/common/CommonState/BatteryStateChanged
    /bebop/states/common/CommonState/WifiSignalChanged
    /bebop/states/common/ControllerState/isPilotingChanged
    /bebop/states/common/FlightPlanState/AvailabilityStateChanged
    /bebop/states/common/FlightPlanState/ComponentStateListChanged
    /bebop/states/common/MavlinkState/MavlinkFilePlayingStateChanged
    /bebop/states/common/MavlinkState/MavlinkPlayErrorStateChanged
    /bebop/states/common/OverHeatState/OverHeatChanged
    /bebop/takeoff
    ```
3. TakeOff / Landing してみる  
    * TakeOff  
        - /bebop/takeoff にパブリッシュしてやる  
    `$rostopic pub /bebop/takeoff std_msgs/Empty`

    * Landing
        - /bebop/land にパブリッシュしてやる  
    `$rostopic pub /bebop/land std_msgs/Empty`
