iwaki-ros-pkg
=============

A ROS wrapper around Iwaki interaction (and dialogue) manager.


Requirements: 
-------------
- RE2 library: http://code.google.com/p/re2/
- ncurses library
- queueio and iwaki libraries: https://github.com/maxipesfix/iwaki
- the example iwaki action executor, generator, calls gstreamer
  to play sound files.

Build:
----- 
In the root of your ROS workspace:
<pre>
catkin_make
</pre>


Nodes:
------
- iwakishi, the ROS wrapper around Iwaki library.
- console, a sample app that supplies input to iwaki manager: it reads 
           terminal input and sends it as messages to iwakishi.
- generator, a sample app that executes iwaki actions: it plays sound
             files as directed by the recipes. 


iwakishi 
--------
<pre>
rosrun iwaki iwakishi -t 0.1 -d DEBUG2 -l ./log1 -p scripts_directory  -i init_file -x
</pre>

In this package, the example scripts_directory is PACKAGEROOT/scripts and
the example init_file is initialize_im.georgi.xml . These example scripts 
are triggered by time (heartbeat), console input lines "h" (how_are_you), "how" (how_are_you_and_you). how_are_you_and_you expects one of the two followups "y" or "n".

Command line args:     
<pre>
 -t period of the main loop in seconds 
 -d debug level: ERROR, WARNING, INFO, DEBUG, DEBUG1, DEBUG2, DEBUG3, DEBUG4
 -l location and prefix of the log file 
 -p path of the top-level script directory containing init file 
 -i name of the init file 
 -x
</pre>



console
-------
<pre>
rosrun console
</pre>


generator
---------
<pre>
rosrun generator -s sound_file_directory
</pre>

In this package, the example sound_file_directory is PACKAGEROOT/sounds .

NOTE: start generator before iwakishi, otherwise first iwakishi action messages
      may never be received.
