---
title: Trenutno Stanje Serverless-a
date: 2024-08-30T00:42:22+02:00
# weight: 1
# aliases: ["/first"]
tags: ["serverless", "architecture", "dev"]
author: "pero020"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

Definicija serverless-a kaže da se u serverless arhitekturi korisnik ne brine o serveru. Uzmemo li za primjer AWS Lambda servis, vidimo da nam on nudi pokretanje našeg koda bez brige gdje i kako se pokreće. Ako pokrenemo Lambda servis i povežemo ga sa serverless DynamoDB bazom podataka, možemo postaviti brojna pitanja. Vrte li se oba servisa na istom računalu? Hoće li njihova komunikacija biti sigurna? Hoće li biti dovoljno brza? Što se događa ako se veza prekine? Što će se dogoditi ako serveru ponestane RAM-a? Ovo su sve pitanja koja bi nam, kao inženjerima, mogla pasti na pamet, ali jednako tako su i pitanja o kojima se u utopijskom serverless-u ne bismo trebali brinuti. Naš posao je smišljati logiku i pisati kod, a posao pružatelja serverless usluge je voditi računa o svemu ispod aplikacijske logike. Današnje stanje serverless servisa nažalost još nije došlo do korisnikove potpune nebrige o serveru, ali se približava.

Opće prihvaćen slučaj u kojemu je dobro koristiti serverless servise kaže: „Ako je promet na aplikaciji rijedak ili nepredvidiv, isplativo ga je napraviti serverless arhitekturom“. S ovom uputom se zajednica softverskih inženjera uvelike slaže, ali ako je usporedimo s definicijom serverless arhitekture iz prethodnog paragrafa, ne postoji jasna poveznica. Razlog tomu je trenutno nedovršeno stanje serverless-a. Zašto bismo koristili serverless samo za aplikacije s varijabilnim prometom? Nije li u svakom slučaju jednostavnije brinuti se isključivo o logičkom kodu aplikacije? Mnogi bi na to pitanje odgovorili s „Bilo bi jednostavnije, ali možda ne bi bilo najefikasnije“. Ovdje dolazimo do razloga zašto je serverless prihvaćen kao dobar izbor arhitekture isključivo za specifične aplikacije. Problem nije u serverless-u samom po sebi nego ograničenosti pružatelja usluga u načinu na koji ga nude. Kao primjer možemo uzeti serverless problem hladnog pokretanja (eng. cold start). Ako korisnik napiše poslovnu logiku za svoju aplikaciju, pružatelj serverless usluge morao bi u skladu s trenutnim tehničkim limitacijama ordrediti je li aplikaciju efikasnije hladno pokrenuti s vremena na vrijeme ili držati je uvijek upaljenu. Sve što korisnik treba učiniti je specificirati koliki mu je vremenski odmak za dobivanje odgovora prihvatljiv, a serverless usluga trebala bi sama procijeniti kojom vrstom konfiguracije i utilizacije servera to najefikasnije postići.

Ukoliko se korisnik brine o tome hoće li za deployment svoje aplikacije koristiti server poput EC2 servisa ili serverless servis poput AWS Lambde i na posljetku izabere Lambdu, korisničko iskustvo već u startu nije u skladu s načelima serverless-a. Korisnik se, iako koristi „serverless“ pristup, brine o vrsti servera koju će iskoristiti, razmišlja o najefikasnijoj konfiguraciji te tek onda izabire serverless u kojemu se naizgled ne brine o tome kakav server se koristi.

Velika je podjela u svijetu IT-a između inženjera koji serverless smatraju budućnošću razvoja svog softvera i onih koji serverless smatraju jednim od alata koji ima svoju svrhu u specifičnim slučajevima. Smatram da su obje grupe u pravu, ali da ne govore o istom pojmu serverless-a. Prva je grupa fokusirana na koncept serverless-a kao arhitekture i usluge koja automatizacijom omogućuje potpuno posvećenje inženjera na pisanje programske logike i maksimalnu utilizaciju hardvera koje svijet posjeduje, dok druga skupina vidi serverless u njegovom trenutnom stanju. Prva skupina slična je vizionarima, a druga realistima te su argumenti i jedne i druge skupine inženjera, u svome pogledu, ispravni.

Vercel-ov deployment NextJS aplikacija primjer je servisa koji se približava utopijskom konceptu serverless-a. Programeri pišu kod te podizanjem koda na Vercelov server, on ga optimizira, čini aplikaciju dostupnom globalno po maksimalnim brzinama, vodi računa o cachiranju podataka, podiže backend resurse na optimalnu vrstu servera i radi mnoge druge funkcije za koje korisnik ne mora znati, no čak i kada bi sve od toga radio savršeno, još uvijek se javlja jedna velika problematika serverless-a, ograničenost pružatelja usluge (eng. vendor lock in). Cijene koje Vercel nudi nisu poput AWS-ovih on-demand usluga koje se naplaćuju iz minute u minutu, ukoliko nam za vlastiti projekt zatreba tehnologija koju Next još ne podržava, bilo iz razloga što je nova ili što nije prioritet Vercelovom timu, nemamo opcije nego privremeno napustiti naš serverless ekosustav i za novu funkciju koristiti novo rješenje, što nas približava mikroservisnom ili preciznije, mikroserverless rješenju. Rješenje za ovaj problem izlazi iz opsega ovoga bloga, ali ga je bitno imati na umu prilikom diskusije o savršenom serverless modelu.