---
layout     : post
title      : "Sut i Ddod yr Arlywydd Mwyaf Amhoblogaidd"
language   : cymraeg
comments   : true
---

Mae bron pawb yn gwybod bod y system ethol cyntaf-i'r-felin wedi torri. Yn America mae'n bosib ennill y bleidlais boblogaidd ond colli'r arlywyddiaeth. Gydag ond 45 diwrnod tan etholiad arlywyddol yr UDA, beth yw'r canran lleiaf bosib sydd angen i ddod yn arlywydd?

# Etholiadau Cyffredinol yn y DU

Mae'r sefyllfa yn y DU mwy syml, felly ystyriwn etholiadau cyffredinol yn y DU yn gyntaf. Mae'r wlad wedi'i rhannu i 650 etholaeth (_constituency_) gyda phoblogaethau bron yn hafal. Mae pob etholaeth yn pleidleisio am AS, fel arfer wedi'i gysylltu â phlaid wleidyddol, sy'n ennill sedd yn Nhŷ'r Cyffredin. Mae gan y blaid sy'n ennill dros hanner y seddi fwyafrif ac felly gallant ffurfio llywodraeth fwyafrifol. Ond, nid yw etholaethau yn ethol AS trwy fwyafrif (_majority_), maent yn ethol gan fwyafrif cymharol (_plurality_). Does dim angen i ymgeisydd ennill mwyafrif o'r pleidleisiau, maen nhw ond angen mwy o bleidleisiau nag unrhyw ymgeisydd arall.

Mae hwn yn arwain i sefyllfaoedd posib lle gall un blaid ennill y mwyafrif o'r pleidleisiau ond methu ffurfio llywodraeth. Er enghraifft:

![]({{site.baseurl}}/images/vote-example-cy.png){: .center-image }

Fan hyn mae chwe etholaeth, mae'r blaid felen yn ennill 4 ohonynt, ac felly'n gallu ffurfio llywodraeth. Serch hynny enillodd y blaid borffor 60.2% o'r pleidleisiau.

Felly - beth yw'r canran lleiaf o'r pleidleisiau gall plaid ennill a dal ffurfio llywodraeth fwyafrifol?

