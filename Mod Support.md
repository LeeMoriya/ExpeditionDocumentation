Below you can find documentation that may be useful for modding the Expedition game-mode in Rain World: Downpour.

## Mod Setup
To start, you will need to set up a new mod directory and folders for the content you plan to add, here's a step-by-step process:

1. Create a new folder in `Rain World\RainWorld_Data\StreamingAssets\mods` this should be lowercase with no spaces, like the others in the folder.
2. Go to the `expedition` mod folder and copy the `modinfo.json` file, paste this into your new mod directory.
3. Open up the `modinfo.json` with notepad or another text editor and change each field for your new mod.
4. In the `requirements` and `requirements_names` fields enter `"expedition"` and `"Expedition"` respectively.

You've now set up a new mod that you can enable in the Remix menu that also requires Expedition to be enabled. You can set up new custom Missions and Quests by following the steps in the sections below.

## Custom Missions
To create custom missions you'll first need to create a `missions` folder in your mod directory. This is where Mission `.json` files will be stored and loaded from. When a custom mission has been detected by the game, a new button will appear on the Progression page labelled "Custom", you can click this to view any mods which add new content to Expedition.

You'll probably want to copy an existing Mission `.json` from `mod\expedition\missions` and modify it to start with. The actual names of the `.json` files in your missions folder don't matter, but their contents do. Here are the available fields you can modify in a Mission file and what each of them do:

### Key
The key is a unique identifier for this Mission and should not be used by any other mission, either in Downpour or added by another mod. The key is what is added to your save data to verify that you have completed a mission, and is also used when defining a Mission as a Quest requirement.

### Name
This is the name of the Mission itself and should be one or two words only in order to fit within the bounds of the Mission button. If the name is too long, the game will attempt to squish the label so it fits but this can look bad the longer the name is.

### Slugcat
The character that will be used for the Mission -- this uses the internal name for that Slugcat, which are:-

`White` `Yellow` `Red` `Gourmand` `Artificer` `Spear` `Rivulet` `Saint`

### Challenges
This is where the actual Challenge data for the Mission is pulled from. Most Challenge strings follow the same format but have different variables depending on what data needs to be tracked for that Challenge. You can find an explanation of each Challenge type's data strings in the [section below.](https://github.com/LeeMoriya/ExpeditionDocumentation/new/main#challenge-data)

### Requirements
The requirements field can be used to force a certain Burden or Perk to be used for the Mission. When the Mission is selected, these requirements will also be enabled and cannot be turned off, however additional Burdens and Perks can be used if desired. If the player doesn't have a requirement unlocked, the Mission will not be selectable.

