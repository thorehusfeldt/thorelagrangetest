---
layout: post
title: "Indledning"
author: "Thore"
categories: journal
tags: [documentation,sample]
image: cards.jpg
---

Indledning
==========

![image](img/stonehenge2.eps){width="5cm"}

Hvis man vil blive billedhugger,\footnote{
Billedet af stenkredsen ved Stonehenge er taget fra \cite{Pin1808}.}
skal man lære en masse grundlæggende teknikker:
Hvor finder man passende sten?
Hvordan flytter man dem, hvordan virker mejslen, hvordan bygger man et stillads, osv.
Når de grundlæggende teknikker er på plads, er man langtfra nogen berømt kunstner, men selv en sjældent talent kan ikke blive berømt uden at beherske grundlaget.
 Wer die Grundtechniken beherrscht, 
Man behøver ikke kende det hele, inden man går i gang med sin første skulptur
Men man skal være parat til at gå tilbage til grundteknikkerne for at blive bedre og bedre.

Dette indledende kapitel spiller en lignende rolle i bogen. Vi
præsenterer de grundlæggende begreber og metoder for at bedre kunne
beskrive og analysere algoritmer i de senere kapitler. Man behøver ikke
at arbejde sig igennem dette kapitel fra A til Z inden man giver sig i
kast med de følgende kapitler. Vi anbefaler ved første læsning at
studere materialet til og med afsnit  grundigt, og skimme de følgende
afsnit. Afsnit  beskriver notation og terminologi for at beskrive
algoritmers kompleksitet kort og præcist. I afsnit  præsenteres en enkel
beregningsmodel, som gør det muligt at abstrahere bort fra mange af de
komplikationer, der ville opstå ved at tage hensyn til egenskaberne ved
moderne maskinarkitektur. Modellen er tilstrækkelig konkret til at
levere nyttige forudsigelser, men tilstrækkelig abstrakt til at tillade
elegante overvejelser. I afsnit  introduceres et notation for
pseudokode, som minder om et højniveausprogrammeringssprog og tillader
en bekvem beskrivelse af algoritmer end maskinmodellens kode. Desuden
giver pseudokoden mulighed for at benytte notation fra matematikken,
uden at vi behøver at bekymre os om, hvordan denne ville skulle
oversættes til en ægte maskine. Vi vil gøre hyppig brug af kommentarer i
programmerne, både for at øge deres læsbarhed og for at gøre det letter
at føre formelle korrekthedsbeviser. Teknikker for den slags beviser er
genstant for afsnit . Afsnit  indeholder det første omfattende eksempel:
Binærsøgning i en sorteret række. I afsnit  beskrives matematiske
teknikker for programmers kompleksitetsanalyse med vægt på indlejrede
løkker og rekursive procedurekald. For analysen af gennemsnitligt
tidsforbrug har vi brug for yderligere teknikker; disse beskrives i
afsnit . Randomiserede algoritmer, præsenteret i afsnit  , gør brug af
tilfældighed ved under udførelsen at kunne slå plat og krone. Afsnit 
handler om grafer, et begreb som spiller en stor rolle i resten af
bogen. I afsnit  diskuteres spørgsmålet, hvornår man skal betegne en
algoritme som effektiv, og kompleksitetsklasserne $\classP$ og $\NP$
samt den vigtige klasse af $\NP$-fuldstændige problemer. Som alle andre
kapitler slutter kapitlet med implementationsaspekter (afsnit ) og
historiske anmærkninger og videre resultater (afsnit ).

Asymptotisk notation
--------------------

Algoritmeanalysens formål er primært at skabe tilforladelige udsagn om
algoritmers opførsel, bl.a. deres kørselstid, som er både præcise,
kortfattede, almentgyldige og begribelige. Det er selvfølgeligt
vanskeligt at opfylde alle disse krav samtidigt. For fx at beskrive
algoritmens tidsforbrug $T$ kan man opfatte $T$ som en funktion, der
afbilder mængden $\mathscr I$ af alle mulige probleminstanser (eller
*input*) til mængden $\RR_+$ af positive reelle tal. For hver instans
$\Input$ til problemet er da $T(\Input)$ kørselstiden på $\Input$. Denne
detaljeringsgrad fører dog til så overvældende meget information, at det
ville være håbløst at udvikle en brugbar teori. I stedet skal vi
betragte  algoritmens opførsel i et mere mere almengyldigt perspektiv.

