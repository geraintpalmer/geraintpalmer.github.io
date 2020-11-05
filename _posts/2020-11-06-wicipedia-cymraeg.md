---
layout     : post
title      : "Pwysigrwydd Wicipedia i Brosesu Iaith Naturiol"
language   : cymraeg
comments   : true
---

Blwyddyn ddiwethaf dechreuais i brosiect ymchwil yn cydweithio gydag [Irena Spasic](http://users.cs.cf.ac.uk/I.Spasic/index.html), [Padraig Corcoran](https://www.cardiff.ac.uk/people/view/155896-corcoran-padraig), [Dawn Knight](https://www.cardiff.ac.uk/people/view/142032-knight-dawn) a [Laura Arman](https://www.corcencc.org/laura-arman/), yn hyfforddi mewnblaniadau geiriau ar gyfer yr iaith Cymraeg. Model yw hwn (mapiad o eiriau i fectorau) sy'n ddefnyddiol mewn nifer o gymwysiadau prosesu iaith naturiol (NLP) defnyddiol megis cyfieithu peirianyddol, dadansoddiad sentiment, adnabod endidau, a pharsio dibyniaethau. [Cyflwynais]({{ site.url }}/talks/mewnblaniadaugeiriau2020.pdf) rannau o'r gwaith yn wythnos yma yn [Symposiwm Offer ac Adnoddau Technoleg Iaith Cymru](https://symposiwm2020.bangor.ac.uk/rhaglen). Mae'r profiad o weithio ar y prosiect hwn wedi rhoi i fi gwerthfawrogiad o bwysigrwydd [Wicipedia](https://cy.wikipedia.org/wiki/Hafan) i ddatblygu modelau NLP Cymraeg a thechnolegau iaith.

Mae'r iaith Gymraeg yn dioddef o fodelau a thechnolegau iaith gyntefig o gymharu ag ieithoedd mwy. Mae hwn yn gwneud defnyddio'r iaith Gymraeg yn anoddach. Mae enghraifft o hwn wrth ddefnyddio Wicipedia ei hun - mae'r teclyn chwilota ar y fersiwn Saesneg yn gallu adnabod camsillafiadau, morffolegau, ac amrywiadau yn ffurf teitl yr erthygl; tra ar y fersiwn Cymraeg mae angen teipio'r teitl yn union, gan gynnwys treigladau a banodau, oherwydd mae'r modelau iaith hyn naill ai ddim ar gael neu ddim yn cael eu defnyddio yn y Gymraeg. Serch hynny mae newyddion da. Roedd yn braf yn y Symposiwm clywed am lwyth o brosiectau NLP newydd fel teclynnau destun-i-lefaredd ac adnabod rhannau ymadrodd.

Mae unrhyw fodel dysgu peirianyddol ond mor dda â'r data y caiff ei hyfforddi arno. Yn achos NLP, y data yw *corpws*, sef casgliad o eiriau mewn cyd-destun, hynny yw swmp mawr o frawddegau. Roedd yn ddiddorol clywed yn y Symposiwm bod casglu corpws Cymraeg digon mawr i hyfforddi modelau NLP a thechnolegau iaith eraill yn sialens ar draws y maes. Ar gyfer ieithoedd prin eu hadnodd, fel Cymraeg a Basgeg, un o'r ffynonellau mwyaf o ran maint, mwyaf hygyrch, mwyaf amrywiol, a mwyaf amlwg yw Wicipedia. Hefyd, Wicipedia yw'r ffynhonnell corpws lle gall unrhyw un cyfrannu ato a'i wella.

Mae Wicipedia Cymraeg ond yn bodoli achos mae gwirfoddolwyr gwych yn gweithio'n galed i gyfrannu ato a'i gynnal. Wrth sylweddoli hyn, penderfynais y galla i roi nôl i Wicipedia, felly dechreuais gyfrannu ato. O Dachwedd 2019 hyd heddiw rydw i wedi ychwanegu 124 erthygl (isod), yn bennaf trwy gyfieithu ac addasu erthyglau Saesneg. Roeddwn i'n canolbwyntio ar ddau agwedd pwysig: cynyddu nifer o eiriau yn y prosiect, a chynyddu amrywiad yr erthyglau sydd yn y prosiect.

+ ***Nifer o eiriau:*** Mae cynyddu nifer o frawddegau yn Wicipedia yn cyfrannu'n uniongyrchol i ansawdd modelau NLP. Mae maint Wicipedia hefyd yn dylanwadu sut mae eraill yn gweld yr iaith, ac efallai hefyd at barodrwydd ymchwilwyr i geisio datblygu modelau yn yr iaith. 

  Mae nifer o [egin](https://cy.wikipedia.org/wiki/Wicipedia:Eginyn) (erthyglau bach bach iawn, braidd brawddeg[^1]) ar Wicipedia Cymraeg yn fawr, ac yn cynyddu trwy'r amser. Mae'r graff isod yn dangos dosraniad nifer o eiriau yn erthyglau Wicipedia (data o 17-10-2020, tua 132 mil o erthyglau). Mae gan hanner yr erthyglau ond 77 gair neu lai, a 63% o erthyglau 92 gair neu lai. Hynny yw mae gan 63% o erthyglau Wicipedia llai o eiriau na'r paragraff hon, a llai nag 0.7% sy'n hirach na'r blog hwn. Felly dwi'n ceisio ychwanegu erthyglau gyda digon o gynnwys.

  ![]({{site.baseurl}}/images/article-lengths-cy.png){: .center-image }


+ ***Amrywiaeth:*** Mae amrywiaeth corpws yn bwysig i NLP. Mae technolegau iaith sydd ond wedi'u hyfforddi ar gorpws arbenigol ond yn mynd i fod yn ddefnyddiol ar gyfer cymwysiadau yng nghyd-destun yr arbenigedd hynny. Mae technolegau iaith sydd wedi'u hyfforddi ar gorpws digon amrywiol yn mynd i fod yn ddefnyddiol ar gyfer amryw o gymwysiadau. Ymhellach, yn fwyfwy nawr datblygir modelau NLP aml-ieithog, sy'n medru gwneud defnydd o adnoddau a chorpera enfawr un iaith er mwyn gwella cymwysiadau mewn iaith arall lleiafrifol. Gall y modelau hyn gwella os yw'r ddau gorpera, er o feintiau gwahanol, yn gyfatebol, hynny yw yn ymdrin â'r un pynciau. Mae cael erthyglau Wicipedia ar ystod eang o bynciau, efallai rhyngwladol neu'n gyffredinol yn eu natur, yn gallu helpu.

  Yn ogystal â hwn, mae Wicipediau ieithoedd lleiafrifol yn cyflawni'r swydd o *gynrychiolaeth*,[^2] maen nhw'n adlewyrchu a chynrychioli diwylliant a diddordebau siaradwyr yr iaith honno ar lwyfan rhyngwladol. Er mwyn sicrhau bod Wicipedia, a'r technolegau iaith sydd wedi'u hyfforddi arno, yn cynrychioli fy niddordebau a'n agweddau[^3] i, mae angen i fi fod yn rhan o'i ddatblygiad. Mae cyfrannu'ch llais i gorpws sy'n cael ei ddefnyddio i astudio ac i ddatblygu technolegau iaith yn golygu eich bod yn dilysu'ch llais. Hynny yw mae'n cadarnhau pwysigrwydd eich diddordebau, geiriau, termau, a defnydd iaith, ac yn sicrhau bod y rhain yn cael eu cynrychioli mewn datblygiadau a thechnolegau iaith. Felly dwi'n ceisio ychwanegu erthyglau o ystod eang o'm ddiddordebau.

Rydw i wedi crynhoi fy meddyliau ar hwn yn y [diagram dolen achosol](https://cy.wikipedia.org/wiki/Diagram_dolen_achosol) isod, mae saeth du'n golygu bod cynnydd yn un yn achosi cynnydd yn y llall, tra bod saeth goch yn golygu bod cynnydd yn un yn achosi lleihad yn y llall. Barn fi yn unig yw hon:

![]({{site.baseurl}}/images/causal-loop.png){: .center-image }

Dyma'r 124 erthygl Wicipedia rydw i wedi cyfrannu yn y flwyddyn ers Tachwedd 2019, yn y drefn creais i nhw, ac wrth gwrs mae cyfranwyr eraill wedi eu golygu, gwirio a'u gwella:

<div style="column-count: 3">
<ul>
<li><a href='https://cy.wikipedia.org/wiki/Hock'>Hock</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Loretta_Lynn'>Loretta Lynn</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Neverwhere_(nofel)'>Neverwhere (nofel)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Oatman,_Arizona)'>Oatman, Arizona</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Community_(cyfres_teledu)'>Community (cyfres teledu)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Emma_o_Normandi'>Emma o Normandi</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Siarter_y_Goedwig'>Siartr y Goedwig</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Lliwio_graffiau'>Lliwio graffiau</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Un_clip_papur_coch'>Un clip papur coch</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Diners,_Drive-Ins_and_Dives'>Diners, Drive-Ins and Dives</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_Simpson'>Paradocs Simpson</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Palas_Herrenhausen'>Palas Herrenhausen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Los_Angeles_Dodgers'>Los Angeles Dodgers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Faróc_Edwardaidd'>Pensaernïaeth Faróc Edwardaidd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Tonkatsu'>Tonkatsu</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_y_morlin'>Paradocs y morlin</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cawl_cregyn_bylchog'>Cawl cregyn bylchog</a></li>
<li><a href='https://cy.wikipedia.org/wiki/G%C3%AAm_bywyd_Conway'>Gêm bywyd Conway</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Only_Connect'>Only Connect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/We_Didn%27t_Start_the_Fire'>We Didn't Start the Fire</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Priodas_y_Dywysoges_Elisabeth_a_Philip_Mountbatten'>Priodas y Dywysoges Elisabeth a Philip Mountbatton</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Corn_Gabriel'>Corn Gabriel</a></li>
<li><a href='https://cy.wikipedia.org/wiki/HMY_Britannia'>HMY Britannia</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Dilema%27r_carcharorion'>Dilema'r carcharorion</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Iwffoleg'>Iwffoleg</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Peiriant_ffa'>Peiriant ffa</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Problem_darnau_arian'>Problem darnau arian</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddf_Little'>Deddf Little</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Parc_Griffith'>Parc Griffith</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_Streisand'>Effaith Streisand</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Plymio_sgwba'>Plymio sgwba</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bitterballen'>Bitterballen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Googie'>Pensaernïaeth Googie</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pad_thai'>Pad Thai</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Sieri'>Sieri</a></li>
<li><a href='https://cy.wikipedia.org/wiki/SS_Great_Britain'>SS Great Britain</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coeden_rhychwantu_leiaf'>Coeden rhychwantu leiaf</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llwybr_Hamiltonaidd'>Llwybr Hamiltonaidd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Star-Spangled_Banner_(baner)'>Star-Spangled Banner (baner)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Kirsty_MacColl'>Kirsty MacColl</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_cobra'>Effaith cobra</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Parks_and_Recreation'>Parks and Recreation</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Banff,_Alberta'>Banff, Alberta</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddfau_Lanchester'>Deddfau Lanchester</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llwybr_Euleraidd'>Llwybr Euleraidd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coridor_Vasari'>Coridor Vasari</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Art_Deco'>Pensaernïaeth Art Deco</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Sosej_cytew'>Sosej cytew</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cydran_gysylltiedig'>Cydran gysylltiedig</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Prifysgol_Twente'>Prifysgol Twente</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Microgenedl'>Microgenedl</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_hydra'>Effaith hydra</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Moana'>Moana</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_Downs%E2%80%93Thomson'>Paradocs Downs-Thomson</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cities:_Skylines'>Cities: Skylines</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Damcaniaeth_amser_rhithiol'>Damcaniaeth amser rhithiol</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Dwight_Yoakam'>Dwight Yoakam</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Santa_Monica,_California'>Santa Monica, Califfornia</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_Thatcher'>Effaith Thatcher</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coron_Sant_Edward'>Coron Sant Edward</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Francisco_de_Zurbar%C3%A1n'>Francisco de Zurbarán</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddf_niferoedd_mawr'>Deddf niferoedd mawr</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bara_banana'>Bara banana</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bragdy_Van_Honsebrouck'>Bragdy Van Honsebrouck</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Synesthesia'>Synesthesia</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Six_(sioe_gerdd)'>Six (sioe gerdd)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Jonas_Jonasson'>Jonas Jonasson</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bomio_edau'>Bomio edau</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Imiwnedd_cenfaint'>Imiwnedd cenfaint</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Manhattanhenge'>Manhattanhenge</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Matanzas'>Matanzas</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Stroganoff_cig_eidion'>Stroganoff cig eidion</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bwystfilod_y_Frenhines'>Bwystfilod y Frenhines</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Judoon'>Judoon</a></li>
<li><a href='https://cy.wikipedia.org/wiki/T%C5%B7_Petersen'>Tŷ Petersen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Egwyddor_dwll_colomen'>Egwyddor twll colomen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cracking_the_Cryptic'>Cracking the Cryptic</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Twyllresymeg_y_chwimsaethwr_o_Decsas'>Twyllresymeg y chwimsaethwr o Decsas</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Baner_Mecsico_Newydd'>Baner Mecsico Newydd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Hafaliadau_Cauchy%E2%80%93Riemann'>Hafaliadau Cauchy-Riemann</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Koppelpoort'>Koppelpoort</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Rhif_Bell'>Rhif Bell</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cerddoriaeth_bachata'>Cerddoriaeth bachata</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cydweddiad_(damcaniaeth_graffiau)'>Cydweddiad (damcaniaeth graffiau)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Theatr_Tsieineaidd_Grauman'>Theatr Tsieineaidd Grauman</a></li>
<li><a href='https://cy.wikipedia.org/wiki/El_Escorial'>El Escorial</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llofruddiaethau_Tylenol_Chicago'>Llofruddiaethau Tylenol Chicago</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Nintendo_Switch'>Nintendo Switch</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pa%C3%ABla'>Paëla</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bias_goroesedd'>Bias goroesedd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Amrywiant'>Amrywiant</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Medal_Fields'>Medal Fields</a></li>
<li><a href='https://cy.wikipedia.org/wiki/The_Louvin_Brothers'>The Louvin Brothers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Twll_offeiriad'>Twll offeiriad</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Ieithoedd_Sbaen'>Ieithoedd Sbaen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/%22Deddf_niferoedd_gwirioneddol_fawr%22'>"Deddf niferoedd gwirioneddol fawr"</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Hallgr%C3%ADmskirkja'>Hallgrímskirkja</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pedwarawd_Anscombe'>Pedwarawd Anscombe</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Matrics'>Matrics</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Lil_Nas_X'>Lil Nas X</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Carlos,_Tywysog_Asturias'>Carlos, Tywysog Asturias</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Little_Shop_of_Horrors_(sioe_gerdd)'>Little Shop of Horrors (sioe gerdd)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Prawf_U_Mann%E2%80%93Whitney'>Prawf U Mann–Whitney</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cerddorion_Bremen'>Cerddorion Bremen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddfau_De_Morgan'>Deddfau De Morgan</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Neo-Andeaidd'>Pensaernïaeth Neo-Andeaidd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Amgueddfa_Hanes_Mecsico_Newydd'>Amgueddfa Hanes Mecsico Newydd</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Siboleth'>Siboleth</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Theorem_gwerth-cymedrig'>Theorem gwerth-cymedrig</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Integru_fesul_rhan'>Integru fesul rhan</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Seiffr_Caesar'>Seiffr Caesar</a></li>
<li><a href='https://cy.wikipedia.org/wiki/John_Mulaney'>John Mulaney</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Y_placiau_Pioneer'>Y placiau Pioneer</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Clystyru_k-cymedr'>Clystyru k-cymedr</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Planet_Zoo'>Planet Zoo</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Aladdin_(ffilm_2019)'>Aladdin (ffilm 2019)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Teyrnwialen'>Teyrnwialen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cadair_y_Coroni'>Cadair y Coroni</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Diagram_dolen_achosol'>Diagram dolen achosol</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Fileteado'>Fileteado</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bhaji'>Bhaji</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Annibyniaeth_(tebygolrwydd)'>Annibyniaeth (tebygolrwydd)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Algorithm_Dijkstra'>Algorithm Dijkstra</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cyfarfodydd_agos'>Cyfarfodydd agos</a></li>
</ul>
</div>

---

[^1]: mae nifer o honiadau bod nifer o erthyglau Wicipedia mewn rhyw iaith yn cyfrannu'n uniongyrchol tuag at gyllido'r iaith hwnnw ([enghraifft](https://cardiffstudentmedia.co.uk/gairrhydd/pam-bod-creu-wicin-wic-ed/), [enghraifft](https://www.youtube.com/watch?v=KSEN_HGGrT8)), er dwi fethu gweld tystiolaeth o hwn. Ond, mae'r egin hyn sgiwio gallu dehongli'r ystadegyn 'nifer o erthyglau' fel mesur o faint Wicipedia.
[^2]: gweler yr erthygl hon am enghraifft: [https://slate.com/technology/2019/08/welsh-wikipedia-google-translate.html](https://slate.com/technology/2019/08/welsh-wikipedia-google-translate.html)
[^3]: yn fy marn i mae gan Wicipedia Cymraeg bias 'gwleidyddiaeth hunaniaeth' - eto, dim ond trwy gyfrannu at y prosiect gall fy agweddau i gael eu cynrychioli.