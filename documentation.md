# Projektdokumentation

* Landrup Dans
* Silje Agø Paldrup, WU10

### Tech-stack:
* React.js, Next.js, TailwindCSS
    * Zod, react-toastify, js-cookie, FramerMotion, react-icons


### Teknisk Dokumentation:
I dette projekt bruger jeg React biblioteket til Javascript med Next.js frameworket. Derudover bruger jeg TailwindCSS som et css framework. Jeg har valgt at bruge disse af flere årsager - hvor den første er, at det er disse, jeg har mest erfaring i. En anden god grund til at bruge React er at det er et komponent baseret bibliotek, og når man bruger Next.js oveni (som jeg gør), så får man også "server side rendering", som både er godt for SEO("search engine optimization") og hurtige indlæsningstider. Med React og Next.js er der desuden et stort fællesskab, hvori det er nemt at søge efter fejl på f.eks. stackoverflow eller github, og der er grundet den store brugerbase, også mange andre værktøjer og små biblioteker man kan bruge. Herunder f.eks. Framer Motion, der er et animations bibliotek skabt til react.

I forhold til f.eks. Vue.js, som er et meget yngre javascript framework, er der ikke ligeså mange tilføjelser/værktøjer man kan putte ovenpå. Det er ifølge mange heller ikke lige så godt til store projekter men udmærker sig ved de små. 

Jeg har også valgt at bruge TailwindCSS, da det er muligt at have fuld kontrol over sit design, i modsætning til f.eks. BootStrap der måske er lidt hurtigere at sætte op, men har faste klasser uden voldsom meget fleksibilitet. 

 #### Npm pakker
 I projektet her, bruger jeg lidt forskellige npm pakker uddybet herunder.

 **Js-cookie**: 
 Bruges til at sætte, få eller slette cookies på client-side sider. Er god til at gemme enkle data, og kan hjælpe med at forsimple ens kode.  
 <br>
 **React-Icons**: 
 Jeg bruger react icons til importerer iconer nemt og hurtigt til min side.  
 <br>
 **FramerMotion**:
 Stort animations bibliotek, med mange muligheder der tilbyder stor kontrol over de forskellige animationer. Desuden er Framer Motion skabt til React.js så samarbejdet mellem de to ting er virkelig godt.
 <br>    
 **Zod**:
 Jeg bruger Zod til at validerer mine formfelter, da det er vigtigt at validerer sine felter både for sikkerheden, men også så man sørger for at ens data man får ud af formfelterne er korrekt og brugbart. Zod gør det også nemt at lave personlige fejlbeskeder, der gør det mere klart for brugeren af siden, hvad der er gået galt.  
 <br>
 **React-Toastify**: Gør det nemmere at lave notifikationer/feedback til brugeren, der ser ens ud over hele appen, og ikke føles forstyrrende som et forstyrrende element (såsom en alert). Det er meget brugervenligt.
 