Vi vil opdele mængden af instanser i klasser af »lignende« instanser og
så sammenfatte algoritmens opførsel på instanser fra samme klasse som et
eneste tal. Det mest gængse kriterium for klassedelingen er instansens
*størrelse*. Sædvanligvis er der en naturlig måde for at bestemme
instansens størrelse. Størrelsen på et heltal er antallet af cifre i
dens binærrepræsentation; størrelsen af en mængde er dens kardinalitet,
dvs. antallet af elementer. Instansstørrelsen er altid et naturligt tal.
Sommetider bruger man mere end én parameter for at angive størrelsen
på en instans; fx er det gængs at karakteriser størrelsen på en graf i
termer af både antal knuder og antal kanter. Vi vil i første omgang se
bort fra de komplikationer, der optræder herved. Mængden af alle
instanser af størrelse $n$ skrives som $\mathscr I_n$ for $n \in mathbf N$. For
instanser af størrelse $n$ kan vi interessere os for maksimale, minimale
og gennemsnitlige kørselstider, defineret på følgende måde: [^1]
\[
T(n) = \begin{cases}
  \max\{T(I)\colon I\in \mathscr I_n\} &
  \text{»i værste fald«}\,, \\
  \min\{T(I)\colon I\in \mathscr I_n\} &
\text{»i bedste fald«}\,, \\
      \displaystyle\frac{1}{|\mathscr I_n|}\sum_{I\in \mathscr I_n}T(I) &
  \text{»i gennemsnit«}\,.
\end{cases}
\]
Den mest interessante af disse størrelser er kørselstiden i
værste fald, fordi den udgør den mest omfattende garanti for algoritmens
opførelse. Sammenligningen af opførelsen i bedste og værste fald
fortæller os, hvor stor variation i kørselstid der kan forekomme mellem
instanser i samme størrelsesklasse. Når afvigelsen mellem bedste og
værste fald er meget stor, kan sommetider en analyse af den
gennemsnitlige kørselstid give nærmere indsigt i algoritmens faktiske
tidsforbrug. Vi skal se nærmere på en eksempel i afsnit .

Vi går endnu et skridt videre i vores forsøg på at informationen mere
overskuelig ved at gøre analysen grovere: Vi koncentrerer os på
kørselstidens *vækstrate* ved at bruge *asymptotisk analyse*. To
funktioner $f(n)$ og $g(n)$ har samme *vækstrate*, hvis der eksisterer
positive konstanter $c$ og $d$, så uligheden $c\le f(n)/g(n)\le d$
gælder der for alle tilstrækkeligt store $n$. Funkionen $f(n)$ *vokser
hurtigere* end $g(n)$, hvis der gælder for hver positive konstant $c$,
at uligheden $f(n)\ge c\cdot g(n)$ for alle tilstrækkeligt store $n$.
For eksempel har funktionerne $n^2$, $n^2 + 7n$, $5n^2 - 7n$ og
$\frac{1}{10}n^2 + 10^6 n$ alle samme vækstrate. Desuden vokser disse
funktioner alle hurtigere end funktionen $n^{3/2}$, som selv vokser
hurtigere end funktionen $n \log n$. Læg mærke til, at vækstraten
fokuserer på opførslen for store $n$, hvilket også er meningen med
begrebet »asymptotisk« i »asymptotisk analyse«.[^2]

Hvad er grunden til, at vi kun interesserer os for vækstrate og
opførslen for store $n$? Hovedårsagen for at udvikle effektive
algoritmer er netop ønsket om at kunne håndtere store instanser. Når
algoritmen $A$ har en lavere vækstrate end algoritmen $B$ for samme
problem, vil $A$ typisk være $B$ overlegen for store $n$. Desuden er
vores maskinmodel i forvejen en abstraktion af de faktiske kørselstider
og nøjes med at bestemme en konkret maskines opførelse inden for en
maskinafhængig konstant faktor. Derfor vil vi ikke skelne mellem
algoritmer, hvis kørselstider har samme vækstrate. Vores indskrænkning
til vækstrater har desuden den glædelige sideeffekt, at algoritmers
kørselstider kan karakteriseres af meget enkle funktioner. Vi vil dog i
bogens implementationsafsnit regelmæssigt se lidt nærmere på de
maskinnære detaljer, som den asymptotiske analyse er blind for. Generelt
bør læseren ved studiet og anvendelsen af algoritmer i denne bog altid
spørge sig selv, om det asymptotiske perspektiv er relevant.

