---
layout     : post
title      : "Creu mapiau gyda Geopandas"
language   : cymraeg
comments   : true
---

Y cwpl o wythnosau diwethaf dechreuais i chwarae gyda chreu mapiau yn Python gan
ddefnyddio'r llyfrgell [Geopandas](http://geopandas.org/index.html).
Mae'r llyfrgell yn anhygoel ac rydw i wedi dod yn ffan fawr.
Mae'r syntax yn debyg iawn i [Pandas](http://pandas.pydata.org/), ac mae'n
gweithio'n grêt gyda [matplotlib](http://matplotlib.org/) hefyd.
Mewn gwirionedd mae'r naid o ddefnyddio Pandas i Geopandas yn fach iawn, ac os
wyt ti'n gyfforddus gyda Pandas, does dim lot o waith o gwbl i ddeall Geopandas.

Fel rhan o fy ngwaith PhD edrychais i mewn i lefelau amddifadedd (deprivation)
yn y pum sir a wasanaethwyd gan Fwrdd Iechyd Aneurin Bevan.
Ges i lot o help i ddeall LSOAau, polygonau, a sgorau WIMD gan fy mrawd
[Rob](https://twitter.com/robipalmer), sydd wedi cynhyrchu mapiau eisoes yn R.
Yn y cofnod blog yma, dangosaf enghreifftiau o'r plotiau rydw i wedi cynhyrchu,
a'r cod syml defnyddiais i'w cynhyrchu.

### Lawrlwytho Data

Yn fy ngwaith canolbwyntiais ar bum sir yn ne ddwyrain Cymru: Blaenau Gwent,
Caerffili, Casnewydd, Sir Fynwy, a Tor-faen.
Hefyd roedd angen edrych ar ardaloedd mwy manwl, mor fach a oedd posib.
Y categori lleiaf ar gyfer ardaloedd yn Gymru yw LSOAau (Local Super Output
Area), sef ardaloedd lle mae rhwng 1000 a 1500 o bobl yn byw.
Mae gan bob LSOA cod ac enw: er enghraifft yr LSOA sy'n cynnwys Castell Cas-gwent
yw "St Mary's", a'i chod yw W01001587.

Er mwyn gallu mapio LSOAau, mae angen gwybod siâp a lleoliad pob ardal.
Diffinnir y rhain gan *polygonau*.
Gellir lawrlwytho rhain mewn fformat geojson o'r ONS.
Dyma linc i'r data defnyddiais i, sy'n cynnwys pob LSOA yn Gymru a Lloegr:

+ <https://data.gov.uk/dataset/lower_layer_super_output_area_lsoa_boundaries>

(Nodwch fod hwn yn set ddata enfawr: 34,753 o LSOAau, pob un yn cynnwys pob
fertig o'r polygon sy'n ei ddiffinio.
Fe fydd hwn yn cymryd amser i lawrlwytho, ac fe fydd yn cymryd amser i agor gan
Geopandas.
Y peth cyntaf wnes i oedd hidlo a safio ffeil geojson arall gydag ond yr LSOAau
o'r pum sir o ddiddordeb.)

Yn ogystal â'r polygonau, fe ddefnyddiais dau set ddata arall, yn cynnwys
gwybodaeth ar fesur amddifadedd WIMD pob LSOA (Welsh Index of Multiple
Deprivation, graddfa lle mae WIMD o 1 yn dynodi'r LSOA mwyaf difreintiedig, a
1909 yn dynodi'r LSOA lleiaf difreintiedig), a phoblogaeth dros 60 oed pob LSOA.
Fe lawrlwythais i rain o StatsWales a'r ONS:

+ <https://statswales.gov.wales/Catalogue/Community-Safety-and-Social-Inclusion/Welsh-Index-of-Multiple-Deprivation/WIMD-2014/wimd2014>

+ [https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/
populationestimates/datasets/lowersuperoutputareamidyearpopulationestimates
](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/lowersuperoutputareamidyearpopulationestimates)

### Darllen Geojson

Mae'n hawdd iawn darllen mewn geojson i geopandas:

{% highlight python %}
import geopandas as gpd
assert geopandas.__version__ == '0.3.0'

world = gpd.read_file('abuhb_world.geojson')
{% endhighlight %}

Mae `world` yn wrthrych `GeoDataFrame`, sydd yn ymddwyn yn union fel `DataFrame`
pandas.
Ar ôl defnyddio Pandas i ddarllen y setiau data poblogaeth ac amddifadedd,
cyfunais y tair ffrâm data (gan ddefnyddio Pandas) felly bod gan `world` tri
colofn ychwanegol: `WIMD`, `Over 60` a `Sir`:

{% highlight python %}
>>> world
    objectid  lsoa11cd    lsoa11nm              lsoa11nmw   st_areasha  st_lengths      geometry                                                         WIMD  Over 60  Sir
0   34131     W01001325   Caerphilly 003A       Caerffili   003A        1.975810e+06    9595.912399  POLYGON ((-3.222590332332996 51.69544541936416...   219   342      Caerffili
1   34132     W01001326   Caerphilly 003B       Caerffili   003B        1.418504e+06    7206.074574  POLYGON ((-3.218658752736475 51.69265017758838...   190   497      Caerffili
2   34133     W01001327   Caerphilly 014A       Caerffili   014A        1.368584e+07    26141.148134 POLYGON ((-3.133625203219097 51.65362006379572...   1114  451      Caerffili
3   34134     W01001328   Caerphilly 014B       Caerffili   014B        2.343212e+06    10639.884639 POLYGON ((-3.126845962218699 51.66067765558952...   815   370      Caerffili
4   34135     W01001329   Caerphilly 014C       Caerffili   014C        4.799436e+05    4207.033238  POLYGON ((-3.124476654827622 51.63506150073896...   692   365      Caerffili
{% endhighlight %}

### Plotio Map

Mae plotio map o'r polygonau yn hawdd:

{% highlight python %}
world.plot()
{% endhighlight %}

![]({{site.baseurl}}/images/abuhb.png)

I ddynodi sut i liwio'r polygonau defnyddiwch ddadlau:

+ Dynodwch pa golofn i'w ddefnyddio fel gwerthoedd gyda `column`
+ Dynodwch y map liw i'w ddefnyddio gyda `cmap`

Gallwch hefyd integreiddio gydag amgylchedd wrthrych matplotlib:

{% highlight python %}
fig, ax = plt.subplots(1)
world.plot(column='Over 60', cmap='viridis_r', ax=ax)
ax.axis('off')
{% endhighlight %}

![]({{site.baseurl}}/images/over60.png)

### Trin Geometreg

Mae nifer o ddulliau i drin geometreg y polygonau.

Dull Geopandas o grwpio yw `dissolve`, sy'n grwpio polygonau gyda rhinweddau
tebyg a chreu un polygon mawr ohonynt.
Grwpio LSOAau gan sir:

{% highlight python %}
>>> siroedd = world.dissolve(by='Sir')
>>> siroedd
                geometry
Sir                                         
Blaenau Gwent   POLYGON ((-3.219457536348314 51.74573457863166...
Caerffili       POLYGON ((-3.123546981902226 51.58721244839312...
Casnewydd       (POLYGON ((-2.903851574580124 51.6274883996199...
Sir Fynwy       (POLYGON ((-2.781429130096552 51.5252840700888...
Tor-faen        POLYGON ((-2.976496118298735 51.64839999700513...
{% endhighlight %}

Gallwn ffeindio canolbwynt polygon gyda `centroid`:

{% highlight python %}
siroedd['centroid'] = siroedd['geometry'].centroid
{% endhighlight %}

Un defnydd o ganolbwynt polygon yw i labelu polygonau:

{% highlight python %}
fig, ax = plt.subplots(1)
siroedd.plot(color='azure', edgecolor='black', ax=ax)
props = dict(boxstyle='round', facecolor='linen', alpha=1)
for point in siroedd.iterrows():
    ax.text(point[1]['centroid'].x,
            point[1]['centroid'].y,
            point[0],
            horizontalalignment='center',
            fontsize=10,
            bbox=props)
ax.axis('off')
{% endhighlight %}

![]({{site.baseurl}}/images/siroedd.png)

Mae Geopandas hefyd yn dod gyda nifer o ddulliau clyfar i ddelio gyda
[dafluniadau map](http://geopandas.org/projections.html) gwahanol.

### Casgliad

Rydw i wedi joio chwarae gyda Geopandas, a chredaf fod y mapiau a chynhyrchwyd
yn brydferth iawn.

Yn olaf, cyfunaf dau fap, LSOAau a siroedd, i edrych ar amddifadedd.
Fan hyn defnyddiaf y GeoDataFrame `siroedd` i ychwanegu llinellau du rhwng y
pum sir.

{% highlight python %}
fig, ax = plt.subplots(1, figsize=(10, 6))
world.plot(column='WIMD', ax=ax, cmap='viridis_r')
siroedd.plot(color='None', edgecolor='black', linewidth=2, ax=ax)
ax.axis('off')
vmin = world['WIMD'].min()
vmax = world['WIMD'].max()

# Creu bar liw
sm = plt.cm.ScalarMappable(cmap='viridis_r', norm=plt.Normalize(vmin=vmin, vmax=vmax))
sm._A = []
cbar = fig.colorbar(sm)
{% endhighlight %}

![]({{site.baseurl}}/images/wimd.png)

Gallwn weld fod gan Sir Fynwy sgorau amddifadedd mwy na'r siroedd eraill.
Wrth gymharu â'r map poblogaeth dros 60 oed, gallwn weld fod gan Sir Fynwy mwy
o bobl henach na'r siroedd eraill.
Mewn gwirionedd, mae patrwm poblogaeth pobl dros 60 oed a phatrwm amddifadedd yn
debyg ofnadwy.
A ydym wedi sylwi ar rywbeth diddorol?
Yw pobl dros 60 yn fwy tebygol i symud i ardaloedd llai difreintiedig?

Er bod y mapiau yn edrych yn neis, mae'n anodd iawn dweud gyda mapiau fel hyn,
gan fod gan wybodaeth geograffeg gymaint o gyd-newidynnau.
Yn yr achos yma, mae WIMD wedi'i chyfrifo o nifer o gyd-newidynnau.
Un ohonynt yw diweithdra: nid yw pobl ymddeol yn cyfri'n ddi-waith, felly os yw
nifer o bobl henach yn bwy mewn ardal, fe fydd diweithdra'r ardal yn disgyn.
Mae'n debyg fod nifer o gyd-newidynnau WIMD yn cael ei effeithio gan boblogaeth
hen bobl, felly ni allwn dynnu unrhyw gasgliadau fan hyn.

Serch hynny, mae Geopandas yn declyn gwych, yn cynhyrchu mapiau pert iawn, ac yn
hawdd i'w ddefnyddio os ydych eisoes yn gyfarwydd gyda Pandas.