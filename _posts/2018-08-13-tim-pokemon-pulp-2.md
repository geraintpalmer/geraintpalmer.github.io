---
layout     : post
title      : "Dewis y tîm Pokémon perffaith gyda Python a PuLP - Rhan 2"
language   : cymraeg
comments   : true
---

Mewn [cofnod blog blaenorol](/2018/05/29/pokemon-team-pulp/) ceisiais ddefnyddio
PuLP i ddewis tîm Pokémon cryf gyda gorchudd gwrthiant-mathau llawn.
Fan hyn, mewn cofnod blog ar y cyd gyda hyfforddwr Pokémon profiadol
[Alastair Harris](https://twitter.com/AlHarris91), fe wnawn ni ceisio gwella'r
canlyniad yna trwy optimeiddio gorchudd mathau yn unig, yn gadael i Alastair
gynghori ar ddewisiadau Pokémon spesifig.

I atgofio, dyma'r matrics gwendidau'r 18 math:

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

+ Mae 7fed colofn y rhes 1af yn dangos fod Pokémon Normal yn wan i ymosodiadau
math Ymladd, yn cymryd 2x y difrod.
+ Mae effeithiau Pokémon sydd a fath-dwbl yn lluosol, felly mae Pokêmon
Dŵr-Trydan ond yn cymryd 0.25x y difrod o ymosodiadau Dur.

Pa chwe math (neu fath-dwbl) dylen ni dewis ar gyfer ein tîm fel bod ganddyn
imiwnedd a gwrthiannau llawn?

Pam bod hwn yn dasg anodd?
Mae 18 math, ac felly mae $$^{18}C_2 = 153$$ cyfuniadau posib ar gyfer Pokémon
math-dwbl.
O rain ni ddefnyddir 37 cyfuniad ar gyfer Pokémon cyffredin (mae rhai heb eu
defnyddio o gwbl, a rhai ar gyfer Pokémon chwedlonol neu esblygiadau-mega yn
unig ac felly nid yw'n rhan o'r dadansoddiad yma), felly $$153 + 18 - 37 = 134$$
ddewis.
Felly mae $$^{134}C_6 = 7177979809$$ tîm o chwe math unigryw i'w ddewis
ohonynt: dros 7 biliwn dewis!

Felly defnyddiwn [`pulp`](https://pythonhosted.org/PuLP/) i ddewis *mathau* ein
tîm o chwe Pokémon.
Yr unig amodau fydd:

 + Ar gyfer pob math y maen posib cael imiwnedd iddo, dylai fod o leiaf un
 Pokémon yn y tîm ag imiwnedd iddo, ac un Pokémon arall â gwrthiant iddo,
 + Ar gyfer pob math arall, dylai fod dau Pokémon ar y tîm â gwrthiant i'r math
 yna.

Y rhaglen linol nawr yw:

+ Gadawer i $$X$$ bod yn fector penderfynu o 134 newidyn deuaidd, sy'n
cynrychioli'r penderfyniad i gynnwys y math hwnna yn fy nhîm.
+ Gadawer i $$T$$ bod yn fector o 134 cysonyn yn cynrychioli rhyw amcan ar
gyfer pob math.
+ Gadawer i $$R$$ bod yn fatrics o gysonion 134 gan 18, lle mae $$R_{ij} = 1$$
os yw math $$i$$ yn gwrthsefyll (cymryd 0.5x neu 0.25x o ddifrod) ymosodiadau o
fath $$j$$.
+ Gadawer i $$I$$ bod yn fatrics o gysonion 134 gan 18, lle mae $$I_{ij} = 1$$
os oes gan fath $$i$$ imiwnedd (cymryd 0x o ddifrod) i ymosodiadau o fath $$j$$.
+ Gadawer i $$P$$ bod y set o fathau y mae'n bosib cael imiwnedd iddynt (Normal,
Trydan, Ymladd, Gwenwyn, Ddaear, Seicig, Ysbryd, Draig).

$$\text{macsimeiddio / minimeiddio:} \quad T_i X_i$$

yn amodol ar:

$$\sum X_i = 6$$

$$\sum I_{ij} X_i \geq 1 \qquad \forall j \text{ os yw } j \in P$$

$$\sum R_{ij} X_i \geq 1 \qquad \forall j \text{ os yw } j \in P$$

$$\sum R_{ij} X_i \geq 2 \qquad \forall j \text{ os yw } j \notin P$$

Edrychwn ar pum ffwythiant amcan:

 1. minimeiddio prif-wendidau ($$T_i$$ yw nifer o fathau ymosodiad mae math
 $$i$$ yn cymryd 4x o ddifrod yn eu herbyn),
 2. minimeiddio gwendidau ($$T_i$$ yw nifer o fathau ymosodiad mae math $$i$$ yn
 cymryd 4x neu 2x o ddifrod yn eu herbyn),
 3. macsimeiddio gwrthiannau ($$T_i$$ yw nifer o fathau ymosodiad mae math $$i$$
 yn cymryd 0.5x neu 0.25x o ddifrod yn eu herbyn),
 4. macsimeiddio prif-wrthiannau ($$T_i$$ yw nifer o fathau ymosodiad mae math
 $$i$$ yn cymryd 0.25x o ddifrod yn eu herbyn),
 5. minimeiddio holl ddifrod ($$T_i$$ yw swm y lluosyddion difrod dros yr holl
 mathau ymosodiad y mae math $$i$$ yn cymryd).

Mae'r holl god [i'w gael fan hyn](https://github.com/geraintpalmer/pokemon-pulp/blob/master/pkmntypes.ipynb).


## 1. Minimeiddio prif-wendidau

  | Math             | Pokémon a awgrymir |
  |------------------|--------------------|
  | Normal-Glaswellt | Sawsbuck           |
  | Tân-Ysbryd       | Chandelure         |
  | Dŵr-Tylwyth      | Primarina          |
  | Ddaear-Tywyll    | Krookodile         |
  | Hedfan-Dur       | Skarmory           |
  | Seicig-Dur       | Metagross          |
  |------------------|--------------------|

<br>

Mae hwn yn dîm yma yn eithafol o gytbwys sy'n gallu goresgyn rhan fwyaf o
fygythiadau mewn haenau UU/NU/OU yn gystadleuol.
Serch hyn does dim siawns o sefydlu iachawr neu wal, felly bydd rhaid i'r tîm
yma dibynnu ar ymosodiadau arbennig a phŵer pur.


## 2. Minimeiddio gwendidau

  | Math             | Pokémon a awgrymir |
  |------------------|--------------------|
  | Normal           | Stoutland          |
  | Tân-Ddaear       | Camerupt           |
  | Dŵr-Hedfan       | Swanna             |
  | Glaswellt-Ysbryd | Trevenant          |
  | Tywyll-Dur       | Bisharp            |
  | Dur-Tylwyth      | Mawile             |
  |------------------|--------------------|

<br>

Mae hwn yn dîm cytbwys gyda phwll o ymosodiadau lled trwy lefelu i fyny, TMau a
tiwtro.
Ond serch hyn ond un Pokémon sydd, Swanna, sy'n gallu gwella iechyd, ac ond
iechyd ei hun.
Mae hefyd eithaf gwan yn amddiffynnol.


## 3. Macsimeiddio gwrthiannau

  | Math              | Pokémon a awgrymir |
  |-------------------|--------------------|
  | Normal-Tân        | Pyroar             |
  | Dŵr-Ysbryd        | Jellicent          |
  | Glaswellt-Tylwyth | Shiinotic          |
  | Ddaear-Dur        | Steelix            |
  | Hedfan-Dur        | Skarmory           |
  | Tywyll-Dur        | Bisharp            |
  |-------------------|--------------------|

<br>

Mae Shiinotic yn wal wych ac yn gallu synnu rhan fwyaf o bobl, a bydd Pokémon
draig yn ei gasáu gyda'i bwlc a'i ymosodiadau 'toxic' a 'spore'.
Bydd 'cursed body' Jellicent yn achosi problemau difrifol i ymosodwyr trwm a
bydd rhaid i'r gweddill dibynnu ar rym llym; serch hyn mae'n dîm mwy cytbwys o
lawer na'r gweddill a generadwyd fan hyn.


## 4. Macsimeiddio prif-wrthiannau

  | Math            | Pokémon a awgrymir      |
  |-----------------|-------------------------|
  | Normal-Ddaear   | Diggersby               |
  | Tân-Ysbryd      | Marowak (ffurf Alola)   |
  | Dŵr-Dur         | Empoleon                |
  | Glaswellt-Draig | Exeggutor (ffurf Alola) |
  | Hedfan-Tylwyth  | Togekiss                |
  | Craig-Tywyll    | Tyranitar               |
  |-----------------|-------------------------|

<br>

Gyda Togekiss a Tyranitar fel prif y prif bwlc bydd y tîm yma'n straffaglu, a
mae'n debyg bod ganddo rhai o'r galluoedd gwaethaf yn gystadleuol.
Mae posibilrwydd o oresgyn rhan fwyaf o fygythiadau, ond bydd yn straffaglu mewn
OU o gymharu â haenau UU/NU.


## 5. Minimeiddio holl difrod

  | Math         | Pokémon a awgrymir |
  |--------------|--------------------|
  | Normal-Draig | Drampa             |
  | Dŵr-Tywyll   | Crawdaunt          |
  | Ddaear-Byg   | Wormadam           |
  | Hedfan-Dur   | Skarmory           |
  | Ysbryd-Dur   | Aegislash          |
  | Dur-Tylwyth  | Klefki             |
  |--------------|--------------------|

<br>

Hwn yw'r tîm fwyaf diddorol gan nad yw unrhyw un yn ategu unrhyw un arall.
Mae Skarmory yn dda ar gyfer sefydlu 'toxic' a speiciau i daflu off
gwrthwynebwyr, mae newidiadau ffurf Aegislash hefyd yn gallu taflu off
chwaraewyr, ond hefyd mae'r ffordd y mae'n ymosod ac amddiffyn yn rhagweladwy,
sy'n ei wneud yn lladd hawdd yn ei ffurf ymosod.
Mae Klefki yn ased ond os yw'n sefydlu 'trick room', a gall wneud unwaith bod
Skarmory wedi sefydlu speiciau.
Gyda rhain gall y tîm yma goroesi a throi’r tablau yn effeithiol dros holl
haenau'r gêm.


## Casgliad

Mewn [cofnod blog blaenorol](/2018/05/29/tim-pokemon-pulp/) nod y rhaglen linol
oedd canfod Pokémon spesifig a oedd yn bodloni rhyw orchuddiad math ac yn
macsimeiddio cyfanswm yr ystadegau.
Ni edrychodd ar imiwneddau o gwbl.
Hefyd tybiodd bod cyfanswm ystadegau Pokémon oedd yr unig ddangosydd o gryfder
neu ddefnyddioldeb y Pokémon.
Ni ystyriwyd lledaeniad yr ystadegau (ymosodiad uchel vs. amddiffyn uchel vs.
popeth mewn cyfartaledd), galluoedd, pwll ymosodiadau, neu brofiad yr hyfforddwr
yn defnyddio'r Pokémon yna.

Canolbwyntiodd y cofnod blog yma ar orchudd math yn unig, er fe all rhai
ymosodiadau (e.e. Odor Sleuth, Smack Down), eitemau (e.e. Ring Target, Air
Balloon) a galluoedd (e.e. Levitate, Motor Drive) gwella neu waethygu'r gorchudd
math a rhoddir.

Hoff dîm Alastair fan hyn: tîm 3.
Mae ganddo fynediad i bwll ymosodiadau mwy lled ac yn galluogi chwarae fwy
diddorol.
Mae hwn yn dangos bod hyfforddwyr Pokémon profiadol mewn gwirionedd yn
gwerthfawrogi priodweddau sy'n eithaf anodd dal trwy ddefnyddio'r modd
rhaglennu llinol, er mae'n generadu syniadau newydd ar gyfer chwarae'r gêm.
