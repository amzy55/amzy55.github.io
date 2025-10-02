---
title: Ability System V2 - Coral Engine
layout: project
project-image: /assets/images/AbilitySystemV2Thumbnail.png
project-gif: /assets/images/AbilitySystemV2Showcase.gif
github-link: https://github.com/GuusKemperman/CoralEngine
itch-link: 
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

<div class="columns">
    <div class="column has-text-centered">
        This is the second iteration of my ability system (made in a new custom engine - Coral), the first version can be found here:  
        <br><a href="{{ 'projects/3-AbilitySystemV1' | absolute_url }}">Ability System V1 - My Custom Engine</a>.
    </div>
    <div class="column content is-narrow">
        <div style="
        width: 1px;
        height: 50px;
        background-color: rgb(54, 54, 54);"></div>
    </div>
    <div class="column has-text-centered">
        The system is later improved again, as well as expanded into a Weapon System for the game Lichgate, the next version can be found here: 
        <br><a href="{{ 'projects/1-Lichgate' | absolute_url }}">Lichgate - Weapon System</a>.
    </div>
</div>

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
    <li>The Ability Functionality Class</li>
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
    <img src="/assets/ASV2/AbilityMoreComplex.png" alt="Missing Media">
</p>

Besides the **On Ability Activate Script** the system allows or a virtually infinite amount of scripts to be utilized either by calling them from the initial script or by adding them to the **Ability Prefab** if the ability has one (like a projectile that needs a physics representation).

Example of an ability prefab:

<p style="text-align: center;">
    <img src="/assets/ASV2/AbilityPrefab.png" alt="Missing Media">
</p>

One big improvement from the previous version was the separation of data - before tha **Ability Settings** struct was a monolithic set of variables that not all abilities needed. Now I spread that into multiple parts like the **Effects Component**, **Projectile Component** or **Lifetime Component** and the user can attach whatever they need to the **Ability Prefab**.

With a lot of the gameplay logic moved to scripts, the **Ability System** (as in the actual ECS system) is now only in charge of the **activation of abilities**, **updating timers** and **managing effects** (durational, DoT and visual effects).

There is also the **The Ability Functionality Class** that includes a lot of helper functions and exposes them to scripting such as:

**Apply Durational Effect()**

<p style="text-align: center;">
    <img src="/assets/ASV2/ApplyDurationalEffect.png" alt="Missing Media">
</p>

**Was The Ability Cast By An Enemy()**

<p style="text-align: center;">
    <img src="/assets/ASV2/WasTheAbilityCastByAnEnemy.png" alt="Missing Media">
</p>

All the parts came together and me and my team created a demo for our engine where my **Ability System** was the focal point, most of the gameplay logic being implemented by me, except parts of the AI:

<p style="text-align: center;">
    <img src="/assets/ASV2/GameplayFinalDemoDust2.gif" alt="Missing Media">
</p>

<a href="https://youtu.be/rJIwqo12_dk?si=efPG4NIHhAW-Vdq8" target="_blank">Demo Video</a>

#### Part 2: Coral Engine

<div class="has-text-centered">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Z4UFHaJ_ulQ?si=1LSgzoy8_2Ge7DN0" title="Coral Engine Trailer" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen=""></iframe>
</div>

#### My Contributions to Coral Engine

While most of my time was spent of the Ability System, I contributed to the engine in other ways too.


**Physics System**

I added the initial implementation of the Physics System to the engine. With resources from teachers and my own research I made a basic 2D Physics System that included:

<div style="margin-left: 10vmax;">
    <ul style="display: block;">
    <li>Physics bodies
        <ul style="display: block;">
            <li>Static</li>
            <li>Dynamic</li>
            <li>Kinematic</li>
        </ul>
    </li>
    <li>Shape Colliders
        <ul style="display: block;">
            <li>Disk Collider</li>
            <li>Polygon Collider</li>
        </ul>
    </li>
    </ul> 
</div>

<br>

Showcase:

<p style="text-align: center;">
    <img src="/assets/ASV2/PhysicsSystemShowcase.gif" alt="Missing Media">
</p>

We decided to go for a 2D physics system because we were developing an engine specifically for top down games - you can read more about my journey with figuring out what approach I should take to physics in this blog I made - <a href="{{ 'blog/ability-system-v1#PhysicsSystem' | absolute_url }}"> Ability System Blog Post 25 Jan 2024 - Physics System</a>.

**Quality of Life Features**

We were initially only programmers working on our engine, but if the engine proved good enough we had the opportunity to take it into the next project to create a game with other disciplines as well - which we succeeded in with <a href="{{ 'projects/1-Lichgate' | absolute_url }}">Lichgate</a>. But in order to achieve that me and one other teammate made sure to play-test our engine with artists and designers too.

For example artists requested better support of the **gizmo snapping** - initially **the input was three values for each axis XYZ**, and even though I could see the thought behind it to give more flexibility to user, it just simply was not intuitive and it made the workflow slower. The snapping value was also **shared between the three transforms** (Translation, Rotation, Scale), so you couldn't have different values for them.

Before:

<p style="text-align: center;">
    <img src="/assets/ASV2/SnappingInitially.png" alt="Missing Media">
</p>

So I made these changes and additionally added **snapping ON by pressing Ctrl** like Unreal has also based on feedback.

After:

<p style="text-align: center;">
    <img src="/assets/ASV2/SnappingImprovement.gif" alt="Missing Media">
</p>

I also pushed for us to have read-only values, which might seem like a small detail, but it goes a long way for the usability of an interface. I was initially doing that manually, but after discussing with our main engine programmer, he ended up adding it as a feature for all editors.

**Read-only values in grey:**

<p style="text-align: center;">
    <img src="/assets/ASV2/ReadOnlyValues.png" alt="Missing Media">
</p>

Alongside having a powerful and extensive engine, ensuring non-programmers can work with our tools has put me and my team ahead of the curve and we were able to go on to the next project and actually **develop our game <b><a href="{{ 'projects/1-Lichgate' | absolute_url }}">Lichgate</a></b> with Coral**!