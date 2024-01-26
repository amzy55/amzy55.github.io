---
layout: post
title:  "Ability System The Right And Wrong Way"
date:   2024-01-25 17:51:46 +0100
categories: jekyll update
permalink: /ability-system
---

**Have you ever thought you found the best solution for your needs, just to realize later it was actually the opposite of that?** Come with me on my journey of figuring out how to build an ability system from scratch.

I am a second year programmer at BUas Games, and over the past 6 weeks I have been working on a **tool that allows designers to create abilities modularly** in my C++ ECS-based custom engine for a top-down combat game.

Here is a sneak peek of the finished product:

![ability_system_final_showcase](../assets/gifs/ability_system_final_showcase_zoom.gif)

This project is very valuable for me, as I am aiming to become a Gameplay Programmer, but I am also interested in tools - so for these reasons I will split this article in two sections: <a href="#part1">**Tools & UI**</a> and <a href="#part2">**Ability System**</a>.

Before starting I want to clarify some terminology and establish my code starting point - so what is an **ECS**? ECS stands for **Entity Component System** - instead of working with classes and inheritance like OOP (Object Oriented Programming), we use a DOD approach (Data Oriented Design). In the previous project I worked on, the goal was to build a game engine around this principle: entities that have components with data attached to them and the functionality is given by the systems - I will assume some basic knowledge of the concept moving forward. So that is my code starting point - my own custom engine.

Now that the structure of my engine is established, I can start talking about the main topic of discussion - the **ability creation tool**. I used the terms ability system and ability creation tool interchangeably, but in actuality they are separate components of the overall system. 

<h2 id="part1"><b> Part 1 - Tools & UI </b></h2>

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
    
    enum State : unsigned int
    {
        Stunned = 1 << 0,
        Rooted = 1 << 1,
        Silenced = 1 << 2,
        Invincible = 1 << 3,
        Dashing = 1 << 4,
    };

    unsigned state = 0;
};
```

Both current and base values are needed because we need a reference point - for example if you have a buff that increases the player's movement by `30%` `from 10 to 13`, well how do you undo that when the buff duration is over? Because if you decrease the same percentage from the current movement speed - `30% from 13` - you get `3.9`, which would result into `9.1` instead of `10`. That is why we need the base stat as well - to have a static reference point.

There is also the state which is a `bitmask` where the different states of the player can be active or not based on the flags. But this can all be understood better through the **Player Stats Window Info Tab**:

![player_stats_window_info](../assets/images/player_stats_window_info.png)
![player_stats_window_edit](../assets/images/player_stats_window_edit.png)

As well as giving the designer a way to edit the base stats of the player in engine through the **Edit Tab**.

But how does one actually affect these stats through abilities? Well it is one of the choices in the user interface - the **Stat Affected** drop-down menu:

![stat_affected](../assets/images/stat_affected.png)

Moving on you may ask "how do we translate the Player Stats Component's members into UI"? Well this one of the weaknesses of my project - it is not straight-forward. In the **Ability Settings** I have `enum classes` for all the different aspect of my ability - in this case the Stat Affected:

```c++
enum class Stat
{
    Health = 0,
    Ammo,
    ReloadSpeed,
    MovementSpeed,
    DealtDamageModifier,
    ReceivedDamageReduction
};
```

But `ImGui` needs strings to be able to print out the options, so we also store an array of char pointers:

```c++
    const char* m_stats[6] = {"Health", "Ammo", "Reload Speed", "Movement Speed", "Dealt Damage Modifier %", "Received Damage Reduction %"};
    int m_statsSelectedItem = 0;
```

This is not ideal, as they all need to be kept in sync. It is not in my nature to utilize a suboptimal method, but sometimes we need to make this kind of choices for the project to progress. But let's not dwell on the dwell on the bad, let's move on to the actual implementation of the abilities!

After the user creates a new ability we need a way to store it - that's where the **Ability Settings** come in! This is where all of the drop-down menus and inputs are saved:

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

Now these are a lot of variables, but bear with me! They each describe a different aspect of an ability - they will never all be used at the same time, but they still need to all be present to ensure homogenous storage of the abilities in the **Ability Manager**. The manager is just a glorified unordered map of ability names as keys, storing Ability Settings:

```c++
std::unordered_map<std::string, AbilitySettings> m_abilities;
```

That is also visualized in engine through the Resource Viewer:

![ability_manager](../assets/images/ability_manager.png)

This way the user has a way of overviewing all of their created abilities, as well as a means to delete them.

But how does one assign abilities to a player to use? That is where the **Player Stats Window Abilities Tab** comes in:

![player_stats_window_abilities](../assets/gifs/player_stats_window_abilities.gif)

Through this window the user can assign different abilities, as well as specify input bindings for them. The abilities section can be either a tab as shown in the video above, or appended to the front page of the Player Stats Window how you will see in the next video.

These quite a bit of menus and windows, for this reason I gave the user the option to turn each one off if they wish to. This is an overview of all of the UI:

![ui_overview](../assets/gifs/ui_overview.gif)

Before moving on to the next section, I want to highlight that is important when creating a tool to make easy to right and hard to use wrong - for this reason I also have errors and warnings to notify the user of possible issues, since I believe that elevates the usability of any tool:

![errors](../assets/images/errors.png)
![warnings](../assets/images/warnings.png)

And that concludes the first section of my article - now we move on to the actual logic of the abilities!

<h2 id="part2"><b> Part 2 - The Ability System </b></h2>