You can find a list of the keys for each Perk and Burden in the [section below.](https://github.com/LeeMoriya/ExpeditionDocumentation/new/main#perks-and-burdens)

### Den
This is the internal name of the room that will be used as the starting location for the Mission. You can find desired starting shelters using something like the Warp mod.

## Challenge Data
In Expedition, save data for Challenges are stored as text strings that look like this: `"HuntChallenge~Vulture><3><0><0><0><0"`. The string is separated into `[Challenge Type]~[Save Data]`. The required variables that need to be tracked for the Challenge are stored in the `[Save Data]` section, separated by `><`.

Below is an explanation of each Challenge string, so you can define your own for Custom Missions.

### Hunting
`"HuntChallenge~Vulture><X><Y><0><0><0"`

- `HuntChallenge` is the challenge type
- `Vulture` is the internal name of the creature that is being hunted
- `X` is the number of this creature to be hunted
- `Y` is the number of this creature that has already been hunted

The last three numbers of each challenge define the following:-

- Whether or not the challenge is complete -- should always be `0`
- Whether or not the challenge is hidden -- set to `1` for yes
- Whether or not the hidden challenge has been revealed -- should always be `0`

These are the same for all challenges so I won't mention them again!

### Passage
`"AchievementChallenge~Saint><0><0><0"`

- `AchievementChallenge` is the challenge type
- `Saint` is the name of the passage used internally

### Cycle Score
`"CycleScoreChallenge~X><0><0><0"`

- `CycleScoreChallenge` is the challenge type
- `X` is the number of points that must be earned in a cycle

### Overall Score
`"GlobalScoreChallenge~X><0><0><0"`

- `GlobalScoreChallenge` is the challenge type
- `X` is the number of points that must be earned over the course of the Expedition

### Echo
`"EchoChallenge~CC><0><0><0"`

- `EchoChallenge` is the challenge type
- `CC` is the region acronym for Chimney Canopy, where the target Echo can be found

### ItemHoardChallenge
`"ItemHoardChallenge~X><Mushroom><0><0><0"`

- `ItemHoardChallenge` is the challenge type
- `X` is the number of this item required
- `Mushroom` is the internal name of the item that must be collected.

The `AbstractObjectType` is what is used to define the target item. By default only a handful of these are used by the Challenge in Expedition, however you can use any item for a Custom Mission, for example `OverseerCarcass` or `SlimeMold`. Keep in mind that if you use a non-default item, the internal name will be used in the challenge description shown in the HUD.

### Neuron Delivery
`"NeuronDeliveryChallenge~X><Y><0><0><0"`

- `NeuronDeliveryChallenge` is the challenge type
- `X` is the number of neurons that need to be delivered
- `Y` is the number of neurons that have already been delivered

### Pearl Delivery
`"PearlDeliveryChallenge~SL><0><0><0"`

- `PearlDeliveryChallenge` is the challenge type
- `SL` is the region the unique colored pearl should be taken from. Any pearl from that region will be valid for the Challenge.

### Pearl Hoarding
`"PearlHoardChallenge~X><Y><SI><0><0><0"`

- `PearlHoardChallenge` is the challenge type
- `X` is whether common grey pearls must be collected, or unique colored pearls -- `1` for common, `0` for unique
- `Y` is the number of pearls that need to be gathered
- `SI` is the internal acronym for the region that pearls need to be gathered in

### Spear Pinning
`"PinChallenge~X><Y><0><0><0"`

- `PinChallenge` is the challenge type
- `X` is the number of creatures to be pinned
- `Y` is the number of successful pins so far

### Vista Visiting
`"VistaChallenge~CC><CC_A10><X><Y><0><0><0"`

- `VistaChallenge` is the challenge type
- `CC` is the internal acronym for the region the Vista Point is found in
- `CC_A10` is the name of the room the Vista Point is found in
- `X` is the X coordinate for a point in the room
- `Y` is the Y coordinate for a point in the room

In the vanilla game, Vista locations are harcoded and picked at random, but for Custom Missions you can set their locations to be wherever you like, even in Custom Regions. With Dev Tools enabled you can see the name of the room you are in at the top of the screen, and you can press `M` to bring up a cursor that tells you the X and Y coordinate for wherever your mouse is, you can use the numbers shown here for the challenge and the Vista will then be found in that spot.

## Perks and Burdens
Below is a list of all the the internal strings used to define specific perks and burdens, you can list these as requirements in custom missions to force them to be enabled for that mission.

### Perks
- `unl-lantern` - Scavenger Lantern
- `unl-vulture` - Vulture Mask
- `unl-bomb` - Scavenger Bomb
- `unl-glow` - Neuron Glow
- `unl-backspear` - Hunter Backspear
- `unl-karma` - Karma Flower
- `unl-passage` - Enable Passages
- `unl-slow` - Slow Time
- `unl-sing` - Singularity Bomb
- `unl-electric` - Electric Spear
- `unl-dualwield` - Spearmaster Dual-wielding
- `unl-explosionimmunity` - Artificer Explosion Immunity
- `unl-explosivejump` - Artificer Explosive Jump
- `unl-crafting` - Gourmand Crafting
- `unl-agility` - Rivulet Agility
- `unl-gun` - Joke Rifle

### Burdens
- `bur-blinded` - BLINDED
- `bur-doomed` - DOOMED
- `bur-hunted` - HUNTED
- `bur-pursued` - PURSUED
