# Network Analaysis: Shortest Paths in Genshin Impact

## Introduction
Genshin Impact is an action RPG game designed by a Chinese game developed called miHoYo. In this game, you can collect characters and level them up to make them stronger. In order to level these characters, you must obtain a certain amount of materials to level them. Furthermore, different characters will require different types of materials. All these materials will be spread throughout Genshin Impact’s world and are available in a limited amount each day. The aim of this project will be to find the shortest path to collect the required materials to level up a character. This is so players can take the most efficient route to collect the materials they need and can spend more time doing other things in the game, such as using their powerful characters to defeat enemies. 

This project will focus on the level-up materials for the character Klee, who requires one type of material that can be collected in the environment and two other material types that are obtained through defeating enemies. Since this project is focused on collecting materials, I will only focus on the material called “Philanemo Mushroom”. 
<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/character_focus.png" width="450">
</p>

## As a Network Problem
To solve the aim of this project, networks can be used. As the materials are spread throughout the world, you can pinpoint their location on a map. Using this map, the locations of the material will be represented as nodes. Some nodes will also be the teleport points on the map, which will be explained in more detail in later sections. The edges will then be the connections between these nodes. There will also be weights to these edges and it will be the time it takes to run from one node to the other. Furthermore, the edges will be undirected because the time it takes from one point to another and the other way around will be roughly the same. The time recorded will not include the time it takes to collect the materials, it will only include the time for travel. Once the data has been obtained and organised, the R package “igraph” will be utilized to find the shortest path by using Dijkstra’s algorithm. Then, we can see what the shortest path is to collect the materials throughout Genshin Impact’s world. 

## Assumptions
For this project, the following assumptions will be used: 
1. The time it takes to run from one node to another and the other way around will be the same, therefore, the edges will be undirected. 
2. The time measured will always be roughly the same because the “running” option will be used when travelling. 
3. The materials will always be in the exact same places when they respawn (i.e., after collecting them, they will be in the same place the next time)