Vi skal nu indføre den gængse notation for funktioners *asymptotiske
opførsel*. Her betegner $f(n)$ og $g(n)$ funktioner, som afbilder
naturlige tal til ikke-negative reelle tal. Vi definerer
$$\begin{aligned}
  O(f(n)) & = \{\,g(n)\colon\exists c>0\colon\exists n_0\in\mathbf N_+\colon\forall n\geq n_0\colon g(n)\leq c\cdot f(n)\}\,,\\
\Omega(f(n)) & = \{\,g(n)\colon\exists c>0\colon\exists n_0\in\mathbf N_+\colon\forall n\geq n_0\colon g(n)\geq c\cdot f(n)\,\}\,,\\
  \Theta(f(n)) & = O(f(n))\cap{}\Omega(f(n))\,,\\
o(f(n)) & = \{\,g(n)\colon\forall c>0\colon\exists n_0\inmathbf N_+\colon\forall n\geq n_0\colon g(n)\leq c\cdot f(n)\,\}\,,\\
\omega(f(n)) & = \{\,g(n)\colon\forall c>0\colon\exists n_0\inmathbf N_+\colon\forall n\geq n_0\colon g(n)\geq c\cdot f(n)\,\}\,.\end{aligned}$$
Venstresiderne læses som »store-o af $f(n)$« og tilsvarende for
»store-omega«, »theta«, »lille-o« og »lille-omega«. Læg mærke til, at
»$f(n)$« i udtrykket »$O(f(n))$« og »$g(n)$« i udtrykket
»$\{\,g(n)\colon \ldots\}$« betegner funktionerne $f$ og $g$ --
notationen forsøger blot at tydeliggøre, at funktionen afhænger af
variablen $n$. Derimod menes i betingelsen
»$\forall n\geq n_0\colon g(n) \le c\cdot f(n)$« funktions*værdien* for
$n$.

Lad os betragte nogle eksempler. Mængden $O(n^2)$ indeholder de
funktioner, som vokser højst kvadratisk. Mængden $o(n^2)$ indeholder de
funktioner ,som vokser langsommere end kvadratisk. Mængden $o(1)$
indeholder de funktioner, som går mod $0$ for voksende $n$, hvor strengt
taget symbolet »$1$« betegner den konstante funktion $n \mapsto 1$, som
altid har funktionsværdien $1$. Dermed tilhører funktionen $f(n)$
mængden $o(1)$, hvis $f(n) \le c\cdot 1$ for hvert positive $c$ og
tilstrækkeligt stort $n$, dvs. når $f(n)$ går mod $0$ for voksende $n$.
Generelt kan man tænke på $O(f(n))$ som mængden af funktioner, som »ikke
vokser hurtigere end« $f(n)$; og på $\Omega(f(n))$ som mængden af
funktioner, som »vokser mindst lige så hurtigt som« $f(n)$. For eksempel
ligger den asymptotiske værstefaldstid for Karatsubas algoritme for
heltalsmultiplikation i $O(n^{1,585})$, mens den asymptotiske kørselstid
for skolemetoden ligger i $\Omega(n^2)$. Derfor kan vi sige, at
Karatsubas algoritme er hurtigere end skolemetoden. Notationen $o(f(n))$
angiver mængden af funktioner, som »vokser skarpt langsommere end«
$f(n)$. Dens modsætning, notationen $\omega(f(n))$, forekommer ganske
sjældent i den grundlæggende algoritmeanalyse og er her kun medtaget for
fuldstændighedens skyld.

De fleste algoritmer i denne bog har kørselstider, som kan skrives som
polynomium eller som logaritmisk funktion, eller som produkt af den
sådanne funktioner. Det næste resultat ser nærmere på polynomier i det
asymptotiske perspektiv; beviset giver nogle eksempler på omgangen med
notationen.

**Lemma 2.1.**
*Lad $p(n)=\sum_{i=0}^ka_in^i$ være et polynomium med reelle
koefficienter, hvor $a_k>0$. Da gælder $p(n)\in \Theta(n^k)$.*

*Bevis*.
Vi skal vise $p(n)\in O(n^k)$ og $p(n)\in \Omega(n^k)$. Vi bemærker
først, at der for $n>0$ gælder
$$p(n)\leq\sum_{i=0}^k\abs{a_i}n^i\leq n^k\sum_{i=0}^k\abs{a_i}\,,$$
hvilket medfører $p(n)\leq (\sum_{i=0}^k\abs{a_i})n^k$ for alle positive
$n$. Derfor gælder $p(n)\in O(n^k)$.

