---
title: 解决GTASA在Windows10/11的兼容性问题
tags: 
date: '2023-01-18 00:00:01'
- GTA
categories:
- 游戏
toc: true
---

众所周知，GTASA Steam Version问题特别多。本文针对这种情况给出了如下的解决方案和优化思路。

如有其他疑问，可以参考https://www.pcgamingwiki.com/wiki/Grand_Theft_Auto:_San_Andreas

## 降级补丁

非常建议打降级补丁，因为GTASA Steam Version真的是出奇的烂。BUG一堆，而且因为版权问题缺少了很多资源。所以最好打降级补丁。如果本身就不是Steam Version，而且版本是v1.0，那么就不需要降级了。

下载GTASA Downgrader来降级：http://downgraders.rockstarvision.com/

![image-20230117175204432](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230117175204432.png)
<!--more-->
将SA DOWNGRADER.rar的内容解压到游戏根目录下\Grand Theft Auto San Andreas：

![image-20230118151202261](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118151202261.png)

运行install.bat程序，系统将会启动cmd窗口，待程序运行后，窗口就会自动关闭。于是就降级成功了。

在往后的游戏中，我们只需执行gta-sa.exe即可：

![image-20230118152359476](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118152359476.png)

如何确定是否降级成功？如果打开游戏出现如下标志就算成功了：



如果游戏启动失败，你可能需要删掉游戏配置文件目录中的gta_sa.set，他一般位于：

```
	%USERPROFILE%\Documents\GTA San Andreas User Files\gta_sa.set
```

其中%USERPROFILE%是指向用户主文件夹的环境变量，俗称“我的文档”的路径。

## Silent Patch解决兼容性问题

如果不出意外，这个时候你就应该遇到鼠标不可用的问题了。不是你鼠标的问题，是早期版本的GTASA并没有适配大于2核的CPU，所以就有这样的问题。

不管怎么样，你都需要打个Silent Patch补丁。不止是因为它解决了鼠标不可用问题，他还修复了特别多的BUGS，比如万恶的锁25FPS的BUG（严格来说不算BUG，但比较恶心人）和切回游戏时鼠标指针乱飘无法控制的BUG等......

以下摘自官网的数据：

