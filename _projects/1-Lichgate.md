---
title: Lichgate
layout: project
project-image: /assets/images/LichgatePoweredByCoralEngine.png
project-gif: /assets/images/lichgate.gif
github-link: 
itch-link: https://buas.itch.io/lichgate
description: An action rogue-like where you must grow stronger to vanquish the undead.
project-type: Released Student Game
engine-tool: Custom Engine (Coral)
year: 2024
team-size: 10 team members
team-breakdown: 10 -> 6 programmers & 4 designers
duration: 8 weeks
key-responsibilities-1: >
    <li>Main Gameplay Programmer</li>
    <li>Weapon System</li>
    <li>Upgrade System</li>
key-responsibilities-2: >
    <li>UI</li>
    <li>Supporting Designers to Learn our Custom Engine</li>
tags:
---

<!--<div class="has-text-centered">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/QzNdgcYAYl4?si=wdbvH2UHfL4PfGgw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen=""></iframe>
</div>
-->

Lichgate is a top-down action rogue-like where you fight hoards of enemies and upgrade your power to emerge victorious. It was made with [Coral Engine](https://github.com/GuusKemperman/CoralEngine), a custom engine me and my teammates made, but I talk more about that in the [Ability System V2 in Coral Engine](../projects/AbilitySystemV2CoralEngine) project, now it's about the creation of the game itself.

I had to adapt my **Ability System** to the needs of our game and development and I upgraded it with a **Weapon System**.

After discussing with our designers what exactly the main abilities of the player will be, I decided that a more specialized system is needed. 

#### Weapon System

<p style="text-align: center;">
    <img src="/assets/Lichgate/LichgateAbilitySystem.gif" alt="Missing Media">
</p>

I build the Weapon System on top of the Ability System, since we knew that the player's main combat abilities will all have the same structure of a weapon, but still kept the base system for general-purpose abilities like for the AI.

I had previously gotten the feedback that it is sometimes hard to keep track of all the variables of an ability, and the player abilities would need a lot of tweaking, so I made this **new interface**.

<p style="text-align: center;">
    <img src="/assets/Lichgate/WeaponEditor.png" alt="Missing Media">
</p>

Using the weapon system I then created **two of the player guns**.

<p style="text-align: center;">
    <img src="/assets/Lichgate/WeaponDescriptions.png" alt="Missing Media">
</p>

**Arcane Surge Weapon:**

<p style="text-align: center;">
    <img src="/assets/Lichgate/ArcaneSurge.gif" alt="Missing Media">
</p>

Arcane Surge was more complicated than initially planned because the designers had a vision that did not align with the system's capabilities at the time, but were adamant that it is **essential to the core of the game**, so we had to discuss the matter. The issue was that this weapon needed **different input** - instead of shooting on button trigger, it would have to **shoot on button release**, the projectile getting bigger and more powerful the longer the button is held down.

It could be done, but it would take time. I gave an **estimate** to the design lead of 3 days for making this change in the system, which was a considerable amount of time in a short project and because I, as the **main gameplay programmer**, would be unavailable for that time. After weighing the different sides, we eventually concluded that having **weapons that feel unique** makes my time worth investing in this change, so that's what I did.

In the user end this was only reflected as a simple **checkmark**, but I had to considerably change the **logic of the weapon activation** to account for this.

<p style="text-align: center;">
    <img src="/assets/Lichgate/Checkmark.png" alt="Missing Media">
</p>

After the initial implementation, **designers were able to seamlessly work with my tool** and make the necessary tweaks without the support of a programmer. That was often not the case for some of our other engine features, as it was all new to them, so I am proud of this achievement. 

**Ability/Weapon Assets in-engine:**

<p style="text-align: center;">
    <img src="/assets/Lichgate/AbilityAssets.png" alt="Missing Media">
</p>

For a breakdown of abilities refer to this project page - [Ability System V2 in Coral Engine](../projects/AbilitySystemV2CoralEngine).

#### Upgrade System

Following the <a href="https://youtu.be/rJIwqo12_dk?si=efPG4NIHhAW-Vdq8" target="_blank">Vampire Survivors</a>/<a href="https://store.steampowered.com/app/1966900/20_Minutes_Till_Dawn/" target="_blank">20 Minutes Till Dawn</a> structure, we also needed upgrades in our game, which I implemented.vThe upgrades used a **power level system** - the higher the level, the more powerful the upgrade, and new ones get unlocked depending on your choices.

<p style="text-align: center;">
    <img src="/assets/Lichgate/UpgradeLevels.png" alt="Missing Media">
</p>

So I made a system that works with that concept, again making sure **designers can work without programmer input**, so I also created **how-to documents**.

<p style="text-align: center;">
    <img src="/assets/Lichgate/UpgradeEditor.png" alt="Missing Media">
</p>

When it came to the **upgrade gameplay logic** I implemented a part of that alongside one of our designers that was able to contribute as well through the use of our visual scripting and the explanations I provided.

<p style="text-align: center;">
    <img src="/assets/Lichgate/UpgradeScript.png" alt="Missing Media">
</p>

**In-game upgrade selection menu:**

<p style="text-align: center;">
    <img src="/assets/Lichgate/UpgradeUI.png" alt="Missing Media">
</p>

#### Runtime Data Issue & Resolution

Having upgrades meant that the **abilities settings needed to change at runtime**. That was an issue because my system had not initially accounted for this scenario when we did not know the specifics of the game.

The impediment was that I was **storing the abilities as assets**, which is compile-time data. We unfortunately discovered this issue very close to our first milestone deadline, so just for the deliverable me and our main engine programmer decided we will do a workaround and make assets run-time editable. We were aware that is not the solution, so after we delivered the build we reverted the changes and **I properly implemented the feature**.

Now the **Abilities On Character Component** holds an **Ability Asset** to derive the base values from, as well as a **Runtime Weapon** where the values can be modified for the upgrades.

<p style="text-align: center;">
    <img src="/assets/Lichgate/AbilitiesOnCharacterComponent.png" alt="Missing Media">
</p>

#### UI

**I created most of the UI/HUD elements** in Lichgate using the UI system made by my teammates.

Showcase:

<p style="text-align: center;">
    <img src="/assets/Lichgate/UIShowcase.gif" alt="Missing Media">
</p>

