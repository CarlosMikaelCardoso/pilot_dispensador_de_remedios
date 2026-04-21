# 📋 Plano de Trabalho (MVP) — Dispensador de Remédios Conectado (IoT)
## Organização por 4 membros (divisão de carga)

## 🎯 Objetivo do projeto
Desenvolver um **MVP funcional (simulado e documentado)** de um **Dispensador de Remédios Conectado (IoT)** capaz de:
- agendar doses,
- alertar o usuário (local),
- dispensar (simulado ou mecanismo básico),
- confirmar tomada (tomou/não tomou),
- registrar eventos e notificar um responsável (ex.: Telegram),
- manter confiabilidade mínima (principalmente tempo e falhas de rede/energia).

---

## 👥 Papéis (4 membros)
> Se quiser, substitua “Membro 1..4” por nomes.

### Membro 1 — Firmware & Arquitetura (ESP32/FreeRTOS/Wokwi)
- Máquina de estados, integração geral, drivers no simulador, logs e organização do repositório.

### Membro 2 — Mecânica/Mecanismo & Sensores (Dispensação)
- Escolha e modelagem do mecanismo de dispensação (servo/stepper/DC), sensores de posição/obstrução, CAD conceitual.

### Membro 3 — Conectividade & Segurança (Wi‑Fi + Telegram / API)
- Comunicação, notificação, sincronização de horário (NTP), retry/backoff, proteção de credenciais e logs de rede.

### Membro 4 — Produto/UX + Documentação + QA
- Benchmark/estudo de caso, fluxos do usuário, telas/mensagens, roteiros de teste, manual e relatório final.

---

## ✅ Definição de Pronto (DoD) — para qualquer atividade
- Artefato funciona no ambiente definido (simulação/PoC)
- Evidência anexada (log/print/vídeo curto)
- Documentação atualizada (docs/README)
- Validação do grupo registrada (OK)

---

# 1) Pesquisa, Ideação e Prototipagem Virtual

## Atividade 1.1 — Pesquisa de mercado e soluções existentes (benchmark)
**Objetivo:** entender soluções do mercado e oportunidades de inovação.

**Responsável principal:** Membro 4  
**Apoio:** Membro 2 (mecânica), Membro 3 (IoT)

**Tarefas**
- Levantar 5+ soluções existentes e links
- Comparar funções: agendamento, trava anti-duplicidade, confirmação, conectividade, acessibilidade, custo
- Identificar limitações recorrentes
- Propor 3–5 inovações viáveis para MVP

**Entregáveis**
- Tabela comparativa + lista de inovações com justificativa

---

## Atividade 1.2 — Estudo de caso (usuários, contextos e riscos)
**Objetivo:** mapear cenários reais, riscos e requisitos de segurança.

**Responsável principal:** Membro 4  
**Apoio:** Membro 1 (estados/segurança), Membro 2 (falhas mecânicas)

**Tarefas**
- Definir 2–3 personas (usuário/cuidador)
- Mapear jornada: configurar → alertar → dispensar → confirmar
- Matriz de riscos: dose duplicada, dose perdida, falha mecânica, falha energia/horário, falha rede
- Mitigações mínimas do MVP

**Entregáveis**
- Personas + jornada + matriz de risco (impacto x probabilidade)

---

## Atividade 1.3 — Definição do MVP (escopo) + inovações selecionadas
**Objetivo:** definir o que entra e não entra no MVP, e as inovações adotadas.

**Responsável principal:** Membro 1  
**Apoio:** Membro 4 (produto), Membro 2 (mecanismo), Membro 3 (notificações)

**Tarefas**
- Definir funções mínimas do MVP (agendamento, alerta, dispensa, confirmação, notificação)
- Definir fora do escopo (ex.: app completo, múltiplos perfis avançados)
- Selecionar 3–5 inovações do benchmark (ex.: anti-duplicidade, RTC/NTP, log auditável)
- Definir critérios mensuráveis (latência, tempo de confirmação, retries)

**Entregáveis**
- Documento “Escopo do MVP” + inovações escolhidas

---

## Atividade 1.4 — Arquitetura macro (hardware, estados, eventos e contratos)
**Objetivo:** desenhar o sistema para integrar sem retrabalho.

**Responsável principal:** Membro 1  
**Apoio:** Membro 3 (eventos/notificações), Membro 2 (sensores/mecanismo), Membro 4 (UX)

