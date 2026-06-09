# Inlämning 3 - Granskningsfasen

Verktyg använda: 
CodeQL (SAST) - analyserar koden och uppmärksammar brister 
Dependabot (SCA)- granskar bibliotek för sårbarheter


Code QL - 8 hot identifierade 
Flera av hoten som codeQL identifierade var bristen på rate limiting på flera av routes i server.js (däribland post/patch/delete endpointsen).
Detta betyder att det inte finns något stopp på antal anrop som kan skickas på dessa routes. En angripare kan alltså tex. anropa post messages i flera hundra gånger per sekund och på så sätt fylla databasen med skräp eller överbelasta servern. 

För att åtgärda detta bör vi installera express-rate-limit bibilioteket vars middleware funktion vi kan kalla på i routen och som räknar antal anrop och blockerar efter bestämt antal. Detta gör vi på precis samma sätt som vi gjort med middleware funktionen authenticateUser från auth.js

Denna sårbarhet kopplar jag främst till nr 5 - security misconfiguration på OWASP top 10, men man kan även argumentera för att det rör sig om nr 4 - insecure design då konfigurationen inte bara var fel konfigurerat utan helt saknades. 

Länk till sårbarheten
https://github.com/popcorn007-commits/SSkursen-/security/code-scanning/5


Dependabot

Dependabot hittade 16 sårbarheter, jag har valt att se närmre på "jsonwebtoken unrestricted key type could lead to legacy keys usage #1" då den var märkt med  värdet "high" och "direct" (vilket betyder att de har en direkt påverkan på produktionskoden och inte endast utvecklingsmiljön).

Sårbarhetenen är kopplad till ett känt fel i äldre versioner av jsonwebtoken som möjliggör att förfalska token då den inte kollar nyckeltypen tillräckligt nogrant (sårbarheten möjliggör tex användningen av publika nycklar istället för hemliga). Uppdaterar vi npm-paketet till version 9.0.0 så är denna sårbarhet åtgärdad. 

Sårbarheten kan alltså kopplas till nr 6 - Vulnerable and outdated components på OWASP top 10. 

Länk till sårbarheten 
https://github.com/popcorn007-commits/SSkursen-/security/dependabot/1