# **Dokumentation: Observabilitet i det Agentiske System**

## **Udfordring: At Se Ind i "Spindelvævet"**

I et distribueret system, hvor mange små services kommunikerer via en effektiv, binær protokol som gRPC, opstår en kritisk udfordring: Hvordan kan vi observere, hvad der sker mellem to services? Uden et "vindue" ind til kommunikationen bliver debugging og overvågning næsten umuligt.

Dette dokument beskriver den strategi, vi vil anvende for at bygge **observabilitet** ind i systemet fra starten. Løsningen er ikke én enkelt service, men en **integreret kapabilitet** i alle vores services.

## **Løsning 1 (Grundlæggende): Logging med gRPC Interceptors**

Dette er vores fundamentale tilgang til at skabe gennemsigtighed.

**::BEGREB: gRPC Interceptor::**

En interceptor er et stykke standardiseret middleware, der "griber ind" i et gRPC-kald (både på klient- og serversiden), før det rammer den egentlige forretningslogik. Vi vil udvikle en standard **logging interceptor**, som bliver en fast del af *hver eneste* gRPC-service i vores system.

**::FUNKTIONALITET::**

For hvert eneste gRPC-kald vil denne interceptor automatisk logge følgende information:

1.  **Request-data:**
    *   Tidspunkt for modtagelse.
    *   Navnet på den kaldte service og metode (f.eks. `ToolRegistry/RegisterTool`).
    *   Indholdet af request-meddelelsen (konverteret til et læsbart format til loggen).
2.  **Response-data:**
    *   Den samlede behandlingstid for kaldet.
    *   Indholdet af response-meddelelsen.
    *   En statuskode, der indikerer, om kaldet lykkedes eller fejlede.

**::UDBYTTE::**
Dette giver os en detaljeret, struktureret og kronologisk log for hver service. Vi kan præcist følge med i, hvilke services der taler sammen, hvornår, med hvilke data, og hvad resultatet var.

## **Løsning 2 (Avanceret): Distributed Tracing**

Når systemet vokser i kompleksitet, er det ikke længere nok at se på logs fra isolerede services. Vi får brug for at følge en *enkelt brugers anmodning* på tværs af hele systemet.

**::BEGREB: Distributed Tracing (via OpenTelemetry)::**

Her udvider vi vores interceptor-koncept.

1.  Når en anmodning starter (f.eks. i Orkestratoren), tildeles den et unikt **Trace ID**.
2.  Dette Trace ID bliver automatisk videresendt som metadata i alle efterfølgende gRPC-kald, der er en del af den oprindelige anmodning.
3.  Hver service logger sine handlinger og knytter dem til det samme Trace ID.

**::UDBYTTE::**
Dette gør det muligt at bruge specialiserede, **web-baserede værktøjer** (som Jaeger eller Zipkin) til at visualisere hele anmodningens "rejse" som et vandfaldsdiagram. Man kan se præcis, hvor lang tid hver del af processen tog, og hvor flaskehalse eller fejl opstår.

## **Anbefaling og Implementering**

*   **Strategi:** Vi starter med at implementere **Løsning 1: Logging Interceptor**. Det er i tråd med KISS-princippet, løser det mest presserende behov og er fundamentet for senere at kunne udvide med Løsning 2.
*   **Hvordan ser man outputtet?**
    *   **CLI-baseret:** I første omgang vil loggene fra vores interceptor være strukturerede tekst-logs. Du kan følge med i realtid via en terminal (CLI) på serveren, der kører servicen.
    *   **Web-baseret:** Når vi implementerer distributed tracing, vil outputtet primært blive analyseret via et web-interface (f.eks. Jaeger).

Vi vil derfor oprette et centralt Go-package (f.eks. `pkg/middleware/interceptors`), hvor denne standardiserede logging-funktionalitet udvikles og vedligeholdes.