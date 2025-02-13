---
title: "Internal: Code Style Guide"
categories:
  - Internal
---

## Unity C# Style Guide for Dinguses

<br>
**Methods**
```cs
public void MethodName() // PascalCase
{
    // Insert code here with this 2 tabs
}
```

**Classes**
```cs
public class MarkusAI() // PascalCase
{
    // this is a class wow
}
```

**If-statements**
```cs
if (true) 
{
    // do things
}
```

**Variables**
```cs
[SerializeField] int UNCHANGING_VALUES; // full caps
int changingValues; // camelCase
Camera _classReferences; // _camelCase
```

**Enums**
```cs
private enum Kongs 
{
    Cranky,
    Diddy,
    Tiny
}
```

**Events**
```cs
public static event Action GameStart;

void Start() 
{
    GameStart += OnGameStart; // For big functions
    GameStart += () => Debug.Log("I'm for tiny anonymous functions, no reason to create a separate function");
}

void OnGameStart() 
{
    // Triggered when game starts
}
```

**Singletons**
```cs
//Keep singletons to a minimum to avoid chaos of scripts calling other scripts from all over, it becomes very difficult to track as the project balloons.
//In many cases, especially if we go multiplayer, create a more structured delivery of information rather than directly asking for the information.

public static SingletonName Singleton { get; private set; }

private void Awake()
{
    if (Singleton != null && Singleton != this) Destroy(this);
    else Singleton = this;
}
```

**Other Tips**
```cs
// Ctrl+K+C = comment, Ctrl+K+U = uncomment.
// When you want a variable to be public, but not shown in the inspector window use 'internal'
```
<br>
# Unity File Structure
## NEW Assets File Structure

We're going to take the previous file structure, but flip it. For example:
```
Assets
    ↳ Enemies
        ↳ RangedEnemy
            ↳ Projectiles
    ↳ Abilities
        ↳ Fireball
            ↳ FireballProjectile.cs
```

Essentially, rather than descending by file type, it's by context. Scripts, materials, prefabs, etc. will be placed in the context in which they're relevant for more intuitive retrieval. Rather than Scripts->Player, it's Player->Scripts. 

If this gets confusing, we can change it, but seems like it'll work for now.


## Avoiding Merge Conflicts
The exception to the above rule will be in Scenes, where some additional precautions have to be taken in order to avoid merge conflicts.  
In Scenes, there are three folders, FinalScenes, PersonalScenes, and TestScenes, each of which have their own specifications 
### Personal Scenes
This is where most of your work will be done. Everyone will have their own personal scene for developing features, which should contain your name in the title. When developing a new feature, be sure to use this scene to avoid conflicts.   
Please don't use other people's scenes.
### Test Scenes
Of course, a personal scene is all well and good, but you'll have to be basing the work off something. You may not want to work out how to, for example, set up and bake a navmesh for enemies when you're developing the player's attack. This is where the test scenes come in. Whenever you complete a feature to a point where someone else could do work on it, you should create a copy of your personal scene, rename it to be whatever feature you implemented in that scene, then move it into test scenes. If someone else wants to expand on your work, they can make a copy of the test scene, replace their personal scene with it, and start working on it.  
Continuing the earlier example, whoever completed work on the enemies would copy their personal scene with their working enemy movement, rename the copy something like EnemyFollowsPlayer, and place it into test scenes. From there, when you started work on the player attack, you would make a copy of EnemyFollowsPlayer, replace your personal scene with it, and begin development on the attack in your personal scene.  
In general, you shouldn't be making changes directly to any test scene. Every so often, Moore will purge the old obsolete ones, but asides from that, they shouldn't really be touched outside of making copies.
### Final Scenes
The big exciting scenes that actually go into the game (hopefully). Most of the time, we won't really be working on these at all. If, for whatever reason, you are, make an announcement in the [\#status-update](https://discord.com/channels/1327076672138248222/1329920049061953728) channel on discord when you start and stop working on it, so that people know when they can and can't touch.  
Please actually check things in and out, if you do a load of work on a main scene only for there to be a conflict because you forgot to check the scene out, you've got only yourself to blame. I will be similarly displeased if you go to bed without checking a scene back in, as no one else will be working on it until you wake up.