### Kode til særlig bedømmelse
```
  //First (1) useEffect
  useEffect(() => {
        const cookieKey = `signedUpActivity_${params.id}`
        const signedUpStatus = Cookies.get(cookieKey) === 'true'
        setIsSignedUp(signedUpStatus)
    }, [params.id])


    //Second (2) useeffect
    useEffect(() => {
        if (isLoggedIn && data) {
            const userAge = parseInt(Cookies.get("LD_age"), 10)
            setIsEligible(userAge >= data.minAge && userAge <= data.maxAge)
        }
    }, [isLoggedIn, data])

    // Third (3) useEffect
    useEffect(() => {
        const role = Cookies.get("LD_role")
        setIsInstructor(role === "instructor")
    }, [])
```
Koden herover er et udpluk fra min src > app > (main) [id] > page.js fil. Jeg har givet dem numre for at referer til dem nemmere i dette afsnit. Den første useEffect, tjekker om der er lavet en cookie der hedder `signedUpActivity_${params.id}`. Dette er nemlig med til at styre hvorvidt knappen på siden hedder "Tilmeld" eller "Afmeld", da det afhænger af cookiens true eller false (boolean) værdi. Den næste useEffect(2) tager ens alder fra den cookie den er gemt i, og tjekker om den er "lovligt" `setIsEligible(userAge >= data.minAge && userAge <= data.maxAge)`. Her sørger den for at alderen er større end eller ligmed minimumsalderen, og mindre end eller ligmed maksimumsalderen. 
Den sidste useEffect (3), sørger for at sætte rollen som intruktør. `setIsInstructor(role === "instructor")` Men altså kun hvis navnet i cookien "LD_role" matcher til værdien som skal være instructor. Hermed hvis man er almindelig bruger og har "LD_role" som "default", så bliver mit state setIsIntructor ikke sat. 
Disse useEffects og de kritierer der bliver sat i dem, bruger jeg i conditional rendering i resten af koden i min SingleActivity funktion, til at bestemme hvilken slags information der vises, og individualisere siden til brugeren der kigger på den.

### Evt. tilføjelser og rettelser
Login siden har jeg valgt at sætte på kalender ikonet i navbaren hvis man IKKE er logget ind, og fjernet derfra såsnart man er logget ind. Hvis man er logget ind, er der altså ikke en måde at navigerer til loginsiden (udover i url). Jeg synes ikke designet lagde op et sted hvor loginknappen kunne være fast, så denne metode synes jeg var bedst. 

Derefter har jeg ændret at kalendersiden, udover at vise hvilke arrangementer man er tilmeldt, også lige viser ens navn og alder. Det gør det mere tydeligt for brugeren, at de rent faktisk er logget ind, samt hvilke oplysninger appen har om en. 

Jeg har også indsat en log ud knap på kalendersiden. Den kan man selvfølgelig vælge at beholde i det færdige design, eller man kan bruge det som et nemt værktøj som udvikler, når man skal skifte mellem default user og instruktør f.eks.
### Valgfri opgave
Jeg har valgt **valgfri opgave B**. her har jeg implementeret animationer ved hjælp af FramerMotion. Ved at have animationer gør jeg appen mere engaerende og interaktiv, samt gøre det mere forståeligt for brugeren hvordan elementer på siden hænger sammen. 

- Animation på knapper:  
Jeg har valgt at animere knapperne så de viser at der er blevet trykket på den, og altså er sket "noget". Da siden er en webapp og de fleste klik events nok bliver touch events, så har jeg valgt, at animationen er en, der giver mening for touch skærm. Altså når brugeren trykker knappen ned og giver slip, så springer knappen op igen bagefter. 

- Animation af sideskift:  
Når man skifter side, ved at klikke i navbaren, bliver den nye side animeret ind fra højre. Det gør oplevelsen af siden mere indlevende, og fanger brugerens øjne så man er bevidst om at der er sket en handling på siden. 

- Animering af aktivitets card:  
Når aktiviteterne bliver loaded i appen, kommer de ind lige efter hinanden, fra en scale på 0,9 til 1 (normal størrelse). Det viser at det er elementer der bliver loaded og bringer fokus på dem. Desuden har jeg sat et delay på at de bliver loaded, så sideanimation når at animere færdig, og det ikke er for voldsomt for brugeren.

### Reflektion

Hvis applikationen skulle skaleres i fremtiden, ville det være en god ide at gemme flere oplysninger om brugeren, såsom: træningsstatestik, favorit aktiviteter, eller en oversigt over tideligere hold.  

Man kunne desuden udvide appen til at vise hvilken instruktør der underviste hvert hold, samt et instruktør afsnit under holdet, der fortæller om instruktørens kvalicifikationer. 

Hvis man gjorde disse ting, ville jeg nok lave lidt om på API strukturen, samt måske omdøbe kalendersiden til en specfik brugerprofil side, som kalenderen så bare er en del af. 