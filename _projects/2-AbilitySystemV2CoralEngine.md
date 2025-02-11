---
title: Ability System V2 - Coral Engine
layout: project
project-image: /assets/images/AbilitySystemV2Thumbnail.png
project-gif: /assets/images/AbilitySystemV2Showcase.gif
project-link: https://github.com/GuusKemperman/CoralEngine
description: >
    "Part 1: A system that allows the creation and management of abilities expanded with the help of visual scripting. <br> 
    Part 2: My contributions to the engine."
project-type: Student Project
engine-tool: Custom Engine (Coral)
year: 2024
team-size: 6 team members
team-breakdown: 6 programmers
duration: 8 weeks
responsibility-subtitles: true
key-responsibilities-1: >
    <h5 class="has-text-grey"> System </h5>
    <li>Ability modularization</li>
    <li>Utilize and Expand Visual Scripting</li>
    <li>User Interface</li>
key-responsibilities-2: >
    <h5 class="has-text-grey"> Engine </h5>
    <li>Player Gameplay Setup</li>
    <li>Physics system</li>
    <li>Engine QOL features</li>
tags:
---

This is the second iteration of my ability system (made in a new custom engine - Coral), the first version can be found here - 
<br><a href="{{ 'projects/3-AbilitySystemV1' | absolute_url }}">Ability System V1 - My Custom Engine</a>.

#### Part 1: Ability System

<a href="https://youtu.be/8dU5pJCtgn4?si=ZOI2gL2VMF7qHqq6" target="_blank">Ability System Showcase Video</a>

Structure of the new system:

<p style="text-align: center;">
    <img src="/assets/ASV2/HowToCreateAnAbility.png" alt="Missing Media">
</p>

The biggest change from the previous version is the addition of **Visual Scripting**, made by my teammate [Guus](https://www.linkedin.com/in/guuskemperman/). The addition of scripting meant the complete modularization of the system so architecture changes needed to be made. These are all the components that go into or are affected by the ability system in this form:

<div style="margin-left: 10vmax;">
    <ul style="display: block;">
    <li>The Ability Asset</li>
    <li>Abilities On Character Component
        <ul style="display: block;">
            <li>Ability Instance</li>
        </ul>
    </li>
    <li>Effects On Character Component
        <ul style="display: block;">
            <li>Durational Effect</li>
            <li>Over Time Effect</li>
            <li>Visual Effect</li>
        </ul>
    </li>
    <li>Character Component (and Player Component)</li>
    <li>Active Ability Component</li>
    <li>Ability Lifetime Component</li>
    <li>Projectile Component</li>
    <li>Prefabs and Scripts</li>
    </ul> 
</div>
<br>

We have the ability editor window where the main script is set along with other meta information about the ability and variables for its activation (like cooldown).

<p style="text-align: center;">
    <img src="/assets/ASV2/AbilityEditor.png" alt="Missing Media">
</p>

The ability activate script can range from very simple to very complex depending on the user's needs.

<p style="text-align: center;">
    <img src="/assets/ASV2/SpawnAbilityPrefab.png" alt="Missing Media">
</p>