## Data Collection
A large part of this project will be spent on collecting the data by playing the game and running from location to location and measuring the time it takes to get from one place to another. Additionally, the same character will be used throughout the entire data collection process. The first step to collecting the data is to find all the locations that have the required material. This will be done by referring to the game’s official website for their interactive map (https://act.hoyolab.com/ys/app/interactive-map/index.html?lang=en-us#/map/2?shown_types=39&center=2008.50,-1084.00&zoom=-3.00). 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/default_map.png" width=600>
</p>

The above is a photo of the part of the map that includes all the locations that have the “Philanemo Mushroom”. They are split into three regions, the middle is “Mondstat”, the middle bottom is “Springvale” and the bottom left is “Dawn Winery”. Three shortest paths will be calculated, one for each region. This is because you can teleport from anywhere on the map, therefore, once the materials have been collected from one region, I will just teleport to the next region. The teleport points are represented through the blue icons, shown below: 

<p align="middle">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/tp_point.png" width=95 />
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/statue_point.png" width=100 />
</p>

Close-up screenshots were taken for each of the three regions and annotated to have the material locations as nodes and edges connecting them. The edges are placed in paths that are most easy to run through and most natural path for a player to take because it may have an already cut-out path on the ground to run on. Nodes are not placed at every individual point where the “Philanemo Mushroom” is, instead, they are placed at a building or a windmill where the mushrooms are grown on. This is because, once you reach a building for example, you can collect a few mushrooms from that building and won’t need to travel to another point that is far.

**Mondstat**
<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/mondstat.png" width=600>
</p>

**Springvale**

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/springvale.png" width=600>
</p>

**Dawn Winery**
<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/mondstat_shortestpath.png" width=600>
</p>

I measured the time it took to run from one node to another node using a stopwatch and always using the “running” option in-game (instead of the “walking” option). I have recorded the times on the images above on the edges, with the time being recorded in seconds. It’s also important to note that measurements such as distance won’t be taken into account because there are many cliffs, mountains, and trees that you have to traverse in-game, therefore, the distance may not be a good measure to show how far the nodes are from each other. Instead, time would be better because we are trying to find the shortest and fastest path to collect the materials, which is solely dependent on the time it takes to run from one point to another, including getting through the obstacles in-game. 

## Analysis from Results
For easy access to shortestpath_analysis.html, click on this link: https://kellyngsf.github.io/shortpath_genshin/shortestpath_analysis.html.

### Mondstat:
After importing the data for the region Mondstat into R, I used the command “shortest_paths” under the R package “igraph” to find the shortest paths. The algorithm used is Dijkstra’s algorithm on default because the command “shortest_paths” works so that it automatically uses Dijkstra’s algorithm when all the edges have a positive weight. 

The results are shown in the image on the below. Since the aim of this project is to collect materials, the most useful paths are the paths with the most nodes, which in this region is: “a -> b -> d -> e -> g -> i”. 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/mondstat_analysis.png" height=600>
</p>

This shortest path is shown below through the highlighted blue path: 
<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/mondstat_shortestpath.png" width=600>
</p>

### Springvale:
Carrying out the same method as Mondstat, the data for Springvale was imported into R and was analysed using the command “shortest_paths”. The results are shown below. Looking at the paths with the most nodes, we find that there are two shortest paths with 4 nodes, “a -> b -> c -> d” and “a -> b -> e -> h”. 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/springvale_analysis.png" height=500>
</p>

The two paths are shown below through two different highlighted paths. If you calculate the total time for both paths, the path with the shorter time is “a -> b -> e -> h” (pink) of time 22.29s. Therefore, you can say that the shortest path is “a b e h” for Springvale. 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/springvale_shortestpath.png" width=600>
</p>

### Dawn Winery:
There are also multiple shortest paths for Dawn Winery. By looking at the paths with the most nodes, the shortest paths are “a -> b -> c” and “a -> b -> d”. 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/dawn_winery_analysis.png" height=400>
</p>

The 2 shortest paths are shown below in two different colours. If you calculate the total time for both paths, the path with the shorter time is “a -> b -> c” (blue). Since these paths include 3 out of 4 of the nodes, we can also interpret from the last remaining node/edge and say that the shortest path with all nodes is “a -> b -> c -> d”. 

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/dawn_winery_shortestpath.png" width=600>
</p>

Hence, the shortest paths with the most nodes from the R analysis are shown in the table below.

<p align="center">
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/final_table_shortestpaths.png" width=450>
</p>

## Limitations and Evaluation
This project successfully managed to calculate the shortest paths in all three regions. However, a limitation of this project is that not all the nodes would be included in the shortest paths, which limits the number of materials that can be collected. Since we want to efficiently level a character, it may limit the efficiency in terms of material collection rate, as we are not collecting all the materials available. However, the advantage to this is that it saves time, while still collecting a sufficient amount of materials to level up characters. 

Another limitation of this project is that sometimes the algorithm in “igraph” will output several shortest paths with the same number of nodes. But when calculating the exact time for the different paths, there is a shorter path (in terms of time). Hence, the disadvantage is that the time needs to be manually calculated, instead of being automated through an algorithm. 

One way to improve this project would be to have someone help with measuring the time it takes to travel from one node to another, instead of doing it myself. I realised while collecting the data that sometimes the time measured might be slightly inaccurate because it would include the time it takes for me to start the stopwatch and start running because my hand would have to move from the stopwatch to my mouse. Therefore, the measured time might be slightly longer than it actually is. 

Another way to improve this project would be to ask other players of Genshin Impact what their preferred path of collecting the material “Philanemo Mushroom” is and test if it actually is the shortest path. This is because I might not have included a specific edge from one node to another, as I only included edges of paths that I take most often. 

## Extension
A possible extension for a follow-up project could be finding the most optimal procedure for levelling a character, because not only does it include levelling them up, but you have to level their weapon and “artifacts” which increase a character’s stats. Through these different activities, I could use the critical path method (CPM) to find out how to organize these tasks for the most efficient way to max-level a character. 
