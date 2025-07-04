---
title: HTTP/2
slug: Glossary/HTTP_2
---

{{GlossarySidebar}}

**HTTP/2** это старшая версия сетевого протокола [HTTP](/ru/docs/Web/HTTP). Основным назначением HTTP/2 является снижение {{glossary("latency","задержки")}} путём реализации полного мультиплексирования запросов и ответов, уменьшения перегруженности протокола при помощи эффективного сжатия заголовков HTTP, а также добавления поддержки приоритетов запроса и "server push"("серверное проталкивание" - сервер имея правила, может проявить инициативу, которые инициируют отправку контента до его запроса, зная о том, что может поступить запрос на их отправку).

HTTP/2 никоим образом не изменяет семантику применяемую HTTP. Все основные концепции HTTP 1.1, такие как методы HTTP, коды статусов, URI, и поля заголовков останутся прежними. Вместо этого HTTP/2 изменит порядок (форму) данных и способ их передачи между клиентом и сервером, которые управляют всем процессом, и скроет сложность применения в новом обрамляющем слое. Это позволит использовать существующие приложения без изменений.

1. Основные сведения
   1. [HTTP на MDN](/ru/docs/Web/HTTP)

2. [Справка](/ru/docs/Glossary)
   1. {{glossary("HTTP")}}
   2. {{glossary("Latency")}}
