

# Tameable Creatures .YML Guide

This mod allows you to **tame nearly any creature in Valheim** by configuring a simple `.yml` file.

You can control:

* Taming time
* Food preferences
* Breeding
* Eggs
* Creature factions
* Boss taming requirements
* Custom offspring
* etc.


The configuration system is designed to be **powerful but easy to maintain** using reusable **groups**.


# Configuration File

The mod uses a **YAML configuration file**.

You can have multiple files in your config folder and it will read all of them. Their names just need to be in the format of ```LetMeTameYou_*.yml``` such as:
```
LetMeTameYou_Vanilla.yml
LetMeTameYou_Monstrum.yml
LetMeTameYou_Bestiary.yml
LetMeTameYou_RtD.yml
```
By default, if no other TameList .yml files are found, a currated default will be created for you that has all of the vanilla creatures:

```
...BepInEx/config/LetMeTameYou_DefaultTameList.yml
```


# Basic Structure

Each creature uses its **prefab name** followed by a colon `:`.

Attributes must then be **indented under the creature name**.

Example:

```yaml
Wolf:
  tamingTime: 1800
  fedDuration: 600
  commandable: true
```

⚠ YAML is indentation-sensitive.
Use **two spaces** before attributes.


# Taming Options

### tamingTime

Time required to tame the creature in seconds.

**Default:** 1800 (30 minutes)

```yaml
  tamingTime: 1800
```



### fedDuration

How long the creature remains full after eating.

**Default:** 600 seconds

```yaml
  fedDuration: 600
```



### commandable

Allows the creature to be commanded to **follow or stay**.

**Vanilla defaults**

| Creature | Value |
| -------- | ----- |
| Wolf     | true  |
| Boar     | false |
| Lox      | false |
| Hen      | false |
| Asksvin      | false |

```yaml
  commandable: true
```



## requiredWorldKeys

Requires specific **world events** before taming becomes possible.

Most commonly used for **boss defeat requirements**.

Multiple keys are separated with commas `,`

Example:

```yaml
  requiredWorldKeys: defeated_dragon,defeated_eikthyr
```

If the requirement is not met, the creature will appear **Feral** instead of **Wild**.



## consumeItems

Defines which items the creature can eat.

Separate items with commas `,`

```yaml
  consumeItems: SerpentMeat,RawMeat,NeckTail,FishRaw
```

__Note:__ Items do **NOT** need to be food.



## consumeSearchRange

Distance the creature will detect food and walk towards it if hungry.

**Default:** 15

```yaml
  consumeSearchRange: 15
```



## consumeSearchInterval

How often the creature checks for nearby food.

**Default:** 10 seconds

```yaml
  consumeSearchInterval: 10
```



## consumeRange

Distance the creature must be within to eat food. Larger creatures may need larger consume range.

```yaml
  consumeRange: 1.5
```



# Breeding Options

## procreation

Allows the creature to breed.
Options are **true** or **false**

**Default:** true
```yaml
  procreation: true
```



## pregnancyChance

Chance to gain a love point when breeding is possible.

Lower value = **higher chance**

**Default:** `0.66`

This is a 33% chance every breeding cycle to gain a love point.

```yaml
  pregnancyChance: 0.66
```



## pregnancyDuration

Time a creature remains pregnant in seconds.

Vanilla values:

| Creature | Duration |
| -------- | -------- |
| Boar     | 60       |
| Wolf     | 60       |
| Hen      | 60       |
| Lox      | 120      |
| Asksvin  | 90 |

```yaml
  pregnancyDuration: 120
```



## maxCreatures

Maximum creatures nearby before breeding stops.

Example:

| Creature | Max |
| -------- | --- |
| Boar     | 5   |
| Wolf     | 4   |
| Lox      | 4   |
| Asksvin  | 10 |
| Hen      | 10  |

```yaml
  maxCreatures: 5
```


## growTime

Time for offspring to grow into adults.

```yaml
  growTime: 3000
```

Example vanilla values:

| Creature | Grow Time |
| -------- | --------- |
| Boar     | 3000      |
| Wolf     | 3000      |
| Lox      | 6000      |
| Asksvin  | 3000 |
| Hen      | 3000  |


## offspringName

Custom name for baby creatures.

Use `_` for spaces.

```yaml
  offspringName: Ulv_Pup
```


# Egg System

Some creatures can **lay eggs instead of giving birth**.

Format:

```yaml
  egg: type(hatchTime:color:size)
```

Example:

```yaml
  egg: drake(1200:#00FF00:0.3)
```

__Meaning:__ The egg will be a copy of the Dragon Egg that is 30% the size and green that will take 1200 seconds (20 minutes) to hatch