**Tarefas**
- Definir módulos: Scheduler, UI, Dispenser, Sensors, Network, Notifier, Logger, Config
- Definir máquina de estados: BOOT/SETUP/READY/ALERTING/DISPENSING/WAIT_CONFIRM/MISSED/ERROR
- Definir eventos e payload (tipo, timestamp, status, detalhes)
- Definir pinagem simulada e componentes do Wokwi

**Entregáveis**
- Diagrama de blocos + diagrama de estados + especificação do evento

---

# 2) Simulação e Provas de Conceito (PoCs)

## Atividade 2.1 — PoC de tempo e agendamento (NTP/RTC/fallback)
**Objetivo:** garantir disparo confiável de dose por horário.

**Responsável principal:** Membro 3 (NTP/tempo)  
**Apoio:** Membro 1 (integração firmware)

**Tarefas**
- Definir estratégia de tempo no MVP (NTP e/ou RTC)
- PoC: relógio + próximo alarme + disparo (log)
- Definir comportamento offline (fallback e tolerância)

**Entregáveis**
- PoC com logs e instruções de execução

---

## Atividade 2.2 — PoC de mecanismo de dispensação + sensores
**Objetivo:** validar atuação e confirmação de posição/dispensa.

**Responsável principal:** Membro 2  
**Apoio:** Membro 1 (driver/controle), Membro 4 (segurança do uso)

**Tarefas**
- Escolher mecanismo do MVP (servo/stepper/DC)
- Definir sensor de confirmação (fim de curso/IR/tempo/posição)
- PoC: mover para posição A/B e confirmar
- Definir falhas típicas e como detectar (jam/timeout)

**Entregáveis**
- PoC do mecanismo + leitura de sensor + log de ok/falha

---

## Atividade 2.3 — PoC de interface local (display + botões + alerta)
**Objetivo:** validar fluxo local de uso sem depender do celular.

**Responsável principal:** Membro 4  
**Apoio:** Membro 1 (integração), Membro 2 (layout físico)

**Tarefas**
- Definir UI mínima (telas e textos curtos)
- PoC: telas READY/ALERTING/CONFIRM/ERROR
- PoC: botão CONFIRMAR e (opcional) SONECA
- Definir padrões de alerta (buzzer/LED)

**Entregáveis**
- PoC de UI com prints/log e instruções

---

## Atividade 2.4 — PoC de conectividade e notificações (Telegram)
**Objetivo:** notificar eventos críticos e registrar tentativas.

**Responsável principal:** Membro 3  
**Apoio:** Membro 1 (fila/arquitetura), Membro 4 (texto das mensagens)

**Tarefas**
- Criar bot e definir envio básico
- Definir formato das mensagens ([DOSE]/[CONFIRM]/[MISSED]/[ERROR])
- Implementar retry/backoff básico
- Garantir que rede não bloqueia tarefas críticas

**Entregáveis**
- PoC Telegram funcionando + exemplos de mensagens

---

# 3) Desenvolvimento do MVP Integrado

## Atividade 3.1 — Modelo de dados (Agenda/Dose/Eventos) + Config mínima
**Objetivo:** padronizar como o sistema representa doses e eventos.

**Responsável principal:** Membro 1  
**Apoio:** Membro 3 (campos úteis para notificação), Membro 4 (campos úteis para usuário)

**Tarefas**
- Estruturar Dose (id, horário, janela, cooldown, etc.)
- Estruturar Evento (tipo, timestamp, status, detalhes)
- Definir persistência mínima (NVS/config) ou simulado

**Entregáveis**
- Estruturas implementadas + logs consistentes

---

## Atividade 3.2 — Máquina de estados end-to-end (fluxo completo)
**Objetivo:** consolidar o fluxo: READY → ALERTING → DISPENSING → WAIT_CONFIRM → READY.

**Responsável principal:** Membro 1  
**Apoio:** Membro 4 (UX de estados), Membro 2 (dispensa), Membro 3 (notificações)

**Tarefas**
- Implementar transições e timeouts
- Implementar anti-duplicidade/cooldown
- Gerar logs claros de cada transição

**Entregáveis**
- Fluxo completo rodando no simulador

---

## Atividade 3.3 — Integração mecanismo + detecção de falha (jam/timeout)
**Objetivo:** tornar a dispensação confiável com falha controlada.

**Responsável principal:** Membro 2  
**Apoio:** Membro 1 (controle e estados), Membro 3 (notificação de erro)

