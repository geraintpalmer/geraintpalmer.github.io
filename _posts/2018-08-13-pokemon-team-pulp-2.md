---
layout     : post
title      : "Choosing the perfect Pokémon team with Python and PuLP - Part 2"
language   : english
comments   : true
---

In a [previous blog post](/2018/05/29/pokemon-team-pulp/) I attempted to use
PuLP to choose a strong Pokémon team with full type-resistance coverage.
Here, in a joint post with experienced Pokémon trainer
[Alastair Harris](https://twitter.com/AlHarris91), we'll try to improve that
result by optimising on type coverage only, allowing Alastair to advise on
specific Pokémon choices.

To recap, here's the weaknesses matrix of the 18 types:

  |         | Nor | Fir | Wat | Ele | Gra | Ice | Fig | Poi | Gro | Fly | Psy | Bug | Roc | Gho | Dra | Dar | Ste | Fai |
  |---------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
  | **Nor** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: grey">0</span>   | 1   | 1   | 1   | 1   |
  | **Fir** | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> |
  | **Wat** | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   |
  | **Ele** | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   |
  | **Gra** | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   |
  | **Ice** | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   |
  | **Fig** | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   |
  | **Poi** | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> |
  | **Gro** | 1   | 1   | <span style="color: red">2</span>   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   |
  | **Fly** | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | <span style="color: grey">0</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   |
  | **Psy** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   |
  | **Bug** | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   |
  | **Roc** | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   |
  | **Gho** | <span style="color: grey">0</span>   | 1   | 1   | 1   | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   |
  | **Dra** | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: red">2</span>   |
  | **Dar** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   |
  | **Ste** | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> |
  | **Fai** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   |
  |---------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|

<br>

+ The 7th column of the 1st row shows that Normal type Pokémon are weak to
Fighting type attacks, taking 2x damage.
+ Effects of dual type Pokémon are multiplicative, so Water-Electric types only
take 0.25x damage from Steel attacks.

Which six typings should we choose for our team so that they have full immunity
and resistance coverage?

Why is this a difficult task?
There are 18 types, and so there is a possible $$^{18}C_2 = 153$$ dual typings.
Of these 37 are unused on regular Pokémon (some totally unused, some
belonging to legendaries or mega-evolutions only and so are excluded from this
analysis), thus $$153 + 18 - 37 = 134$$ typings to choose from.
Therefore there are $$^{134}C_6 = 7177979809$$ unique teams of 6 typings to
choose from: over 7 billion choices!

Therefore, we'll use [`pulp`](https://pythonhosted.org/PuLP/) to choose the
*types* of our team's six Pokémon.
The only contraints here will be:

 + For each type which it is possible to be immune to there should be one
 Pokémon on the team that is immune, and another Pokémon on the team that
 resists that type,
 + For all other types, there should be two Pokémon on the team that resists
 that type.

Now formulate the linear program:

+ Let $$X$$ be a decision array of 134 binary variables, representing the
decision to include that typing in my team.
+ Let $$T$$ be an array of 134 constants representing some objective for each
typing.
+ Let $$R$$ be a 134 by 18 matrix of constants, where $$R_{ij} = 1$$ if typing
$$i$$ is resistant (taking 0.5x or 0.25x damage) to attacks from type $$j$$.
+ Let $$I$$ be a 134 by 18 matrix of constants, where $$I_{ij} = 1$$ if typing
$$i$$ is immune (taking 0x damage) to attacks from type $$j$$.
+ Let $$P$$ be the set of types it is possible to be immune to (Normal, Electic,
 Fighting, Poison, Ground, Psychic, Ghost, Dragon).

$$\text{maximise / minimise:} \quad T_i X_i$$

subject to:

$$\sum X_i = 6$$

$$\sum I_{ij} X_i \geq 1 \qquad \forall j \text{ if } j \in P$$

$$\sum R_{ij} X_i \geq 1 \qquad \forall j \text{ if } j \in P$$

$$\sum R_{ij} X_i \geq 2 \qquad \forall j \text{ if } j \notin P$$

We'll investigate five objective functions:

 1. minimising super-weaknesses ($$T_i$$ is the number attack types that type
 $$i$$ takes 4x damage against),
 2. minimising weaknesses ($$T_i$$ is the number attack types that type $$i$$
 takes 4x or 2x damage against),
 3. maximising resistances ($$T_i$$ is the number attack types that type $$i$$
 takes 0.5x or 0.25x damage against),
 4. maximising super-resistances ($$T_i$$ is the number attack types that type
 $$i$$ takes 0.25x damage against),
 5. minimising total damage ($$T_i$$ is the sum of the damage multiplyers across
 all attack types that type $$i$$ takes).

All code is [available here](https://github.com/geraintpalmer/pokemon-pulp/blob/master/pkmntypes.ipynb).

## 1. Minimising super-weaknesses

  | Type           | Suggested Pokémon |
  |----------------|-------------------|
  | Normal-Grass   | Sawsbuck          |
  | Fire-Ghost     | Chandelure        |
  | Water-Fairy    | Primarina         |
  | Ground-Dark    | Krookodile        |
  | Flying-Steel   | Skarmory          |
  | Psychic-Steel  | Metagross         |
  |----------------|-------------------|

<br>

This is an extremely well balanced team that's able to overcome most threats in
UU/NU/OU tiers competitively.
However there's not much chance to set up a healer or wall, so this team will
have to rely on special attacks and pure power. 


## 2. Minimising weaknesses

  | Type           | Suggested Pokémon |
  |----------------|-------------------|
  | Normal         | Stoutland         |
  | Fire-Ground    | Camerupt          |
  | Water-Flying   | Swanna            |
  | Grass-Ghost    | Trevenant         |
  | Dark-Steel     | Bisharp           |
  | Steel-Fairy    | Mawile            |
  |----------------|-------------------|

<br>

It's a well balanced team that'll have a wide move pool from levelling up, TMs
and move tutoring.
Having said this there's only one Pokemon, Swanna, to use for healing, and can
only heal itself.
It's also quite poor defensively.


## 3. Maximising resistances

  | Type           | Suggested Pokémon |
  |----------------|-------------------|
  | Normal-Fire    | Pyroar            |
  | Water-Ghost    | Jellicent         |
  | Grass-Fairy    | Shiinotic         |
  | Ground-Steel   | Steelix           |
  | Flying-Steel   | Skarmory          |
  | Dark-Steel     | Bisharp           |
  |----------------|-------------------|

<br>

Shiinotic is a great wall and can take most people by surprise, dragon Pokémon
will hate this with it bulk and access to toxic and spore.
Jellicent with cursed body will cause major problems for heavy hitters and the
rest will rely on brute force; however it is far more balanced compared to the
other teams generated here. 


## 4. Maximising super-resistances

  | Type           | Suggested Pokémon      |
  |----------------|------------------------|
  | Normal-Ground  | Diggersby              |
  | Fire-Ghost     | Marowak (Alola form)   |
  | Water-Steel    | Empoleon               |
  | Grass-Dragon   | Exeggutor (Alola form) |
  | Flying-Fairy   | Togekiss               |
  | Rock-Dark      | Tyranitar              |
  |----------------|------------------------|

<br>

With Togekiss and Tyranitar being the main bulk this team may struggle and
probably has some of the worst abilities competitively.
It could possibly overcome most threats, but would struggle in OU compared to
UU/NU tiers.


## 5. Minimising total damage

  | Type           | Suggested Pokémon |
  |----------------|-------------------|
  | Normal-Dragon  | Drampa            |
  | Water-Dark     | Crawdaunt         |
  | Ground-Bug     | Wormadam          |
  | Flying-Steel   | Skarmory          |
  | Ghost-Steel    | Aegislash         |
  | Steel-Fairy    | Klefki            |
  |----------------|-------------------|

<br>

This is the most interesting team as none compliment one another.
Skarmory is good for setting up spikes and toxic to throw opponents off,
Aegislash's form change can again throw many players off but, is also
predictable in the way it attacks and defends, which makes it an easy kill in
its attack form.
Klefki is an asset but only in trick room play which it can set up nicely once
Skarmory has set up spikes.
With these the team may survive and turn the tables effectively across all tiers
of gameplay.


## Conclusion

In a [previous blog post](/2018/05/29/pokemon-team-pulp/) the aim of the linear
program was to find the specific Pokémon satisfied some type coverage and
maximised total stats.
This fell short of ensuring immunities to types it is possible to be immune to.
It also assumed that a Pokémon's total base stats was the singular indicator of
a Pokémon's strengths or usefulness.
It does not consider the stats' spread (high attack vs. high defence vs. average
everything), abilities, move pool, or the trainer's experience with using that
Pokémon.

This post focussed on type coverage only, though it should be noted that some
even here some moves (e.g. Odor Sleuth, Smack Down), items (e.g Ring Target, Air
Balloon) and abilities (e.g. Levitate, Motor Drive) may enhance or corrupt the
type coverage given.

Alastair's favourite team here: team 3.
It has access to a wider move pool and allows more interesting play.
This shows that Pokémon trainers actually value characteristics that are quite
difficult to capture using this linear programming approach, though it does
generate new ideas for gameplay.