| Description  | Options     | 
| --------- | --------------- |
| Egg type     | drake, chicken, asksvin       |
| Hatch time      | Any number of seconds*    | 
| Color    | A colour in hex code format*\*           |
| Size multiplier      | Any number between 0.1 and 10 |

\* Default hatch time for Hen and Asksvin is 1800 seconds (30 minutes)

*\*For hex codes, you can use [this website](https://htmlcolorcodes.com/) 


# Trading Taming (Experimental)

Allows creatures to be tamed by **trading items instead of feeding**.

Format:

```yaml
  trade: Item=Amount:Item=Amount
```

Example:

```yaml
  trade: TrophyKvastur=10:YggdrasilWood=100
```


# AI Changes

## hostileToSelf

If enabled, the creature will **fight its wild counterparts**.

Example:

```yaml
  hostileToSelf: true
```


## specialGroup

Creatures in the same `specialGroup` **will not attack each other**, even if one is tamed.

Example:

```yaml
  specialGroup: AllGoblin
```
If all fulings have this special group then tamed standard fuling will not attack a wild berserker for example.



## followDistMulti

Adjusts the follow distance multiplier.

```yaml
  followDistMulti: 2
```



# Groups System (Recommended)

Groups allow you to **reuse shared settings** across many creatures.

Group names must start with:

```
group_
```

The **group_Default** is a special group as it is automatically applied without referencing it.

Example groups:

```yaml
group_Default:
  tamingTime: 1800
  fedDuration: 300
  commandable: true
  consumeSearchInterval: 10
  pregnancyChance: 0.5

group_Tier1:
  tamingTime: 1500
  pregnancyDuration: 90
  growTime: 2100
  maxCreatures: 7

group_Vegetarian:
  consumeItems: Raspberry,Blueberries,Carrot,Turnip,Mushroom,Cloudberry,OnionSoup,Onion

group_SizeMedium:
  consumeRange: 1.4
  consumeSearchRange: 15
  size: 1.5
```


## Using Groups

Assign groups to creatures with the `groups` attribute.

```yaml
Deer:
  groups: Tier1,Vegetarian,SizeMedium
```

Groups load **left → right**.

Later groups __override__ earlier groups.

In this example:
**group_Default** adds: 
`tamingTime: 1800`
`fedDuration: 300`
  `commandable: true`
  `consumeSearchInterval: 10` and
  `pregnancyChance: 0.5`

Then **group_Tier1** adds:
  `pregnancyDuration: 90`
  `growTime: 2100` 
  `maxCreatures: 7` and overrides taming time from __group_Default__ with
  `tamingTime: 1500`

Then **group_Vegetarian** adds:
  `consumeItems: Raspberry,Blueberries,Carrot,Turnip,Mushroom,Cloudberry,OnionSoup,Onion`

and finally **group_SizeMedium** adds:
  `consumeRange: 1.4`
  `consumeSearchRange: 15` and
  `size: 1.5`

### This would be equivalent to the following:
```yaml
Deer:
  tamingTime: 1500
  fedDuration: 300
  commandable: true
  consumeSearchInterval: 10
  pregnancyChance: 0.5
  pregnancyDuration: 90
  growTime: 2100
  maxCreatures: 7
  consumeItems: Raspberry,Blueberries,Carrot,Turnip,Mushroom,Cloudberry,OnionSoup,Onion
  consumeRange: 1.4
  consumeSearchRange: 15
  size: 1.5
```
## Overriding Group Values

Creature attributes override group settings.

Example:

```yaml
Serpent:
  groups: Tier3,RawCarnivore,SizeLarge
  tamingTime: 1800
```

Here `tamingTime` overrides the group value.


# Multiple Creatures in One Entry

You can configure multiple prefabs together by separating them with a comma `,`.

Example:

```yaml
Charred_Twitcher,Charred_Twitcher_Summoned:
  groups: Ashlands
```
# Remove Taming

## removeTameable

Removes taming from creatures. This can be used to remove taming from already tameable creatures or to disable the creature in the config without deleting the creature entry from the config.

```yaml
  removeTameable: true
```



# Example Creature Configuration

```yaml
Wolf:
  groups: Tier4,RawCarnivore,SizeMedium
  offspringName: Wolf_Pup
  commandable: true
```

This configuration means:

* Uses Tier 4 difficulty
* Eats raw meat
* Medium creature size
* Custom offspring name
* Can be commanded to follow


# Tips

✔ Use groups whenever possible
✔ Creature attributes override groups
✔ YAML formatting requires **correct indentation**
✔ Misspelled prefab names will break the configuration
