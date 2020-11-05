---
layout     : post
title      : "The Importance of Wicipedia to NLP"
language   : english
comments   : true
---

Last year I started a research project collaborating with [Irena Spasic](http://users.cs.cf.ac.uk/I.Spasic/index.html), [Padraig Corcoran](https://www.cardiff.ac.uk/people/view/155896-corcoran-padraig), [Dawn Knight](https://www.cardiff.ac.uk/people/view/142032-knight-dawn) and [Laura Arman](https://www.corcencc.org/laura-arman/), training word embeddings for the Welsh language. This is a model (a mapping from words to vectors) that are useful in a number of downstream natural language processing (NLP) applications such as machine translation, sentiment analysis, entity recognition, and dependency parsing. [I presented]({{ site.url }}/talks/mewnblaniadaugeiriau2020.pdf) parts of this research this week at the [Wales Academic Symposium on Language Technologies](https://symposiwm2020.bangor.ac.uk/programme). The experience of working on the project has given me an appreciation of the importance of [Wicipedia](https://cy.wikipedia.org/wiki/Hafan) (the Welsh version of Wikipedia) to Welsh NLP models and language technologies.

The Welsh language suffers from primitive language models and technologies in comparison to larger languages. This makes using the Welsh language more difficult. There's an example of this on Wikipedia itself - the search tool on the English version can recognise mis-spellings, morphologies, and variations in the form of the article title; while on the Welsh version we have to type the title exactly, including mutations and accents, because these language models aren't available or aren't used in Welsh. Despite this there is good news. It was great at the Symposium to hear about a load of new NLP projects such as text-to-speech and part of speech recognition tools.

Any machine learning model is only as good as the data it is trained on. For NLP the data is a *corpus*, which is a collection of words in context, that is a big bunch of sentences. It was interesting to hear in the Symposium that collecting a large enough Welsh corpus to train NLP models and other language technologies is a challenge across the field. For low resource languages, such as Welsh and Basque, one of the biggest sources in terms of size, the most accessible, the most varied, and the most obvious, is Wicipedia. Also, Wicipedia is the corpus source that anyone can contribute to and improve.

Wicipedia only exists thanks to amazing volunteers that work hard contributing to and maintaining it. When I realised this, I decided that I could give back to Wicipedia, and started contributing to it. From November 2019 to now I have added 124 articles (below), mainly by translating and adapting English articles. I was concentrating on two important aspects: increasing the number of words in the project, and increasing the variety of articles in the project.

+ ***Number of words:*** Increasing the amount of sentences on Wicipedia contributes directly to the quality of NLP models. Wicipedia's size also influences how others see the language, and prehaps also at the readiness of researchers to attempt to develop models in the language.

  There number of [stubs](https://en.wikipedia.org/wiki/Wikipedia:Stub) (very very short articles, hardly a sentence[^1]) on Welsh Wicipedia is massive, and increasing all the time. The graph below shows the distribution of numbers of words in Wicipedia articles (data from 17-10-2020, around 132 thousand articles). Half the articles have just 77 words or less, and 62% of articles have 90 words or less. That is, 62% of Wicipedia articles have less words than this paragraph, and less than 0.7% are longer than this blog. Therefore I'm trying to add articles with plenty of content.

  ![]({{site.baseurl}}/images/article-lengths-en.png){: .center-image }


+ ***Variety:*** A corpus's diversity is important for NLP. Language technolodies trained on a specialist corpus are only going to be useful in applications in that specialised context. Language technologies trained on a diverse enough corpus will have uses in a variety of applications. Furthermore, more and more multi-lingual NLP models are being developed, which can make use of resources and huge corpera in one language to improve models and applications in another minority or low resource language. These models may improve if the two corpera, although different sizes, are comparable, that is they are about the same topics. Having Wicipedia articles on a wide range of topics, prehaps with an international or generalised nature, can help.

  Also, minority language Wikipedias fulfil the function of *representation*,[^2] they reflect and represent the culture and interests of that language's speakers on an international stage. In order to ensure that Wicipedia, and the language technologies trained upon it, represent my interests and attitudes[^3], I need to be part of its development. Contributing your voice to a corpus that is used to study and develop language technologies mean that your are legitimising your voice. It confirms the improtance of your interests, words, terminology, and language use, and ensures that these are represented in language developments and technologies. Therefore I'm trying to add articles from a wide range of my interests.

I've summarised my thoughts on this in the [causal loop diagram](https://en.wikipedia.org/wiki/Causal_loop_diagram) below, black arrows mean that an increase in one end causes and increase at the other, while a red arrow means that an increase in one end causes an reduction in the other. This is my opinion only:

![]({{site.baseurl}}/images/causal-loop-en.png){: .center-image }

Here's the 124 articles I've contributed to Wicipedia in the year since November 2019, in the order I created them, and of course other users have edited, corrected and improved them:

<div style="column-count: 3">
<ul>
<li><a href='https://cy.wikipedia.org/wiki/Hock'>Hock</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Loretta_Lynn'>Loretta Lynn</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Neverwhere_(nofel)'>Neverwhere (novel)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Oatman,_Arizona)'>Oatman, Arizona</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Community_(cyfres_teledu)'>Community (TV series)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Emma_o_Normandi'>Emma of Normandy</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Siarter_y_Goedwig'>Charter of the Forest</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Lliwio_graffiau'>Graph colouring</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Un_clip_papur_coch'>One red paper clip</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Diners,_Drive-Ins_and_Dives'>Diners, Drive-Ins and Dives</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_Simpson'>Simpson's paradox</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Palas_Herrenhausen'>Herrenhausen Palace</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Los_Angeles_Dodgers'>Los Angeles Dodgers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Faróc_Edwardaidd'>Edwardian Baroque architecture</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Tonkatsu'>Tonkatsu</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_y_morlin'>Coastline paradox</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cawl_cregyn_bylchog'>Clam chowder</a></li>
<li><a href='https://cy.wikipedia.org/wiki/G%C3%AAm_bywyd_Conway'>Conway's Game of Life</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Only_Connect'>Only Connect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/We_Didn%27t_Start_the_Fire'>We Didn't Start the Fire</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Priodas_y_Dywysoges_Elisabeth_a_Philip_Mountbatten'>Wedding of Princess Elizabeth and Philip Mountbatten</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Corn_Gabriel'>Gabriel's Horn</a></li>
<li><a href='https://cy.wikipedia.org/wiki/HMY_Britannia'>HMY Britannia</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Dilema%27r_carcharorion'>Prisoner's dilemma</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Iwffoleg'>Ufology</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Peiriant_ffa'>Bean machine</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Problem_darnau_arian'>Coin problem</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddf_Little'>Little's law</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Parc_Griffith'>Griffith Park</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_Streisand'>Streisand effect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Plymio_sgwba'>Scuba diving</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bitterballen'>Bitterballen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Googie'>Googie architecture</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pad_thai'>Pad Thai</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Sieri'>Sherry</a></li>
<li><a href='https://cy.wikipedia.org/wiki/SS_Great_Britain'>SS Great Britain</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coeden_rhychwantu_leiaf'>Minimum spanning tree</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llwybr_Hamiltonaidd'>Hamiltonian path</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Star-Spangled_Banner_(baner)'>Star-Spangled Banner (flag)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Kirsty_MacColl'>Kirsty MacColl</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_cobra'>Cobra effect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Parks_and_Recreation'>Parks and Recreation</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Banff,_Alberta'>Banff, Alberta</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddfau_Lanchester'>Lanchester's laws</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llwybr_Euleraidd'>Eulerian path</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coridor_Vasari'>Vasari Corridor</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Art_Deco'>Art Deco architecture</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Sosej_cytew'>Toad in the hole</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cydran_gysylltiedig'>Connected component</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Prifysgol_Twente'>University of Twente</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Microgenedl'>Micronation</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_hydra'>Hydra effect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Moana'>Moana</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Paradocs_Downs%E2%80%93Thomson'>Downs-Thomson paradox</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cities:_Skylines'>Cities: Skylines</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Damcaniaeth_amser_rhithiol'>Phantom time hypothesis</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Dwight_Yoakam'>Dwight Yoakam</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Santa_Monica,_California'>Santa Monica, California</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Effaith_Thatcher'>Thatcher effect</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Coron_Sant_Edward'>St Edward's Crown</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Francisco_de_Zurbar%C3%A1n'>Francisco de Zurbarán</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddf_niferoedd_mawr'>Law of large numbers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bara_banana'>Banana bread</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bragdy_Van_Honsebrouck'>Van Honsebrouck Brewery</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Synesthesia'>Synesthesia</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Six_(sioe_gerdd)'>Six (musical)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Jonas_Jonasson'>Jonas Jonasson</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bomio_edau'>Yarn bombing</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Imiwnedd_cenfaint'>Herd immunity</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Manhattanhenge'>Manhattanhenge</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Matanzas'>Matanzas</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Stroganoff_cig_eidion'>Beef Stroganoff</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bwystfilod_y_Frenhines'>The Queen's Beasts</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Judoon'>Judoon</a></li>
<li><a href='https://cy.wikipedia.org/wiki/T%C5%B7_Petersen'>Petersen House</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Egwyddor_dwll_colomen'>Pigeonhole principle</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cracking_the_Cryptic'>Cracking the Cryptic</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Twyllresymeg_y_chwimsaethwr_o_Decsas'>Texas sharpshooter fallacy</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Baner_Mecsico_Newydd'>Flag of New Mexico</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Hafaliadau_Cauchy%E2%80%93Riemann'>Cauchy-Riemann equations</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Koppelpoort'>Koppelpoort</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Rhif_Bell'>Bell number</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cerddoriaeth_bachata'>Bachata (music)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cydweddiad_(damcaniaeth_graffiau)'>Matching (graph theory)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Theatr_Tsieineaidd_Grauman'>Grauman's Chinese Theatre</a></li>
<li><a href='https://cy.wikipedia.org/wiki/El_Escorial'>El Escorial</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Llofruddiaethau_Tylenol_Chicago'>Chicago Tylenol murders</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Nintendo_Switch'>Nintendo Switch</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pa%C3%ABla'>Paella</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bias_goroesedd'>Survivorship bias</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Amrywiant'>Variance</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Medal_Fields'>Fields Medal</a></li>
<li><a href='https://cy.wikipedia.org/wiki/The_Louvin_Brothers'>The Louvin Brothers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Twll_offeiriad'>Priest hole</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Ieithoedd_Sbaen'>Languages of Spain</a></li>
<li><a href='https://cy.wikipedia.org/wiki/%22Deddf_niferoedd_gwirioneddol_fawr%22'>Law of truly large numbers</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Hallgr%C3%ADmskirkja'>Hallgrímskirkja</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pedwarawd_Anscombe'>Anscombe's quartet</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Matrics'>Matrix</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Lil_Nas_X'>Lil Nas X</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Carlos,_Tywysog_Asturias'>Carlos, Prince of Asturias</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Little_Shop_of_Horrors_(sioe_gerdd)'>Little Shop of Horrors (musical)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Prawf_U_Mann%E2%80%93Whitney'>Mann–Whitney U test</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cerddorion_Bremen'>Town Musicians of Bremen</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Deddfau_De_Morgan'>De Morgan's laws</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Pensaern%C3%AFaeth_Neo-Andeaidd'>Neo-Andean architecture</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Amgueddfa_Hanes_Mecsico_Newydd'>New Mexico History Museum</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Siboleth'>Shibboleth</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Theorem_gwerth-cymedrig'>Mean value theorem</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Integru_fesul_rhan'>Integration by parts</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Seiffr_Caesar'>Caesar cipher</a></li>
<li><a href='https://cy.wikipedia.org/wiki/John_Mulaney'>John Mulaney</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Y_placiau_Pioneer'>Pioneer plaques</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Clystyru_k-cymedr'>k-means clustering</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Planet_Zoo'>Planet Zoo</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Aladdin_(ffilm_2019)'>Aladdin (2019 film)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Teyrnwialen'>Sceptre</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cadair_y_Coroni'>Coronation Chair</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Diagram_dolen_achosol'>Causal loop diagram</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Fileteado'>Fileteado</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Bhaji'>Bhaji</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Annibyniaeth_(tebygolrwydd)'>Independence (probability theory)</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Algorithm_Dijkstra'>Dijkstra's algorithm</a></li>
<li><a href='https://cy.wikipedia.org/wiki/Cyfarfodydd_agos'>Close encounter</a></li>
</ul>
</div>

---

[^1]: there's a number of claims that the number of Wikipedia articles in some language contributes directly towards funding that language ([example](https://cardiffstudentmedia.co.uk/gairrhydd/pam-bod-creu-wicin-wic-ed/), [example](https://www.youtube.com/watch?v=KSEN_HGGrT8)), though I can't find evidence of this. However, these stubs do skew being able to interpret the statistic 'number of articles' as a measure of the size of Wicipedia.
[^2]: see [this article](https://slate.com/technology/2019/08/welsh-wikipedia-google-translate.html) for an example.
[^3]: in my opinion Welsh Wicipedia has an 'identity politics' bias - again, only by contributing to the project can my attitudes be represented.
