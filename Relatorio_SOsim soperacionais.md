
# Relatório - Atividade com SOsim

## Identificação
- Nome: Marcos Filipe Sousa Cardoso 
- Disciplina: Sistemas Operacionais  
- Ferramenta: SOsim  
- Data: 22/09/2025

## 1. Observações da Simulação (registro)
- Tempo da simulação analisada: **524** ticks.  
- Processos observados (PIDs): 4934893, 5039960, 5151015, 5257873, 5404202.  
- Eventos registrados (do log):  
  - t = 472 : 4934893 — Pronto → Exec.  
  - t = 505 : 5151015 — Exec → I/O (Bloqueado).  
  - t ≈ 507–509 : 5257873 — Pronto → Exec.  
- Trocas de contexto: aparecem no log toda vez que um `Pronto -> Exec` ocorre para um PID diferente.  
- Total Page Faults observado (na simulação mostrada): **20**.

*(Anexe captura de tela da janela Log, Gerência de Processos e Estatísticas.)*

## 2. O que ocorre quando um processo passa de Pronto para Executando
Quando um processo muda de **PRONTO** para **EXECUTANDO**:
1. O escalonador escolhe o próximo processo na fila de prontos.  
2. O sistema operacional realiza a troca de contexto: salva registradores do processo anterior e carrega o contexto do novo.  
3. O processo sai da fila de pronto e seu estado passa a **Executando**.  
4. Caso precise de páginas, pode ocorrer **page fault** antes da execução.  
5. O timer é configurado (em escalonadores preemptivos).  
6. A CPU executa as instruções do processo.  

## 3. Experimentos de Escalonamento
Configurações: manter mesmas cargas de processos e variar apenas o algoritmo.

Algoritmos testados:
- **FIFO (First In First Out)**
- **Round Robin (quantum = 3)**
- **SJF (Shortest Job First)**

Métricas coletadas: tempo médio de espera, turnaround médio, throughput, trocas de contexto, utilização CPU.

Resultados esperados (teoria):
- SJF deve apresentar menor tempo médio de espera.  
- FIFO pode ter maior tempo de espera em cenários com processos longos.  
- Round Robin equilibra responsividade e overhead, dependendo do quantum.  

**Tabela para preenchimento:**
- FIFO: Waiting avg = __ ; Turnaround avg = __ ; Context switches = __ ; CPU util = __  
- RR (q=3): Waiting avg = __ ; Turnaround avg = __ ; Context switches = __ ; CPU util = __  
- SJF: Waiting avg = __ ; Turnaround avg = __ ; Context switches = __ ; CPU util = __  

## 4. Questões de Escalonador
- **Qual algoritmo apresentou menor tempo médio de espera?**  
  - Resposta teórica: **SJF**.  
  - Resposta prática: preencher com valores coletados.  

- **No Round Robin, como o quantum influencia?**  
  - Quantum pequeno: mais trocas de contexto, menor latência, maior overhead.  
  - Quantum grande: menos overhead, mas pode aumentar tempo de resposta.  
  - Quantum ideal é próximo do tempo médio de burst de CPU.  

## 5. Experimento de Paginação
Configuração: criar processo maior que a RAM disponível.  
Observar páginas carregadas, faltas de página e política de substituição.

**Registros:**
- Quantidade de páginas do processo: __  
- Quantidade de páginas carregadas na memória: __  
- Total de faltas de página: __  
- Política de substituição: __  

## 6. Questões de Paginação
- **O que é uma falta de página?**  
  - Quando um processo acessa uma página não presente na RAM.  
  - O SO atende a falta carregando a página do disco para a memória.  
  - Atualiza tabela de páginas e reinicia a instrução.  

- **Comparação com/sem paginação:**  
  - Com paginação: suporta memória virtual maior que a física, mais flexibilidade.  
  - Sem paginação: acesso mais rápido, mas restrito ao tamanho da RAM.  
  - Vantagens da paginação: isolamento, proteção, execução de processos grandes.  
  - Desvantagem: atrasos devido a page faults.  

## 7. Capturas de Tela
- Console / Log mostrando transições  
- Gerência de Processos (PIDs)  
- Gerência de Memória / Arquivo de Paginação  
- Estatísticas (Tempo, Page Faults, Throughput)  
