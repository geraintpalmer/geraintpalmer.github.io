---
layout     : post
title      : "Model arwahanu Schelling"
language   : cymraeg
comments   : true
---

Dros yr wythnosau diwethaf cefais nifer o sgyrsiau am fodelu wedi'i seilio ar
asiantau (*agent based modelling*, ABM).
Mae'r pwnc yma i'w weld yn ddiddorol, ac er nad ydwyf wedi ei ddefnyddio yn fy
ngwaith ymchwil i, mae'n rhywbeth rwy'n awyddus defnyddio yn y dyfodol.

Er mwyn cynyddu fy nealltwriaeth o ABM, penderfynais ail-greu model ABM cynnar,
sydd nawr yn fodel enwog: Model Arwahanu Schelling.
Roedd [Thomas Schelling](https://en.wikipedia.org/wiki/Thomas_Schelling) yn
economegydd a chreodd y model, a ddefnyddiwyd i ddangos fod dewis bach ar gyfer
cael cymydog o'r un dosbarth/hil a dy hun yn gallu arwain tuag ag arwahanu llwyr.
Chwaraeodd Schelling y model gan ddefnyddio darnau arian a phapur graff, ond ers
ni mae nifer o fodelau efelychiad cyfrifiadurol wedi'i rhedeg.

Diffinnir y model:

  + Mae grid o sgwariau yn cynrychioli’r byd, gyda phob sgwâr yn cynrychioli
  plot o dir lle mae un asiant yn byw.
  + Mae'r byd wedi'i phoblogi (ar hap ar y dechrau) gan nifer o wahanol fathau o
  asiant (yn yr achos yma, 2), gan adael ffracsiwn o'r sgwariau yn wag.
  + Mae gan yr asiantau rhyw *ddewis* ar gyfer y nifer o'u cymdogion (asiantau
  sy'n byw yn y plotiau o dir cyfagos, gan gynnwyd yn groeslin) i fod yr un fath
  a nhw. Os yw'r nifer o gymdogion tebyg yn llai na'r dewis yma, yna daeth yr
  asiant yn *anhapus*.
  + Pob tro, mae pob* asiant anhapus yn symud i blot o dir wag wedi'i ddewis ar
  hap.

Gweithredais i hwn yn Python, yn defnyddio gwrthrychau fel asiantau.
Er mwyn gwneud y codio yn haws, mae'r model yma yn tybio fod y byd yn dorws,
hynny yw mae'r chwith eithafol yn gymdogion i'r dde eithafol, ac mae'r top
eithafol yn gymdogion i'r gwaelod eithafol.
Rydw i hefyd yn torri'r rheolau ychydig, ac yn lle *pob* asiant anhapus yn symud
pob tro, ond rhai asiantau sy'n symud, yn dibynnu os yw nifer o asiantau anhapus
yn fwy na nifer o blotiau gwag.
Rhoddir y cod sy'n diffinio'r dosbarthau Python `Agent` a `World` ar ddiwedd y
cofnod yma.

Mae rhaglennu gwrthrych-gyfeiriadol yn ddull amlwg o weithredu ABM gan fod y
gwrthrychau eu hun yn dod yn asiantau: priodweddau'r gwrthrych yw briodweddau'r
asiant, a dulliau'r gwrthrych yw'r hyn mae'r asiantau yn gwneud.

Gadewch i ni weld yr efelychiad ar waith.
Mae sgwariau gwyn yn cynrychioli plotiau gwag, mae sgwariau melyn a phorffor yn
cynrychioli lle mae'r ddau fath gwahanol o asiant yn byw.
Mae'r animeiddiad isod yn dangos grid byd 80x80 sgwâr, lle mae gan asiantau
dewis i gael 70% o gymdogion tebyg:

![]({{site.baseurl}}/images/atlas.gif){:width='500px' .center-image}

Mae'r efelychiad yn stopio unwaith bod 99.995% o'r asiantau yn hapus.
Mae gan y boblogaeth sy'n dychwel tebygrwydd cymdogion cyfartalog, neu
hapusrwydd cyfartalog o 99.51%, lot mwy na'r dewis gwreiddiol o 70%.

Fe ellir rhedeg arbrofion i dangos sut mae'r model yn ymddwyn gyda gwahanol
dewisiadau.
Rhedir yr arbrofion yma ar grid byd 40x40 sgwâr:

![]({{site.baseurl}}/images/increase_preference_cy.png)

Wrth i ddewis yr asiantau unigol cynyddu, mae'r byd yn dod fwy a fwy ar wahân.
Gallwn weld yn y plot isod po fwyaf dewis yr asiantau unigol, po fwyaf yw
hapusrwydd cyfartalog y byd.
Fe fydd hapusrwydd cyfartalog y byd trwy'r amser llawer uwch na dewis yr
asiantau unigol:

![]({{site.baseurl}}/images/preference_meanhappiness_cy.png)

Mesur arall arwahanu yw nifer o 'gytrefi' a ffurfiwyd.
Hynny yw faint o glystyrau o asiantau tebyg a ffurfiwyd.
Am resymau darluniadol yn unig, fe fyddaf *yn fras ac yn amwys* yn diffinio
cytref fel y ganlyn:

*Dychmygwch y grid o sgwariau fel rhwydwaith o fertigau, lle mae ymyl rhwng dau
fertig os yw'r sgwariau yna yn gymdogion ac wedi'i chyfanheddu gan asiantau o'r
un fath.
Yna cytref yw [cydran gysylltiedig](https://en.wikipedia.org/wiki/Connected_component_(graph_theory))
o'r rhwydwaith.*

Gan ddefnyddio [NetworkX](https://networkx.github.io/) mae ffeindio nifer o
gydrannau cysylltiedig yn syml.
Mae'r plot isod yn dangos fod nifer o gytrefi yn gostwng yn ddramatig wrth i
ddewis yr asiantau cynyddu, ac mewn gwirionedd mae'r gostyngiad mwyaf yn digwydd
ar lefel dewis isel iawn:

![]({{site.baseurl}}/images/preference_components_cy.png)

Yn fras, mae byd wedi poblogi gan asiantau gyda dewis 30% am gymdogion tebyg yn
bennu gyda byd wedi'i arwahanu 40 gwaith yn fwy na byd wedi poblogi gan asiantau
gyda dewis 10% am gymdogion tebyg.

Mae'r ABM yma yn dangos ymddygiad *allddodol* (emergent).
Ni wnaeth unrhyw un dweud wrth yr asiantau i arwahanu a ffurfio cytrefi.
Cafodd yr asiantau rheolau syml i ddilyn: edrychwch ar eich cymdogion a
penderfynwch os yn hapus, os yn anhapus, symudwch.
Fe wnaeth ymddygiad system gyfan, arwahanu a ffurfio cytrefi, tyfu mas o'r
rheolau syml yma.
Mae hwn yn union fel mae ymddygiad cymdeithasol yn tyfu mas o weithredau
unigolion.

Dyma [rhestr ddiddorol](https://ccl.northwestern.edu/netlogo/models/) o fodelau
ABM [NetLogo](https://ccl.northwestern.edu/netlogo/).
Gwelwch fod y fath o fodelu yma wedi cael eu defnyddio mewn meysydd mor wahanol
a bioleg, gwyddoniaeth gymdeithasol, a mathemateg.
Ar hyn o bryd maen nhw'n cael eu defnyddio mewn ymchwil gweithrediadol hefyd,
sef rhywbeth hoffwn ddarllen mwy amdano.

Mae'r holl god a defnyddiais i greu canlyniadau'r cofnod yma ar gael
[ar Github fan hyn](https://github.com/geraintpalmer/schelling_abm_test).

*Cod yn diffinio dosbarthau `Agent` a `World`:*
{% highlight python %}
class Agent:
    def __init__(self, x, y, kind, preference, world):
        self.x = x
        self.y = y
        self.kind = kind
        self.preference = preference
        self.world = world
    
    def know_neighbours(self):
        self.neighbours = [self.world.coords[x % self.world.size, y % self.world.size]
                           for x, y in itertools.product(range(self.x-1, self.x+2),
                                                         range(self.y-1, self.y+2))]
    
    def swap(self, partner):
        self.kind, partner.kind = partner.kind, self.kind
    
    def happiness(self):
        neighbour_kinds = [n.kind for n in self.neighbours]
        numsame = neighbour_kinds.count(self.kind)
        numvacant = neighbour_kinds.count(0)
        if numvacant == 8:
            if self.vacant():
                return 1.0
            return 0.0
        return (numsame - 1) / (8 - numvacant)
    
    def dissatisfied(self):
        return self.happiness() < self.preference
    
    def vacant(self):
        return self.kind == 0
{% endhighlight %}

{% highlight python %}
class World:
    def __init__(self, size, kinds, probs, preference):
        self.size = size
        self.preference = preference
        self.coords = self.populate_world(kinds, probs, preference)
        [a.know_neighbours() for row in self.coords for a in row]
        self.num_dissatisfied = size ** 2
        self.num_vacant = sum([a.vacant() for row in self.coords for a in row])
    
    def populate_world(self, kinds, probs, preference):
        return np.array([[Agent(x, y, np.random.choice(kinds, p=probs), preference, self)
                          for y in range(self.size)] for x in range(self.size)])
    
    def atlas(self):
        return np.array([[a.kind for a in row] for row in self.coords])
    
    def happiness_distribution(self):
        return [a.happiness() for row in self.coords for a in row if not a.vacant()]
    
    def advance_turn(self):
        dissatisfied = []
        vacant = []
        for row in self.coords:
            for a in row:
                if a.vacant():
                    vacant.append(a)
                elif a.dissatisfied():
                    dissatisfied.append(a)
        self.num_dissatisfied = len(dissatisfied)
        np.random.shuffle(dissatisfied)
        np.random.shuffle(vacant)
        num_swap = min(self.num_dissatisfied, self.num_vacant)
        for indx in range(num_swap):
            dissatisfied[indx].swap(vacant[indx])
    
    def play(self, threshold=0.01):
        while self.num_dissatisfied / (self.size ** 2) > threshold:
            self.advance_turn()
{% endhighlight %}