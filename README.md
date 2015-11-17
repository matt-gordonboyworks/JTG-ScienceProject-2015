# JTG-ScienceProject-2015
Jack Gordon's 2015 Edison Elementary Science Fair Project

##Me: What question do you want to answer for the science fair this year?
##Jack: What's the best sort of renewable energy for Denver, wind or solar?

After a school field trip to NREL in Golden, CO, and during his classroom module on energy, Jack has become very interested in renewable energy.  When it came time to choose a science fair project for this year, Jack envisioned an experiment that would help test whether solar or wind power produced more usable electricity for our location in Denver.

##Experimental Setup
For the experimental setup, we opted to build a homemade wind turbine and buy a Goal Zero solar panel off eBay.  The wind turbine consists of a 3-d printed darrieus VAWT turning a nema-17 stepper motor as an alternator via a 3:1 reduction gear.  The solar panel was hacked to bypass the USB charging circuitry and directly connect to the power coming off the panel.  To provide a more direct comparison between the DC power produced by the panel and the AC power produced by the turbine, the turbine alernator's phases were fed through a bridge rectifier (that Dad designed and Jack built,) and a smoothing capacitor to provide DC output.
For data logging and reporting, we selected a Particle Photon microcontroller due to ease of programming and ease of integration with web services for data logging & analysis.  DC power is fed independently from the solar panel and the turbine's rectifier to a voltage splitter consisting of a 470ohm and 220ohm resistor; this accounts for the 3.3v limit on the Photon's analog pins.  Our voltage divider reduces the input voltage according the the following equation:
##Vout = R2/R1+R2 * Vin, or 220/470+220 * Vin
What we're really interested in, however is the power generated by each of the two generation systems.  To satsify Watt's law (P=V*I) we need to know the current in the system.  Fortunately, Ohm's Law:
##I=V/R
tells us that our voltage divider represents a known resistive load from which we can calculate current, given a measured voltage:
##I=V/(220+470)
That about sums up the circuit design of the whole contraption, at least the relevant parts.  There are also lots of jumpers, breadboards and a voltage regulator involved to power the Photon.
##Logical Design
In the Photon firmware, we're reading voltage from the A0 and A1 pins, applying the appropriate calculations, and storing variables for voltage, current and power from each of the two systems.  Once each second, we're reading those pins and then writing the values to an Azure Event Hub via a Particle webhook.  Azure Table Storage is used for the storage of the logged data, and PowerQuery/PowerView are being used in Excel to visualize the data.
#Teachable Moments
Why such a complicated project for a 9 year old?  First and foremost, we'll be intellectually honest and admit that Dad did all of the system design, much of the assembly and all of the coding.  Design & fabrication of a mechanical system like this, writing the firmware for the microcontroller and cloud-enabling the whole solution are beyond the grasp of most 9 year olds, Jack included.  First, there's the flip, "why not?"  More importantly, in Dad's opinion is the opportunity for a child to observe that complex, multidiscplinary projects can be successfully taken on when curiosity and hard work are applied to a series of well organized tasks.  Be it community/national/professional pride, anti-consumerism, the next industrial revolution or the fusion of the artisan and technologist, there's an important lesson in creativity and self-reliance that needs to be intentionally passed down.
##Core Concepts
Beyond the philosophical teachable moments, there are some very practical lessons Jack was able to take from this project experience.
1. If you want to make something real, there's a defined set of steps from envisioning to CAD to CAM to machine control to a real thing in the real world.  Proficiency with these tools makes lots of interesting things possible.
2. Jack developed the basic experimental construct through a series of probing questions.  His original idea was that he'd need to measure how much energy is generated by a wind turbine and a solar panel over time, in the same location.  Dad merely provided the money and labor to make it real.
3. Jack is already thinking about Science Project mk2 - what could we do to improve the systems? How could we be more efficient?  More practical?  Could we actually build something useful?
