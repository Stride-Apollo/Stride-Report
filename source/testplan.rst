Testplan
========

Algemeen
--------

We gebruiken gtest voor onze tests. De tests zelf splitsen we op in 2 grote delen, de unit tests die normaal snel uitgevoerd kunnen worden en de scenario tests die een pak meer tijd in beslag nemen. Via een parameter die at runtime wordt meegegeven kiezen we tussen de twee delen.

Continuous Integration
----------------------

Er zijn 4 verschillende keuzes te maken:

- (korte) unit tests of (lange) scenario tests

- gcc of clang

- TBB of OpenMP

- met of zonder MPI (maar, zie Multiregio hieronder)

Unit tests worden dikwijls uitgevoerd; namelijk bij alle commits. Een pull request mag niet doorgaan tenzij CI zegt dat het ok is (bovenop een manuele review). Zo’n snelle test bestaat dus uit 8 verschillende configuraties, die telkens de volledige testsuite draaien. 

Opdrachten
----------

Voor elke deelopdracht overlopen we even hoe we deze functionaliteit gaan testen.

HDF5 checkpointing

Checkpointing testen we op verschillende manieren. Een eerste vorm van testen is het nagaan van het formaat en de inhoud van verschillende hdf5 files. Hierbij maken we een onderscheid tussen happy-day scenario files en foutieve files (niet conform met het opgestelde formaat, verschillend van de toestand van de simulator, ...). Vervolgens doen we een aantal scenario tests van verschillende tussentijdse checkpoints. Ten slotte vergelijken we de uitkomsten van continue runs (runs die van begin tot einde zijn uitgevoerd) met checkpointed runs (runs die starten vanuit een checkpoint).

TBB Parallellisatie

Om TBB te testen hebben we gekozen om eerst scenario’s te schrijven, dan deze scenario’s manueel uit te voeren. We gaan vervolgens de bekomen resultaten na. Als deze resultaten geen fouten bevatten, gebruiken we deze om test cases (gtest) te maken.

Populatie generator

Er zijn enkele klassen die de generator helpen bij het genereren van de populatie. Zo zijn er bijvoorbeeld de alias-methode en de klasse die berekeningen doet met geo-coördinaten. Deze hulpklassen zullen getest worden op zowel gewone scenario's als randgevallen.
De tests van de generator zelf worden onderverdeeld in 3 delen. Het eerste onderdeel zijn de input files. Als deze files semantisch of syntactisch niet correct zijn moet de generator hiermee om kunnen gaan. Ten tweede moeten we de gegenereerde verdelingen nakijken. Extreme waardes zouden bij voldoende grote populaties niet mogen voorkomen. Het is bijvoorbeeld bijna onmogelijk dat er in een random gegenereerde populatie van 1 000 000 mensen met een werkloosheidsgraad van 10% 700 000 werklozen zijn. Ten slotte wordt er ook nog getest op de effectieve waarden. Bijvoorbeeld: alle gezinssamenstellingen zijn van het begin af aan bekend. Het zou niet mogen dat er een familie wordt gegenereerd waarvan de samenstelling eigenlijk niet bestaat.

Multiregio

In onze architectuur plannen we om de details van de MPI communicatie volledig weg te abstraheren in een interface die gelijk is voor zowel shared-memory implementatie als voor de MPI implementatie. Eens de implementatie van die interface voor MPI klaar is, testen we dit uitgebreid. Wegens de extra complexiteit die gedistribueerd testen met zich meebrengt, gaan we dit manueel doen (en dus liefst maar 1 keer). Testen met meerdere processen (en niet meerdere machines) kan wel iets meer herhaald worden.
In de build configuratie kan MPI nog steeds aan of af gezet worden, maar er worden geen unit tests gedraaid die specifiek communicate tussen meerdere machines testen. Dit is dus eigenlijk specifiek om te zien of alles nog compileert en niet interfereert met andere componenten.
Om unit tests te schrijven voor multiregio, gebruiken we dan uitsluitend de shared-memory implementatie. In theorie, als de interface zich hetzelfde gedraagt voor shared-memory als voor MPI, is dit voldoende. Om dat op te vangen plannen we om extra aandacht te besteden aan code reviews van MPI-specifieke code.

Wetenschappelijke Visualisatie

Wetenschappelijke visualisatie is voornamelijk een GUI implementatie en is dus zeer moeilijk automatisch testbaar. De kwaliteit van deze visualisatie is ook niet objectief meetbaar. We zullen de wetenschappelijke visualisatie voornamelijk doorheen het project manueel testen.
