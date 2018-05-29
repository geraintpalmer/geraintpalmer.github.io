---
layout     : post
title      : "Choosing the perfect Pokémon team with Python and PuLP"
language   : english
comments   : true
---

I'm currently right in the endgame of writing up my PhD thesis, much stress, so
I of course have started playing Pokémon again.
A worrying amount of my thoughts have gone towards working out what is the best
Pokémon team of six, so I'll use some mathematics to put my mind at ease.
(Yes, I know I have more important things to do...)
In particular I'm looking for:

+ the strongest team
+ that has resistances to as many types as possible.

In this post I'll use some methematics, Python's
[`requests`](http://docs.python-requests.org/en/master/) library to gain Pokémon
data, and [`pulp`](https://pythonhosted.org/PuLP/) to solve a linear program
which will give me my perfect team.

In the Pokémon games a player adventures around catching various species of
Pokémon which they can then use in battles.
Each player may only carry six Pokémon with them at a time, and so finding a
stong all-round team of six is vital.
Pokémon have six 'stats' which determine their stengths: Attack, Special Attack,
Defence, Special Defence, Speed and HP.
Here I'll use the Pokémon's total base 'stats' to measure their overall
strength.

Another important concept in the games is Pokémon 'types'.
There are 18 types: Normal, Fire, Water, Electric, Grass, Ice, Fighting, Poison,
Ground, Flying, Psychic, Bug, Rock, Ghost, Dragon, Dark, Steel and Fairy.
A Pokémon's type determines its weaknesses or resistances to different attck
types according to the following table:

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

So looking at the first row, a Normal type Pokémon takes 1x damage from a Normal
type move, but take 2x damage from a Fighting type move, and 0x damage (total
immunity) from a Ghost type move.

Adding further complexity, some Pokémon are dual type, in which case effects are
multiplicative: for example a Water-Ground type Pokémon would be damaged
$$2 \times 0 = 0$$x by an Electric attack, and $$0.5 \times 2 = 1$$x by a Water
attack, and so on.

I want the strongest (largest total base stats) team, where at least one Pokémon
is resistant (damaged less than 1x) to each type.

First, let's use Python's `requests` library, and the
[Pokéapi API](https://pokeapi.co/) to get data on all Generation 1 Pokémon.
(The dictionary `type_weaknesses` is a dictionary containing the rows of the
table above as lists).
Here, if a Pokémon has two types, I use `numpy` to apply elementwise
multiplication to their weaknesses:

{% highlight python %}
>>> import requests
>>> import numpy as np

>>> names = []
>>> totalstats = []
>>> weaknesses = []

>>> for pkmn in range(1, 152):
...     r = requests.get('https://pokeapi.co/api/v2/Pokémon/' + str(pkmn) + '/')
...     name = r.json()['name']
...     total_stats = sum([r.json()['stats'][i]['base_stat'] for i in range(5)])
...     type1 = r.json()['types'][0]['type']['name']
...     weakness = type_weaknesses[type1]
...     try:
...         type2 = r.json()['types'][1]['type']['name']
...         weakness = list(np.array(type_weaknesses[type1]) * np.array(type_weaknesses[type2]))
...     except:
...         KeyError
...     names.append(name)
...     totalstats.append(total_stats)
...     weaknesses.append(weakness)
{% endhighlight %}

In addition I'll restrict my team to one starter and zero legendary or
pseudo-legendary Pokémon.
Their numbers (Python indexing from 0) are:

{% highlight python %}
>>> starters = [0, 1, 2, 3, 4, 5, 6, 7, 8]  # Bulbasaur to Blastoise
>>> legendaries = [143, 144, 145, 149, 150]  # Legendary birds, Mewtwo and Mew
>>> pseudolegendaries = [146, 147, 148]  # Dratini, Dragonair, Dragonite
{% endhighlight %}

Now we have all the data, let's formulate a linear program that will maximise a
team's total stats whilst ensuring all type attacks are covered by at least one
resistant Pokémon.

+ Let $$X$$ be a decision array of 151 binary variables, representing the decision
to include that Pokémon in my team.
+ Let $$T$$ be an array of 151 constants representing each Pokémon's total base
stats.
+ Let $$S$$, $$L$$ and $$P$$ be the sets of starter, legendary and
pseudo-legendary Pokémon respectively.
+ Let $$R$$ be a 151 by 18 matrix of constants, where $$R_{ij} = 1$$ if Pokémon
$$i$$ is resistant (taking 0.5x or less damange) to attacks from type $$j$$.
$$R$$ is constructed by:

{% highlight python %}
>>> resistances = [[1 if r <= 0.5 else 0 for r in weaknesses[i]] for i in range(151)]
{% endhighlight %}

Now the linear program becomes:

$$\text{maximise:} \quad T_i X_i$$

subject to:

$$\sum X_i = 6$$

$$\sum_{i \in S} X_i \leq 1$$

$$\sum_{i \in L \cup P} X_i = 0$$

$$\sum R_{ij} X_i \geq 1 \quad \forall \quad j$$

This can be solved using `pulp`.
Define the problem and the variables:

{% highlight python %}
>>> import pulp
>>> prob = pulp.LpProblem("PerfectPokemonTeam", pulp.LpMaximize)
>>> x = pulp.LpVariable.dicts("x", range(151), cat=pulp.LpBinary)
{% endhighlight %}

Add the objective function:

{% highlight python %}
>>> objective_function = sum(totalstats[pkmn] * x[pkmn] for pkmn in range(151))
>>> prob += objective_function
{% endhighlight %}

Add the constraints and solve:

{% highlight python %}
>>> prob += sum([x[pkmn] for pkmn in range(151)]) == 6
>>> prob += sum([x[pkmn] for pkmn in starters]) <= 1
>>> prob += sum([x[pkmn] for pkmn in legendaries + pseudolegendaries]) == 0
>>> for tp in range(18):
...     prob += sum([resistances[pkmn][tp] * x[pkmn] for pkmn in range(151)]) >= 1
>>> prob.solve()
1
{% endhighlight %}

Once solved, the solution $$X$$ can be read:

{% highlight python %}
>>> for i in range(151):
...     if x[i].value() == 1:
...         print(names[i])
charizard
arcanine
poliwrath
magneton
cloyster
tauros
{% endhighlight %}

This yields the perfect Pokémon team (Generation 1) as Charizard, Arcanine,
Poliwrath, Magneton, Cloyster and Tauros!

| Pokémon   | Type           | Resistances                                                | Total Stats |
|-----------|----------------|------------------------------------------------------------|-------------|
| Charizard | Fire/Flying    | Fir, Gra, Fig, Gro, Bug, Ste, Fai                          | 456         |
| Arcanine  | Fire           | Fir, Gra, Ice, Bug, Ste, Fai                               | 465         |
| Poliwrath | Water/Fighting | Fir, Wat, Ice, Bug, Roc, Dar, Ste                          | 420         |
| Magneton  | Electric/Steel | Nor, Ele, Gra, Ice, Poi, Fly, Psy, Bug, Roc, Dra, Ste, Fai | 415         |
| Cloyster  | Water/Ice      | Wat, Ice                                                   | 475         |
| Tauros    | Normal         | Gho                                                        | 415         |
|-----------|----------------|------------------------------------------------------------|-------------|

<br>

Interestingly this team only covers eight types: Fire, Flying, Water, Fighting,
Electric, Steel, Ice and Normal.
Tauros' presence is curious, as a purely Normal type with resistance to only
Ghost type Pokémon; and Arcanine's presence is surprising, given Fire types are
already covered with Charizard.
In fact Arcanine is not needed for type coverage at all: Arcanine has resistance
to Ice, the only resistance it has that Charizard does not, however Ice
resistance is covered by Poliwrath, Cloyster and Magneton.
The same is true for Cloyster.
This indicates maybe only four Pokémon are needed for type coverage, and there's
slack to choose two more based on pure strength.

This method would easily generalise to inculde more generations, however
retreiving the data would take longer.

The mathematics used here is a standard operational research technique, and is
used in many other more serious applications such as nurse rostering, exam
timetabling, and surgery scheduling.
This linear program has 151 variables and 21 constraints.
In more serious applications these may have thousands of variables and thousands
of constraints, and so solvers such as PuLP become invaluable.