Dechreuwn trwy ganfod strategaeth gan ddefnyddio [PuLP](https://coin-or.github.io/pulp/). Er mwyn gwneud hwn, tybiwn fod wyth etholaeth, mae gan bob etholaeth poblogaethau hafal, mae'r nifer sy'n dewis pleidleisio yn hafal ym mhob etholaeth, ac ond dwy blaid sy'n ymgeisio. Gadewch i $$C$$ bod y set o'r etholaethau wedi'u indecsio gan $$i$$, gadewch i $$v_i$$ bod y canran o bleidleisiau ar gyfer y blaid felen yn etholaeth $$i$$, a gadewch i $$s_i$$ bod y newidyn deuaidd yn dynodi os enillodd y blaid felen sedd yn etholaeth $$i$$. Nawr byddwn yn lleiafsymio'r canran o bleidleisiau y enillodd y blaid felen tra'n sicrhau ei bod dal gallu ffurfio llywodraeth fwyafrifol:

$$\text{Lleiafsymio: } \sum_i \frac{v_i}{|C|}$$

O dan yr amodau:

$$v_i \geq 0 \quad \forall \; i \in C$$

$$v_i \leq 1 \quad \forall \; i \in C$$

$$s_i \leq v_i + \frac{1}{2} \quad \forall \; i \in C$$

$$\sum_i s_i \geq \frac{|C|}{2} + 1 \quad \text{os yw } c \text{ yn eilrif}$$

$$\sum_i s_i \geq \frac{|C|}{2} \quad \text{ow ys } c \text{ yn odrif}$$

{% highlight python %}
import pulp
nifer_etholaethau = 8

prob = pulp.LpProblem("EtholiadGwaethaf", pulp.LpMinimize)
pleidleisiau = pulp.LpVariable.dicts("v", range(nifer_etholaethau))
seddi = pulp.LpVariable.dicts("s", range(nifer_etholaethau), cat=pulp.LpBinary)

for etholaeth in range(nifer_etholaethau):
    prob += pleidleisiau[etholaeth] >= 0.0
    prob += pleidleisiau[etholaeth] <= 1.0
    prob += seddi[etholaeth] <= pleidleisiau[etholaeth] + 0.5
if nifer_etholaethau % 2 == 0:
    prob += sum([seddi[s] for s in range(nifer_etholaethau)]) >= (nifer_etholaethau / 2) + 1
else:
    prob += sum([seddi[s] for s in range(nifer_etholaethau)]) >= (nifer_etholaethau / 2)

ffwythiant_amcan = sum([pleidleisiau[v] for v in range(nifer_etholaethau)]) / nifer_etholaethau
prob += ffwythiant_amcan
prob.solve()
{% endhighlight %}

Mae hwn yn rhoi'r strategaeth ganlynol:

| Etholaeth | Canran y Bleidlais    | Sedd |
|-----------|-----------------------|------|
| 0         | 50% (ac un pleidlais) | 1    |
| 1         | 50% (ac un pleidlais) | 1    |
| 2         | 50% (ac un pleidlais) | 1    |
| 3         | 50% (ac un pleidlais) | 1    |
| 4         | 50% (ac un pleidlais) | 1    |
| 5         | 0%                    | 0    |
| 6         | 0%                    | 0    |
| 7         | 0%                    | 0    |
|-----------|-----------------------|------|


Felly mae gennym strategaeth - angen ennill ond 50% (ac un bleidlais) mewn _ond_ dros hanner yr etholaethau. Fan hyn mae'r blaid felen yn ffurfio llywodraeth fwyafrifol gydag ond 31.25% y bleidlais - tra bod y blaid borffor methu ffurfio llywodraeth er bod 68.75% y wlad wedi pleidleisio drostynt!

Os defnyddiwn y strategaeth hon ar gyfer $$n$$ etholaeth, y canran lleiaf, $$m(n)$$, fydd:

$$
m(n) =
\begin{cases} \frac{1}{4} + \frac{1}{2n} & \text{os yw } n \text{ yn eilrif}\\
\frac{1}{4} + \frac{1}{4n} & \text{os yw } n \text{ yn odrif.}
\end{cases}
$$

Wrth i $$n$$ mynd yn fwy ac yn fwy, mae hwn yn tueddu i 25%. Felly, yn y DU gyda 650 etholaeth, mewn system dwy-blaid, gall plaid ennill gydag ond 25.08% y pleidleisiau a dal ffurfio llywodraeth fwyafrifol - tra gall plaid ennill 74.92% o'r pleidleisiau a methu ffurfio llywodraeth!

# Mwy o bleidiau?

Beth os oes mwy o bleidiau? Yn defnyddio'r un strategaeth, os oes $$p$$ plaid, yna'r canran lleiaf o bleidleision sydd angen er mwyn ennill sedd yw $$\frac{1}{p}$$ ac un bleidlais, gyda'r gweddill y pleidleisiau wedi'u rhannu'n hafal rhwng y pleidiau eraill. Ar gyfer $$n$$ etholaeth a $$p$$ plaid y canran lleiaf o'r pleidleisiau $$m(n, p)$$ fydd:

$$
m(n, p) =
\begin{cases} \frac{1}{2p} + \frac{1}{2n} & \text{os yw } n \text{ yn eilrif}\\
\frac{1}{2p} + \frac{1}{4n} & \text{os yw } n \text{ yn odrif.}
\end{cases}
$$

Ar gyfer 650 etholaeth gwelwn effaith ychwanegu mwy o bleidiau:

![]({{site.baseurl}}/images/min-votes-cy.png){: .center-image }

Os oes 10 plaid, yna mae'n bosib ffurfio llywodraeth fwyafrifol gydag ond 5% o'r pleidleisiau!

# Y Coleg Etholiadol


Yn etholiadau arlywyddol yn yr UDA maen nhw'n defnyddio system debyg iawn a elwir y Coleg Etholiadol. Gallwn ystyried hwn fel set o etholaethau gyda _phoblogaethau anhafal_ a _phwysau anhafal_. Mae gan bob talaith, gan gynnwys Ardal Columbia, nifer penodol o 'etholwyr', yn gyfrannol i faint y boblogaeth maent yn cynrychioli. Er enghraifft mae pleidleiswyr yng Nghaliffornia yn etholi 55 etholwr, tra bod Mecsico Newydd yn etholi 5. O fewn pob talaith mae ymgeisydd yn cymryd pob etholwr neu dim ohonynt: yn tybio nad oes ymgeisiwr 3ydd plaid, os yw ymgeisydd yn ennill o leiaf 50% ac un bleidlais yng Nghaliffornia, maen nhw'n ennill _pob un_ o'r 55 etholwr[^1]. Yr ymgeisydd sy'n ennill hanner yr etholwyr yw'r arlywydd nesaf.

Felly beth yw'r canran lleiaf o bleidleisiau sydd angen er mwyn ennill yr arlywyddiaeth?. Mae ond angen gwneud mân newidiadau i'r cod PuLP uchod er mwyn ystyried y poblogaethau anhafal a'r pwysau anhafal, a gallwn ganfod strategaeth a fydd yn lleiafsymio'r nifer o bleidleisiau sydd angen er mwyn dod yn arlywydd.


{% highlight python %}
# https://www.federalregister.gov/documents/2020/02/14/2020-03000/estimates-of-the-voting-age-population-for-2019
etholwyr = [9, 3, 11, 6, 55, 9, 7, 3, 3, 29, 16, 4, 4, 20, 11, 6, 6, 8, 8, 4, 10, 11, 16, 10, 6, 10, 3, 5, 6, 4, 14, 5, 29, 15, 3, 18, 7, 7, 20, 4, 9, 3, 11, 38, 6, 3, 13, 12, 5, 10, 3]
pleidleisiau_posib = [3814879, 551562, 5638481, 2317649, 30617582, 4499217, 2837847, 770192, 577581, 17247808, 8113542, 1116004, 1338864, 9853946, 5164245, 2428229, 2213064, 3464802, 3561164, 1095370, 4710993, 5539703, 7842924, 4336475, 2277566, 4766843, 840190, 1458334, 2387517, 1104458, 6943612, 1620991, 15425262, 8187369, 581891, 9111081, 3004733, 3351175, 10167376, 854866, 4037531, 667558, 5319123, 21596071, 2274774, 509984, 6674671, 5951832, 1432580, 4555837, 445025]

prob = pulp.LpProblem("EtholiadGwaethaf", pulp.LpMinimize)
pleidleisiau = pulp.LpVariable.dicts("v", range(51))
taleithiau_a_ennillir = pulp.LpVariable.dicts("s", range(51), cat=pulp.LpBinary)

for talaith in range(51):
    prob += pleidleisiau[talaith] >= 0.0
    prob += pleidleisiau[talaith] <= pleidleisiau_posib[talaith]
    prob += taleithiau_a_ennillir[talaith] <= (pleidleisiau[talaith] * (1 / pleidleisiau_posib[talaith])) + 0.5
prob += sum([taleithiau_a_ennillir[s] * etholwyr[s] for s in range(51)]) >= (sum(etholwyr) / 2) + 1

ffwythiant_amcan = sum([pleidleisiau[v] for v in range(51)]) / sum(pleidleisiau_posib)
prob += ffwythiant_amcan
prob.solve()
{% endhighlight%}

Mae hwn yn rhoi just 21.68% o bleidleisiau!

Mae hwn yn golygu gall ymgeisydd colli trwy ennill 78.32% o'r pleidleiswyr! I roi hwn mewn persbectif, ond un arlywydd mewn hanes cyfan America, James Monroe yn 1820, sydd wedi _ennill_ etholiad gyda chanran mwy o bleidleisiau!

Sut all rhywun gwneud hwn? Gyda strategaeth debyg i'r DU uchod: enillwch 50% ac un bleidlais ym mhob talaith heblaw am Arizona, Califfornia, Fflorida, Georgia, Massachusetts, New Jersey, Efrog Newydd, Gogledd Carolina, Ohio, Pennsylvania, Tecsas, a Washington, lle nad ydych yn ennill unrhyw bleidleisiau o gwbl, fel yn y map isod (melyn yn ennill a phorffor yn colli).

![]({{site.baseurl}}/images/electoralcollage.png){: .center-image }

Ond, yn wahanol i etholiadau cyffredinol yn y DU, mae ymgeiswyr arlywyddol yn ennill popeth neu dim byd. Nid oes gan y 78.32% o'r pleidleiswyr a chollodd llais yn Y Tŷ Gwyn! Nid yw eu pleidleisiau, fel yn y DU, yn cyfrannu rhywfaint tuag at seddi yn y senedd, mae etholiadau cyngresol a seneddol ar gyfer hynny, gyda mecanweithiau cyfri gwahanol.

Nawr mewn gwirionedd nid yw dibynnu ar set leiaf penodol o daleithiau yn ymarferol gan fod gan bob talaith poblogaeth amrywiaethol. Ond os allwn fapio grwpiau lleiafrifol a grwpiau diddordeb arbennig i boblogaethau'r taleithiau, gallwn ganfod strategaeth i ennill etholiad yn hawdd sy'n targedu'r nifer lleiaf o grwpiau homogenaidd, neu sydd angen y swm lleiaf o gyfaddawdau gwleidyddol. Er dydw i ddim yn creu bod unrhyw beth rydw i wedi ysgrifennu yn foesol, mae'n ddiddorol.

---

[^1]: Heblaw am Nebraska a Maine lle ond hanner yr etholwyr sy'n gweithio fel hyn. Serch hynny nid yw hwn yn effeithio'r dadansoddiad hwn.