> **Featured fixes:**
>
> -  14ms frame delay has been removed. As a result, game now locks properly on 30 FPS instead of 25 FPS
> -  More precise frame limiter, reducing lag spikes a bit when playing with Frame Limiter on
> - Game timers now tick in a more accurate manner, making them not freeze if framerate exceeds 1000 frames per second; in other words, this fixes occasional freezes on fadeouts if playing with Frame Limiter off
> -  Mouse should not lock up randomly when exiting the menu on newer systems anymore
> -  Mouse vertical axis sensitivity now matches horizontal axis sensitivity
> -  Mouse vertical axis does not lock during camera fadeins now
> - NUM5 is now bindable (like in 1.01)
> - 16:9 resolutions are now selectable (like in 1.01)
> -  If the settings file is absent, the game will now default to your desktop resolution instead of 800x600x32
> -  DirectPlay dependency has been removed - this should improve compatibility with Windows 8 and newer
> -  Path to the GTA San Andreas User Files directory is now obtained differently, increasing compatibility and future-proofing the games more
> - A heap corruption in one place is now fixed (did not affect gameplay but could potentially make the game crash)
> -  EAX/NVIDIA splashes are now removed
> -  Subtitle and Radio text sizes can now be toggled between the original release and updated Steam version
> -  Area name colour now matches the gang colour of the gang that owns that territory (off by default)
> - Wet road reflections render properly again (just like with Road Reflections Fix)
> -  Fixed sun lens flare effect not appearing with AMD/Intel graphics cards
> -  Fixed an issue introducing graphical artifacts from ped animations with high RAM usage - so called “streaming memory bug”
> -  Fixed a bug causing cheat-spawned melee weapons to be forcibly replaced by other melee weapons upon walking into a pickup
> -  Helicopter rotors and plane propellers now work correctly. They now have a blurring effect present in VC and PS2 version of SA
> - Hunter interior does not dissapear when viewed through the glass door panel
> -  Dual rear wheels now show up properly (Yosemite, Tanker etc.)
> - Weapons are now visible when viewed through a vehicle window
> - Holding a weapon will not cause some objects to be incorrectly lit anymore
> - Blown up vehicles are now correctly coloured and no longer shine (like in 1.01 and Steam versions)
> - Dirty cars are now able to get clean (like in 1.01)
> - Each car has an unique numberplate now
> - Custom numberplates now show up correctly in all cases
> - Custom numberplates are now also allowed on bikes
> - Numberplates are now bilinear filtered, resulting in a smoother look
> - Vehicle lights do not get dark after being being initially lit anymore (like on PS2)
> - Detached vehicle parts will now remain the same colour as the vehicle they came from
> - Detached vehicle parts now render from both sides
> -  Some car panels now swing after car’s explosion (like they were meant to be but the code forcibly fixed them immediately after damaging)
> - Moonphases now show up correctly, like on PS2 version (only when playing in 32-bit colour mode)
> - Toggling car lights on does not make windows invisible when viewed from inside anymore
> - Illumination value from timecyc.dat now accepts any float value in 0.0-2.0 ranges, not just 0.0, 1.0 and 2.0
> - In addition, if illumination value is absent from the timecycle (like on a stock PC timecycle), the game will now default to 1.0
> - Lights now get casted on vehicles and peds properly - previously, they’d dissapear under some conditions
> -  In addition, when playing on Visual FX Quality higher than low, the game will now cast up to 6 lights on each model both indoors and outdoors (on Low details, game’s stock behaviour has been kept - allowing up to 4 lights per model outdoors and 6 indoors)
> - Muzzle flash looks better now
> -  Muzzle flash will now show up when firing the last bullet from the clip
> - Coronas’ don’t have a Z test forced all the time now - as a result, sunglare now matches original PS2 version
> - With User Tracks automatic scan enabled, MP3 playback will now work properly if QuickTime is not installed
> - User Tracks now supports the FLAC codec (Only 8/16/24bits, Mono/Stereo and up to 48Khz)
> - PCM WAVE has been expanded to also accept additional profiles (Now 8/16/24bits, Mono/Stereo and up to 48Khz)
> - PCM WAVE files with an ID3-TAG will now also work with the game
> - Temple and Queens are now correctly called on the police scanner
> - Travelling far away from the map will no longer trigger the extra gang territories glitch, nor will it corrupt the Taxi Driver submission
> -  Gym glitch (“You have worked out enough…” showing infinitely) has been fixed
> -  Saving in Madd Dogg’s mansion will no longer trigger the missing basketball glitch
> -  Fixed an occasional softlock in Mountain Cloud Boys - the player will not freeze after arriving to the meeting anymore
> -  Possible softlock in Sweet’s Girl initial cutscene fixed
> -  Quadruple Stunt Bonus now works correctly
> -  Script sprites now have bilinear filtering applied
> -  Car generator counters now work properly for generators with fixed amount of spawns
> - Impound garages now function correctly, allowing the player to recover his last vehicle after it had vanished after a mission start
> - In addition, impound garages will now store player’s car when he’s busted
> - Streamed entity list has been expanded a bit, so now the game world shouldn’t flash when looking down with high Draw Distance settings anymore
> - Mouse rotates an airborne car only with Steer with Mouse option enabled
> - Towtruck tow hitch does not get bugged after it has been fixed anymore
> - Plane doors don’t corrupt after the plane has been fixed anymore
> - Fixing a plane will now reset its moving props to an undamaged state
> - Several vehicle components (most notably, Rumpo’s front bumper and Bandito’s moving prop) will not get glitched after the vehicle has been fixed anymore
> - Weapons and a jetpack now cast proper shadows
> - Crosshair doesn’t mess up weapon icon when on a jetpack anymore
> - Free resprays will not carry on a New Game now
> - Fixed ambulance and firetruck dispatch timers - they reset on New Game now
> - Several stat counters now reset on New Game - so the player will not level up quicker after starting New Game from a save
> - “To stop Carl…” message now resets properly on New Game
> - Previously present only on PS2, ‘Cars drive on water’ cheat is now toggleable - its string is SEAROADER
> -  Randomizer error causing peds not to spawn in some areas has been fixed
> -  Randomizer error causing prostitutes to be quiet during solicit has been fixed
> -  Text boxes now can show together with a Mission Passed text
> - Fixed a 1.01 only tiny memory leak which occured every time the player switched a radio station
> -  Fixed an occasional crash when Alt+Tabbing back to the game while standing next to a mirror
> -  Mirror reflection doesn’t break with Anti-Aliasing enabled anymore
> -  With Visual FX Quality set to Very High, mirror reflection quality has been bumped
> -  Anti-Aliasing option has been altered - instead of listing 1, 2, 3 options (which in fact are 2x/2x/4x MSAA), the game will now show proper MSAA values from 2x up to 16x (depending on max MSAA level supported by the graphics card)
> -  Colliding with another car will now damage proper parts on both cars - previously, both cars got damaged the same way
> -  Fixed a crash on car explosions - most likely to happen when playing with a multimonitor setup
> -  Fixed a crash when entering advanced display options on a dual monitor machine after: starting game on primary monitor in maximum resolution, exiting, starting again in maximum resolution on secondary monitor. Secondary monitor maximum resolution had to be greater than maximum resolution of primary monitor.
> -  Fixed an occasional crash occuring when standing next to escalators
> -  Slightly reduced stencil shadows memory overhead
> -  Fixed an AI issue where enemies became too accurate after the player has been in the car earlier
> - IMGs bigger than 4GB are now handled properly
> -  Alt+F4 now works properly
> - Several vehicles now have extra animated components: Phoenix hood scoops, Sweeper brushes, Newsvan antenna, radars on several boats, extra flaps on Stuntplane and Beagle
> - Animated engine components on Bandito, BF Injection and Hotknife will not animate if the engine is off
> -  Fixed a crash occuring when the vending machine was continuously used for an extended period of time
> -  FILE_FLAG_NO_BUFFERING flag has been removed from IMG reading functions - speeding up streaming
> -  Fixed a streaming related deadlock, which could occasionally result in game being stuck on black screen when entering or exiting interiors (this is the issue people used to fix by setting CPU affinity to one core)
> -  Metric-to-imperial conversion constants have been replaced with more accurate ones
> -  Fixed a glitch where random cars would end up being impounded to garage, replacing player’s vehicles
> - Very long loading times will now loop loading screens, as opposed to fading to white
> -  Sun reflections on peds and vehicles now change direction depending on time of day, like in III and VC (off by default)
> -  Dancing minigame timings have been improved, now they do not lose accuracy over time depending on PC’s uptime
> -  Car generators placed in interiors are now placed correctly - this ‘unhides’ two vehicles in Madd Dogg’s mansion, which were always there but they were not visible
> -  Bombs in cars stored in garages now save properly
> -  Fixed an issue which would cause games to freeze if III/VC/SA were running at the same time
> -  Streaming has been greatly improved during Supply Lines mission (or more general, any time when using an RC vehicle) - it now behaves as expected, as opposed to displaying LODs way too quickly
> -  Health triangle displaying when aiming at peds is now properly orientated (it’s now upside down) for peds player can recruit
> -  Setting a BMX on fire will not set CJ on fire anymore
> -  Keyboard input latency decreased by one frame
> - Rhino does not gain extra wheels after being fixed anymore
> - Firetruck (firela variant) now has a functional ladder - it can be raised by moving right analog stick down/pressing Num2
> - artict3 trailers now can be chained (as it was most likely intended, since the model has a hook dummy which was not functional until now)
> - Tug now has a functional tow bar (model has a hook dummy which was not functional until now)
> - DFT-30 left middle wheel now displays properly (game now accepts a typo present in its naming)
> - Pushing pedestrians against the wall with a vehicle will not trigger passenger’s voice lines anymore - instead, now they are triggered when player runs over pedestrians
> - Pay ‘n Spray will not clean the car BEFORE garage doors close anymore - now it cleans them while the car is hidden behind the garage door
> -  “True Invicibility” option has been added - with the option enabled, police helicopter will not hurt the player when they have an Invicibility cheat enabled (off by default)
> -  Made the game select metric/imperial units basing on system locale settings
> - Fixed a bug where paintjobs would vanish from cars stored in garage if they were stored without looking at them
> -  Coronas now properly rotate as camera is getting closer to them, like on PS2
> -  Light shadows from fire now show up properly
> -  Fixed parachute animations
> -  “Keep weapons after wasted” and “keep weapons after busted” now reset on New Game
> -  Fixed a glitch allowing bikes without engines to spawn
> -  Allowed extra6 part to be picked when a random extra is to be picked
> -  Fixed in-car camera mouse behaviour when looking left/right/behind
> -  Steam and RGL versions have proper aspect ratios now
> -  Steam/RGL version of the game will not reject 1.0/1.01 saves anymore (still, a compatible SCM is needed for the save to work)
> -  Censorships from Steam and RGL versions for German players have been removed
> -  Steam/RGL versions will now default Steer with Mouse option to disabled, like in 1.0/1.01

