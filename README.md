# RSS Dataset for Outdoor Localization Algorithms
This dataset is a complete set of Received signal strength (RSS) reads collected by a Target node Raspberry Pi 4 model B that is intended to capture probe requests (WiFi) and advertisement packets (BLE) sent by anchor nodes Raspberry Pi Zero W located in the scenario.
For conducting the tests, different scenarios were created in the outdoor/indoor parking lots of the Faculty of Engineering, University of Cagliari. 

The purpose of this dataset is to provide real RSS measurements, thus affected by propagation disturbances such as typical of these scenarios, by means of which to be able to test RSS-based localization algorithms. 
The dataset is organized into folders, with one folder assigned for each scenario. Furthermore, the folders are divided into subfolders according to the type of technology that was analyzed, either WiFi or BLT. Lastly, each subfolder contains a CSV file for each node included in the dataset.
The CSV files for each anchor differ in the number of columns depending on the scenario and technology under measurement. In scenario 0, there are 2 and 3 columns for the Bluetooth and WiFi files, respectively. These columns are: Rx Power [dBm] indicating the RSS measurement; Timestamp and Date ISO indicating the time the measurement was acquired.
For scenarios A, B, and C, there are 5 and 6 columns for Bluetooth and WiFi files, respectively. These columns include Timestamp, Date ISO, Rx Power [dBm], Relative Coordinates [m], Target Coordinates [m], and Target Distance - anchor [m]. In addition to those in Scenario 0, Relative Coordinates [m] refers to the coordinates of the anchor node in the reference scenario, Target-Anchor Distance [m] indicates the distance between the anchor node and the target node, and Target Coordinates [m] refers to the relative coordinates of the target in the reference scenario. 


# Scenarios
The test scenario (0) was created in the outdoor parking lots by placing 5 anchor nodes along a straight line at the distances of 5, 10, 15, 20 and 25 meters from a target node.

<p align="center">
  <b> Experimental scenario 0 </b>
</p>
<p align="center">
<img src="img/Scenario 0.png" width="75%" height="75%">
</p>

The first scenario (A) was created in the outdoor parking lots by placing around the perimeter of a 21.10 x 30-m rectangle 6 anchor nodes in line-of-sight (LOS) with a target positioned in coordinates [0, 0] as in the figure.

<p align="center">
  <b> Experimental scenario A </b>
</p>
<p align="center">
<img src="img/Scenario A.png" width="75%" height="75%">
</p>

The second scenario (B) was created in the outdoor parking lots by placing along the perimeter of a 32.8 x 30 meter rectangle 7 anchor nodes (including 4 in LOS and 2 in NLOS) and a target positioned in coordinates [4.6, 0] as in the figure.

<p align="center">
  <b> Experimental scenario B </b>
</p>
<p align="center">
<img src="img/Scenario B.png" width="75%" height="75%">
</p>

The third scenario (C) was created in the indoor parking lots by placing along the perimeter of a 21.10 x 30-m rectangle 6 anchor nodes and a target positioned in coordinates [4.6, 0] as in the figure. As we can see in the figure, there are elements within the scenario such as cars and pillars not present in the previous two scenarios.

<p align="center">
  <b> Experimental scenario C </b>
</p>
<p align="center">
<img src="img/Scenario C.png" width="75%" height="75%">
</p>

## Devices
Two types of devices were used to conduct the acquisition campaign: Raspberry Pi 4 model B for the Target node, Raspberry Pi Zero W for the anchor nodes.

<p align="center">
  <b> Anchor and Target devices </b>
</p>
<p align="center">
<img src="img/devices.png" width="75%" height="75%">
</p>

The Target node was equipped with an external WiFi interface that would allow it to sniff the network and consecutively capture probe requests sent by the anchor nodes. From the capture of these frames, various information can be extracted, including the RSS on which we focus in this work. 
To perform the captures, all devices were placed on a tripod at a height of 1.5 meters above the ground as can be seen in the figure. This choice was made after conducting various tests at different heights that showed that better results could be obtained using this configuration. For each anchor in the scenario, target acquisition lasted 15 minutes. 

<p align="center">
  <b> Experimental setup </b>
</p>
<p align="center">
<img src="img/setup.png" width="50%" height="50%">
</p>

On the software side, I used, as far as the target node is concerned, a python language script and the PyShark library. Using one of the functions of this library, the script allowed me to access the external interface in monitor mode thus going on to capture all Probe Requests sent by all devices within a certain range of the anchor node's coverage. Next, a part of the script took care of filtering these packets going to retain only those sent by the anchor nodes, using the MAC ADDRESS of the devices as the discriminating information. 
The same logic was used for Bluetooth measurements by exploiting this time the bluepy library.
On the other hand, as far as the anchor nodes are concerned, I used a script in Python that would allow a continuous scan of the WiFi networks present, thus indirectly going to force the forwarding of Probe Requests. 