**Tarefas**
- Implementar confirmação de dispensa/posição
- Implementar tentativas limitadas
- Definir comportamento em ERROR (alerta local + notificação)

**Entregáveis**
- Dispensa OK + caminho de falha simulável

---

## Atividade 3.4 — Integração UI (telas + botões) com estados e eventos
**Objetivo:** garantir uso simples e claro.

**Responsável principal:** Membro 4  
**Apoio:** Membro 1 (estados), Membro 3 (textos de mensagens consistentes)

**Tarefas**
- Implementar telas por estado
- Implementar botão confirmar (e soneca opcional)
- Definir mensagens curtas e acessíveis

**Entregáveis**
- UI integrada ao fluxo completo

---

## Atividade 3.5 — Integração conectividade (fila de eventos, retry, offline)
**Objetivo:** notificar e registrar sem travar o firmware.

**Responsável principal:** Membro 3  
**Apoio:** Membro 1 (fila), Membro 4 (conteúdo), Membro 2 (eventos mecânicos)

**Tarefas**
- Implementar fila de eventos para envio
- Implementar reconexão Wi‑Fi + retry Telegram
- Implementar comportamento offline (log local e envio posterior, se adotado)

**Entregáveis**
- Notificação integrada e resiliente

---

# 4) Validação, Modelagem e Entrega

## Atividade 4.1 — Roteiros de teste + evidências
**Objetivo:** validar o MVP e gerar evidências para avaliação.

**Responsável principal:** Membro 4 (QA)  
**Apoio:** Todos (testes de sua parte)

**Tarefas**
- Definir casos: dose ok, confirmação ok, não confirma, falha dispensa, falha Wi‑Fi
- Executar e registrar evidências (prints/log/vídeo)
- Consolidar checklist final

**Entregáveis**
- Checklist de testes preenchido + evidências

---

## Atividade 4.2 — CAD/modelagem do dispositivo + especificação do mecanismo
**Objetivo:** apresentar o “produto” e viabilizar evolução do MVP.

**Responsável principal:** Membro 2  
**Apoio:** Membro 4 (UX/ergonomia), Membro 1 (posicionamento de componentes)

**Tarefas**
- CAD conceitual (corpo, compartimentos, saída, acesso recarga)
- Alocar motor/sensores/display no layout
- Render/vistas e explicação do mecanismo

**Entregáveis**
- Imagens CAD + descrição técnica do mecanismo

---

## Atividade 4.3 — Manual do usuário + guia de configuração
**Objetivo:** tornar o MVP apresentável e utilizável.

**Responsável principal:** Membro 4  
**Apoio:** Membro 3 (rede/telegram), Membro 1 (modo teste), Membro 2 (recarga)

**Tarefas**
- Passo a passo: ligar, configurar (se houver), testar, confirmar
- Troubleshooting: sem Wi‑Fi, erro de dispensa, relógio incorreto
- Instruções de segurança (não duplicar dose etc.)

**Entregáveis**
- Manual em Markdown com imagens/prints

---

## Atividade 4.4 — Relatório técnico + benchmark + inovações
**Objetivo:** consolidar decisões e resultados.

**Responsável principal:** Membro 4  
**Apoio:** Membro 1 (arquitetura), Membro 3 (conectividade), Membro 2 (mecânica)

**Tarefas**
- Descrever benchmark e inovações implementadas
- Descrever arquitetura, estados e eventos
- Incluir resultados dos testes e limitações
- Próximos passos pós-MVP

**Entregáveis**
- Relatório final

---

## Atividade 4.5 — Preparação do repositório + demo/pitch
**Objetivo:** garantir entrega limpa e demo estável.

**Responsável principal:** Membro 1  
**Apoio:** Todos

**Tarefas**
- README “como rodar a simulação”
- Roteiro de demo (READY → ALERTA → DISPENSA → CONFIRMA → NOTIFICA)
- Ensaiar apresentação e preparar evidências

**Entregáveis**
- Repo organizado + demo pronta (e vídeo opcional)

---

# 📦 Checklist final de entrega do MVP
- [ ] Simulação end-to-end funcionando com roteiro de demo
- [ ] Notificações (Telegram ou equivalente) integradas
- [ ] CAD/modelagem conceitual do dispositivo + mecanismo descrito
- [ ] Roteiros de teste + evidências (logs/prints/vídeo)
- [ ] Manual do usuário + README
- [ ] Relatório final com benchmark e inovações
