---
layout: post
title:  "Ability System The Right And Wrong Way"
date:   2024-01-25 17:51:46 +0100
categories: jekyll update
permalink: /ability-system
---

**Have you ever thought you found the best solution for your needs, just to realize later it was actually the opposite of that?** Come with me on my journey of figuring out how to build an ability system from scratch.

I am a second year programmer at BUas Games, and over the past 6 weeks I have been working on a **tool that allows designers to create abilities modularly** in my C++ ECS-based custom engine for a top-down combat game.

![ability_system_final_showcase](../assets/gifs/ability_system_final_showcase_zoom.gif)

In this article I will assume a basic knowledge of C++ concepts and terminology, and I will only skim over some topics that are not the main focus.

First off what is an **ECS**? ECS stands for **Entity Component System** - instead of working with classes and inheritance like OOP (Object Oriented Programming), we use a DOD approach (Data Oriented Design). In the previous project I worked on, the goal was to build a game engine around this principle: entities that have components with data attached to them and the functionality is given by the systems - I will assume some basic knowledge of the concept moving forward. So that is my code starting point - my own custom engine.

Now that the structure of my engine is established, I can start talking about the main topic of discussion - the **ability creation tool**. I am using the terms ability system and ability creation tool interchangeably, but in actuality they are separate components of the overall system. 

In the starting video you can see a few types of abilities that my system supports - but how does one go about creating one? This is achieved through the user interface:

![ability_creation_menu](../assets/gifs/ability_creation_menu_small.gif)

All of my menus are created using <a href="https://github.com/ocornut/imgui">ImGui</a>, more specifically all the dropdown menus are achieved through the `ImGui::Combo()` method, so that different settings can be selected from a set collection of options. These options are based off the **Ability Settings** and the **Player Stats Component**.

The Player Stats Component is mainly comprised of a set of attributes the player has, that abilities can alter:

```c++
struct PlayerStatsComponent
{
    int id = -1;
    int teamId = -1;

    float baseHealth = 50.0f;
    float currentHealth = baseHealth;

    float baseAmmo = 3.f;
    float currentAmmo = baseAmmo;

    float baseReloadSpeed = 0.5f;
    float currentReloadSpeed = baseReloadSpeed;

    float baseMovementSpeed = 5.0f;
    float currentMovementSpeed = baseMovementSpeed;

    float baseDealtDamageModifier = 1.f;
    float currentDealtDamageModifier = baseDealtDamageModifier;

    float baseReceivedDamageReduction = 1.f;
    float currentReceivedDamageReduction = baseReceivedDamageReduction;
};
```

Both current and base are needed because we need a reference point - for example if you have a buff that increases the player's movement by `30%` `from 10 to 13`, well how do you undo that when the buff duration is over? Because if you decrease the same percentage from the current movement speed - `30% from 13` - you get `3.9`, which would result into `9.1` instead of `10`. That is why we need the base stat as well - to have a static reference point.

The player stats can be altered by an ability by selecting the **Stat Affected** from the user interface:

![stat_affected](../assets/images/stat_affected.png)

Which in turn are part of the **Ability Settings**:

```c++
struct AbilitySettings
{
    Target targetTeam = Target::Hostile;
    float aoeRadius = 0.f;
    int numberOfProjectiles = 1;
    float projectileRange = 0.f;
    float projectileRadius = 0.f;
    float projectileSpeed = 0.f;
    ProjectileShootType shootType = ProjectileShootType::Line;
    float spaceBetweenProjectiles = 0.f;
    float coneAngle = 0.f;
    CastType castType = CastType::Projectile;
    ApplyType applyType = ApplyType::Instant;
    InstantType instantType = InstantType::Effect;
    float dashSpeed = 0.f;
    StatusEffectType statusEffectType = StatusEffectType::Stun;
    Stat statAffected = Stat::Health; // stat affected!
    float statAffectAmount = 0.f;
    IncreaseOrDecrease increaseOrDecrease = IncreaseOrDecrease::Decrease;
    bool clampToMax = true;
    AppliedAs appliedAs = AppliedAs::Percentage;
    float durationAmount = 0.f;
    int numberOfTicks = 0;
    float aoeDuration = 0.2f;
};
```

Now these are a lot of member variables, but bear with me! They each describe a different aspect of an ability - they will never be used all at the same time, but they still need to all be stored to ensure homogenous storage.
