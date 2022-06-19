##### Table of Contents  
[About the Project](#project)  
[Implementation Logical Description](#logic)  
[Address Table](#addressing)  
[Material](#material)  
[Results](#results)

# Sorting Station

<a name="project"/>

## About the Project
In this work, an application is implemented in Ladder, simulated in [Siemens's TIA Portal V15](https://new.siemens.com/global/en/products/automation/industry-software/automation-software/tia-portal.html?gclid=Cj0KCQjwqKuKBhCxARIsACf4XuFAMB-0TO1Dr0LAtD0IdDRiWIuuLU7WvIdBNcHoMLemTrMuXtZVnvYaAtS3EALw_wcB) for a sorting station modelled by [Factory IO](https://factoryio.com/), in order to sort material of different colors to their respective ramps.
<!-- 
<p align="center">
<img width="400" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/Sorting%20Station.png>
</p>

<p align="center"> 
<b>Figure 1:</b> Sorting Station.
</p> -->

Three types of material are considered, Green, Gray and Blue, which are identified by the Vision Sensor ilustrated in Figure 2. Then led through the conveyors to the ramps 1(Green), 2(Gray) and 3(Blue), in Figure 3, by the triggering of the sorters at the top of the image.

<!-- <p align="center">
<img width="200" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/Vision%20Sensor.png>
</p>

<p align="center"> 
<b>Figure 2:</b> Vision Sensor.
</p>

<p align="center">
<img width="400" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/Ramps.png>
</p>

<p align="center"> 
<b>Figure 3:</b> Ramps 1, 2 and 3 from right to left and Sorters 1, 2 and 3, also from right to left.
</p> -->

The user can start the process by pressing the green Start button at the left of Figure 4, and to stop it, the red Stop button at the center of the same figure is available.

<!-- <p align="center">
<img width="250" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/Automation%20Cabinet.png>
</p>

<p align="center"> 
<b>Figure 4:</b> Automation Cabinet with Start button in green at left and Stop button in red at center implemented.
</p>
 -->
<a name="logic"/>

## Implementation Logical Description

[Siemens's TIA Portal V15](https://new.siemens.com/global/en/products/automation/industry-software/automation-software/tia-portal.html?gclid=Cj0KCQjwqKuKBhCxARIsACf4XuFAMB-0TO1Dr0LAtD0IdDRiWIuuLU7WvIdBNcHoMLemTrMuXtZVnvYaAtS3EALw_wcB) was used for the development of the Ladder code which can be resumed in two parts.
First, Figure 5 shows that as the user press a named *Start* button, all conveyors are energized and will not cease until a second button named *Stop* is pressed.

<!-- <p align="center">
<img width="500" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/LAD_buttons.png>
</p>

<p align="center"> 
<b>Figure 5:</b> Ladder code implementig Start and Stop buttons feeding Conveyors.
</p> -->

Secondly, once the conveyors are on, it is a matter of time util a block of material reaches the *Vision Sensor* that will send its readings in DInt type, associating a number to a respective color as the table shows below:

<!-- | Color           | Number |
| --------        | -------:|
| Blue            |  1  |
| Green           |  4  |
| Gray            |  7  | -->

Those readings are compared in the first part of Figure 6. Once a true reading happens, a timmer associated *Valve* is energized starting a TON Timmer (Generate on-delay) set to activate a specific *Sorter* related to a color, with the delay necessary for the material to reach the correct ramp entrance. After the synchronized delay, once the material reaches the expected point on the conveyor, the Sorter is activated and another TOF Timmer (Generate off-delay) certifies that it will remain on time enough for the material to be pushed down the correct ramp.

<!-- <p align="center">
<img width="500" height="300" src=https://github.com/Vangasse/sorting_station/blob/main/img/LAD_timmers.png>
</p>

<p align="center"> 
<b>Figure 6:</b> Ladder code processing Vision Sensor and setting timmers.
</p> -->


<a name="addressing"/>

## Adress Table

The table below contains the compontent adresses used in the implementation.

<!-- | Artifact        | Type | Address |
| -------------   |:----:| -------:|
|                 | Bool |  %I0.0  |
| Start           | Bool |  %I0.1  |
| Stop            | Bool |  %I0.3  |
|                 | Bool |  %I0.7  |
| Vision Sensor   | DInt |  %ID30  |
|                 | DInt |  %ID31  |
|                 | DInt |  %ID32  |
| Entry Conveyor  | Bool |  %Q0.0  |
| Exit Conveyor   | Bool |  %Q0.2  |
| Sorter 1 Turn   | Bool |  %Q0.3  |
| Sorter 1 Belt   | Bool |  %Q0.4  |
| Sorter 2 Turn   | Bool |  %Q0.5  |
| Sorter 2 Belt   | Bool |  %Q0.6  |
| Sorter 3 Turn   | Bool |  %Q0.7  |
| Sorter 3 Belt   | Bool |  %Q1.0  |
| Timmer 1 Valve  | Bool |  %Q1.4  |
| Timmer 2 Valve  | Bool |  %Q1.5  |
| Timmer 3 Valve  | Bool |  %Q1.6  | -->

<a name="material"/>

## Material
<!-- 
- [SortinStation](https://github.com/Vangasse/sorting_station/tree/main/SortinStation): Contains the TIA Portal V15 project;
- [Sorting Station.factoryio](https://github.com/Vangasse/sorting_station/blob/main/Sorting%20Station.factoryio): Contains the schene from Factory IO. -->

<a name="results"/>

## Results

<!-- The image below contains a link to a video of the results:

[![Sorting Station w/ Color Sensor Video](https://img.youtube.com/vi/B6Ax-FoA5KM/0.jpg)](https://youtu.be/B6Ax-FoA5KM)
[Sorting Station w/ Color Sensor Video](https://youtu.be/B6Ax-FoA5KM) -->
