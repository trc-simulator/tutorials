===========================
 Basic usage of Choreonoid
===========================

In this chapter, we will learn basic usage of Choreonoid using sample project.

Running
-------

Specify path of sample project "SR1Walk.cnoid" to load after the startup.
                
.. code-block:: bash

 $ choreonoid ~/catkin_ws/devel/share/choreonoid-1.5/project/SR1Walk.cnoid

Following display should be appeared.

.. image:: images/choreonoid_SR1Walk.png

.. note::
              
  Specify following option to load OpenHRP format model after the startup.

  .. code-block:: bash

   $ choreonoid --hrpmodel ~/catkin_ws/devel/share/choreonoid-1.5/model/SR1/SR1.wrl


Main display
------------

Components of "main window" shown after the Choreonoid startup is shown as follows.

.. image:: images/choreonoid_SR1Walk_comment.png

Main menu
#########

In above image, the main menu is shown in title bar of the window.
In default setting of Ubuntu, main menu is shown in the menu bar of whole desktop, but you can change the setting on [system setting]-[display]-[behavior]-[show window menu].

Tool bar area
#############

Displays various tool bars.
Tool bars can be turned on/off by [main menu]-[view]-[show toolbar].

View area
#########

Displays various views.
In above image, "item" "property" "link" "body/link" "joint slider" "scene" "message" "Python console" view is shown.
You can also stack the view and switch by tab.

The view can be turned on/off by [main menu]-[view]-[show view].
By selecting [create view] you can also create multiple views of same kind as well.
For example, you can create multiple "scene" views to display multiple view angles of simulation world or display robot camera.

In above image, messages in red color is displayed.
When there is problem in Choreonoid, warning and error messages are displayed in the message view.
Please check these messages in case of trouble (in above case, the message complains there is no ODE or Bullet plugins, which cause no problem).

Status bar
##########

Status bar under the main window displays short message about the current process proceeding in Choreonoid.

Region of the status bar is separated to two parts. Left part displays begging and end of process. Right part displays status of the object currently pointed in the current view.


.. note::

   Due to problem of some graphics driver, GUI elements of Choreonoid sometimes give no response except for 3D display. In such case, please once resize the Choreonoid window and the GUI elements will activated again.


Control of view angle
---------------------

By placing the mouse cursor over the scene view and apply following actions, you can control the 3D graphics of the simulated world.

* Left button click and drag: Rotate around the point you have clicked.
* Center button click and drag: Parallel translation.
* Wheel: Extend or shrink.
* Shift+Left drag: Snap horizontally or vertically.

Also, you can change the view angle to overview the whole simulation world by clicking the following button on the tool bar.
This button is useful when you lost your current view angle and want to reset.

.. image:: images/scenebar_look_over_button.png


Switching of camera
--------------------

The camera used to render view angle can be switched using pull down widget in the scene bar.
Click and focus the scene view you want to switch and select the camera you want to display on the pull down widget.

.. image:: images/scenebar_camera_select.png

Default cameras
###############

Following cameras are prepared as default.

* System - Perspective

* System - Orthographic

Robot cameras
#############

When the robot model loaded in Choreonoid has cameras, it will be listed to pull down widget as follows.

* Robot_name - Camera_name

Tracking camera
###############

You can automatically track the model by using BodyTrackingCameraItem.

1. Create "BodyTrackingCameraItem" as a child item for the target BodyItem and check the item.

2. Name of the item will be appeared on the camera selection widget. Select the name.

3. If you set "Keep Relative Attitude" property to true, direction of the camera will be also tracked.


Control shading
---------------

Default scene view of Choreonoid is configured with shading enabled.
If you want to disable the shading, click configure button of the scene bar and uncheck the lighting option.

.. image:: images/scenebar_shading.png

Wire frame display
------------------

With wire frame display, you can have transparent view of all the objects.
To switch to wire frame mode, click "Toggle the wireframe mode" button of the scene bar.

.. image:: images/scenebar_wireframe.png

Collision display
-----------------

During the simulation, we sometimes want to check the collision between the objects.
To switch to the collision line visible mode, click "Toggle the collision line visibility" button of the scene bar.
Then click on the AISTSimulator item on the item view and set the "Record collision data" property to True.

.. image:: images/scenebar_collision.png
   
Start/pause/stop the simulation
--------------------------------

To start the simulation, click on the following buttons on the "simulation" bar.

.. image:: images/simulationbar.png

Each buttons has following functions respectively (from left side);

