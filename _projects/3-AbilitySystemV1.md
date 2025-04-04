---
title: Ability System V1 - My Custom Engine
layout: project
project-image: /assets/images/AbilitySystemV1Thumbnail.png
project-gif: /assets/images/AbilitySystemV1Showcase.gif
github-link: 
itch-link: 
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

This is my first implementation on an ability system, the improved version can be found here - 
<br><a href="{{ 'projects/2-AbilitySystemV2CoralEngine' | absolute_url }}">Ability System V2 - Coral Engine</a>.

Check out the blog I wrote about my process of creating this system here - 
<br><a href="{{ 'blog/ability-system-v1' | absolute_url }}"> Ability System Blog Post 25 Jan 2024</a>.

#### Part 1: Ability System & Its Interface

The abilities have a set of predefined behaviors that the user can configure through the <a href="https://github.com/ocornut/imgui" target="_blank">ImGui</a>-based interface. The set of properties was self-imposed by doing a <a href="/assets/a-s-v1-post/gifs/BrawlStarsAbilitiesPersonalBreakdown.gif" target="_blank">personal breakdown</a> of the character abilities and stats in <a href="https://supercell.com/en/games/brawlstars/" target="_blank">Brawl Stars</a>.

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/gifs/ability_creation_menu_small.gif" alt="Missing Media">
    <img src="/assets/a-s-v1-post/images/PlayerStatsWindow.png" alt="Missing Media">
</p>

The ability creation menu is **dynamic** and displays different **settings** based on the current settings, as to not overwhelm the user with all the information. Additionally, after **testing** my tool with a few designers, based on their **feedback** I added **quality of life features** that account for human error:

<p style="text-align: center;" class="is-centered">
    <img src="/assets/a-s-v1-post/images/warnings.png" alt="Missing Media">
    <img src="/assets/a-s-v1-post/images/errors.png" alt="Missing Media">
    <br>
    <img src="/assets/a-s-v1-post/images/ConfirmOverrideWindow.png" alt="Missing Media">
    <img src="/assets/a-s-v1-post/images/ToolTipExample.png" alt="Missing Media">
    TootTip
</p>

After an ability is created and assigned to a player, the **Ability System** manages its lifetime, along with some additional visual elements. The ability is then created by retrieving the **Ability Settings** from the **Ability Resource Manager** and assigning it its caster that is then used for hostile/friendly logic.

```c++
entt::entity abilityEntity = m_registry.create();
auto& abilityComponent = m_registry.emplace<AbilityComponent>
    (abilityEntity, castByPlayer, Engine.ResourceManager().GetAbilityManager().Get(abilityName).value());
```

<br>

Its runtime behavior is then handled by the **UpdateAbilities** function, that has a lot of conditional code that is improved in the next version (<a href="{{ 'projects/2-AbilitySystemV2CoralEngine' | absolute_url }}">Ability System V2</a>).

For example, for this ability below the system facilitates the **`  `** with the following settings:

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/images/AbilityCreationSettings3Projectiles.png" alt="Missing Media">
    <img src="/assets/a-s-v1-post/gifs/AbilitySystemV13Projectiles.gif" alt="Missing Media">
</p>

The system is in charge of **creating** those **projectiles** with a certain **size and speed** for the physics body, **destroying** them on collision or when the **max range** is reached, **dealing damage** if it encounter a **hostile entity** and everything else that goes into the logic behind an ability.

**Showcase of various abilities and their effects:**

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/gifs/ShowcaseOfVariousAbilitiesAndEffects.gif" alt="Missing Media">
    <img src="/assets/a-s-v1-post/images/VisualEffectsEditor.png" alt="Missing Media">
</p>

#### Part 2: Custom Engine Development

This system was done in my **ECS** <a href="https://github.com/skypjack/entt" target="_blank">EnTT</a> custom engine - I was in charge of the architecture of how I implement the idea of <br> **entities**, **components** and **systems** (having the graphics side provided by teachers).

**Engine structure:**

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/images/engine_hierarchy.png" alt="Missing Media">
</p>

**GLTF loading** with **transform hierarchy:**

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/gifs/hierarchy_showcase.gif" alt="Missing Media">
</p>

**Particle system:**

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/gifs/particle-system-full-costumization.gif" alt="Missing Media">
</p>

I also implemented a **Resource Manager** and even a bit of **Lua Scripting** by binding some basic functionality like input and transforms.

At the end of the project my engine could **create and manipulate entities**, with the foundation laid for **extra components and systems to be added in the future** - which is how I added the **ability system** explained above.

**Engine showcase:**

<p style="text-align: center;">
    <img src="/assets/a-s-v1-post/gifs/engine_final.gif" alt="Missing Media">
</p>

While engine development is not my passion, I still enjoyed working on this project and **I learned so much from creating my own architecture** instead of just working with an existing code base.