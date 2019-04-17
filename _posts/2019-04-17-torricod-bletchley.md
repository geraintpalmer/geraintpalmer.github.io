---
layout     : post
title      : "Gwibdaith i Fletchley"
language   : cymraeg
comments   : true
---

Ar ddydd Llun cymerais i ddiwrnod bant o'r gwaith (hwrê!) ac es i ar wibdaith.
Ymwelon ni â [Pharc Bletchley](https://bletchleypark.org.uk/), leoliad y
gweithrediad cyfrinachol torri-codiau enwog Prydeinig yn ystod yr ail ryfel byd.
Fan hyn gweithiodd mathemategwyr, 'dynion a menywod o'r fath proffeswr',
gweision sifil, a staff a recriwtiwyd o'r Gwasanaethau Menywod, i ddehongli
negeseuon radio a rhyng-gipiwyd o'r lluoedd arfog Almaeneg, Eidaleg, a
Japaneaidd.
Arbedodd y cudd-ymchwil a chafwyd o'r negeseuon hyn nifer di-rif o fywydau, a
chredir cyfrannodd i ddiwedd cynnar y rhyfel, er ni ddatgelir natur eu gwaith
i'r cyhoedd nes degawdau ar ôl i'r rhyfel gorffen.

Rhai uchafbwyntiau dysgais yn ystod fy amser yno:

+ Doedd yr holl beth ddim am Alan Turing! Roedd y tîm torri codiau yn enfawr, a
chyfrannodd pob un ohonynt yn sylweddol i'r wybodaeth a'r dulliau. Maent yn
cynnwys Gordon Welchman, Bill Tutte, Mavis Batey, Gwen Watkins, Hugh Alexander,
Joan Clarke a nifer mwy. Gwnaeth yr amgueddfa gwaith da yn dangos hyn.
+ Twyll cudd-ymchwil enfawr oedd
['Operation Fortitude'](https://en.wikipedia.org/wiki/Operation_Fortitude), yn
gollwng ffug-wybodaeth yn fwriadol er mwyn perswadio'r Almaenwyr bod y glaniadau
D-Day yn mynd i ddigwydd yn Calais, nid yn Normandi. Roedd hwn ond yn bosib
oherwydd rhoddodd y negeseuon a ddehonglir ym Mletchley mewnwelediad i
anymddiriedaeth Hitler yn ei gweithwyr, gweithrediadau cudd-ymchwil yr
Almaenwyr, a'r hyder bod yr Almaenwyr wedi cwympo am y twyll. Oherwydd hyn roedd
y glaniad D-Day yn llwyddiannus, gyda milwyr y Cynghreiriaid yn wynebu llawer
llai o filwyr Almaeneg yn Normadi gan eu bod nhw yn aros am y glaniadau yn
Calais.
+ Roedd rhaid bod yn ofalus iawn gyda'r wybodaeth a chafwyd trwy ddadgryptio'r
negeseuon: ni all unrhyw un gwybod am y gwaith torri-codiau, felly roedd rhaid
cuddwisgo'r negeseuon fel tystiolaeth a chafodd ei ddwyn gan ysbiwyr cyn eu rhoi
i swyddogion uwch! Weithiau roedd yn well peidio gweithredu ar y wybodaeth o
gwbl, i sicrhâi ni fydd yr Almaenwyr yn ddrwgdybus bod ei codiau yn cael eu torri.

Hefyd rhoddodd yr amgueddfa gwybodaeth ar y broses torri-codiau.
Fan hyn byddai'n edrych ar un dull gwaeth dal fy sylw, gan ddefnyddio cod Python
ar gael [fan hyn](https://gist.github.com/geraintpalmer/e2d0e5f82f5508444caef1f5a50744a3)
i ddefnyddio'r seiffrau.

Dechreuwn gyda seiffr hen: y seiffr sifft Caesar:

# Y Seiffr Sifft Caesar

Hwn yw un o'r seiffrau symlaf.
Seiffrwyd neges trwy sifftio pob llythyren o'r neges ar hyd y wyddor Saesneg
nifer sefydlog o weithiau.
Er enghraifft bydd y neges 'ALAN TURING', gydag allwedd 3, yn sifftio A gan 3 er
mwyn cael D, L gan 3 er mwyn cael O, ac yn y blaen:

{% highlight python %}
>>> import cypher
>>> cypher.caesar('ALANTURING', 3)
'DODQWXULQJ'
{% endhighlight %}

Gyda'r allwedd, mae dadseiffro yn hawdd, just gweithio yn ôl yn sifftio pob
llythyren am yn ôl gan 3:

{% highlight python %}
>>> cypher.caesar('DODQWXULQJ', -3)
'ALANTURING'
{% endhighlight %}

Ond os rhyng-gipiwyd neges heb yr allwedd, sut allwn dorri'r seiffr?
Y beth pwysig fan hyn yw sylweddoli rhywbeth am yr iaith cafodd y neges ei
ysgrifennu ynddi.
Yn Saesneg y llythrennau E, T ac A a ddefnyddir mwyaf aml, ac X, J, Q a Z a
ddefnyddir lleiaf aml.

Ystyriwch y neges isod a chafodd ei rhyng-gipio, a chredwn taw Saesneg yw iaith
y neges.

{% highlight python %}
>>> neges_sgramblo
'BJMTQIYMJXJYWZYMXYTGJXJQKJANIJSYYMFYFQQRJSFWJHWJFYJIJVZFQYMFYYMJDFWJJSITBJIGDYMJNWHWJFYTWBNYMHJWYFNSZSFQNJSFGQJWNLMYXYMFYFRTSLYMJXJFWJQNKJQNGJWYDFSIYMJUZWXZNYTKMFUUNSJXXYMFYYTXJHZWJYMJXJWNLMYXLTAJWSRJSYXFWJNSXYNYZYJIFRTSLRJSIJWNANSLYMJNWOZXYUTBJWXKWTRYMJHTSXJSYTKYMJLTAJWSJIYMFYBMJSJAJWFSDKTWRTKLTAJWSRJSYGJHTRJXIJXYWZHYNAJTKYMJXJJSIXNYNXYMJWNLMYTKYMJUJTUQJYTFQYJWTWYTFGTQNXMNYFSIYTNSXYNYZYJSJBLTAJWSRJSYQFDNSLNYXKTZSIFYNTSTSXZHMUWNSHNUQJXFSITWLFSNENSLNYXUTBJWXNSXZHMKTWRFXYTYMJRXMFQQXJJRRTXYQNPJQDYTJKKJHYYMJNWXFKJYDFSIMFUUNSJXXUWZIJSHJNSIJJIBNQQINHYFYJYMFYLTAJWSRJSYXQTSLJXYFGQNXMJIXMTZQISTYGJHMFSLJIKTWQNLMYFSIYWFSXNJSYHFZXJXFSIFHHTWINSLQDFQQJCUJWNJSHJMFYMXMJBSYMFYRFSPNSIFWJRTWJINXUTXJIYTXZKKJWBMNQJJANQXFWJXZKKJWFGQJYMFSYTWNLMYYMJRXJQAJXGDFGTQNXMNSLYMJKTWRXYTBMNHMYMJDFWJFHHZXYTRJIGZYBMJSFQTSLYWFNSTKFGZXJXFSIZXZWUFYNTSXUZWXZNSLNSAFWNFGQDYMJXFRJTGOJHYJANSHJXFIJXNLSYTWJIZHJYMJRZSIJWFGXTQZYJIJXUTYNXRNYNXYMJNWWNLMYNYNXYMJNWIZYDYTYMWTBTKKXZHMLTAJWSRJSYFSIYTUWTANIJSJBLZFWIXKTWYMJNWKZYZWJXJHZWNYDXZHMMFXGJJSYMJUFYNJSYXZKKJWFSHJTKYMJXJHTQTSNJXFSIXZHMNXSTBYMJSJHJXXNYDBMNHMHTSXYWFNSXYMJRYTFQYJWYMJNWKTWRJWXDXYJRXTKLTAJWSRJSYYMJMNXYTWDTKYMJUWJXJSYPNSLTKLWJFYGWNYFNSNXFMNXYTWDTKWJUJFYJINSOZWNJXFSIZXZWUFYNTSXFQQMFANSLNSINWJHYTGOJHYYMJJXYFGQNXMRJSYTKFSFGXTQZYJYDWFSSDTAJWYMJXJXYFYJXYTUWTAJYMNXQJYKFHYXGJXZGRNYYJIYTFHFSINIBTWQI'
{% endhighlight %}

Yna ystyriwn amledd y llythrennau:

{% highlight python %}
>>> from collections import Counter
>>> amleddau = Counter(neges_sgramblo)
{% endhighlight %}

![]({{site.baseurl}}/images/caesar_freq_cy.png)

J sy'n digwydd mwyaf aml, felly a all hyn fod yn E?
Bydd hwnna'n golygu sifft o 5.
C, E a V yw'r llythrennau sy'n digwydd lleiaf aml.
O dan sifft o 5 y llythrennau hyn fydd Q, X a Z.
Felly efallai bod sifft o 5 yn gwneud synnwyr:

{% highlight python %}
>>> cypher.caesar(neges_sgramblo, -5)
'WEHOLDTHESETRUTHSTOBESELFEVIDENTTHATALLMENARECREATEDEQUALTHATTHEYAREENDOWEDBYTHEIRCREATORWITHCERTAINUNALIENABLERIGHTSTHATAMONGTHESEARELIFELIBERTYANDTHEPURSUITOFHAPPINESSTHATTOSECURETHESERIGHTSGOVERNMENTSAREINSTITUTEDAMONGMENDERIVINGTHEIRJUSTPOWERSFROMTHECONSENTOFTHEGOVERNEDTHATWHENEVERANYFORMOFGOVERNMENTBECOMESDESTRUCTIVEOFTHESEENDSITISTHERIGHTOFTHEPEOPLETOALTERORTOABOLISHITANDTOINSTITUTENEWGOVERNMENTLAYINGITSFOUNDATIONONSUCHPRINCIPLESANDORGANIZINGITSPOWERSINSUCHFORMASTOTHEMSHALLSEEMMOSTLIKELYTOEFFECTTHEIRSAFETYANDHAPPINESSPRUDENCEINDEEDWILLDICTATETHATGOVERNMENTSLONGESTABLISHEDSHOULDNOTBECHANGEDFORLIGHTANDTRANSIENTCAUSESANDACCORDINGLYALLEXPERIENCEHATHSHEWNTHATMANKINDAREMOREDISPOSEDTOSUFFERWHILEEVILSARESUFFERABLETHANTORIGHTTHEMSELVESBYABOLISHINGTHEFORMSTOWHICHTHEYAREACCUSTOMEDBUTWHENALONGTRAINOFABUSESANDUSURPATIONSPURSUINGINVARIABLYTHESAMEOBJECTEVINCESADESIGNTOREDUCETHEMUNDERABSOLUTEDESPOTISMITISTHEIRRIGHTITISTHEIRDUTYTOTHROWOFFSUCHGOVERNMENTANDTOPROVIDENEWGUARDSFORTHEIRFUTURESECURITYSUCHHASBEENTHEPATIENTSUFFERANCEOFTHESECOLONIESANDSUCHISNOWTHENECESSITYWHICHCONSTRAINSTHEMTOALTERTHEIRFORMERSYSTEMSOFGOVERNMENTTHEHISTORYOFTHEPRESENTKINGOFGREATBRITAINISAHISTORYOFREPEATEDINJURIESANDUSURPATIONSALLHAVINGINDIRECTOBJECTTHEESTABLISHMENTOFANABSOLUTETYRANNYOVERTHESESTATESTOPROVETHISLETFACTSBESUBMITTEDTOACANDIDWORLD'
{% endhighlight %}

Ac rydym wedi cracio'r cod, hwn yw datganiad annibyniaeth yr Unol Daleithiau!

{% highlight python %}
>>> datganiad = cypher.caesar(neges_sgramblo, -5)
{% endhighlight %}


# Y Peiriant Enigma

Yn ystod yr ail ryfel byd defnyddiodd yr Almaenwyr peiriant seiffro
soffistigedig o'r enw Enigma, a ddangosir isod.
Yn gyntaf bydd anfonwr yn *gosod y peiriant*, yna byddant yn *gosod y safleoedd
dechreuol*.
Yna'n defnyddio'r allweddell byddant yn teipio'u neges, a bydd y neges seiffr yn
goleuo wrth i chi deipio, yna bydd cydweithiwr yn ysgrifennu i lawr y neges
seiffr cyn ei anfon dros y radio mewn
[cod Morse](https://en.wikipedia.org/wiki/Morse_code).

<img src="{{site.baseurl}}/images/enigma.jpg" width="250">{: .center-image }

Nodwedd bwysig o'r peiriant yw ei fod yn wrthdro ei hun.
Gan ddefnyddio'r un gosodiadau, a'r un safleoedd dechreuol, gallwch deipio mewn
y neges seiffr a bydd y neges wreiddiol yn goleuo.


{% highlight python %}
>>> cypher.enigma('ALANTURING', 'BFG')
'CKYCEZCDZB'

>>> cypher.enigma('CKYCEZCDZB', 'BFG')
'ALANTURING'
{% endhighlight %}


#### Sut oedd yn gweithio

Roedd y peiriant wedi'i greu allan o switsfwrdd, tri rotor, ac adlewyrchydd.

+ Bydd y switsfwrdd yn achosi 10 amnewidiad syml: h.y. amnewid A i K a K i A;
amnewid M i U ac U i M, ac yn y blaen.
+ Mae pob rotor yn ymddwyn fel seiffr sifft Caesar ar wyddor wedi'i gymysgu lan.
Roedd y cymysgu hyn yn unigryw i'r rotor, ac roedd angen dewis tri rotor allan o
bump. Hefyd, gall y trefn y wyddor cymysg ar bob rotor cael ei addasu ymhellach.
+ Mae'r adlewyrchydd yn paru llythrennau o'r wyddor, ac yn eu hamnewid nhw.
Mae'r darn hwn yn hanfodol er mwyn i'r peiriant bod yn wrthdro ei hun.

Felly os oeddwn am wasgu'r llythyren Q:

+ Yn gyntaf bydd yn mynd trwy'r switsfwrdd, a all amnewid Q i T.
+ Yna bydd yn mynd trwy'r rotor $$1^{\text{af}}$$, yn sifftio'r T hyn ar hyd wyddor gymysg i gael U.
+ Yna bydd yn mynd trwy'r $$2^{\text{il}}$$ rotor, yn sifftio'r U hyn ar hyd wyddor gymysg i gael M.
+ Yna bydd yn mynd trwy'r $$3^{\text{ydd}}$$ rotor, yn sifftio'r M hyn ar hyd wyddor gymysg i gael R.
+ Yna mae'n bwrw'r adlewyrchydd, yn amnewid R i Y.
+ Yna bydd yn mynd trwy'r $$3^{\text{ydd}}$$ rotor am yn ôl, yn sifftio'r Y i C.
+ Yna bydd yn mynd trwy'r $$2^{\text{il}}$$ rotor am yn ôl, yn sifftio'r C i A.
+ Yna bydd yn mynd trwy'r rotor $$1^{\text{af}}$$ am yn ôl, yn sifftio'r A i G.
+ Yn olaf bydd yn mynd trwy'r switsfwrdd eto, a all amnewid G i L.

Yna mae L yn goleuo.
Felly mae Q wedi'i mapio i L.

Hawdd?

Ond cyn teipio'r llythyren nesaf, mae'r rotor cyntaf yn cylchdroi gan un
lythyren, yn y bôn yn cynyddu sifft y seiffr Caesar hynny gan un.
Felly bydd gan y llythyren nesaf mapiad gwahanol.
Pob tro mae'r rotor cyntaf yn sifftio 26 gwaith, mae'r ail rotor yn sifftio.
A pob tro mae'r ail rotor yn sifftio 26 gwaith, mae'r trydydd rotor yn sifftio.
Felly mae'r $$26^3 = 17576$$ llythyren gyntaf wedi'i seiffro gan fapiadau
gwahanol.

Mae safleoedd dechreuol y tri rotor yn penderfynu lle yn y cylchred o 17576
mapiad mae'r neges yn dechrau.

Yn cyfuno'r dewis a threfn y tri rotor, addasiadau i bob rotor, cyfuniadau'r
switsfwrdd, a safleoedd dechreuol y tri rotor, mae yna 156 miliwn miliwn miliwn
seiffrau bosib gall cael ei ddefnyddio i seiffro neges.
Felly os rhyng-gipiwyd neges, sut torron nhw'r cod?


#### Torri'r cod

Roedd gwallau dynol yn helpu fan hyn.

Pob diwrnod bydd pob neges anfonwyd gan yr Almaenwyr yn defnyddio'r un tri rotor
yn yr un drefn, yr un addasiadau i'r tri rotor, a'r un cyfuniadau switsfwrdd.
Unwaith roedd y rhain wedi'u darganfod (gan ddefnyddio nifer o ddulliau clyfar
arall) yr unig amrywiant yn seiffrau'r negeseuon mewn un dydd oedd safleoedd
dechreuol y tri rotor.

Un dull clyfar iawn oedd "Banburismus", a oedd yn manteisio ar diogi'r bobl oedd
yn anfon y negeseuon.
Weithiau roedd anfonwyr ond yn newid y safleoedd dechreuol gan maint bach rhwng
anfon negeseuon.
Felly gallwn gymharu dwy neges o'r un anfonwr.


*Ffaith ddefnyddiol:*

+ Wrth roi dau ddilyniant o lythrennau 'ar hap' ar ben ei gilydd, byddant yn
cyd-daro gyda thebygolrwydd $$\frac{1}{26}$$.
+ Wrth roi dwy frawddeg Saesneg ar ben ei gilydd, byddant yn cyd-daro yn fwy
aml.

Does dim ots os yw'r llythrennau wedi'i seiffro neu beidio!
Cyhyd â'u bod nhw wedi'u seiffro yn yr un modd.

*Ffaith ddefnyddiol arall:*

+ Mae neges wedi'i seiffro gyda'r safle dechreuol 'ATT' yr un peth a'r neges
wedi'i seiffro gyda'r safle dechreuol 'CTT', os yw'r ail neges yn dechrau o'r
drydedd lythyren (gan fod C dwy lythyren i ffwrdd o A).

{% highlight python %}
>>> cypher.enigma('ALANTURING', 'ATT')
'RCJCXBVLLJ'

>>> cypher.enigma('ANTURING', 'CTT')
'JCXBVLLJ'
{% endhighlight %}

Mae Banburismus yn manteisio ar y ddwy ffaith hyn, yn gwirio'r tebygolrwydd o
ddwy lythyren yn cyd-daro ar negeseuon sydd wedi'i rhoi ar ben ei gilydd ac wedi
sifftio gan gyfyngau gwahanol.
Mae'r cyfwng sy'n rhoi'r tebygolrwydd mwyaf o gyd-daro yn rhoi cliw mawr i beth
yw'r cyfwng rhwng safleoedd dechreuol a ddefnyddiwyd ar gyfer y ddwy neges.

Dychmygwch ein bod wedi rhyng-gipio neges o gryptograffwr diog, ac rydym wedi
rhywsut darganfod taw'r safleoedd dechreuol oedd 'BLY':


{% highlight python %}
>>> datganiad_seiffro = cypher.enigma(datganiad, 'BLY')
>>> datganiad_seiffro
'KHCJOAPGJHDYMYXVPFCNJTGIAZYLORJQWXDQNPYPNKPUIFOHEIBACXLREMQSNVOXAJXINLJGYMLUPRADTWNGPTKFIPNEWRJMEFVIQYVWYVCGSSOBPVBEDOMPNUXGFLISPMMTLNKOQPFRMDMMQZIKEYJXLSJOYKUVQCTJOHUPCPLMUSKBOWAHIUCHWZILPIPODHQRUSRVQCBRUALWVSYWNMUTWJHGJJHREBFOJUBSADCOGYSJURQJNTQSERODIVEUTMGCURIOEIWYRAWDSRWCOQGEUQBSOFDFBMBZZECZNDVJDCTFDQDDRXBCZLJKPYUBYIRSSDFGKCVXNBVJSFYEFNKWWLWDAPIAMVSWMVLEKXPVSNCWRFZHDDPCIGYZIDERHXZOQPCLXDDNHIYONAUMSWWPLNKRQHQTJCGNNCBEDPTYVVBZOQCJVXBRXJHKYZBKLGIEBYXQPDIJFNUUZZTKFJDUURUNJVOMQRUFJKGVRRJKORMQQBYEGDKJAQFYZNKCVVUDPFWYJMJJOHPMOTDXIYZWZCQHIYXCQWMAXZEXEFWXPQKRGSDKJPZSRANMTLOSYOUUJLNMQDQSZZUQJAVBOZJBZYJZLJKMNIZLJKMGCTNNRVAJZLWBREMJAEWPKRJPHFRCJZQWCITVTTPURCNYDKHWNQYBLPHBHVJNTICQCAZVCEDLAZEHVRCUTVLRXBYAQWENDXVWOPJINTFWPKLWKDFBWCMFWLYGPKVHAIOEWPARVYLYAWSNKLPCNJJWCIYLVZPSHZKVLTFTZVIDFERWVMUVGGEMLQGXCGMBDTLTTBVTMKICXFZTQURQZVOUMNPQPKETNTXBDEXGERBRUGXUUXAWMOMXEHVORITUSDHNFQPYAQBVFAWJSYYPVZHWAZWVXMEDAOXGOLBNJPZADJQSJBYMHLHZDWUVCBXDLJVHGYSYSUHPJIUDILUTAHDJSJVYCVJAJNWIFOBMBMVHDGZUMJDDAWVSPCOVIOMKFPBSYDUCFGRZEPJQDUHQTHYXJRAZPDPNIPQZJJEGQRTJBDGRFGYRJJSEXDDDOIPPFRUWCXHHJYFORFGFISSKADJKQUBBFQODJKFJKUZDHHFLFKWGOQRZUVYVDSUPOPQXCJBFXQBQZQHCISIAJGQCOFIWEUADFMDOLAJQLRDBWTTKWJGWEAAQJCHLLHTSUJYSTKIZMYFHQZDNDKHTSTBVFQZWZQXJKULQDDGJQTRIOKCYSHSUWCAUCLWAOMUVGGHZMNJIAMCKWCTRJRNFMATDXYQWMIFYTCMSWZUMVWHXPKFGONWZUBOWUHJBAMCXSKTFWBMIOFT'
{% endhighlight %}

Yn hwyrach ar yr un diwrnod rydym yn rhyng-gipio neges arall o'r un
cryptograffwr diog:

{% highlight python %}
>>> neges_sgramblo
'WHQLPKVQNJDIBDWMHWJVKBWJFMKRAAXPIEAQUDAVCVRBQUMDXKJFFGSMUNKTUVDSRFAXOVWYOXWHEMYVUDRDTMRZPRKOSXJHOBVOADVLCSJZYUUEGISZVDUVLJOWXBTULWVJOWKSEHSJMVSNUTUQCTFAHMSFTVCQOZSDYAFKRZYDDFVVFDCIQWABWWWMCAEIUPLPIRKOIIDMHSRZJCGSIHCSURUBZACFEKBEQCREQBVRWDUDCNYCTYWDJVHBWFNCJWGDHNJPLBMJITSOYYLMFHTBPXRUOESXQQLKFNAFZYBWLBLFPPNVEUSXKRCYKWCGMQSVEGRBJEKQTBWGPPXKNRSHCMKNCGODDKWOBKVZLMAZEBGDHJNDUIWKJBLVWVBXXZUECIYXEJFBBBJLQFGXFUEOMPOTMPAJQDZBTGPCAZQXIOTHKYJJWDOYFTJFWFNYGHEYHRVPLMMSUPJJHCGWMIHDNFXWPPUBYRMNJQVKHZTYVYLJVZIDVBZQDXXWGBJYQJCGHRWSAKDRJJTPGPEZHKYLRTROXIPWUTZMPRKTGALBCHDHKBVTVUPIMNWOQBJCGRRBJKWVNVSCKUMYGBRXJSWTOXVZKWKRSRGNKJTDAPNRSDJMEKRJBHXTITRMUJGOOGMCFCNEJTKSHCJSBUNFCJNALNGUYBURDAJGZKMSFDKQBABJXHBRKTFCVRGPQKAEDJHCEUFXQXYNQYLPTSZEJZHCKVHBDYEZLPGHYATRSNJCDIRBOUXYQWZGSBNSVZCIAYIWBDBNXBEYEYEMMLOAUGHFGIYPIDRVPKBMXXHMHCBFYHYZPEOOBDROQKUZNMIYITELSFGWXZCMKYURZXSNOCCMMCAHFGMMECLPSZDSJFWLVIHKESTEONHYFKOXSBXGCXGAPHGAVJXAHBXKWWQBQQRQGNJVXXIMTJBKHMGBNEBJNMOWGLWNECVGPMHVVKJTIVGSHBSFQLDEHWXNQSVBHJIDYNKCYUZVQPMANTKOHNOCMXCOWKJNARDKVEIXZECCJVEXXDHTHYHZUPFZZJQMTJOYPBPNVUGUCNKHGIDYEVRDQARXKGAXEJVGFSQZIVJVABAPZALTMVGRVMNUPFLQBKAZSXJFUICWSUDUWUDZVUKRGACIXQVCJBHNHKBHODVGOFYUKKJUXOZBWVGURPAEAQLCBDOEEJIVVUWEPUANUCGSEGGMJMKNYODVZDDFSRDMOLFKSSYGWOEXRXDHZOALEVJIXEGMDYYSCGMUUTLXAQREZZZZYWPZZRJAVPWPBXLGPQKFDEEJSKNWSAGUAKEYBIRKKAYEMSOKMJRXRTAXSOYDXGQJQXUNGDQKOYRSKUTHZLXRBEXOSNMZDQJXWTNXYXBCQTOGXZHAVBBGGCPCAMSKOXCFQTPRWCUDMQORRVABBISD'
{% endhighlight %}

Nawr dydyn ni ddim yn gwybod beth yw'r safleoedd dechreuol a ddefnyddiwyd i
seiffro'r neges hyn, ond rydym yn gwybod bod y cryptograffwr hyn yn ddiog, felly
ni fydd rhy bell i ffwrdd o 'BLY'.
Nawr defnyddiwn Banburismus i ganfod tebygolrwydd o lythrennau'n cyd-daro ar
gyfer pob sifft:

{% highlight python %}
>>> def banburismus(l1, l2, sifft):
...     cyddaro = [a == b for a, b in zip(l1[sifft:], l2)]
...     return sum(cyddaro) / len(cyddaro)

>>> banburismus(datganiad_seiffro, neges_sgramblo, 1)
0.040090771558245086
{% endhighlight %}

Defnyddiwn hwn ar gyfer nifer o sifftiau:

![]({{site.baseurl}}/images/banburismus_cy.png)

Mae sifft o 11 yn rhoi'r tebygolrwydd mwyaf o lythrennau'n cyd-daro, felly gall
hyn fod yn ddyfaliad da.
'BLY' wedi sifftio gan 11 yw 'MLY', felly:

{% highlight python %}
>>> cypher.enigma(neges_sgramblo, 'MLY')
'ALLHUMANBEINGSAREBORNFREEANDEQUALINDIGNITYANDRIGHTSTHEYAREENDOWEDWITHREASONANDCONSCIENCEANDSHOULDACTTOWARDSONEANOTHERINASPIRITOFBROTHERHOODEVERYONEISENTITLEDTOALLTHERIGHTSANDFREEDOMSSETFORTHINTHISDECLARATIONWITHOUTDISTINCTIONOFANYKINDSUCHASRACECOLOURSEXLANGUAGERELIGIONPOLITICALOROTHEROPINIONNATIONALORSOCIALORIGINPROPERTYBIRTHOROTHERSTATUSFURTHERMORENODISTINCTIONSHALLBEMADEONTHEBASISOFTHEPOLITICALJURISDICTIONALORINTERNATIONALSTATUSOFTHECOUNTRYORTERRITORYTOWHICHAPERSONBELONGSWHETHERITBEINDEPENDENTTRUSTNONSELFGOVERNINGORUNDERANYOTHERLIMITATIONOFSOVEREIGNTYEVERYONEHASTHERIGHTTOLIFELIBERTYANDSECURITYOFPERSONNOONESHALLBEHELDINSLAVERYORSERVITUDESLAVERYANDTHESLAVETRADESHALLBEPROHIBITEDINALLTHEIRFORMSNOONESHALLBESUBJECTEDTOTORTUREORTOCRUELINHUMANORDEGRADINGTREATMENTORPUNISHMENTEVERYONEHASTHERIGHTTORECOGNITIONEVERYWHEREASAPERSONBEFORETHELAWALLAREEQUALBEFORETHELAWANDAREENTITLEDWITHOUTANYDISCRIMINATIONTOEQUALPROTECTIONOFTHELAWALLAREENTITLEDTOEQUALPROTECTIONAGAINSTANYDISCRIMINATIONINVIOLATIONOFTHISDECLARATIONANDAGAINSTANYINCITEMENTTOSUCHDISCRIMINATIONEVERYONEHASTHERIGHTTOANEFFECTIVEREMEDYBYTHECOMPETENTNATIONALTRIBUNALSFORACTSVIOLATINGTHEFUNDAMENTALRIGHTSGRANTEDHIMBYTHECONSTITUTIONORBYLAWNOONESHALLBESUBJECTEDTOARBITRARYARRESTDETENTIONOREXILEEVERYONEISENTITLEDINFULLEQUALITYTOAFAIRANDPUBLICHEARINGBYANINDEPENDENTANDIMPARTIALTRIBUNALINTHEDETERMINATIONOFHISRIGHTSANDOBLIGATIONSANDOFANYCRIMINALCHARGEAGAINSTHIM'
{% endhighlight %}

Ac rydym wedi cracio'r cod, hwn yw'r datganiad cyffredinol am hawliau dynol!

Anfanteision o'r dull hwn yw'r angen i gael negeseuon hir, ac mae hefyd angen
ein bod wedi cracio neges arall yn gynharach y diwrnod hwnnw.
Datblygwyd nifer o ddulliau arall ym Mletchley gan gynnwys Cribio, lle mae angen
dyfalu bod y neges yn dechrau gyda geiriau cyffredin fel 'tywydd', a chael
gwared â nifer o safleoedd dechreuol bosib o'r ffaith nad yw Enigma yn gallu
mapio unrhyw lythyren i'w hunain.
Daeth y dulliau hyn gyda'i gilydd wrth adeiladu'r peiriant Bombe er mwyn
awtomeiddio nifer o dasgau yn gloi iawn, ond yn yr amgueddfa doedd yr esboniad o
sut oedd hyn yn gweithio ddim yn dda iawn.

Ar y cyfan ces i ddiwrnod allan dda iawn yn cyfuno fy niddordebau mewn hanes a
mathemateg, a datblygais ysbrydoliaeth (a bach o wladgarwch) o'r gwaith
ddigwyddodd yna.
Gorffennwn ni'r diwrnod yn gwrando ar y [podleidiad Maths at the Movies](http://www.mathsat.co.uk/2017/11/maths-at-movies-imitation-game-plus.html)
a oedd yn trafod y ffilm The Imitation Game.
