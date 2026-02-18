# speculative-tcp-handshake
Idea for accelerating TCP handshake with bidirectional speculative data transfer
Title (Working Title): Speculative Bidirectional Transaction Setup Protocol (S-BTSP) / TCP Handshake with Predictive Pipelining

English Version
Title (Working Title): Speculative Bidirectional Transaction Setup Protocol (S-BTSP) / TCP Handshake with Predictive Pipelining
Core Idea:
A modification to the TCP three-way handshake process designed to accelerate data transfer by eliminating idle acknowledgments and utilizing handshake packets for data exchange and prefetch requests.
Proposed Mechanism:
Client -> Server: Instead of an empty SYN, the client sends a SYN packet containing the first chunk of data (e.g., the beginning of an HTTP request).
Server -> Client: Instead of an empty SYN-ACK, the server responds with a SYN-ACK packet containing:
The first chunk of response data (if available).
A speculative request for the next chunk of data the client will likely need.
Client -> Server: Instead of an empty ACK, the client sends an ACK packet containing the second (requested) chunk of data.
Goal:
To compress 2-3 Round Trip Times (RTT) into approximately 1.5 RTT by loading control packets with meaningful payload, effectively creating a "dual-load" handshake.
Key Differentiator from existing solutions (TCP Fast Open, TLS 1.3 0-RTT):
The server not only sends data preemptively but also requests the next portion of data within the same handshake acknowledgment packet, enabling continuous, bidirectional data flow from the very first interaction.

Русская версия
Название (рабочее): Спекулятивный протокол с двунаправленной конвейеризацией на этапе установки соединения (S-BTSP)
Суть идеи:
Модификация процесса установки TCP-соединения (тройного рукопожатия) для ускорения передачи данных путем исключения "пустых" подтверждений.
Как работает (логика):
Клиент -> Сервер: Вместо пустого SYN клиент отправляет SYN + первая часть данных (например, начало HTTP-запроса).
Сервер -> Клиент: Вместо пустого SYN-ACK сервер отправляет SYN-ACK + первая часть ответных данных (то, что успел подготовить) + специальный запрос (Request) на следующую часть данных, которая потребуется клиенту.
Клиент -> Сервер: Вместо пустого ACK клиент отправляет ACK + вторая (запрошенная) часть данных.
Цель: Сжать 2-3 круглых похода (RTT) в 1.5, нагружая служебные пакеты полезной информацией.
Ключевое отличие от существующих решений (TCP Fast Open, TLS 1.3 0-RTT):
Сервер не просто отвечает данными, но и упреждающе запрашивает следующую порцию данных в том же пакете, где подтверждает соединение, создавая эффект "двойной загрузки".

Date of idea: 18 February 2026
