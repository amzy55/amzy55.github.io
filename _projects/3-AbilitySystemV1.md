---
title: Ability System V1 - My Custom Engine
layout: project
project-image: /assets/images/AbilitySystemV1Thumbnail.png
project-gif: /assets/images/AbilitySystemV1Showcase.gif
description: "Part 1: A system that allows the creation and management of abilities with configurable predefined behavior via dynamic ImGui menus. <br> Part 2: Custom engine development."
project-type: Personal/Student Project
engine-tool: Custom Engine
year: 2023-2024
team-size: Solo
team-breakdown: Solo
duration: 8 + 8 weeks
responsibility-subtitles: true
key-responsibilities-1: >
    <h5 class="has-text-grey"> System </h5>
    <li>Ability Gameplay Code</li>
    <li>Ability Visualization</li>
    <li>Research</li>
    <li>Intuitive Interface Design</li>
key-responsibilities-2: >
    <h5 class="has-text-grey"> Engine </h5>
    <li>ECS / EnTT Library</li>
    <li>Particle System</li>
    <li>GLTF file loading</li>
    <li>Resource Management</li>
    <li>Serialization</li>
tags:
---

<a href="{{ 'blog/ability-system-v1' | absolute_url }}"> Ability System Blog Post 25 Jan 2024</a>

#### Part 1: Ability System 

I created both the user interface, as well as the gameplay logic that powers the abilities, along with its underlying systems.

The abilities have a set of predefined behaviors that the user configure through the <a href="https://github.com/ocornut/imgui" target="_blank">ImGui</a>-based interface. The set of behaviors was self-imposed by doing a <a href="/assets/a-s-v1-post/gifs/BrawlStarsAbilitiesPersonalBreakdown.gif" target="_blank">personal breakdown</a> of the character abilities and stats in <a href="https://supercell.com/en/games/brawlstars/" target="_blank">Brawl Stars</a>.

![ability_creation_menu](/assets/a-s-v1-post/gifs/ability_creation_menu_small.gif)
![player_stats_window_info](/assets/a-s-v1-post/images/player_stats_window_info.png)