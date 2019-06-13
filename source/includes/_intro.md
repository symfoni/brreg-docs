# Introduction

Velkommen til Brønnøysundregistrenes Aksjeeierbok Utviklerportal (beta). Alle aksjeselskaper skal ha en aksjeeierbok. Denne skal inneholde en oversikt over hvem som til enhver tid er aksjeeiere, og den vil normalt være avgjørende for hvem som kan utøve aksjonærrettigheter. Aksjeeierboken er offentlig - slik at alle har rett til å se den.

<aside class="notice">
Lovhjemmel: <a href="https://lovdata.no/dokument/NL/lov/1997-06-13-44/KAPITTEL_4-1">Lov om aksjeselskaper – kapittel 4 § 4-5.</a>
</aside>

## Hva er en aksjeeierbok
Når en aksjeeier er innført i aksjeeierboken, skal selskapet gi aksjeeieren melding om dette. Aksjeeierboken skal oppdateres ved eierskifte eller pantsettelse av aksjer etter fastsatte regler i aksjeloven (§ 4-7).

Aksjer kan fritt selges eller gis bort uten betaling, med mindre noe annet fremkommer av lov, vedtekter eller avtale mellom aksjeeierne. Ved salg skal prisen normalt beregnes ut fra markedsverdi. Salg under markedsverdi kan også skje. Da foreligger det et gavesalg. På samme måte som når aksjer gis bort, vil dette kunne utløse en skatteplikt.

Når aksjonærer selger eller på annen måte realiserer aksjer, vil gevinsten være skattepliktig.

Aksjeloven har regler om samtykke ved erverv av aksjer, og regler om forkjøpsrett for de andre aksjonærene. Avtale om overføring av aksjer skal meldes til styret i aksjeselskapet av den som overtar aksjene. Avtalen bør som et minimum inneholde hvem avtalen gjelder for, hvor mange aksjer som overføres, og til hvilken pris.

Overføringer gjort i Brønnøysundregistrenes Aksjeeierbok er innrapportert umiddelbart. Den nye aksjeeieren skal ha melding fra selskapet om at han/hun er innført i aksjeeierboken, og hva som er notert.

<aside class="success">Selskapet trenger ikke ytterligere føre egen aksjeeierbok. Løsningen overholder automatisk aksjeloven mtp. datering, krav til tilgjengelighet og krav til oppbevaring.</aside>

Hvis overdragelsen fører til at det skjer endringer i selskapets vedtekter, eller for eksempel at styrets sammensetning endres, skal endringen <a href="https://www.altinn.no/skjemaoversikt/bronnoysundregistrene/registrere-nye-og-endre-eksisterende-foretak-og-enheter---samordnet-registermelding/">meldes til Brønnøysundregistrene på skjemaet "samordnet registermelding"</a>.

<aside class="success">
Selve aksjeoverføringen er ikke nødvendig å melde inn til Aksjonærregisteret når man bruker Brønnøysundregistrenes Aksjeeierbok, da det er automatisk rapportert. 
</aside>

### Avtaler mellom selskapet og selskapets ledelse, aksjonærer eller nærstående
Selskapet og aksjonærene i selskapet kan inngå avtaler med hverandre, men det foreligger da skjerpede krav til fremgangsmåten. Utgangspunktet er at enhver avtale som har en verdi som utgjør mer enn en tidel av aksjekapitalen, skal godkjennes av generalforsamlingen. Fra dette utgangspunktet er det listet opp en del unntak i aksjeloven. Reglene gjelder også for aksjeeiers nærstående, som for eksempel nær familie.

### Aksjonæravtaler
Aksjonæravtale inngås normalt mellom aksjeeierne i et selskap, og regulerer forholdet mellom dem. Aksjonærene er ikke pliktig til å inngå en slik avtale, men det kan være nyttig. Aksjonæravtalen forplikter de aksjeeierne som underskriver avtalen. Det finnes ikke noen krav til hvordan avtalen skal se ut eller hva den skal inneholde. Eksempler på forhold som kan reguleres i en aksjonæravtale er særlige regler knyttet til eierskapet, krav på utbytte, konkurranseklausul, habilitet og krav om arbeidsinnsats.

### Konflikt mellom aksjeeiere
Det er ikke uvanlig at det kan oppstå konflikter mellom aksjonærer om organiseringen av selskapet. Hva som ligger til grunn for konfliktene er i forkant vanskelig å si noe om, men det kan være fornuftig å ha et bevisst forhold til dette. Erfaringsmessig kan det være fornuftig å

* unngå å være to eiere som eier 50 % hver av aksjene, fordi dette vanskeliggjør flertallsbeslutninger
* inngå aksjonæravtale som avklarer hvordan forholdet mellom aksjonærene skal være i tilfelle uenighet
I tilfeller hvor aksjonærene ikke lenger klarer å samarbeide med hverandre, kan tingretten, etter søksmål fra en aksjeeier eller fra selskapet, beslutte innløsning eller utløsning av en aksjeeiers aksjer. Slike søksmål må anses som siste utvei, og det må foreligge tungtveiende grunner.

## Funksjoner i Brønnøysundregistrenes Aksjeeierbok

Som tjenesteleverandør kan man enten bruke Aksjeeierbok SDK (Javascript) til å gjøre read/writes mot aksjeeierbøker, eller man kan utvide registeret med data og funksjonalitet ved å skrive smartkontrakter i Solidity og laste opp til tjenestens blokkjede.

Kom veldig gjerne med tilbakemelding ved å opprette et Issue på Github. Siden dette er en åpen beta står oppfordringen til å bidra tilbake med dine opplevelser spesielt høyt. 

## Users

En bruker er en aksjonær og/eller daglig leder og/eller styreleder. En bruker er enten aktiv eller passiv.

En aktiv bruker er autentisert og kan skrive endringer direkte i aksjeeierboken, som å overføre aksjer eller endre adressen sin. 

En passiv bruker er en aksjonær som ikke er registrert på plattformen. Brukeren kan ikke gjøre endringer i aksjeeierboken, og eventuelle overføringer må legges inn av styreleder på vegne av aksjonæren.

<aside class="notice">
Alle endringer i aksjeeierboken må godkjennes av styreleder. I fremtidige versjoner vil godkjennelsen kunne gis automatisk ved at vedtekter og aksjonæravtaler kontrolleres automatisk.
</aside>

# Installation

TODO How to install the SDK
 