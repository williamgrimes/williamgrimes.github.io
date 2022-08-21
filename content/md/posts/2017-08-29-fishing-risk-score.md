{:title "A Fishing Risk Framework from Satellites and Ocean Data"
 :layout :post
 :toc false
 :tags  ["illegal-fishing" "machine-learning"]}

This proof-of-concept system assess vessels in a risk framework considering multiple factors to suggest the likelihood that a vessel has been engaging in illegal, unregulated, or unreported (IUU) fishing. The framework combines automatic identification system (AIS) tracking data with satellite imagery in construction of a risk framework. The framework combines several indicators including: the likelihood that a vessel has previously fished in a marine protected area (MPA) or exclusive economic zone (EEZ), and the intermittency of the vessel's AIS signal.

Vessel risk indicators may be considered individually, or weighted according to the users interest, or combined into a unified vessel risk score. This information is displayed in a front end web application, which gives governments, NGOs, retailers, and enforcement agencies the information to distinguish responsible and legitimate vessels from vessels engaging in IUU fishing. For example, this could be used by retailers to check the risk score of vessels that supply their tuna, or to guide enforcement agencies in choosing which areas to patrol.

The below image demonstrates how the tool can be interacted with to show for a unique vessel its aggregate risk score as well as the components contributing to this score, and it's most recent location.

<div align="center">
    <img src="/img/front_end.jpg" alt="Front End" style="width:60%">
</div>

### Background
Illegal and overfishing are devastating our oceans. It is estimated that 70% of global fisheries are overexploited and many are now on the brink of collapse. Tuna populations, which are a critical apex predator in many marine ecosystems, have declined by over 90% in the past 40 years. Unless serious action is taken, we may be on the brink of large scale fisheries collapse, which could devastate the environment and the livelihoods of millions around the world that depend on such fisheries.

Given concern about the challenges facing our oceans, the United Nations convened a High Level Summit in June 2017 at the UN Headquarters in New York to review progress on the Ocean SDG (Goal 14). At this summit, the World Economic Forum helped convene major retailers, fishery firms, Governments and Civil Society around a Declaration to fully trace our most precarious fisheries by 2020, starting with Tuna fisheries. DSSG also made a commitment to help develop Data Science and Machine Learning Talent to support such efforts on our oceans.

In just the last 5 years, new data tracking technologies have come online, triggered by low cost satellites and sensors and rapid advances in data processing and machine learning. This has given fisheries managers powerful new resources to track fishing activity globally, and identify risky or illegal activity.

One particularly challenging problem historically had been to identify and end Illegal, Unreported and Unregulated fishing (IUU). These IUU fishing techniques include illegally extracting fish from waters of other nations, removing fish from designated Marine Protected Areas, catching fish using illegal and ecologically damaging techniques, and under-declaring fish by transshipment at sea. Such practices are especially rife in the rich tropical waters of Southeast Asia due to the burgeoning demand in the region, and challenges of enforcement.

Our goal is to create an Open-Source Risk Tool by combining multiple satellite data sources (including combining AIS with satellite imagery and machine learning) to help combat IUU fishing, and creating a ‘DSSG Fishing Risk Score’. This data science approach to detecting IUU fishing could ultimately guide governance, inform policy making and improve enforcement. In this effort we are advised by a global network of experts. The DSSG Fishing Risk Framework, Vessel Scoring, and project results will be public, and all code will be made available as open source to contribute to the ongoing efforts of NGOs, Universities and International Organizations to end IUU fishing globally.

## Presentation
<div align="center">
<iframe title="YouTube video player" class="youtube-player" type="text/html"
width="560" height="315" src="http://www.youtube.com/embed/f4Q858hmZP0"
frameborder="0" allowFullScreen></iframe>
</div>

## People
**Fellows:** William Grimes, Iván Higuera-Mendieta, Shubham Tomar

**Mentor:** Jane Zanzig

**Project Manager:** Paul van der Boor

**Project Partner:** World Economic Forum’s New Vision for Oceans Initiative (Nishan Degnarain), Spire (Theresa Condor, Kyle Brazil), Digital Globe (Rhiannan Price, Har-Noy, Shay), Planet Labs (Will Marshall, Joseph Mascaro)

**Project Chair:** Euro Beinat

**Expert Advisors:** Steve Adler (IBM Watson), Dan Schaeffer (Pew Trusts), Prof. Douglas McCauley (UCSB), Dr. Gregory Stone (Conservation International), Paul Wood (Skytruth, Nathan Miller), Kim Friedman (FAO)

## Resources
* <a href="https://github.com/DSSG2017/wef_oceans/" target="_blank">Github</a>
* <a href="https://dssg.uchicago.edu/project/fishingriskframework/" target="_blank">Website</a>
* <a href="/docs/poster_wef.pdf" target="_blank">Poster</a>
* <a href="http://www.youtube.com/embed/f4Q858hmZP0" target="_blank">Presentation</a>

