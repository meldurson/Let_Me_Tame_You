![Title](https://raw.githubusercontent.com/meldurson/Let_Me_Tame_You/main/Pics/Banner.png)

Complete overhaul of creature taming, extracted and expanded from **AllTameable**.

---

## ✨ Features

* 🐗 Tame **(almost)** any creature
* 🐉 Works with **bosses**
* 🍖 Fully customizable **food systems**
* 🐣 **Breeding & egg mechanics**
* ⚙️ Powerful **.yml configuration system**
* 🧩 Modular **group-based** settings
* 🎯 Control **taming requirements, factions, and behavior**
* 🤝 Designed for **mod compatibility**

---

## 📦 What is this mod?

**Let Me Tame You** is the **taming system extracted from AllTameable**, redesigned to be:

* More modular
* Easier to configure
* Cleaner to maintain
* Better for modpacks

This mod focuses purely on **taming mechanics**. If you want the full overhaul experience that **AllTameable** added, check out:

### 🐉 Creature Genetics: 
* Advanced breeding and genetic changes

### 🛠 TamingTools: 
* Adds taming meads and food to improve taming

---

![Deer](https://raw.githubusercontent.com/meldurson/Let_Me_Tame_You/main/Pics/DeerHover_5to1Zoom.png)
## ⚙️ Configuration

This mod is almost entirely controlled through the **YAML config files**.

You can customize:

* Taming time
* Food preferences
* Breeding behavior
* Egg laying creatures
* Boss requirements
* Factions and hostility
* Creature AI changes

 ## ❗📃 Explanation  and overview of how to format the **TameList** can be found on the **[wiki](https://github.com/meldurson/Let_Me_Tame_You/blob/main/Tamelist_YML_Wiki.md)** ❗

---
### Example

```yaml
Wolf:
  groups: Tier4,RawCarnivore,SizeMedium
  offspringName: Wolf_Pup
  commandable: true
```
---
## 🔒 Progression Control
![Progression](https://raw.githubusercontent.com/meldurson/Let_Me_Tame_You/main/Pics/DragonTower5to1.png)
Gate taming behind boss progression:

```yaml
requiredWorldKeys: defeated_eikthyr:defeated_dragon
```

Creatures will appear **"Feral"** until requirements are met.

---

## ⚔️ Factions & Behavior

Control how creatures interact:

```yaml
hostileToSelf: true
specialGroup: AllGoblin
```

* `hostileToSelf` → tamed vs wild will fight
* `specialGroup` → prevents friendly fire within a group of like creatures

**Note:** ```hostileToSelf``` will override ```specialGroup```

---

## 🔄 Multiple Creatures

You can assign settings to multiple prefabs at once:

```yaml
Charred_Twitcher,Charred_Twitcher_Summoned:
  groups: Ashlands
```

---
## 🛠 Installation

1. Install **BepInEx**
2. Install this mod (or add the .dll to the Bepinex/plugins folder)
3. Launch the game once to generate config

Config file will be created at:

```
...BepInEx/config/LetMeTameYou_DefaultTameList.yml
```
You can then edit this file to your hearts content!

---
![Egg](https://raw.githubusercontent.com/meldurson/Let_Me_Tame_You/main/Pics/SeekerSoldierEgg_5to1.png)
## ⚠️ Compatibility

✔ Works with most mods
✔ Designed for modpacks
✔ Works alongside other tame creature mods

❌ Not compatible with:

* Other mods that modify **taming systems directly**
* Other “all creatures tameable” mods
* Some mods have custom AI that may not allow for adding taming/procreation to.

---


## 🚧 Planned Features

* Expanded **trading-based taming**
* Better modded creature support

---



## ❓Contact:
The most reliable way to reach out would be to ping me in the [Valheim Modding Discord](https://discord.com/invite/GUEBuCuAMz) under @Meldurson. or dm me on Discord.

If you want to support me you can do so through my Ko-fi account:

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/B0B3NARM0)


