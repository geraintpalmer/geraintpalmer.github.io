---
layout     : post
title      : "Mewnblaniadau Geiriau Cymraeg"
language   : cymraeg
comments   : true
---

Dros y ddwy flwyddyn ddiwethaf rydw i wedi mwynhau bod yn rhan o ddau brosiect y cyllidir gan Lywodraeth Cymru yn cyd-weithio gyda chyd-weithwyr o’r Ysgol Cyfrifiadureg a’r Ysgol Saesneg ([Irena Spasic](https://www.cardiff.ac.uk/people/view/118164-spasic-irena), [Padraig Corcoran](https://www.cardiff.ac.uk/people/view/155896-corcoran-padraig), [Dawn Knight](https://www.cardiff.ac.uk/people/view/142032-knight-dawn), [Luis Espinosa Anke](https://www.cardiff.ac.uk/people/view/1063569-anke-luis), [Vigneshwaran Muralidaran](https://www.cardiff.ac.uk/people/view/1764539-muralidaran-vigneshwaran), [Maxim Filimonov](https://www.cardiff.ac.uk/people/view/1764540-filimonov-maxim), a [Laura Arman](https://www.cardiff.ac.uk/people/view/2521321-)). Pwrpas y prosiectau hyn, fel rhan o [Gynllun Gweithredu Technoleg Cymraeg y Llywodraeth](https://llyw.cymru/sites/default/files/publications/2018-12/cynllun-gweithredu-ar-gyfer-technoleg-cymraeg-a-chyfryngau-digidol.pdf), oedd hyfforddi mewnblaniadau geiriau ar gyfer yr iaith Gymraeg, a mewnblaniadau geiriau traws-ieithyddol o’r gofod geirfaol cyfunedig Cymraeg a Saesneg. O’r prosiect daeth dau gyhoeddiad academaidd a phennod mewn e-lyfr:

1. 2021: **Creating Welsh Language Word Embeddings.**<br>*Corcoran P, Palmer GI, Arman L, Knight D, & Spasić I.* [Applied Sciences](https://www.mdpi.com/2076-3417/11/15/6896) 11(15), 6896.
2. 2021: **English–Welsh Cross-Lingual Embeddings.**<br>*Espinosa-Anke L, Palmer GI, Corcoran P, Filimonov M, Spasić I, & Knight D.* [Applied Sciences](https://www.mdpi.com/2076-3417/11/14/6541) 11(14), 6541.
3. 2021: **Golwg Agosach ar Fewnblaniadau Geiriau Cymraeg.** [(en)](http://techiaith.cymru/wp-content/uploads/2021/10/Language-and-Technology-in-Wales-Volume-I.pdf)<br>*Palmer GI, Corcoran P, Arman L, Knight D, & Spasić I.* [Language and Technology in Wales: Volume I](http://techiaith.cymru/wp-content/uploads/2021/10/Iaith-a-Thechnoleg-yng-Nghymru-Cyfrol-I.pdf).

Cafodd yr un olaf o rain ei ysgrifennu'n wreiddiol yn Gymraeg, yn defnyddio technoleg cyfieithu awtomatig er mwyn ei gyd-ysgrifennu gyda phobl nad oedd yn siarad Cymraeg, sy'n eithaf cwl.
Yn ogystal i rain, datblygon ni'r adnoddau canlynol:

+ [Fideo tiwtorialau iaith Cymraeg am y gwaith](https://www.youtube.com/playlist?list=PLSkPgScy-DkHuXKwFC0xSVaIxSVALy_HD),
+ [Mewnblaniadau geiriau Cymraeg a setiau data gwerthuso, yn ffynhonnell agored](https://datainnovation.cardiff.ac.uk/is/wecy/access.html),
+ [Mewnblaniadau geiriau traws-ieithyddol Saesneg-Cymraeg gyda chod hyfforddi a theclyn dadansoddi sentiment, yn ffynhonnell agored](https://github.com/cardiffnlp/en-cy-bilingual-embeddings).

Dyma bwnc doeddwn i heb weithio arno o'r blaen, felly roeddwn eisiau ysgrifennu crynodeb yn cyflwyno'r gwaith.

# Mewnblaniadau geiriau?
Cynrychioliadau fector o eiriau yw mewnblaniadau geiriau. Maen nhw'n mapiad rhwng pob gair mewn iaith ag $$\mathbb{R}^n$$, y set o fectorau $$n$$-dimensiwn o rifau real. Felly, er enghraifft, gall y gair "eliffant" cael ei mapio i'r fector:

$$\mathbf{v}_{\text{eliffant}} = \{0.75, 3.43, -1.22, 1.91, -0.44, -5.72\}$$


Gall y rhain fod yn defnyddio er mwyn meintioli a disgrifio perthnasoedd semanteg mewn iaith fectorau. Felly, mewn set o fewnblaniadau geiriau 'da' rydym eisiau i'r perthnasoedd rhwng y fectorau adlewyrchu'r perthnasoedd cyfatebol rhwng y geiriau. Er mwyn gallu cofnodi digon o wybodaeth ar gyfer hwn, fel arfer dewision $$n$$ i fod rhwng 100 a 500. Os caiff y wybodaeth hon ei gofnodi, yna dylen ni gallu arsylwi:

+ bod fectorau o eiriau gyda pherthynas agos eu hunain fod wedi lleoli'n agos, e.e. wedi symleiddio mewn dau-dimensiwn:
  
  <img src="{{site.baseurl}}/images/mewnblaniadau_enghraifft.png" width="450">{: .center-image }

+ a bod meintiau a chyfeiriadau rhwng fectorau yn hafal os yw'r ystyr semanteg rhwng eu geiriau yn hafal, e.e. $$\mathbf{v}_{\text{mab}} - \mathbf{v}_{\text{merch}} = \mathbf{v}_{\text{actor}} - \mathbf{v}_{\text{actores}}$$. Gallwn weld trwy ail-drefni fod gan y mewnblaniadau'r pŵer i ragfynegi o'r cyd-destun geiriau anhysbys neu sydd heb ei weld o'r blaen.


# Sut?
Mae unrhyw fapiad rhwng geiriau â fectorau unigryw yn fewnblaniadau geiriau. Ond gall mewnblaniadau geiriau da, rheini sy'n dangos y priodweddau dymunol hyn, cael eu hyfforddi ar gorpws mawr o destun. Corpws yw nifer mawr o frawddegau, hynny yw geiriau *yn eu cyd-destun*. Mae nifer o algorithmau ar gael er mwyn gwneud hwn, ac maent yn dibynnu ar [ddamcaniaeth semanteg ddosrannol](https://en.wikipedia.org/wiki/Distributional_semantics), sy'n nodi bod gan eiriau sy'n ymddangos mewn cyd-destunau tebyg ystyr tebyg.

Ystyrion ni dau algorithm, *Skip-gram* a *CBOW*. Yn gyffredinol mae'y rhain yn pasio trwy'r corpws yn edrych ar bob gair yn ei dro, a'i ffenestr cyd-destun, hynny yw ei $$k$$ gair agosaf yn ei frawddeg. Yna maent yn ceisio canfod fector ar gyfer pob gair sy'n uchafsymio'r tebygoliaeth-log o ganfod y gair hwnna yn y ffenestr cyd-destun honno (neu, yn dibynnu ar yr algorithm, y tebygoliaeth-log o ganfod y ffenestr cyd-destun honno o gwmpas y gair hwnnw), lle diffinnir y tebygolrwydd gan y pellter SoftMax rhwng fector y gair a fectorau'r geiriau yn y ffenestr cyd-destun.

Mae amrywiadau eraill ystyrion ni oedd trin is-eiriau neu eiriau rhannol ar wahanol, sy'n ddefnyddiol mewn ieithoedd gyda morffoleg gyfoethog. Mae'r algorithmau hyn ar gael yn y llyfrgell Python ffynhonnell agored [`gensim`](https://radimrehurek.com/gensim/index.html).

Heb os, prif ffynhonnell ansawdd mewnblaniadau geiriau, yn enwedig mewn ieithoedd prin eu hadnoddau megis Cymraeg, yw maint ac ansawdd y corpws hyfforddi. Rydw i'n siarad am hwn, a sut gallwn ni gyd helpu, yn [blog arall](/2020/11/06/wicipedia-cymraeg/). Casglon ni corpws o 92,963,671 o eiriau, yn casglu o nifer o is-gorpera llai gan gynnwys Wicipedia Cymraeg, trafodion y cynulliad cenedlaethol, wefannau newyddion BBC, nifer o gofnodion ar y cyfryngau cymdeithasol, CorCenCC, y Beibl, Gwerddon, a mwy o blogiau, cylchgronau a thestunau academaidd.

Ar ôl hyfforddi'r corpws ar nifer o setiau o'r tra-baramedrau'r algorithmau, dewision ni'r mewnblaniadau a berfformiodd orau, ac maent ar gael fan hyn: [https://datainnovation.cardiff.ac.uk/is/wecy/access.html](https://datainnovation.cardiff.ac.uk/is/wecy/access.html).

# Pa mor dda ydynt?
Unwaith caiff ei lawr-lwytho gallwn lwytho'r mewnblaniadau geiriau hyn gyda:

{% highlight python %}
import gensim
from gensim.models.callbacks import CallbackAny2Vec

class EpochLogger(CallbackAny2Vec):
    '''Callback to log information about training'''

    def __init__(self):
        self.epoch = 0

    def on_epoch_begin(self, model):
        print("Epoch #{} start".format(self.epoch))

    def on_epoch_end(self, model):
        print("Epoch #{} end".format(self.epoch))
        self.epoch += 1

model = gensim.models.FastText.load('FastText_WNLT_SkipGram/skipgram_subword_model.model')
{% endhighlight %}

Nawr bod gennym y model wedi llwytho, edrych ar y mewnblaniadau geiriau. Beth yw'r fector sy'n cyfateb i'r gair "nofio"?

{% highlight python %}
>>> model.wv['nofio']
{% endhighlight %}

Mae hwn yn rhoi fector hir iawn o rifau, ac nid yw'n ddarllenadwy iawn. Gallwn ganfod y 10 fector agosaf i hwn, a'i geiriau cyfatebol. Y mesur safonol o 'agosrwydd' rhwng fectorau yn y cyd-destun hwn yw'r [tebygrwydd cosin](https://en.wikipedia.org/wiki/Cosine_similarity):

{% highlight python %}
>>> model.wv.most_similar(positive=['nofio'], topn=10)
[('nofiol', 0.6012746095657349),
 ('nofiodd', 0.5929412841796875),
 ('nofi', 0.5893375277519226),
 ('pwll', 0.5836290717124939),
 ('swimsuit', 0.5183103084564209),
 ('heicio', 0.5182317495346069),
 ('canwio', 0.5022277235984802),
 ('rhwyfo', 0.4894988536834717),
 ('caiacio', 0.4887942969799042),
 ('phlymio', 0.48672929406166077)]
{% endhighlight %}

Fan hyn gwelwn eiriau tebyg: cwpl o gamsillafiadau, `nofiodd`, `pwll`, `swimsuit` yn Saesneg, `heicio`, `canwio` , `rhwyfo`, `caiacio`, a `phlymio`.

Beth am ragfynegi geiriau newydd? Uchod nodwn gallwn ragfynegi'r fector ar gyfer "actores" trwy ail-drefnu'r hafaliad sy'n nodi hafaledd gwahaniaethau'r fectorau: $$\mathbf{v}_{\text{actores}} = \mathbf{v}_{\text{actor}} - \mathbf{v}_{\text{mab}} + \mathbf{v}_{\text{merch}}$$:

{% highlight python %}
>>> actor, mab, merch = model.wv['actor'], model.wv['mab'], model.wv['merch']
>>> dyfaliad_actores = actor - mab + merch
>>> model.wv.most_similar(positive=[dyfaliad_actores], topn=10)
[('actor', 0.7876081466674805),
 ('actores', 0.7131889462471008),
 ('actorion', 0.5787793397903442),
 ('berfformwraig', 0.5728527307510376),
 ('comediwraig', 0.5709209442138672),
 ('digrifwraig', 0.5636816024780273),
 ('sgriptwraig', 0.5622066259384155),
 ('athletwraig', 0.5469273328781128),
 ('merch', 0.5440044403076172),
 ('actoresau', 0.5389758944511414)]
{% endhighlight %}

Mae nifer o'r geiriau hyn yn agos iawn i ystyr "actores": `actor`, `actores`, `actorion`, `berfformwraig`, `comediwraig` a `digrifwraig`, `sgriptwraig`, `athletwraig`, `merch`, ac `actoresau`.

Dyma un enghraifft yn unig o berthynas gramadegol rhwng geiriau, cyfnewid rhywedd. Mae perthnasoedd eraill gallwn eu gwirio yn gynnwys rhedeg y berfau, ansoddeiriau a'i eithafion lluosogion, a hyd yn oed gwledydd a'u cenedligrwyddau. Un perthynas gramadegol a gwirion ni sy'n arbennig i Gymraeg oedd geiriau cyfatebol yn dafodieithoedd y De a'r Gogledd.

Awtomeiddion ni'r proses gwirio a gwerthuso hwn ar nifer mawr o enghreifftiau safonol er mwyn cael ystadegau mesurol o werthusiad er mwyn cymharu'r modelau. Yn wir, rhan fawr o'r gwaith oedd datblygu rhestrau safonol o eiriau cymaradwy a strwythurau gramadegol i ddefnyddio ar gyfer y Gymraeg am y tro cyntaf. Mae tasgau gwerthuso arall yn cynnwys defnyddio'r mewnblaniadau geiriau er mwyn canfod geiriau cyfystyr, a thasgau clystyru geiriau. Serch hynny, roedd gwerthusiad ansoddol ar raddfa lai gan siaradwr Cymraeg (fi!) hefyd yn rhan hollbwysig o'r proses gwerthuso.


# Beth yw'r pwynt?

Mae cynnwys mewnblaniadau geiriau fel rhan o dasgau prosesu iaith naturiol ([NLP](https://en.wikipedia.org/wiki/Natural_language_processing)) wedi dangos i wella'u perfformiad, yn enwedig mewn ieithoedd prin eu hadnoddau lle efallai mai data hyfforddi yn anodd cael caffael arno. Un rheswm am hyn yw bod mewnblaniadau geiriau yn helpu modelau 'deall' geiriau nad ydynt wedi gweld o'r blaen yn y data hyfforddi.

Gan gymryd y syniad hwn ymhellach, mae modelau yn ieithoedd prin eu hadnoddau yn gallu buddio o fewnblaniadau geiriau traws-ieithyddol, yn cymryd mantais o iaith arall, sydd a digon o adnoddau. Mae mewnblaniadau geiriau traws-ieithyddol yn fapiad o eiriau o ddwy iaith i mewn i ofod fector a rennir, wedi'i gadw gyda'i gilydd ond ar wahanol. Gallwn feddwl am hyn fel 'alinio' dau set o fewnblaniadau geiriau o ddwy iaith wahanol.
Felly gallwn hyfforddi model NLP o iaith brin eu hadnodd ar ddata mewn iaith mwy yn unig!

Hyfforddon ni mewnblaniadau geiriau traws-ieithyddol Saesneg-Cymraeg, sydd ar gael fan hyn: [https://github.com/cardiffnlp/en-cy-bilingual-embeddings](https://github.com/cardiffnlp/en-cy-bilingual-embeddings).

Hefyd yn y linc yna mae cyfarwyddiadau ar gyfer hyfforddi model dadansoddi sentiment traws-ieithyddol. Mae model [dadansoddi sentiment](https://en.wikipedia.org/wiki/Sentiment_analysis) yn fodel dysgu peirianyddol dan oruchwyliaeth sy'n rhagfnyegi sentiment brawddeg (positif, niwtral, negatif). Gallwch hyfforddi'r un yma ar ddata Saesneg yn unig, yn yr achos hwn adolygiadau IMDB, ond gall cael ei ddefnyddio ar dasgau iaith Cymraeg, er nad yw'r model wedi gweld data hyfforddi Cymraeg!


