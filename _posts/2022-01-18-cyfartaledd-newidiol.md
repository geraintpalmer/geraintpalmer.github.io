---
layout     : post
title      : "Cymryd Cyfartaleddau Newidiol gyda Chyfyngau Afreolaidd"
language   : cymraeg
comments   : true
---

Ar hyn o bryd does gan Pandas ddim gallu neis i gymryd cyfartaleddau newidiol o gyfresi amser gyda chyfyngau afreolaidd, yn enwedig os nad yw'r data yn y fformat `datetime`. Mae gan y llyfrgell [`traces`](https://github.com/datascopeanalytics/traces) y gallu hwn. Dangosaf gydag enghraifft yn Ciw.

Ystyriwch giw M/M/c gydag amserlen ar gyfer y gweinyddion, 1 gweinydd am dri diwrnod, a 2 gweinydd am y pedwar nesaf, sy'n rhedeg am bedwar flwyddyn:

{% highlight python %}
>>> import ciw
>>> N = ciw.create_network(
...     arrival_distributions=[ciw.dists.Exponential(rate=5)],
...     service_distributions=[ciw.dists.Exponential(rate=7)],
...     number_of_servers=[[[1, 3], [2, 7]]]
... )

>>> ciw.seed(0)
>>> Q = ciw.Simulation(N, tracker=ciw.trackers.SystemPopulation())
>>> Q.simulate_until_max_time(365 * 4)
{% endhighlight %}

Fan hyn rydym yn defnyddio [traciwr cyflwr](https://ciw.readthedocs.io/cy/latest/Guides/state_trackers.html) er mwyn tracio cyflwr y system dros amser. Mae'n recordio hanes cyfan y newidiadau mewn cyflwr, hynny yw cyfres amser gyda chyfyngiadau afreolaidd:

{% highlight python %}
>>> Q.statetracker.history
[[0.0, 0],
 [0.3721214222130447, 1],
 [0.48126405132136324, 2],
 [0.541192513764126, 3],
 [0.5747827297804392, 2],
 [0.6489374706664274, 1],
 [0.6843834637175561, 2],
 [0.7566671923851261, 3],
 ...
{% endhighlight %}

Nid yw plotio hwn yn rhoi llawer o fewnwelediad, gan ei fod rhy stocastig:

{% highlight python %}
>>> plt.plot(
...     [t[0] for t in Q.statetracker.history],
...     [t[1] for t in Q.statetracker.history],
...     c='black'
... )
>>> plt.xlabel('Diwrnodau')
>>> plt.ylabel('Cwsmeriaid')
{% endhighlight %}

![]({{site.baseurl}}/images/state-cy.png){: .center-image }

Mae gan y llyfrgell [`traces`](https://github.com/datascopeanalytics/traces) y gallu i gymryd cyfartaleddau newidiol dros y gyfres amser afreolaidd hon, gydag unrhyw faint ffenest sydd angen, e.e. cyfartaledd newidiol 7-diwrnod, cyfartaledd newidiol 30-diwrnod, neu gyfartaledd newidiol chwarterol:

{% highlight python %}
>>> series = traces.TimeSeries()
>>> for timestamp, state in Q.statetracker.history:
...     series[timestamp] = state

>>> series_ma7 = series.moving_average(7, pandas=True)
>>> series_ma30 = series.moving_average(30, pandas=True)
>>> series_maQ = series.moving_average(365/4, pandas=True)

>>> series_ma7
0.0       1.164410
7.0       0.805528
14.0      1.780030
21.0      1.076819
28.0      1.224057
            ...   
1428.0    0.834888
1435.0    0.966756
1442.0    2.827261
1449.0    1.074443
1456.0    0.775233
Length: 209, dtype: float64
{% endhighlight %}

MAe hwn yn rhoi rhywbeth bach mwy deongladwy:

{% highlight python %}
>>> plt.plot(series_ma7, c='black', alpha=0.3, label='CN 7 diwrnod')
>>> plt.plot(series_ma30, c='black', linestyle='dotted', label='CN 30 diwrnod');
>>> plt.plot(series_maQ, c='black', label='CN Chwarterol');
>>> plt.legend()
>>> plt.xlabel('Diwrnodau')
>>> plt.ylabel('Cwsmeriaid')
{% endhighlight %}

![]({{site.baseurl}}/images/state_ma-cy.png){: .center-image }


Mae'r llyfrgell [`traces`](https://github.com/datascopeanalytics/traces) hefyd yn ein galluogi i wneud hwn o ffeil, ac rydw i'n credu bod hwn yn neisiach:

{% highlight python %}
>>> Q.write_records_to_file('records.csv')

>>> series = traces.TimeSeries.from_csv(
...     filename="records.csv",
...     time_column=3,  # Dyddiadau cyrraedd
...     time_transform=float,
...     value_column=4, # Amseroedd aros
...     value_transform=float
... )

>>> series_wait_ma = series.moving_average(30, pandas=True)

>>> plt.plot(series_wait_ma, c='black')
>>> plt.xlabel('Diwrnodau')
>>> plt.ylabel('Amser Aros')
{% endhighlight %}

![]({{site.baseurl}}/images/wait_ma-cy.png){: .center-image }

Wrth gymryd cyfartaledd newidiol gallwn allbynnu cyfres [pandas](https://pandas.pydata.org/), felly mae hwn yn gydnaws gyda dadansoddiadau eraill hefyd. Mae'r llyfrgell hwn lot neisiach na fy null blaenorol o drawsnewid y data i `datetime` a nôl!