* Start the simulation from initial position.
* Start the simulation from current position.
* Pause the simulation.
* Stop the simulation.

You can once stop the simulation and play the result using the slider on the "time" bar. You can enter the exact time on the time bar as well.

.. image:: images/timebar_slider.png

To restart the paused simulation, click the "pause the simulation" button.


Save/load/play the simulation result
-------------------------------------

In Choreonoid, we can save the simulation result (trajectory data) and later play the simulation result using the data.
Here, we will explain how to do using sample project "PA10Pickup.cnoid".

Save the simulation result
##########################

1. Run Choreonoid
  
   .. code-block:: bash

    $ choreonoid ~/catkin_ws/devel/share/choreonoid-1.5/project/PA10Pickup.cnoid

2. After simulation is started, BodyMotion items named "AISTSimulator-XXX" is generated under the BodyItem of moving objects such as robot. These BodyMotion items stores motion trajectory data of simulation result. In following example, BodyMotion items are generated for "PA10" and "box3" items.

   .. list-table::

      * - Before simulation starts
        - After simulation starts
      * - .. image:: images/motion-recording-1.png
        - .. image:: images/motion-recording-2.png
           
3. Select each BodyMotion items (it is OK to select multiple items as well) and save the data by selecting [file]-[save as] menu.

   .. image:: images/motion-recording-3.png

   Files are saved for each BodyMotion items, so please specify the file name containing name of parent item.

   .. note::

      To select multiple items in item view, press Ctrl key and click the item.
      
      If you press Shift key and click, multiple items in range can be selected.

Load and play the simulation result
###################################

1. Let's, once close the Choreonoid and restart.
  
   .. code-block:: bash

    $ choreonoid ~/catkin_ws/devel/share/choreonoid-1.5/project/PA10Pickup.cnoid

2. Select the target BodyItem in the item view, and load corresponding BodyMotion item from file. Select [file]-[open...]-[body motion] menu.

   .. list-table::

      * - Before loading (BodyItem is selected)
        - After loading
      * - .. image:: images/motion-recording-4.png
        - .. image:: images/motion-recording-5.png

   Load the corresponding BodyMotion data for the other BodyItems as well.
          
3. To play the loaded motion data, we have to select the BodyMotion items (select all the BodyMotion items if there is multiple objects).

   .. image:: images/motion-recording-6.png

4. Click "start animation" button on the time bar to play the simulation result.

   .. image:: images/motion-recording-7.png


.. _howto-use_view_edit_mode_label:

View mode and edit mode
-----------------------

In the scene view, we usually control the 3D graphics of the simulation world using view mode.
But by switching to edit mode, we can control the objects in the simulation world.

* Mode can be switched by pressing ESC key or by double click the background of the scene view.

  * Shape of mouse cursor is changed to hand shape when in edit mode.

* We recommend to use scene view in view mode in normal operation to avoid accidental editing of object.

* In edit mode, you can pull to move the objects in following situations.

  * Set initial pose of the object (before the simulation).

  * Give external force to the robot (during the simulation).


Generate movie of simulation result
-----------------------------------

1. Once apply the simulation and make motion playable using the play button on the time bar.

   .. image:: images/motion-movie-1.png

2. Select [Tools]-[Movie Recorder] menu. "Movie recorder" dialog will be shown.

   .. image:: images/motion-movie-2.png

3. Set following parameters.
   
   a. Select target view to record.

   b. Select recording mode to offline.

   c. Enter directory you want to output the serial capture image file.

   d. Enter base file name to save serial capture image file.

   e. Set "Start time" and "Finish time".

   f. Set frame rate.

   g. Image size can be specified by checking "image size". This function will crop the captured image to specified size. Thus, the original size of view has to be larger than the specified size. Please adjust the view size to be larger than the specified size before beginning the recording.

      .. warning::

       The section 5 in generate of the movie in format of yuv420p. This format is need specify even pixel size. If specify odd pixel size, fail to generate of the movie file.

   .. image:: images/motion-movie-6.png

4. Press "Record" button to output the serial capture image files.
   Serial capture image files are generated in specified directory as follows.
   
   .. image:: images/motion-movie-7.png
   
5. Enter following command to generate movie from the serial capture image files.

   .. code-block:: bash

    $ avconv -i scene%08d.png -r 30 -an -vcodec libx264 -pix_fmt yuv420p video.mp4

   .. note::

    If avconv command not found, run the follow commnad.

      .. code-block:: bash

         $ sudo apt-get install libav-tools


.. toctree::
   :maxdepth: 2
