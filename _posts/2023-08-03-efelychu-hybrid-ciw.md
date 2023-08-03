---
layout     : post
title      : "Canllaw Adeiladu Efelychiad Hybrid DES+SD gyda Ciw"
language   : cymraeg
comments   : true
---

Bydd hwn yn ganllaw ar sut i adeiladu efelychiad DES+SD gyda [Ciw](https://ciw.readthedocs.io/). Mae'r efelychiadau hybrid hyn yn fodelau sy'n cyfuno methodoleg amser arwahanol efelychu digwyddiadau arwahanol (DES), a methodoleg amser di-dor deinameg systemau (SD). Ysgrifennais bapur gyda myfyrwraig gwrs meistr, Yawen Tian, cwpl o flynyddoedd yn ôl yn esbonio sut mae hwn yn bosib mewn Python gan ddefnyddio'r llyfrgelloedd Ciw a SciPy, yn esbonio'r fethodoleg, strwythur y modelau, a phroblemau cydamseredd, gyda rhai enghreifftiau: ["Implementing hybrid simulations that integrate DES+SD in Python"](https://www.tandfonline.com/doi/full/10.1080/17477778.2021.1992312). Yn y papur hwnnw rydym yn dangos taw prif ran y dull yw datrys hafaliadau differol y gydran SD rhwng pob un digwyddiad arwahanol y gydran DES, gan ddiweddaru'r holl baramedrau ym mhob achos. Fan hyn, trwy enghraifft, rydw i eisiau canolbwyntio ar y camau cymeron ni i addasu ffynhonnell côd Ciw er mwyn adeiladu'r modelau, fel canllaw i fyfyrwyr neu bobl eraill sydd eisiau ailgynhyrchu'r gwaith.

Bydd angen:
  + Bach o ddealltwriaeth am efelychu digwyddiadau arwahanol
  + Bach o ddealltwriaeth am deinameg systemau
  + Wedi darllen y [papur uchod](https://www.tandfonline.com/doi/full/10.1080/17477778.2021.1992312)
  + Python (bydd bendant yn gweithio gyda fersiwn 3.7)
  + Ciw (bydd bendant yn gweithio gyda fersiwn 2.3.5)
  + SciPy (bydd bendant yn gweithio gyda fersiwn 1.7.3)

# Problem

Mae Amazon Kindle yn ychwanegu nifer fawr o lyfrau i'w siop pob diwrnod. Mae rhyw debygolrwydd penodol y bydd y llyfrau hyn yn cynnwys gwallau. Unwaith mae'r llyfrau ar werth yn y siop, gall darllenwyr adrodd y gwallau maent yn eu canfod. Mae'r adroddiadau gwall hyn yn ymuno â chiw a chaiff eu cywiro gan nifer penodol o staff. Pan nad ydynt yn cywiro gwallau, mae'r staff yn gweithio tuag at ganfod a chywiro gwallau yn y llyfrau sydd ar werth yn y siop Kindle.

Mae'n cymryd aelod o staff rhwng 1 a 2 awr, wedi'i dosrannu'n unffurf, i gywiro gwall. Caiff gwallau eu hadrodd ar hap gyda chyfradd $$r$$, ac maen yn ymuno â'r ciw er mwyn cael eu cywiro yn ô dosraniad esbonyddol.

Faint o aelodau o staff dylai'r siop Kindle cyflogi i wneud y swydd hon?


# Cam 1 - Fformiwleiddio

Pam fod model hybrid DES+SD yn addas fan hyn? I ddechrau dydyn ni ddim yn gweld unrhyw elfennau amser di-dor, a gallwn fodelu'r holl system gan ddefnyddio DES yn unig. Ond, mae nifer o lyfrau a gwallau sydd gennym yn uchel iawn, a gall hwn cymryd lot mawr o gof cyfrifiadurol ac amser hir i'w rhedeg. Felly, gall SD fod yn well. Wrth edrych ar faint o fanylder sydd angen, mae yna giw gyda nifer cyfanrifol o adroddiadau gwall, a nifer cyfanrifol o weinyddion, felly mae'n gwneud synnwyr modelu'r gydran hon fel DES. Ar gyfer popeth arall, maent wedi'u disgrifio gyda chyfraddau, maent yn niferoedd mawr iawn neu'n aml iawn, a does dim angen lot o fanylder, felly gallwn eu modelu fel SD. Felly, rhain fydd ein dwy gydran.

Gallwn weld fod y ddwy gydran yn rhyngweithio'n agos iawn - bydd lefelau stoc a chyfraddau o'r SD yn effeithio ar y ciw DES (e.e. mae nifer o lyfrau gyda gwallau ynddynt yn effeithio ar gyfradd dyfodi'r ciw), a bydd manylion o'r DES yn effeithio ar yr SD (e.e. mae nifer o weinyddion rhydd yn effeithio ar gyfradd newid niferoedd o lyfrau). Felly mae angen DES+SD cyfannol. Gan ddefnyddio iaith y [papur uchod](https://www.tandfonline.com/doi/full/10.1080/17477778.2021.1992312): mae'r gydran DES yn byw o fewn byd wedi'i disgrifio gan SD, ac felly mae gennym system $$DES \subset SD$$.

Gadewch i ni fformiwleiddio'r model:

+ Gadewch i $$B_0$$, $$B_1$$, $$B_2$$ a $$B_3$$ cynrychioli niferoedd o lyfrau gyda 0, 1, 2, a 3 gwall, yn ôl eu trefn (`B`),
+ gadewch i $$T$$ cynrychioli cyfanswm nifer y gwallau sydd, lle $$T = \max(B_1 + 2B_2 + 3B_3, 1)$$, sy'n sicrhau bod byth sero gwall (`total_errors`),
+ gadewch i $$\eta$$ cynrychioli'r gyfradd y mae llyfrau newydd yn cael eu hychwanegu i'r siop (`new_book_rate`),
+ gadewch i $$p$$ bod y tebygolrwydd bod gan lyfr un gwall (`prob_error`),
+ gadewch i $$r$$ bod y gyfradd y mae darllenwyr yn adrodd gwallau (`report_rate`),
+ gadewch i $$s$$ bod y gyfradd y mae staff yn canfod gwallau (`search_rate`),
+ gadewch i $$\Lambda$$ bod y gyfradd y mae gwallau yn cael eu hadrodd (`rate`),
+ gadewch i $$c$$ bod nifer o staff (`number_of_servers`),
+ gadewch i $$c_f$$ bod nifer of staff sydd yn rhydd i ganfod a chywiro gwallau (`free_staff`).
+ Byddwn yn tybio fod nifer o wallau mewn pob llyfr yn dilyn dosraniad geometrig (blaendor), felly trwy adael i $$p_i$$ bod y tebygolrwydd bod gan lyfr $$i$$ gwall, yna mae $$p_i = \frac{(1 - p)p^i}{1 - p^4}$$ (`ps`).

Gallwn dynnu llun o'r cydberthynasau fel diagram ciwio/stoc-a-llif fel hyn::

![]({{site.baseurl}}/images/hybrid.jpg){: width="800"}{: .center-image }

O hwn gallwn ysgrifennu i lawr y system o hafaliadau differol sy'n disgrifio'r gydran SD:

$$
\begin{align*}
\frac{dB_0}{dt} &= p_0 \eta + \frac{s c_f}{T} B_1\\
\frac{dB_1}{dt} &= p_1 \eta + \frac{s c_f}{T} (B_2 - B_1)\\
\frac{dB_2}{dt} &= p_2 \eta + \frac{s c_f}{T} (B_3 - B_2)\\
\frac{dB_3}{dt} &= p_3 \eta - \frac{s c_f}{T} B_3
\end{align*}
$$

Y gydran DES yw ciw sengl gyda $$c$$ o weinyddion, a thri dosbarth o gwsmer. Cwsmeriaid yw'r adroddiadau gwall, ac mae pob dosbarth yn cynrychioli gwallau o lyfrau gydag 1, 2 neu 3 gwall ynddynt. Mae amseroedd rhwng-dyfodi pob dosbarth wedi'i dosrannu'n esbonyddol gyda chyfradd dyfodi $$\Lambda_i = irB_i$$. Mae'n cymryd rhwng 1 a 2 awr, yn unffurf, i gywiro gwall. Mae'r paramedr $$c_f$$ yn ddeinameg a chaiff ei gyfrifo o'r gydran DES.

Ymhellach, wrth gywiro gwall (hynny yw cwblhau gwasanaeth) o fath $$i$$, cymerwn 1 i ffwrdd o $$B_i$$ ac ychwanegwn 1 i $$B_{i-1}$$. Maen hwn yn cynrychioli llyfr yn colli un o'i wallau.


# Cam 2 - Ysgrifennu'r Gydran SD

Nawr ein bod wedi diffinio'r holl gydberthnasau, gallwn ysgrifennu'r gydran SD. Bydd hwn yn ddosbarth Python gyda thri dull: `__init__`; `differential_equations`; a `solve`.

+ `__init__`: mae hwn yn cymryd dadleuon ac yn sefydlu priodweddau'r gwrthrych sy'n cyfateb i'r paramedrau a'r newidynnau uchod. Darn pwysig fan hyn yw i hefyd diffinio'r briodwedd `time`, sef arae NumPy o'r pwyntiau amser y byddwn wedi datrys yr hafaliadau differol drostynt yn rhifiadol. Am nawr, gan fod dim wedi'i ddatys eto, gosodwn hwn i fod fector yn cynnwys sero.

  ```python
    import numpy as np
    from scipy.integrate import odeint
  
    class SD():
        """
        A class to hold the SD component.
        """
        def __init__(
            self,
            initial_number_of_errors,
            new_book_rate,
            prob_error,
            report_rate,
            search_rate,
            **kwargs
        ):
            """
            Initialised the parameters for the SD component
            """
            p = prob_error
            self.ps = [(1 - p) * (p ** i) / (1 - (p ** (4))) for i in range(4)]
            self.B = [[initial_number_of_errors * pi] for pi in self.ps]
            self.new_book_rate = new_book_rate
            self.report_rate = report_rate
            self.search_rate = search_rate
            self.time = np.array([0])
  ```

  Nodwch fan hyn bod `self.B` yn rhestr sy'n cynnwys pedwar rhestr, pob un yn cynrychioli gwerthoedd $$B_0$$, $$B_1$$, $$B_2$$ a $$B_3$$ dros y parth amser. Ar hyn o bryd rydym wedi'u llenwi gyda'u gwerthoedd cychwynnol ar amser 0, hynny yw $$p_i$$ wedi lluosi gan `initial_number_of_errors`.


+ `differential_equations`: mae hwn yn cymryd y fector cyfredol o'r $$B_i$$, y parth amser, a rhai dadleuon eraill a fydd yn newid gyda'r gydran DES, ac yn allbynnu'r pedwar deilliad enydaidd y diffinnir uchod.
  
  ```python
        def differential_equations(self, y, time_domain, free_staff):
            """
            Defines the differential equations that define the system.
            Returns the value of the derivatives for each B_i.
            """
            B0, B1, B2, B3 = y
            total_errors = max(B1 + (2 * B2) + (3 * B3), 1)
            dB0dt = (self.ps[0] * self.new_book_rate) + (self.search_rate * free_staff * ((B1) / total_errors))
            dB1dt = (self.ps[1] * self.new_book_rate) + (self.search_rate * free_staff * ((B2 - B1) / total_errors)  )
            dB2dt = (self.ps[2] * self.new_book_rate) + (self.search_rate * free_staff * ((B3 - B2) / total_errors)  )
            dB3dt = (self.ps[3] * self.new_book_rate) + (self.search_rate * free_staff * ((-B3) / total_errors))
            return dB0dt, dB1dt, dB2dt, dB3dt
    ```

  Fan hyn `y` yw fector o werthoedd cychwynnol (eu gwerthoedd ar adeg y digwyddiad arwahanol olaf) $$B_0$$, $$B_1$$, $$B_2$$ a $$B_3$$. Mae'r dull hwn yn cyfateb yn union i'r system o hafaliadau differol y diffinnir uchod. Y ddadl `time_domain` bydd arae NumPy sy'n cyfateb i'r pwyntiau amser y byddwn yn datrys yr hafaliadau differol hyn drostynt, hynny yw, yr amser o'r digwyddiad arwahanol diwethaf i'r amser presennol. Nid yw'n cael ei defnyddio o fewn y dull, ond mae ei angen er mwyn i SciPy gallu datrys yr hafaliadau yn rhifiadol. Mae un ddadl ychwanegol: `free_staff` ($$c_f$$). Bydd hwn yn dod o'r gydran DES, felly does dim angen i ni boeni am o le mae'n dod eto.


+ `solve`: mae hwn yn defnyddio'r llyfrgell SciPy er mwyn datrys yr hafaliadau differol rhwng y digwyddiadau arwahanol y gydran DES.
  
  ```python
      def solve(self, t, **kwargs):
          """
          Solves the differential equations from
          the time of the pervious event to time t.
          """
          leaving_class = kwargs['leaving_class']
          free_staff = kwargs['free_staff']
          
          # Solve the SD over the relevant time domain
          y = (self.B[0][-1], self.B[1][-1], self.B[2][-1], self.B[3][-1])
          relevant = (self.time_domain <= t) & (self.time_domain >= self.time[-1])
          times_between_events = np.concatenate(
              (np.array([self.time[-1]]), self.time_domain[relevant], np.array([t])),
              axis=None
          )
          results = odeint(
              self.differential_equations,
              y,
              times_between_events,
              args = (free_staff,)
          )
          
          B0, B1, B2, B3 = results.T
          self.B[0] = np.append(self.B[0], B0)
          self.B[1] = np.append(self.B[1], B1)
          self.B[2] = np.append(self.B[2], B2)
          self.B[3] = np.append(self.B[3], B3)
          
          # Add and subtract the current error from it's pool
          f = [1 if i == leaving_class else 0 for i in range(3)]
          self.B[0][-1] = self.B[0][-1] + f[0]
          self.B[1][-1] = max(self.B[1][-1] + f[1] - f[0], 0)
          self.B[2][-1] = max(self.B[2][-1] + f[2] - f[1], 0)
          self.B[3][-1] = max(self.B[3][-1] - f[2], 0)

          # Update the times over which we've already solved the SD
          self.time = np.append(self.time, times_between_events)
  ```

  Prif nod y dull hwn yw defnyddio ffwythiant `odeint` SciPy er mwyn datrys yr hafaliadau differol yn rhifiadol o adeg y digwyddiad arwahanol diwethaf (`self.time[-1]`), i'r amser presennol (y ddadl `t`). Hwn yw'r parth amser `relevant` (neu'r `times_between_events` wrth gynnwys y diweddbwyntiau). Caiff eu cyfrifo trwy gymryd sleisiau o'r `self.time_domain`, heb ei diffinio eto, y dylid fod fector o bwyntiau amser bylchau cyfartal o 0 i'r amser mwyaf byddwn yn rhedeg yr efelychiad.

  Ar ôl datrys yr SD rhwng y digwyddiadau, gallwn ddileu'r gwall a chafodd ei gywiro o'r stoc berthnasol o wallau. Rydym yn gwneud hwn trwy adio neu dynnu o werth diweddaraf pob fector o `self.B`.

  Sylwch, er mwyn gwneud hyn, mae agen dwy ddadl: `leaving_class` a `free_staff`. Caiff y rhain eu rhoi i'r ffwythiant trwy ddadleuon allweddeiriau. Eto, dydyn ni ddim yn gwybod sut i gyfrifo'r rhain eto, dyna yw swydd y gydran DES.


# Cam 3 - Deall sut mae'r Cydrannau SD a DES yn Siarad â'i Gilydd

Nawr mae angen i ni feddwl am sut bydd digwyddiadau'r gydran DES effeithio ar baramedrau'r gydran SD, a pha ddigwyddiadau o'r DES sydd angen gwybodaeth o'r gydran SD. Dyma'r digwyddiadau byddwn yn datrys y gydran SD rhyngddynt. Yn yr achos hwn mae gennym:

+ Rhyddhau unigolion - Wrth ryddhau unigolyn, mae angen i ni ddiweddaru'r gydran SD trwy symud gwall o un stoc, $$B_i$$, i'r stoc nesa, $$B_{i-1}$$. Bydd hwn yn effeithio ar wrthrych nôd Ciw.
+ Samplu dyfodiadau - Mae'r dosraniadau amseroedd rhwng-dyfodiad yn dibynnu ar baramedrau o'r gydran SD, felly pan fyddwn yn samplu dyfodiadau mae angen sicrhau bod gennym baramedrau mwyaf diweddar o'r gydran SD. Bydd hwn yn effeithio ar wrthrych dosraniad Ciw.

Yn ogystal â rhain, mae hefyd angen i ni ddatrys yr SD ar ddiwedd yr efelychiad, rhwng y digwyddiad olaf ac amser terfyn yr efelychiad.


# Cam 4 - Ysgrifennu Templed ar gyfer y Gydran DES

Yn gyntaf ysgrifennwn wrthrych efelychu cyffredinol sy'n cynnwys y gydran SD a ysgrifennwn uchod. Mae hwn yn etifeddu o ddosbarth `Simulation` Ciw, ac yn ychwanegu'r priodweddau a dulliau priodol er mwyn siarad gyda'r gydran SD.

Noder, efallai bydd angen i ni ail-ysgrifennu hwn nes ymlaen i sicrhau bod yr holl wybodaeth gywir yn cael eu pasio i bob gwrthrych, ond am nawr:

```python
import ciw

class HybridSimulation(ciw.Simulation):
    """
    A Simulation object that includes the SD component as an
    attribute and communicates with it at the relevant points
    of the simulation.
    """
    def __init__(self, network, **kwargs):
        """
        Initialises the HybridSimulation object.
        Creates and attaches the SD component.
        """
        self.SD = SD(**kwargs)
        super().__init__(network=network, node_class=HybridNode)
        
    def simulate_until_max_time(self, max_simulation_time, n_steps):
        """
        Runs the simulation until the max_simulation time.
        Creates the time domain, runs the simulation, and solves
        the SD component one last time.
        """
        self.SD.time_domain = np.linspace(0, max_simulation_time, n_steps)
        super().simulate_until_max_time(max_simulation_time)
        self.SD.solve(
            t=max_simulation_time,
            leaving_class=None,
            free_staff=None
        )
```

+ Ail-ysgrifennwyd y dull `__init__`. Mae hwn yn ychwanegu achos i'r dosbarth `SD` fel priodwedd. Mae hefyd yn sicrhau ein bod yn defnyddio `HybridNode` (heb ei ddiffinio eto) yn lle dosbarth nôd arferol Ciw.

+ Ail-ysgrifennwyd y dull `simulate_until_max_time`. Yn gyntaf, rhoddir priodwedd `time_domain` i'r gydran SD. Mae hwn yn arae o `n_steps` pwynt amser bylchau cyfartal rhwng 0 a'r `max_simulation_time`. Yna, ar ôl rhedeg yr efelychiad, caiff y gydran SD ei ddatrys unwaith eto o amser y digwyddiad olaf i'r `max_simulation_time`.


# Cam 5 - Cwblhau Ysgrifennu'r Gydran DES

Gwnaethon ni adnabod dau ddigwyddiad lle mae'r gydran DES angen rhyngweithio gyda'r gydran SD: rhyddhau unigolion, a samplu amseroedd rhwng-dyfodi. Cymerwn ni rhain yn eu tro:

+ **Rhyddhau unigolion:**
  Yn gyntaf, er mwyn datrys y gydran SD, mae angen pasio `free_staff` iddo, sy'n cynrychioli'r nifer o aelodau staff sydd heb wedi bod yn brysur ers y digwyddiad olaf. Felly, y peth cyntaf sydd angen i ni wneud yw creu gwrthrych `HybridNode`, sy'n etifeddu o wrthrych `Node` Ciw, ac sy'n tracio faint o weinyddion rhydd sydd (bydd angen i ni osod gwerth cychwynnol y briodwedd hon ar ddechrau'r efelychiad nes ymlaen):

  ```python
  class HybridNode(ciw.Node):
      """
      A Node object that communicates with the SD component at
      the relevant points of the simulation.
      """
      def update_free_staff(self):
          """
          Updates the `free_staff` attribute with the number
          of staff that are currently free.
          """
          self.free_staff = sum(not s.busy for s in self.servers)
  ```
  
  Nawr mae angen i ni ail-ysgrifennu'r dull `release` fel ei fod yn datrys y gydran SD. Mae un peth ychwanegol sydd angen: `leaving_class`, dosbarth y cwsmer sydd yn cael ei ryddhau. Cawn hwn yn llinell gyntaf y dull isod. Yna, rydym yn rhyddhau'r unigolyn fel arfer, datrys yr SD, a diweddaru'r nifer o staff sydd ddim yn brysur.

  ```python
      def release(self, next_individual_index, next_node):
          """
          Releases the current individual at the end of their service.
          Solves the SD component.
          """
          leaving_class = self.all_individuals[next_individual_index].customer_class
          super().release(next_individual_index, next_node)
          self.simulation.SD.solve(
              t=self.get_now(),
              leaving_class=leaving_class,
              free_staff=self.free_staff
          )
          self.update_free_staff()
  ```

  Nawr, cofiwch dywedon ni bod angen gosod gwerth cychwynnol `free_staff` ar ddechrau'r efelychiad. Felly ychwanegwn linell yn gwneud hynny i'r dull `simulate_until_max_time` o Gam 4, ac wedyn pasiwn y briodwedd honno i'r gydran SD wrth iddo ddatrys yr hafaliadau differol. Felly mae'r dosbarth `HybridSimulation` yn edrych fel:

  ```python
  class HybridSimulation(ciw.Simulation):
      """
      A Simulation object that includes the SD component as an
      attribute and communicates with it at the relevant points
      of the simulation.
      """
      def __init__(self, network, **kwargs):
          """
          Initialises the HybridSimulation object.
          Creates and attaches the SD component.
          """
          self.SD = SD(**kwargs)
          super().__init__(network=network, node_class=HybridNode)
          
      def simulate_until_max_time(self, max_simulation_time, n_steps):
          """
          Runs the simulation until the max_simulation time.
          Sets the `free_staff` attribute, creates the time
          domain, runs the simulation, and solves the SD
          component one last time.
          """
          self.nodes[1].free_staff = self.nodes[1].c
          self.SD.time_domain = np.linspace(0, max_simulation_time, n_steps)
          super().simulate_until_max_time(max_simulation_time)
          self.SD.solve(
              t=max_simulation_time,
              leaving_class=None,
              free_staff=self.nodes[1].free_staff
          )
  ```


+ **Samplu amseroedd rhwng-dyfodiad:**
  
  Wrth samplu amser rhwng-dyfodiad ar gyfer cwsmeriaid dosbarth $$i$$, y gyfradd dyfodi yw $$\Lambda_i = irB_i$$, ac felly mae angen y wybodaeth fwyaf diweddar o'r gydran SD. Felly cyn samplu amser rhwng0dyfodiad, mae angen datrys y gydran SD. Bydd hwn yn digwydd o fewn y gwrthrych dosraniad. Felly byddwn yn creu dosbarth dosraniad newydd trwy etifeddu o ddosbarth dosraniad cyffredinol Ciw.

  Nawr mae gennym tri dosbarth o gwsmer, pob un gyda chyfradd dyfodi gwahanol. Felly mae angen tri gwrthrych dosraniad gwahanol. Gallwn greu'r rhain gyda ffwythiant, yn allbynnu gwrthrych gwahanol ar gyfer pob $$i$$:

  ```python
  def get_arrival_distribution(i):
      """
      Creates a distribution class and returns and instance of that class.
      Creates a distribution class for arrivals from B_i.
      Solves the SD component before sampling.
      """
      class SolveSDArrivals(ciw.dists.Distribution):
          def sample(self, t=None, ind=None):
              if t > 0:
                  self.simulation.SD.solve(
                      t=t,
                      leaving_class=None,
                      free_staff=self.simulation.nodes[1].free_staff
                  )
              rate = self.simulation.SD.B[i][-1] * i * self.simulation.SD.report_rate
              return ciw.dists.Exponential(rate).sample()
      return SolveSDArrivals()
  ```
  
  Yn union fel [dosraniadau cwstwm eraill](https://ciw.readthedocs.io/en/latest/Guides/set_distributions.html), mae angen i ni ail-ysgrifennu'r dull `sample`. Yn gyntaf datryswn y gydran SD, yna cyfrifwn y gyfradd trwy ddefnyddio paramedrau'r gydran SD, yna gallwn samplu o ddosraniad Esbonyddol gan ddefnyddio'r gyfradd honno.


# Cam 6 - Cyfuno Popeth a Diffinio'r System

Nawr mae gennym yr holl wrthrychau sydd angen arnom i ddiffinio'r system, adeiladu'r gwrthrych efelychu, a'i rhedeg. Isod yw'r system gydag 8 aelod o staff, cyfanswm o 200 gwall i ddechrau, $$\eta = 100$$, $$p = 0.1$$, $$r = 1$$, $$s = 0.4$$. Yr unedau amser yw diwrnodau.

```python
N = ciw.create_network(
    arrival_distributions={
        'Class 0': [get_arrival_distribution(1)],
        'Class 1': [get_arrival_distribution(2)],
        'Class 2': [get_arrival_distribution(3)]},
    service_distributions={
        'Class 0': [ciw.dists.Uniform(1/24, 2/24)],
        'Class 1': [ciw.dists.Uniform(1/24, 2/24)],
        'Class 2': [ciw.dists.Uniform(1/24, 2/24)]},
    number_of_servers=[8]
)

Q = HybridSimulation(
    network=N,
    initial_number_of_errors=200,
    new_book_rate=100,
    prob_error=0.1,
    report_rate=1,
    search_rate=0.4
)
```


# Cam 7 - Rhedeg yr Efelychiad a Chasglu Canlyniadau

Nawr gallwn redeg yr efelychiad am 6 wythnos. Fan hyn dewision i ddatrys y gydran SD mewn camau amser o $$100^{fed}$$ diwrnod.

```python
n_weeks = 6
Q.simulate_until_max_time(
	max_simulation_tim=n_weeks * 7,
	n_steps=n_weeks * 7 * 100
)
```

Unwaith mae wedi gorffen rhedeg, gallwn arsylwi'r cydrannau DES ac SD er mwyn cael canlyniadau. E.e., fan hyn rydym yn gallu edrych ar gyfanswm nifer o wallau dros y parth amser:

```python
total_errors = Q.SD.B[1] + (2 * Q.SD.B[2]) + (3 * Q.SD.B[3])    
```

Er mwyn esmwytho effaith amrywioldeb a achosir gan haprwydd, dylwn redeg nifer o dreialai a chymryd cyfartaleddau. Gan ddefnyddio Pandas neu NumPy gallwn gymryd cyfartaleddau dros y treialai _ar gyfer pob cam amser yn y parth amser_. Mae hwn yn rhoi canlyniadau cyfres amser llyfn.



# Arbrofion

Nawr bod yr efelychiad hybrid wedi'i adeiladu ac rydym yn gwybod sut i'w rhedeg, gallwn ei ddefnyddio er mwyn deall y system. Dyma ddwy enghraifft:

Yn gyntaf efallai hoffwn wybod, ar gyfer rhyw set o baramedrau, os yw cyfanswm nifer o wallau yn cyrraedd cyflwr cyson, neu yw'n cynyddu'n afreolus. Gallwn edrych ar gyfartaledd `total_errors` dros amser. Gallwn gymharu hwn ar gyfer gwahanol werthoedd o $$r$$ a wahanol werthoedd o $$c$$. Mae pob paramedr arall yn aros yn gyson. Wrth blotio'r cyfartaledd dros 18 treial a chymryd cyfartaledd newidiol, cawn:

![]({{site.baseurl}}/images/hybrid_total_errors_over_time_by_server_by_prob_cy.jpeg){: width="1000"}{: .center-image }

Pan mae $$r=0.05$$ mae cyfanswm nifer o wallau yn aros yn sefydlog, er bod ganddo amrywioldeb uchel, ar gyfer pob un nifer of staff y modelir. hefyd, mae'r gwerth sefydlog hwn yn lleihau wrth i'r nifer o weinyddion cynyddu. Wrth i $$r$$ cynyddu, mae'r gwerthoedd sefydlog hyn hefyd yn cynyddu. Serch hynny, gallwn hefyd gweld fod yna rhai cyfuniadau o $$r$$ ac $$c$$ lle nad yw'r cyfanswm o wallau yn aros yn sefydlog, ond maent yn cynyddu'n afreolaidd - er enghraifft $$r=0.2$$ ac $$c=6$$. O'r patrymau hyn, efallai byddwn yn dyfalu bod y trothwy ar gyfer y nifer o weinyddion sydd angen ar gyfer sefydlogrwydd yn cynyddu wrth i $$r$$ cynyddu.

Nesaf byddwn yn sefydlogi $$r$$ ac ymchwilio'r nifer o wallau ar ôl 8 wythnos wrth i ni gynyddu'r nifer of staff. Mae'r plotion focs a ffidil yn dangos y dosraniad o'r cyfanswm o wallau dros 50 treial, ac mae'r llinell yn dangos y cymedr dros y treialai:

![]({{site.baseurl}}/images/hybrid_total_errors_by_server_cy.jpeg){: width="800"}{: .center-image }

Gwelwn fod yna cwymp serth yn niferoedd o wallau hyd at $$c = 12$$, a chwymp mwy ysgafn ar ôl y pwynt hwn, Efallai bod hwn yn dangos pan mae $$c \leq 12$$ nid yw'r system yn cyrraedd cyflwr cyson ac mae'r nifer o wallau y adroddwyd yn cynyddu yn y ciw; ond pan mae $$c > 12$$ mae'r system yn cyrraedd cyflwr cyson, ac mae'r staff ychwanegol yn gweithio'n galed yn canfod gwallau yn eu hamser rhydd, ac felly'n lleihau'r cyfanswm nifer o wallau ar ôl 8 wythnos. Yn y modd hwn, gall Amazon Kindle penderfynu, os hoffent llai na 50 gwall yn ei siop ar ôl 8 wythnos, bydd angen iddynt gyflogi o leiaf 30 aelod o staff.


_Mae'r holl côd a defnyddiais er mwyn creu'r canllaw hwn ar gael yn: [https://github.com/geraintpalmer/KindleErrors](https://github.com/geraintpalmer/KindleErrors)_.
