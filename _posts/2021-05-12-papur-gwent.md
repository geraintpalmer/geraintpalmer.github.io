---
layout     : post
title      : "Allosod galw ar draws daearyddiaethau"
language   : cymraeg
comments   : true
---

Cyhoeddwyd ein papur diweddaraf ar-lein yn ddiweddar: ["Modelling changes in healthcare demand through
geographic data extrapolation"](https://www.tandfonline.com/doi/full/10.1080/20476965.2021.1906764), gyda [Paul Harper](https://sites.google.com/site/profpaulharper/home), [Vincent Knight](https://vknight.org/), ac Cathy Brooks yn y cyfnodolyn Health Systems. Yn anffodus, mae'r papur tu ôl i wal dâl, felly dyma grynodeb bach.

Roedd y gwaith yn rhan o'm PhD, lle gweithiais gyda [Bwrdd Iechyd Prifysgol Aneurin Bevan](https://bipab.gig.cymru/) yng Ngwent, De Ddwyrain Cymru, i geisio modelu effaith roedd ymyriad gofal iechyd newydd yn cael ar anghenion gofal iechyd poblogaeth, yn arbennig y galw mewn sawl cyfleuster gofal iechyd amrywiol.
Fe elwir yr ymyriad yn Stay Well Plans (SWPau), a fe'i cynigwyd i is-set o'r boblogaeth pobl dros 60 mlwydd oed.
Felly, yn ddelfrydol, byddwn yn dewis is-set wir ar hap o'r boblogaeth i'w cynnig SWP, recordio'r gweithgareddau gofal iechyd cyn ac ar ôl iddynt gael eu cynnig, a'u cymharu. Defnyddiwn y data cyn ac ar ôl i barametreiddio model o'r galw am ofal iechyd, rhedeg y model, a chymharu'r canlyniadau.

Ond, dechreuodd y gwaith hwn ar ôl i'r cynllun dechrau.
Felly nid oeddwn yn casglu'r holl ddata priodol er mwyn gwneud hynny.
Yn bwysig, ond i is-set o boblogaeth Sir Casnewydd cafodd y SWPau treialu eu cynnig, ac roeddwn ni eisiau gwerthuso'u heffaith ar draws Gwent cyfan, sy'n cynnwys Sir Casnewydd a phedwar sir arall.
Felly ein tasg oedd allosod paramedrau'r model ar gyfer y siroedd eraill yng Ngwent, o'r paramedrau ar gyfer Sir Casnewydd.
Gwnaethon ni hwn trwy addasu ar gyfer tri ffactor roeddwn ni'n eu credu i fod yn wahaniaethau sylfaenol rhwng daearyddiaethau a demograffegau'r siroedd.

# Y Model

Adeiladon fodel system gyfan o'r llif claf, yn cynnwys gofal argyfwng, eilaidd, cymuned, a phreswyl, fel y dangosir isod.

<img src="{{site.baseurl}}/images/gwent_pathway.png" width="700">{: .center-image }

Caiff hwn ei model fel [model Markov](https://en.wikipedia.org/wiki/Markov_model), wedi'i paramedreiddio gan wahanol gyfraddau dyfodi, cyfraddau gwasanaeth, a thebygolrwyddau trosi ar gyfer y bobl o bob sir wahanol.
Ymhellach, o fewn pob sir gallwn adnabod tri math o unigolyn: nhw ni chynigwyd SWP iddynt (gan eu bod yn ddigon iachus i beidio ei angen), nhw y cynigwyd SWP a'i derbyn, a nhw y cynigwyd SWP a'i gwrthod. Bydd gan bob un o rain set o baramedrau ei hun hefyd.

Ond mae gennym baramedrau Casnewydd yn unig. Beth allwn ni gwneud?

# Y Fethodoleg

Canfuom ni tri gwahaniaeth pwysig rhwng y siroedd roeddwn yn credu gall effeithio ar y galw am wasanaethau gofal iechyd: maint poblogaethau (po fwyaf y boblogaeth, po fwyaf y galw); lefelau amddifadedd (credir po fwyaf amddifad mae ardal, y llai tebygol bydd ei thrigolion o dderbyn SWP); a phellteroedd i'r ysbytai (mae pobl yn fwy tebygol o fynychu eu hysbyty agosaf).

1. *Maint poblogaeth*:

   Mae hwn eithaf syml: ar gyfer pob sir, rydym yn lluosi'r gyfradd galw gan $$\frac{N_c}{N}$$, lle $$N_c$$ yw maint poblogaeth y sir, ac $$N$$ yw poblogaeth y maint poblogaeth yr is-set treial gwreiddiol.

2. *Lefel amddifadedd*:
   
   Edrychon ar y perthynas rhwng lefelau amddifadedd (gan ddefnyddio'r [Mynegai Amddifadedd Lluosog Cymru](https://wimd.gov.wales/?lang=cy) (WIMD), sy'n trefnu pob Ardal Cynnyrch Ehangach Haen Is (LSOA) yng Nghymru) a thebygolrwydd derbyn SWP o fewn yr is-set treial gwreiddiol. Roeddwn yn lwcus iawn fan hyn. Mae Gwent yn amrywiol i'r eithaf o ran amddifadedd, mae'n cynnwys yr ardal fwyaf a'r ardal leiaf amddifad yng Nghymru, gyda gwahaniaethau mawr rhwng yr ardaloedd gwledig cyfoethog a'r cymoedd ôl-ddiwydiannol llai cyfoethog. Yn ffodus, mae Sir Casnewydd, o le ddaeth ein his-set treial gwreiddiol, yr un mor amrywiol. Adeiladon ni model [atchweliad logistaidd](https://en.wikipedia.org/wiki/Logistic_regression) i ddisgrifio a rhagfynegi tebygolrwydd derbyn SWP o'r lefel amddifad.

   ![]({{site.baseurl}}/images/gwent_logistic.png)

   Er nad yw'r perthynas yn edrych yn gryf, mae'r ystadegol ystyrlon, ac yn bwysig mae'n cyd-fynd gyda barn arbenigwyr yn y bwrdd iechyd. Felly, defnyddiwn ni'n atchweliad logistaidd o fewn pob LSOA i ragfynegi'r nifer o bobl sy'n derbyn neu wrthod SWP, a'u cydgasglu ar draws y siroedd. Yna gallwn addasu'r gyfradd galw yn briodol.

3. *Pellteroedd i'r ysbytai*:
   
   Nawr mae angen edrych ar y pellteroedd i bob un o'r tri ysbyty yn y model hwn: Ysbyty Brenhinol Gwent yn ninas Casnewydd, Ysbyty Nevill Hall yn Y Fenni, ac Ysbyty Ystrad Fawr yn Ystrad Mynach. Tybiwn fod y tebygolrwydd o fynychu pob un ysbyty mewn cyfrannedd gwrthdro bras i'r pellter cymharol i'ch gartref. Yn fanwl cywir:

   $$a_{gl} = \frac{w_g d_{gl}^{-n}}{\sum_j w_j d_{jl^n}}$$

   lle $$a_{gl}$$ yw'r gyfran o bobl o LSOA $$l$$ sy'n mynd i ysbyty $$g$$; $$w_g$$ yw maint ysbyty $$g$$, $$d_{gl}$$ yw'r pellter o LSOA $$l$$ i ysbyty $$g$$, ac mae'r swm dros y tri ysbyty.
   Mae $$n$$ yn dra-baramedr y gellir ei diwnio i ffitio'r model i ddata'r is-set treial gwreiddiol.
   Unwaith bod gennym rhain ar gyfer pob LSOA, gallwn eu cyd-gasglu ar draws eu poblogaethau er mwyn cael y tebygolrwyddau cymharol o fynd i bob ysbyty o bob sir:

   <img src="{{site.baseurl}}/images/gwent_distances.png" width="800">{: .center-image }

   Nawr, cofiwch ddaeth pob cyfradd galw a thebygolrwydd trosi sylfaenol o'r is-set treial gwreiddiol, hynny yw o Gasnewydd. Felly ar gyfer pob un i'r siroedd eraill, rydym yn rhannu'r rhain gyda'r tebygolrwyddau y cyfrifon ar gyfer Casnewydd, a'u lluosi gyda'r tebygolrwyddau y cyfrifon ar gyfer y sir honno. Mae gan hwn yr effaith o symud y galw gofal iechyd i'r ysbytai eraill mewn cyfrannedd gyda'u pellteroedd cymharol i'r poblogaethau maent yn gweinyddu.

Rhoddir y model llawn wedi'i paramedreiddio yn y papur.
Yna defnyddiwn fodelau Markov wedi'u cyd-gasglu i ganfod y galw effeithiol ym mhob cyfleuster gofal iechyd.
Er mwyn ystyried peth o wybodaeth ar yr amrywioldeb, rydyn hefyd yn rhedeg [efelychiad Monte Carlo](https://en.wikipedia.org/wiki/Monte_Carlo_method), gan dybio [dyfodiadau Poisson](https://en.wikipedia.org/wiki/Poisson_distribution).

# Y Canlyniadau

Caiff y model ei ddefnyddio er mwyn rhedeg tri senario, trwy newid y ffracsiwn o'r boblogaeth y cynigir SWP iddynt ym mhob sir:

1. Beth os ni chynigir SWPau? (y gorffennol)
2. Beth os ond cynigir SWPau yng Nghasnewydd? (y presennol)
3. Beth os cynigir SWPau ym mhob sir yng Ngwent? (y dyfodol)

Dangosir canlyniadau'r model Markov (sêr) a'r efelychiadau Monte Carlo (plotiau bocs a ffidl) isod:

<img src="{{site.baseurl}}/images/gwent_results.png" width="800">{: .center-image }

Yn bennaf roedd hwn yn dangos bod cynnig SWPau yn gallu achosi ailddosbarthiad o'r galw ar draws y gwasanaethau breuder; cynnydd mawr yn y galw ar gyfer gwasanaethau gofal cymuned; a lleihad mawr yn y galw ar gyfer gofal preswyl.
Roedd hwn yn ffafriol, gan ei fod yn awgrymu bod y SWPau yn gwneud eu swydd, sef cynnig i gleifion gofal yn y gymuned a'u cadw yn eu cartrefi eu hunain am hirach.

Yn y [papur](https://www.tandfonline.com/doi/full/10.1080/20476965.2021.1906764) rydym hefyd yn cynnig modelu pellach, yn ystyried newid demograffegau yn y dyfodol, a golwg agosach ar y galw am ofal preswyl. Cafodd y gwaith ei drafod hefyd yn fy [noethuriaeth PhD](http://orca.cf.ac.uk/117490/), lle defnyddiais i'r canlyniadau er mwyn ystyried goblygiadau i'r gweithlu.
