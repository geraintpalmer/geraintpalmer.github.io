---
layout     : post
title      : "Y Theorem Borsuk-Ulam"
language   : cymraeg
comments   : true
---

Heddiw dysgais i rywbeth oni'n meddwl oedd yn anhygoel.
Cyflwynodd fy nghydweithiwr
[Dr. Timm Oertel](https://www.cardiff.ac.uk/people/view/192658-oertel-timm)
y theorem fach neis yma: y theorem Borsuk-Ulam.
Yn fras mae'n dweud: *Mae gan bob ffwythiant di-dor ar n-sffêr i n-gofod
Ewclidaidd pâr o bwyntiau antipodal gyda'r un gwerth*.

Beth yw hwn yn golygu?

# Cylchoedd

**Ar gyfer ffwythiant di-dor ar gylch, bodoler pâr o bwyntiau cyferbyn ar y
cylch gyda'r un gwerth.**

Dychmygwch fyd 2D wedi'i orchuddio mewn mynyddoedd di-dor (dim clogwyni fertigol
na chwympiau):

<img src="{{site.baseurl}}/images/globe.png" width="350">{: .center-image }

Mae'r theorem yma yn dweud wrthym fod yna pâr o bwyntiau union cyferbyn a'i
gilydd, gyda'r union un uchder mynydd:

<img src="{{site.baseurl}}/images/globe_antipodal.png" width="350">{: .center-image }

Pam bod hyn yn wir?
Wel gallwn ni fflatio'r byd yma fel ffwythiant un dimensiwn $$f(x)$$, yn cymharu
top y cylch ($$x$$ positif) a gwaelod y cylch ($$x$$ negatif):

<img src="{{site.baseurl}}/images/flattened.png" width="750">{: .center-image }

+ Mae pâr o bwyntiau cyferbyn ar y cylch yn negatif y llall, $$y$$ a $$-y$$.
+ Os oes gan y ddau'r un gwerth neu uchder, yna $$f(y) - f(-y) = 0$$.
+ Ystyriwch y ffwythiant $$g(x) = f(x) - f(-x)$$.
+ Mae hwn yn ffwythiant od, gan fod
$$g(-x) = f(-x) - f(x) = -\left(f(x) - f(-x)\right) = -g(x)$$:

<img src="{{site.baseurl}}/images/flattened_diff.png" width="750">{: .center-image }

Mae gan bob ffwythiant od di-dor sero (mae'r di-dor felly nad oed neidiau, ac
rhaid iddo basio o $$-g(x)$$ i $$g(x)$$).
Felly rhaid bod yna rhyw werth $$y$$ fel bod $$g(y) = f(y) - f(-y) = 0$$, hynny
yw pwyntiau cyferbyn sydd a'r un uchder.


# Sfferau

Mewn mwy nag un dimensiwn mae hwn hyd yn oed yn fwy gwallgof!
Mae datganiad llawn y theorem yn rhoi fod ar gyfer unrhyw ffwythiant di-dor
$$f: S^n \rightarrow \mathbb{R}^n$$ bodoler pwynt $$y$$ fel
bod $$f(y) = f(-y)$$.

Ar sffêr, mae $$f$$ yn ffwythiant gyda dau werth.
Er enghraifft ystyriwch y Ddaear yn sffêr, ac $$f$$ yw ffwythiant sy'n rhoi
gwerthoedd y tymheredd a'r lleithder (yn tybio'n rhesymol bod y ddau yn
ddi-dor).
Bodoler dau bwynt yn union cyferbyn a'r gilydd ar y Ddaear sydd a'r union un
tymheredd a lleithder!

Trafodir hyn hefyd yn [erthygl Forbes](https://www.forbes.com/sites/kevinknudson/2016/05/28/how-topology-affects-the-weather/#775f680535a5).
Bydd ystyried unrhyw ddimensiynau mwy yn brifo'n ymennydd, ond mae'r esiamplau
yma yn syfrdanol.
