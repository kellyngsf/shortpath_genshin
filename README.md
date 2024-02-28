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
  <img src="https://github.com/kellyngsf/shortpath_genshin/blob/main/images/default_map.png" width 600>
</p>