Sæt $A=\sum_{i=0}^{k-1}\abs{a_i}$. For alle $n>0$ har vi nu $$p(n)\geq
  a_kn^k-An^{k-1}=\frac{a_k}{2}n^k+n^{k-1}\left(\tfrac{a_k}{2}n-A\right)\,,$$
og derfor $p(n) \geq (\frac{1}{2}a_k)n^k$ for $n > 2A/a_k$. Ved at vælge
$c=\frac{1}{2}a_k$ og $n_0=2A/a_k$ i definitionen af $\Omega(n^k)$ ses
nu, at $p(n)$ tilhører $\Omega(n^k)$.

**Opgave 2.1**
Sandt eller falskt? (a) $n^2 + 10^6 n \in O(n^2)$; (b) $n \log n
\in O(n)$; (c) $n \log n \in \Omega(n)$; (d) $\log n \in o(n)$.

Asymptotisk notation er så udbredt i algoritmeanalysen, at man af
bekvemmelighedsgrunde ofte anvender den præcise notation på en mere
fleksibel måde. Ikke mindst benytter man ofte betegnelser for
funktionsmængder (fx $O(n^2)$) som om de selv var en enkelt funktion.
Især plejer man at skrive $h(n)= O(f(n))$ i stedet for $h(n)\in O(f(n))$
og $O(h(n))= O(f(n))$ is stedet for $O(h(n)) \subseteq O(f(n))$, som fx:
$$3n^2 + 7n = O(n^2) = O(n^3) \,.$$ Følger af »ligninger« med
$O$-notation skal strengt taget opfattes som udsagn om tilhørsforhold og
mængdeinklusioner, og de giver kun mening læst fra venstre til højre.

For en funktion $h(n)$, funktionsmængder $F$ og $G$ og en operator
$\diamond$ (fx $+$, $\cdot$ eller $/$) lad $F\diamond G$ være en
forkortelse for $\{\,f(n) \diamond g(n)\colon f(n)\in F, g(n)\in G\,\}$,
og $h(n)\diamond F$ være en forkortelse for $\{h(n)\} \diamond F$. Med
denne konvention betegner $f(n)+o(f(n))$ altså mængden af funktioner
$f(n) + g(n)$ med den egenskab, at $g(n)$ vokster stærkt langsommere end
als $f(n)$, dvs. at kvotienten $(f(n) + g(n))/f(n)$ går mod $1$ for
$n\to\infty$. Ækvivalent skrives $(1+o(1))f(n)$. Vi bruger denne
notation, når vi vil understrege $f(n)$s rolle som »*førende term*«, i
forhold til hvilken »*termer af lavere orden*« kan ignoreres.

**Lemma 2.2 (regneregler).**
*Der gælder*
$$\begin{aligned}
cf(n)&=\Theta(f(n))\text{, for hver positive konstant $c$,}\\
f(n)+g(n)&=\Omega(f(n))\,,\\
f(n)+g(n)&=O(f(n))\text{, når }g(n)=O(f(n))\,,\\
O(f(n)) \cdot O(g(n)) &= O(f(n) \cdot g(n))\,.\end{aligned}$$

**Opgave 2.2.** Bevis lemma .

**Opgave 2.3.** Skærp lemma  ved at vise $p(n)=a_kn^k+o(n^k)$.

**Opgave 2.4.** 
Bevis, at der gælder $n^k = o(c^n)$ for heltal $k$ og vilkårligt
$c > 1$. Hvor står $n^{\log\log n}$ i forhold til $n^k$ og $c^n$?

[^1]: Vi vil altid sikre, at mængden
    $\{T(I)\colon I\in\mathscr I_n\}$ har både maksimum og
    minimum, og at mængden $\mathscr I_n$ er endelig, når vi beregner
    gennemsnit.

[^2]: Ovs. anm.: Ordet »asymptotisk« er kendt fra matematisk analyse,
    hvor det betegner opførslen af en funktion, som nærmer sig en
    grænseværdi uden at antage den. Funktionen $x\mapsto 1/x$ har fx
    $y$-aksen som asymptote for $x\rightarrow 0$. Ordet er græsk og
    betyder »ikke-sammenfaldende« og betoner altså, at funktionen nærmer
    sig, men aldrig helt når, en bestemt linje. I modsætning hertil vil
    man lede forgæves efter en god forklaring for, hvorfor man i
    algoritmeanalysen bruger »asymptotisk« for at betegne noget i
    retning af »opførsel for store $n$«.
