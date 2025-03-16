# Bausteine
Bestimmte Elemente tauchen in Architekturen immer wieder auf, z.B. Proxies, Gateways etc. Diese Begriffe und 
ihre Einsatzmöglichkeiten werden hier zusammengefasst.

## Gateway
Ein Gateway ist eine Softwarekomponente, die als Vermittler zwischen verschiedenen Systemen oder Diensten fungiert. Es kapselt den Zugriff auf externe Systeme, abstrahiert deren Schnittstellen und kann zusätzliche Funktionen wie Authentifizierung, Routing oder Caching übernehmen.

Abstrahierung externer Systeme

    Ein Gateway kann verschiedene externe APIs (z. B. OpenAI, Anthropic) unter einer einheitlichen Schnittstelle zusammenfassen.
    Dadurch wird dein System nicht direkt von den spezifischen APIs abhängig.

Flexibilität und Austauschbarkeit

    Falls später ein neuer Anbieter (z. B. Mistral) hinzugefügt werden oder einen bestehender ersetzt werden soll, muss nur das Gateway angepasst werden, nicht das gesamte System.

Sicherheitsmechanismen

    Ein Gateway kann Authentifizierung und Autorisierung für den Zugriff auf externe APIs übernehmen, z. B. API-Schlüssel verwalten oder Tokens generieren.

Lastverteilung und Load Balancing

    Falls mehrere Anbieter genutzt werden, kann das Gateway Anfragen verteilen, um Kosten oder Antwortzeiten zu optimieren.

Monitoring und Logging

    Ein Gateway kann alle API-Requests und Responses zentral protokollieren, was die Analyse von Nutzung und Fehlern erleichtert.

## Proxy
Proxies gibt es als Reverse Proxy und Forward Proxy. Wenn in der Industrie von Proxy gesprochen wird, dann ist meistens ein Forward Proxy gemeint.

Forward Proxy
- Ein Server der zwischen Client/s und Server/n sitzt
- Er "handelt" im Auftrag der Clients
- Wenn ein Cilent mit einem Server kommuniziert und der forward proxy korrekt konfiguriert ist, geht der Request erst an den Forward Proxy der diesen an den Server weiterleitet (forward). Der Server antwortet dem Proxy.
- Die IP-Adresse im Request entspricht dann der des Proxies.
- VPNs arbeiten vereinfacht ausgedrückt so.

Reverse Proxy
- Reverse Proxies arbeiten im Auftrag eines Servers
- Sitzt zwischen Client und Server
- Der Client setzt Requests an den Reverse Proxy ab, denkt aber, der Request geht an den Server
- Der echte Server antwortet dem Reverse Proxy, welcher wiederum dem Client antwortet
- Der Client bekommt nicht mit, dass es einen Proxy zwischen ihm und dem Server gibt
- Ein DNS würde die IP-Adresse des Reverse Proxies zurückgeben, wenn ein Client einen Request absetzt aber denken, es wäre die IP des eigentlichen Servers

Beim Forward Proxy weiß der Server nicht, dass es einen Proxy ist, der die Anfragen sendet, beim Reverse Proxy weiß der Client nicht, dass er die Anfragen an einen Proxy sendet.

Anwendungsfälle Reverse Proxy
- Reverse Proxy filtert unerwünschte Requests heraus
- Logging, Metriken
- Caching
- Als Load Balancer verwenden
- Security Ramifications: Client ist korrumpiert und will Server lahmlegen, indem er DDoS Attacken ausführt. Der Reverse-Proxy kann als Load Balancer die Requests auf die anderen Server verteilen.