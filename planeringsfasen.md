# Inlämning 1 - Planeringsfasen
// 
PRIORITERING

Browser/Frontend (0) --> Express/Backend & API (1) --> Databas (5) 


ESTRID

Browser/Frontend <--> (TI) <--> Express/Backend & API (ESRD) <--> (TI) <--> Databas (E)

Elevation of Priviledge (E):
Risk i zoner som går från lägre till högre känslighet, manipulation av behörighet.
Alltså märks både Ecpress/Backend & API och Databasen med denna risk. 

Spoofing (S): 
Risk i zoner där externt system möter internt system, därför märks Express/Backend & API zonen med denna risk. Metod där någon utger sig för att vara något annat än den är, tex. någon försöker logga in på en annas konto. 

Tampering (T): 
Risk för manipulering av data som går från lägre till högre känslighet. 
Därför märks kommunikationen från Browser/frontend till Express/Backend & API, samt kommunikation från Express/Backend & API till Databas med risken (T). 

Repudiation (R): 
Risk för repudiation finns på de delar av systemet som även är i risk för Elevation of privilidge & Spoofing. Därför är risk för Repudiation applicerbar på vårt Express/Backend & API system. Risken innebär en bristande spårbarhet. 

Information Disclousure (I): 
Risk att information läcker från högre till lägre säkerhetszon. 
Därför markeras flödet från Databasen till Express/Backend & API samt flödet från Express/Backend & API till Browser/Frontend med denna risk (I). 

Denial of Service: 
Risken uppstår där externt system möter internt och riskerar att överbelastas. 
Därför markeras Express/Backend & API med risken. 


SÄKERHETSKRAV 

Tydliga gränser mellan behörigheter:
- Användare måste vara inloggade för att skriva, redigera och radera meddelanden. Redigering och radering får endast göras på meddelanden som tillhör det inloggade kontot. --> Kopplat till risk E 

Input avgränsningar: 
- Alla input fält ska ha tydliga tecken begränsningar. --> kopplat till minska risken D i form av överbelstningsattacker samt risk E & S i form av risk för input av kod (sql injections) som ett sätt att kringå behörighetskrav/ lura datorn att den är del av utvecklar teamet som byggt appen. 

Timeout:
- Efter 3 misslyckade inloggningförsök ska inloggningsförsök blockeras i 30 minuter för att göra appen oattracktiv för tex. brute force attacker --> kopplat till risk S genom att försvåra försök till inlogg av obehörig användare och risk D genom att försvåra överbelsntningsttacker.

HTTPS:
- Appen ska använda sig av HTTPS så att kommunikationen mellan systemet är krypterat och därmed försvåra avlyssning som ökar risken för Tampering (T). 

Loggning: 
-Meddelanden ska ha en tidstämpel som visar när det skickades, raderades och ändrades. --> kopplat till risk R 

Output avgränsnignar: 
- Felmeddelanden ska vara generella för så att de inte avslöjar användbarn information för potentiella angripare. 
- Databasen ska aldrig retunera lösenord eller annan känslig information till frontend. 
--> Bägge kopplade rill risk I 

