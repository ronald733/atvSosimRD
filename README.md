# Trabalho Prático – Simulação com SoSim
Disciplina: Sistemas Operacionais  
Professor: [NOME DO PROFESSOR]  
Aluno: Ronald Silva  

---

## 1. Gerenciador de Processos

### Configuração
Foram criados **5 processos com tempos de execução distintos** no módulo **Gerência de Processos** do SoSim.  
Durante a execução, os processos passaram pelos estados:

- **Novo** → processo foi criado.  
- **Pronto** → processo aguardando a CPU.  
- **Executando** → processo em uso da CPU.  
- **Bloqueado (I/O ou Page Fault)** → processo aguardando operação de entrada/saída ou carregamento de página.  
- **Finalizado** → execução concluída.  

Também foi possível observar os **momentos de troca de contexto**, quando a CPU interrompe a execução de um processo e passa a atender outro (visível no log do simulador).

### Questão 1
**O que ocorre quando um processo passa do estado Pronto para Executando?**  
Quando um processo está no estado **Pronto**, ele está na fila aguardando o uso da CPU.  
Ao passar para o estado **Executando**, significa que o **escalonador escolheu esse processo** para ocupar a CPU.  
Ou seja, as instruções dele começam a ser efetivamente processadas.

---

## 2. Escalonador de Processos

### Configuração
Foram simulados os algoritmos:
- **FIFO (First In, First Out)**  
- **Round Robin** com quantum = 3  
- **SJF (Shortest Job First)**  

Cada execução gerou um **diagrama de Gantt** e os cálculos de tempo médio de espera.

### Resultados
- **FIFO** → Os processos são atendidos em ordem de chegada. Tempos de espera maiores para processos que chegam depois.  
- **Round Robin (q=3)** → Houve várias trocas de contexto. Processos curtos não ficaram parados por muito tempo, mas o overhead de trocas aumentou.  
- **SJF** → Os processos de menor duração foram atendidos primeiro, reduzindo significativamente o tempo médio de espera.  

### Questão 2
1. **Qual algoritmo apresentou menor tempo médio de espera?**  
   → O **SJF (Shortest Job First)** apresentou o menor tempo médio de espera, pois prioriza processos curtos.  

2. **No Round Robin, como o quantum influencia no desempenho do sistema?**  
   → O **quantum** define quanto tempo cada processo pode executar antes de ser interrompido:  
   - Quantum **pequeno** → mais alternâncias de processos, maior justiça, mas também **mais trocas de contexto** (overhead).  
   - Quantum **grande** → menos trocas de contexto, mas o algoritmo se aproxima do FIFO e processos curtos podem demorar para terminar.  

---

## 3. Paginação

### Configuração
Foi criado um processo que **demandava mais memória que a RAM disponível**.  
O sistema utilizou **paginação** para permitir a execução.  
Foram observados:
- Quantidade de páginas carregadas na RAM.  
- Quantidade de **faltas de página** durante a execução (processo acessou página que não estava carregada).  

### Questão 3
1. **Explique o que é uma falta de página e como o sistema operacional a trata.**  
   - Uma **falta de página** ocorre quando o processo tenta acessar uma página que não está na RAM.  
   - O sistema operacional interrompe o processo, busca a página no disco (swap in) e a carrega na memória. Depois, a execução é retomada.  

2. **Compare a execução com e sem paginação. Quais vantagens observou?**  
   - **Sem paginação**: processos que exigem mais memória que a RAM não conseguem ser executados.  
   - **Com paginação**: processos maiores que a memória física podem rodar, já que o sistema carrega dinamicamente apenas as páginas necessárias.  
   - **Vantagens**: melhor aproveitamento da RAM, suporte à multiprogramação e possibilidade de rodar programas maiores do que a memória disponível.  

---

## 4. Evidências
As capturas de tela do SoSim (Gerenciador de Processos, Escalonador e Paginação) estão disponíveis na pasta **/imagens** deste repositório.

---
