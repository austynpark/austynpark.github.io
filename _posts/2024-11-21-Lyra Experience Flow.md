---
layout: post
title: 1. Lyra Experience Load
subtitle: Lyra
categories: Unreal Engine 5
tags: [C++, UE5, Lyra]
---
 
## Lyra Game 분석 

# 1.InitGame()
- Call HandleMatchAssignmentIfNotExpectingOne() next frame

# 2.InitGameState()
- Register OnExperienceLoaded Delegates to ExperienceManagerComponent
- ExperienceManagerComponent->CallOrRegister_OnExperienceLoaded(OnExperienceLoaded);
- On all the actors 'PostInitializerComponent()', ExperienceManagerComponent->CallOrRegister_OnExperienceLoaded(OnExperienceLoaded) are called.

# 3.HandleMatchAssignmentIfNotExpectingOne()
- Find ExperienceID from GameMode Options string or use Default Experience's ID
- Call OnMatchAssignment(ExperienceID)

# 4.OnMatchAssignment(ExperienceID)
- ExperienceManagerComponent->ServerSetCurrentExperience(ExperienceID)

# 5.ServerSetCurrentExperience(ExperienceID)
- Get Asset Path & Default Class
- StartExperienceLoad()

# 6.StartExperienceLoad()
- Load Experience Asset (All the game features / game actions)
- Register Delegate OnAssetLoadedDelegate(OnExperienceLoadComplete())

# 7.OnExperienceLoadComplete
- Add GameFeature Plugin URL that needs to be enabled (CurrentExperience->GameFeaturesToEnable)
- Add GameFeature Plugin URL of CurrentExperience->ActionSets
- ExperienceManager::NotifyOfPluginActiovation(PluginURL): Track all the plugins that are currently activated
- GameFeatureSubSystem::Get().LoadAndActivateGameFeaturePlugin(PluginURL, OnGameFeaturePluginLoadComplete)

# 8. OnExperienceFullLoadCompleted
- Register, Load and Activate all the game feature action
- BroadCast OnExperienceLoaded Delegates (Functions registered from CallOrRegister_OnExperienceLoaded)

<br>
<br>