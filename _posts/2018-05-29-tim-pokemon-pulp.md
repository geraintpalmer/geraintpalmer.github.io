---
layout     : post
title      : "Dewis y tîm Pokémon perffaith gyda Python a PuLP"
language   : cymraeg
comments   : true
---

Rydw i reit yng nghanol ysgrifennu lan y traethawd PhD, lot o bwysau gwaith,
felly wrth gwrs rydw i wedi dechrau chwarae Pokémon eto.
Mae canran pryderus o’m hamser wedi’i threulio’n trio gweithio mas beth yw’r tîm
o chwe Pokémon gorau sydd, ac felly fe ddefnyddiaf fathemateg i setlo’n meddwl.
(Ie, rwy’n gwybod bod pethau mwy pwysig gyda fi i’w wneud...)
Yn arbennig rwy’n edrych am:

+ y tîm cryfaf
+ sy'n gwrthsefyll cymaint o 'fathau' ac sy'n bosib.

Yn y blog yma defnyddiaf fathemateg, llyfrgell
[`requests`](http://docs.python-requests.org/en/master/) Python i casglu data'r
Pokémon, a [`pulp`](https://pythonhosted.org/PuLP/) i ddatrys rhaglen llinol a
fydd yn rhoi'r tîm perffaith.

Yn y gemau Pokémon mae chwaraewr yn anturiaethu o gwmpas yn dal rhywogaethau
gwahanol o Pokémon ac yna yn eu defnyddio mewn brwydrau.
Fe all pob chwaraewr ond cario chwe Pokémon ar y tro, ac felly mae canfod tîm
cryf amryddawn o chwech yn hanfodol.
Mae gan Pokémon chwe 'stats' sy'n penderfynu eu cryfderau: Ymosod, Ymosod
Arbennig, Amddiffyn, Amddiffyn Arbennig, Cyflymder, ac HP.
Fan hyn byddaf yn defnyddio cyfanswm 'stats' sylfaen y Pokémon i fesur eu
cryfder cyffredinol.

Cysyniad pwysig arall yn y gemau yw 'mathau' Pokémon.
Mae yna 18 fath: Normal, Tân, Dŵr, Trydan, Glaswellt, Iâ, Ymladd, Gwenwyn,
Daear, Hedfan, Seicig, Byg, Craig, Ysbryd, Draig, Tywyll, Dur a Thylwyth.
Mae math Pokémon yn penderfynu ei gwendidau neu wrthiannau yn erbyn
ymosodiadau o fathau gwahanol yn ôl y tabl yma:

  |         | Nor | Tân | Dŵr | Try | Gla | Iâ  | Yml | Gwe | Dae | Hed | Sei | Byg | Cra | Ysb | Dra | Tyw | Dur | Tyl |
  |---------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
  | **Nor** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: grey">0</span>   | 1   | 1   | 1   | 1   |
  | **Tân** | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> |
  | **Dŵr** | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   |
  | **Try** | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   |
  | **Gla** | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   |
  | **Iâ** | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   |
  | **Yml** | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   |
  | **Gwe** | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> |
  | **Dae** | 1   | 1   | <span style="color: red">2</span>   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   |
  | **Hed** | 1   | 1   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | <span style="color: grey">0</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   |
  | **Sei** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   |
  | **Byg** | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   |
  | **Cra** | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   |
  | **Ysb** | <span style="color: grey">0</span>   | 1   | 1   | 1   | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: green">0.5</span> | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   | 1   | <span style="color: red">2</span>   | 1   | 1   |
  | **Dra** | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | <span style="color: red">2</span>   |
  | **Tyw** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: red">2</span>   |
  | **Dur** | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | <span style="color: grey">0</span>   | <span style="color: red">2</span>   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | 1   | <span style="color: green">0.5</span> | <span style="color: green">0.5</span> |
  | **Tyl** | 1   | 1   | 1   | 1   | 1   | 1   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   | 1   | 1   | <span style="color: green">0.5</span> | 1   | 1   | <span style="color: grey">0</span>   | <span style="color: green">0.5</span> | <span style="color: red">2</span>   | 1   |
  |---------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|

<br>

Felly wrth edrych ar y rhes gyntaf, mae Pokémon math Normal yn cymryd niwed 1x o
ymosodiad Normal, ond yn cymryd niwed 2x o ymosodiad Ymladd, a niwed 0x
(imiwnedd llwyr) o ymosodiad Ysbryd.

I ychwanegu mwy o gymhlethdod, mae gan rai Pokémon dwy 'fath'.
Yn yr achosion yma mae'r effaith yn lluosol: er enghraifft bydd Pokémon math
Dŵr-Daear yn cymryd niwed $$2 \times 0 = 0$$x o ymosodiad Trydan, a niwed
$$0.5 \times 2 = 1$$x o ymosodiad Dŵr, ac yn y blaen.

Rydw i eisiau'r tîm cryfaf (y cyfanswm 'stats' sylfaen mwyaf), lle mae o leiaf
un Pokémon yn gwrthsefyll (yn cymryd llai na 1x y niwed) pob math o ymosodiad.

Yn gyntaf defnyddiwn y llyfrgell `requests` Python, a'r
[Pokéapi API](https://pokeapi.co/) i gasglu data ar holl Pokémon Cenhedlaeth 1.
(Mae'r geiriadur `gwendidau_math` yn eiriadur sy'n cynnwys rhesi'r tabl uchod
fel rhestrau).
Os oes gan Pokémon dwy 'fath' yna defnyddiaf `numpy` i luosi’r ddwy restr o
gwendidau yn ôl yr elfennau:

{% highlight python %}
>>> import requests
>>> import numpy as np

>>> enwau = []
>>> cyfanswnstats = []
>>> gwendidau = []

>>> for pkmn in range(1, 152):
...     r = requests.get('https://pokeapi.co/api/v2/Pokémon/' + str(pkmn) + '/')
...     enw = r.json()['name']
...     cyfanswm_stats = sum([r.json()['stats'][i]['base_stat'] for i in range(5)])
...     type1 = r.json()['types'][0]['type']['name']
...     gwendid = gwendidau_math[type1]
...     try:
...         type2 = r.json()['types'][1]['type']['name']
...         gwendid = list(np.array(gwendidau_math[type1]) * np.array(gwendidau_math[type2]))
...     except:
...         KeyError
...     enwau.append(enw)
...     cyfanswnstats.append(cyfanswm_stats)
...     gwendidau.append(gwendid)
{% endhighlight %}

Hefyd fe wnâi cyfyngu'r tîm i un Pokémon dechreuol, a dim Pokémon chwedlonol neu
ffug-chwedlonol.
Eu rhifau (gyda Python yn indecsio o 0) yw:

{% highlight python %}
>>> dechreuwyr = [0, 1, 2, 3, 4, 5, 6, 7, 8]  # Bulbasaur i Blastoise
>>> chwedlonwyr = [143, 144, 145, 149, 150]  # Adar chwedlonol, Mewtwo a Mew
>>> ffugchwedlonwyr = [146, 147, 148]  # Dratini, Dragonair, Dragonite
{% endhighlight %}

Nawr bod gennym ni'r data i gyd, lluniwn y rhaglen linol a fydd yn macsimeiddio
cyfanswm 'stats' sylfaen y tîm, wrth sicrhau rhyw wrthiant i bob 'math' o
ymosodiad.

+ Gadawer i $$X$$ bod yn fector penderfynu o 151 newidyn deuaidd, sy'n
cynrychioli'r penderfyniad i gynnwys y Pokémon hwnna yn fy nhîm.
+ Gadawer i $$T$$ bod yn fector o 151 cysonion sy'n cynrychioli cyfanswm 'stats'
sylfaen pob Pokémon.
+ Gadawer i $$S$$, $$L$$ a $$P$$ bod y setiau o Pokémon dechreuol, chwedlonol a
ffug-chwedlonol yn ôl eu trefn.
+ Gadawer i $$R$$ bod yn fatrics 151 gan 18 o gysonion, lle $$R_{ij} = 1$$ os yw
Pokémon $$i$$ yn gwrthsefyll (yn cymryd niwed 0.5x neu lai) ymosodiadau o fath
$$j$$. Adeiladwyd $$R$$ gan:

{% highlight python %}
>>> gwrthiannau = [[1 if r <= 0.5 else 0 for r in gwendidau[i]] for i in range(151)]
{% endhighlight %}

Y rhaglen linol nawr yw:

$$\text{macsimeiddio:} \quad T_i X_i$$

yn amodol ar:

$$\sum X_i = 6$$

$$\sum_{i \in S} X_i \leq 1$$

$$\sum_{i \in L \cup P} X_i = 0$$

$$\sum R_{ij} X_i \geq 1 \quad \forall \quad j$$

Gall datrys hwn gan ddefnyddio `pulp`.
Diffinio'r broblem a'r newidynnau:

{% highlight python %}
>>> import pulp
>>> prob = pulp.LpProblem("TimPokemonPerffaith", pulp.LpMaximize)
>>> x = pulp.LpVariable.dicts("x", range(151), cat=pulp.LpBinary)
{% endhighlight %}

Ychwanegu'r ffwythiant amcan:

{% highlight python %}
>>> ffwythiant_amcan = sum(cyfanswnstats[pkmn] * x[pkmn] for pkmn in range(151))
>>> prob += ffwythiant_amcan
{% endhighlight %}

Ychwanegu'r cyfyngiadau, a datrys:

{% highlight python %}
>>> prob += sum([x[pkmn] for pkmn in range(151)]) == 6
>>> prob += sum([x[pkmn] for pkmn in dechreuwyr]) <= 1
>>> prob += sum([x[pkmn] for pkmn in chwedlonwyr + ffugchwedlonwyr]) == 0
>>> for tp in range(18):
...     prob += sum([gwrthiannau[pkmn][tp] * x[pkmn] for pkmn in range(151)]) >= 1
>>> prob.solve()
1
{% endhighlight %}

Unwaith ei fod wedi'i datrys, darllen y datrysiad $$X$$:

{% highlight python %}
>>> for i in range(151):
...     if x[i].value() == 1:
...         print(enwau[i])
charizard
arcanine
poliwrath
magneton
cloyster
tauros
{% endhighlight %}

Rhoddir hwn y tîm Pokémon perffaith (Cenhedlaeth 1) fel Charizard, Arcanine,
Poliwrath, Magneton, Cloyster a Tauros!

| Pokémon   | Math           | Gwrthsefyll                                                | Cyfanswm Stats |
|-----------|----------------|------------------------------------------------------------|----------------|
| Charizard | Fire/Flying    | Fir, Gra, Fig, Gro, Bug, Ste, Fai                          | 456            |
| Arcanine  | Fire           | Fir, Gra, Ice, Bug, Ste, Fai                               | 465            |
| Poliwrath | Water/Fighting | Fir, Wat, Ice, Bug, Roc, Dar, Ste                          | 420            |
| Magneton  | Electric/Steel | Nor, Ele, Gra, Ice, Poi, Fly, Psy, Bug, Roc, Dra, Ste, Fai | 415            |
| Cloyster  | Water/Ice      | Wat, Ice                                                   | 475            |
| Tauros    | Normal         | Gho                                                        | 415            |
|-----------|----------------|------------------------------------------------------------|----------------|

<br>

Mae'n ddiddorol bod y tîm yma ond yn cynnwys wyth 'math': Tân, Hedfan, Dŵr,
Ymladd, Trydan, Dur, Iâ a Normal.
Mae presenoldeb Tauros yn ddifyr, fel Pokémon unfath Normal mae'r gwrthsefyll
ond ymosodiadau Ysbryd; ac mae presenoldeb Arcanine yn synod, oherwydd mae'r
math Tân wedi'i llenwi gan Charizard.
Mewn gwirionedd nid oes angen Arcanine i orchuddio'r mathau y mae'r tîm yn
gwrthsefyll o gwbl: mae Arcanine yn gwrthsefyll ymosodiadau Iâ, yr unig fath
nad yw Charizard yn gwrthsefyll, serch hynny mae Poliwrath, Cloyster ac Magneton
hefyd yn gwrthsefyll ymosodiadau Iâ.
Mae'r un peth yn wir ar gyfer Cloyster.
Mae hwn yn dangos efallai ond pedwar Pokémon sydd angen i wrthsefyll ymosodiadau
o bob math, ac mae yna le llac i ddewis dau Pokémon arall ar sail eu cryfder yn
unig.

Mae'r dull yma yn cyffredinoli'n hawdd cynnwys mwy o genedlaethau, ond bydd
casglu'r data yn cymryd mwy o amser.

Mae'r fathemateg a defnyddir yma yn dechneg safonol yn ymchwil gweithrediadol,
a'i defnyddir mewn nifer o gymwysiadau mwy difrifol megis rostro nyrsion,
amserlennu arholiadau a llawdriniaethau.
Mae gan y rhaglen linol yma 151 newidyn a 21 cyfyngiad.
Gall cymwysiadau mwy difrifol cael miloedd o newidynnau a miloedd o gyfyngiadau,
ac felly mae datrysiadau fel PuLP yn amhrisiadwy.