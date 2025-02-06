---
title: "Devlog: Soup Synergy System"
categories:
  - Devlog
---

## CLEARING THE AIR
Following post-rogue-like-decision-day, we finally had a goalpost we were trying to reach, but the exact implementation was still extremely vague. Thus, we spent the past week constructing design docs to clear the air on what this little soup game actually is. And now, I'm proud to say... **there are no big mysteries left!!!!**... for now. Who knows, we might get sued by Big Soup.

I figured it'd be nice to showcase the 'Soup System Overview' design doc since it forms the foundation for our moment-to-moment core gameplay. So without further ado, here it is!

***

## 1	Brief Summary
The goal of this system is to impart the feeling of someone foraging for meal ingredients, a la “Oooo this truffle will pair beautifully with this oregano I found”. Players should be continuously planning their soups and making choices on which items to grab that best suit their desires.

The player wields several spoon weapons. Cooking soups then places a spoon into it. Abilities are infused into soups and accessed via using its corresponding spoon (aka taking a spoonful). Buffs then augment those abilities, creating highly customizable spoon weapons. For example, if you combine a projectile ability ingredient with an onion that grants +10 speed, then when you use the spoon, it’ll shoot the projectile faster. Adding an additional +10 damage cucumber then would make the projectile deal more damage, and so on.

## 2	Cooking and Spoons
Similar to Gungeon, the player will always have an infinite-use, dinky wooden spoon that does a short-ranged melee swing. To get more powerful spoons, you must cook bowls of soup to dip them in. All spoons can be cycled between, but the powerful spoons have limited uses based on the ingredients of the soup.

There are now two types of ingredients: **Abilities** and **Flavors**. While at a cooking station, players can form bowls of soup by combining up to 5 ingredients and at least one ability. The ability ingredients determine the type of action that occurs when you use the spoon while flavors augment those abilities. 

Infused spoons will have limited uses and you may cook up to 3 soups. Once a soup is used up, it’ll disappear and free up a soup spot. You may also dump out soups at cooking stations.

A sprint 3 goal could be to make soup bowls + spoons be collectibles and you can only store a single soup per bowl before it crumbles away. That way, bowls can be rewarded in chests and can hold its own synergetic properties (ex: all Buffs are doubled).

## 3	Abilities
Abilities will be split up into **Ability Classes** each with several variants. The more abilities within those 5 soup ingredients, the more uses (ex: each Single Projectile (See 3.1) may have 20 uses, so including four will produce a soup with 80 uses). Different ability classes can be mixed and matched freely within the same soup, they’ll just be executed concurrently. The total uses for a soup will always be the sum of its ability ingredients’ use counts, regardless of class. Including multiple ability ingredients, means less slots are available for flavors, forcing players to balance where ingredients are allocated and judge what’s most important to collect in the first place.

Ability ingredients are derived mostly if not exclusively from enemies. Each enemy grants a specific ability ingredient. Typically, enemies that grant ingredients within an ability class will share the same species (e.g. all enemies that grant projectiles will be potatoes).

### 3.1 Projectiles
Projectiles fire from the player upon use. Projectiles will have 2 variants (can always add more): **Single Projectile** and **Double Projectile**. 

![projectile class](/csgd-capstone-site/assets/images/ProjectileClass.png)

> *EXAMPLE RECIPE*
- *SINGLE PROJECTILE (x20 uses) +*
- *SINGLE PROJECTILE (x20 uses) +*
- *DOUBLE PROJECTILE (x20 uses) =*
    - *Triple Shot (60x uses)* <br>
>
> ![triple shot](/csgd-capstone-site/assets/images/TripleShot.png)

### 3.2 Zones
Zones apply effects to any entity that enters within it (players or enemies). They persist for several seconds (depending on persistence flavor), but can only apply once per entity (no walking out and back in). 

![zone](/csgd-capstone-site/assets/images/Zone.png)

Zones will have 2 variants (can always add more): **Player Zone** and **Ranged Zone**.

The Player Zone will spawn at the players feet and apply effects immediately.

The Ranged Zone will be launched from the player towards the direction they’re facing. The distance traveled will be based on the distance of the mouse from the player, the zone ingredients base travel time, and the persistence flavor attached. Once landed, then it’ll begin applying effects.

### 3.3 Melee
Deals damage in front of the player. Melee comes with 2 variants: **Standard Slash** and **Charge**. 

Standard Slash is essentially the same as the base uninfused spoon if it could be infused. 

Charge will cause the player to dash in the direction they’re facing, inflicting damage on anything in the path.

## 4	Flavors
Now this is where it gets spicy. Ingredients foraged from the environment hold one or more flavors. Each flavor is associated with a specific stat (See 4.1 & 4.2 below). There’s two categories of flavors: **Buffs** and **Statuses**. Buffs augment the ability itself, while Statuses are inflicted upon anything the ability contacts. Buffs can either add (ex: +10 damage) or multiply (ex: +10% damage).

This system would allow players the freedom to construct fireballs themselves by combining a Single Projectile ability + Spicy Peppers, or restore health by combining a Player Zone + Gummy Worm (+10 health). To be robust, it must treat all entities identically, meaning theoretically if an enemy walked into a health zone, they’d also gain health.

### 4.1 Buff Example List

| Buff | Add  | Multiple  |
| -------- | ------- | ------- |
| Sweet  | +2 seconds persistence | +200% seconds persistence |
| Sour |   +10 critical strike chance   | +100% critical strike damage |
| Salty    | +1 size    | +50% size |
| Bitter    | +10 speed    | +50% speed |

### 4.2 Status Example List

| Status | Add | Multiple |
| -------- | ------- | ------- |
| Spicy | +1 burn | x3 burn |
| Frosty | +1 freeze | x3 freeze |
| Slimy | +10 health | +50% health |
| Earthy | +2 attack damage | +50% attack damage |