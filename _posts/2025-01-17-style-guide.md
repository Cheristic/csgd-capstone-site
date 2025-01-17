---
title: "Code Style Guide"
categories:
  - Blog
tags:
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
    if (Main != null && Main != this) Destroy(this);
    else Main = this;
}
```

**Other Tips**
```cs
// Ctrl+K+C = comment, Ctrl+K+U = uncomment.
// When you want a variable to be public, but not shown in the inspector window use 'internal'
```
