# henry-minimal-webapp

## Install and run Minimal GUI

Install dependencies

```
cd ~/catkin_ws/
rosdep install --from-paths src --ignore-src -r -y
```

Build project

```
cd ~/catkin_ws/
catkin_make
```

Start application

```
roslaunch robot_gui_bridge websocket.launch
```
## Serve on local network

Prerequisites: Installation of Apache `sudo apt install apache2`.

To configure apache to serve the GUI HTML open the site configuration in a text editor (By default it is here `/etc/apache2/sites-enabled/000-default.conf`).
Now configure apache to serve the GUI HTML page as <host>/henry by adding this line to the VirtualHost, you want to use (by default there is only one at port 80, which is fine).
```
<Directory "~/catkin_ws/src/robot_gui_bridge/gui>
	Require all granted
</Directory>

Alias /henry ~/catkin_ws/src/robot_gui_bridge/gui
```
To apply the settings restart the apache server (on Ubuntu you can do that with the command `sudo systemctl restart apache2`).

### Access the GUI

To determine the address type `hostname -I` in a terminal.
You will receive an IP-address, which can be used by other devices *on the same network* to communicate with this device.
Log the other device on the same network, open a browser and type: `http://<hostname>/henry`.
Have fun remote controlling your robot.

## Install dependencies for GUI

### Prerequisites

Install NPM: Ubuntu `sudo apt install node`, Mac OS `brew install node`

### Working with NPM

```
cd gui/
npm install
```

Install new packages:

```
npm i newpackage
```

Uninstall an unused package:
```
npm uninstall oldpackage
```

Linking a used package in an html-file:
```
<script type="text/javascript" src="./node_modules/roslib/build/roslib.min.js"></script>
```