### 安装ASI Loader

安装Silent Patch之前，你需要ASI Loader，他是GTA脚本和mods的加载器，安装方法也非常简单。先从https://1drv.ms/u/s!AmZlhUlwACFugeJqDV40RgU5NAN9-g?e=dc3GRg  下载Ultimate ASI Loader（同样适用于Rockstar Games Launcher）

![image-20230118161839382](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118161839382.png)

直接解压到游戏根目录\Grand Theft Auto San Andreas即可：

![image-20230118154229841](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118154229841.png)

### 安装Silent Patch

接下来从https://cookieplmonster.github.io/mods/gta-sa/  下载Silent Patch：

![image-20230118154424304](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118154424304.png)

得到：

![image-20230118154510785](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118154510785.png)

将除了Readme.txt以外的文件复制粘贴到\Grand Theft Auto San Andreas\scripts内：

![image-20230118154732112](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118154732112.png)

进入游戏，如果你的鼠标问题解决了，就说明Silent Patch安装成功了。

提一嘴，Silent Patch同样解决了宽屏适配问题，16:9和16:10分辨率都能适配上了。但我还是建议专门装一个修复宽屏适配问题的插件，这一会在解释。

## ThirteenAG's Widescreen Fix

虽然Silent Patch修复了高分屏适配问题，但是效果比较一般般。比如游戏画面宽屏修复了，但是游戏UI却没有。ThirteenAG's Widescreen Fix可以修复这个问题，其文件在github仓库里：https://github.com/ThirteenAG/WidescreenFixesPack/releases/tag/gtasa

