---
layout     : post
title      : "How much of English life has Elizabeth II reigned over?"
language   : english
comments   : true
---

This week Her Majesty Queen Elizabeth II sadly passed away. On the news an interviewee said "We are so lucky to have live during her reign". That got me thinking, exactly _how lucky_ are we? Here I want to calculate the proportion of English life lived during her reign.

I will restrict this analysis to England as they have a more consistent royal history and population statistics than the other nations and realms. I will only consider English history since 1066, the invasion of William the Conqueror.

Since then England has been under the reign of 42 monarchs from William I to the newly proclaimed Charles III. So Elizabeth II has reigned over 1/42 = 2.3% of English life right? No, as each monarch reigns for different amounts of time.

Elizabeth II reigned from 06/02/1952 to 08/09/2022, that is 70.57 years, out of 956.7 years of English history. So Elizabeth reigned over 70.57 / 956.7 = 7.376% of English life? Not necessarily, as there are far more people living in England today than there were in medieval times, and so more life to reign over.

[This Wikipedia page](https://en.wikipedia.org/wiki/Demography_of_England) combines a number of sources in order to give the estimated population of England from 1086 to the present day. Linearly interpolating between data points:

![]({{site.baseurl}}/images/pop_england_en.png){: width="500"}{: .center-image }

In this image we can see the rapid increase in population from the early nineteenth century due to the industrial revolution. We can also see a sudden drop in population during the twelfth century due to the black death, and a kink in the mid twentieth century due to the two world wars.

The area under this curve should give an estimate for the total number of life years lived in England between 1066 and today. Therefore narrower slices can give an estimate of the amount of life years lived in England during a shorter period, for example a monarch's reign. The following shaded area represents the total number of life years lived in England during the reign of Queen Victoria (1837-1901).

![]({{site.baseurl}}/images/pop_victoria_en.png){: width="500"}{: .center-image }

Dividing this by the total area under the curve will give an estimate of the proportion of the number of life years lived in England under a monarch. I did this for all 42 monarchs. The following table lists some of the most famous:

|Monarch | Percent
|---|----|
|Elizabeth II | 34.8% |
|Victoria | 13.9% |
|George V | 9.4% |
|George VI | 6.1% |
|George III | 5.0% |
|... | ... |
|Edward III | 1.765% |
|Elizabeth I | 1.668% |
|Edward I | 1.638% |
|... | ... |
|Henry VIII | 0.982% |
|... | ... |
|Richard III | 0.0465% |
|Edward VIII | 0.3456% |
|Edward V | 0.004588% |
|---|----|


So, by this metric, **I estimate that Queen Elizabeth II has reigned over 34.8% of English life since 1066!** That's over a third. While poor Edward V only reigned over 0.004588% of English life, for less than three months while locked in the Tower of London. Interestingly, 0.6136% of English life was experienced during the Interregnum, the eleven years in the mid seventeenth century England had no monarchy at all.


This historic moment has also prompted me to update [my pervious effort](https://twitter.com/GeraintPalmer/status/1095425414036709376) to visualise the English royal timeline:


![]({{site.baseurl}}/images/timeline.jpeg){: .center-image }


*Note:* Throughout this post I've assumed that every year is 365 days. That not only disregards leap years, but also glosses over the [mess of historical calendars](https://en.wikipedia.org/wiki/Calendar_Act_1750) and year lengths and labelling.