![image-20230118160241489](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118160241489.png)

下载后得到这样的文件：

![image-20230118160418017](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118160418017.png)

注意，需要你提前安装ASI Loader。

直接copy到游戏根目录\Grand Theft Auto San Andreas即可。

## 高清加载

游戏内加载时的图片都比较模糊，可以替换成高清的。在ThirteenAG's Widescreen Fix的Github仓库中还有个前端版本frontend，所以可以安装这个：

![image-20230118161223306](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118161223306.png)

得到的如下的文件：

![image-20230118161324116](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118161324116.png)

将他copy到\Grand Theft Auto San Andreas\models下替换原文件：

![image-20230118161405353](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118161405353.png)

这样图片就是高清版本了，很有feel。

## Chiri's resolution forcing tool

GTASA默认的刷新率是60HZ，无论你的屏幕刷新率多高都是60HZ。Chiri's resolution forcing tool可以修复（必须先装ThirteenAG's Widescreen Fix）：https://helixmod.blogspot.com/2013/02/chiris-force-certain-resolutionhertz.html

![image-20230118162243312](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118162243312.png)

得到如下文件：

![image-20230118162322752](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118162322752.png)

将d3d9.dll和d3dx.ini复制到\Grand Theft Auto San Andreas

![image-20230118162434430](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118162434430.png)

修改d3dx.ini中的refresh_rate即可：

![image-20230118162521809](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118162521809.png)

## 无边框窗口化（与Chiri's resolution forcing tool冲突）

在安装了ThirteenAG's Widescreen Fix的条件下，在游戏根目录\Grand Theft Auto San Andreas下新建一个wndmode.ini文件即可实现无边框窗口化，但由于是窗口化，那么这个时候游戏的刷新率跟你的屏幕一致了，于是就不需要Chiri's resolution forcing tool了。

![image-20230118163703333](https://cdn.jsdelivr.net/gh/InverseDa/image@master/image/image-20230118163703333.png)
