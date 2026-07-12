# Projeto 03: Paradigmas Lógico + Orientado a Aspectos

## Descrição

### Condições de conclusão

Programas de pós-graduação acompanham o progresso de discentes de mestrado ao longo de um plano de trabalho de aproximadamente 24 meses, considerando tarefas, prazos, créditos, atividades creditáveis, prorrogações e requisitos de integralização. As regras que regem esse acompanhamento são numerosas, mudam com o tempo e atravessam vários módulos do sistema, o que torna o domínio adequado para exercitar dois paradigmas de forma combinada.

O objetivo deste projeto é desenvolver um **Sistema de Acompanhamento Acadêmico da Pós-Graduação** que combine:

1. **Programação Lógica**, por meio de um motor de inferência construído do zero, responsável por decidir situações acadêmicas a partir de fatos cadastrados (por exemplo, se um aluno está apto à defesa, em risco ou se seus créditos satisfazem os grupos obrigatórios).
2. **Programação Orientada a Aspectos**, usando apenas recursos nativos do Python, para tratar preocupações transversais que se repetem em quase todas as operações do sistema (autorização, auditoria, histórico de alterações, validação de prazos e geração de alertas).

A integração entre os paradigmas é o ponto central do projeto. O motor lógico decide o que é verdade no sistema. Os aspectos definem como cada operação que consulta ou alimenta esse motor é interceptada e enriquecida, sem poluir a lógica de negócio com código repetido.

---

# Domínio do Sistema

O sistema gerencia as seguintes entidades e processos.

### 01. Gestão de discentes

Cadastro de alunos e associação entre aluno, orientador e coorientador opcional. Cada aluno possui uma situação, definida pelos seguintes estados:

- regular (dentro do prazo e com o plano em dia);
- em prorrogação (com semestre adicional concedido e em curso);
- em risco (com pendências ou prazos estourados que ameaçam a integralização);
- qualificado (aprovado na qualificação);
- em fase de defesa (apto à defesa e com a defesa encaminhada);
- concluído (integralizou o curso e defendeu);
- desligado (removido do programa).

A mesma lista de estados vale para a situação registrada e para a situação inferida pelo motor.

### 02. Plano de trabalho

Cada aluno possui um plano dividido em etapas (revisão bibliográfica, definição do problema, desenvolvimento, experimentos, escrita, qualificação, defesa). Cada etapa possui *tasks* cadastradas pelo orientador, e o aluno registra atualizações de progresso vinculadas a uma *task*.

### 03. Atividades creditáveis

Atividade creditável é o termo guarda-chuva para tudo que gera crédito.

A coordenação cadastra tipos de atividade creditável (artigo publicado, artigo submetido, software registrado, patente, participação em banca, estágio docência, disciplina cursada, entre outros), cada um com pontuação, limites e requisitos de comprovação.

Produção é o subtipo bibliográfico da atividade creditável (por exemplo, artigo publicado ou submetido). Toda produção é vinculada a um veículo (evento ou revista), e cada veículo possui um nível de relevância configurável a nível de programa, sem ficar preso a uma escala fixa como o Qualis.

Cada produção registrada possui ainda um campo de observação livre, porque duas produções no mesmo veículo podem ter impactos diferentes na avaliação do programa.

O aluno ou orientador registra uma atividade creditável, e a coordenação valida ou rejeita.

### 04. Checklist de integralização

O aluno visualiza os requisitos para concluir o curso (créditos mínimos, créditos por grupo, proficiência, qualificação, atividade creditável validada, defesa, versão final), e o sistema indica itens cumpridos, pendentes e em risco.

### 05. Prorrogação de prazo

Solicitação de semestre adicional com justificativa, plano atualizado e parecer do orientador, sujeita a regras configuráveis sobre quantidade de prorrogações.

### 06. Dashboard

Visões agregadas para aluno, orientador e coordenação.

### 07. Relatórios

Visões gerenciais agregadas, como alunos em atraso, alunos por status e por orientador, tempo médio de integralização e produção por aluno e por professor, exibíveis na interface.

---

# Histórias de Usuário

1. Como coordenação, quero cadastrar alunos, orientadores e a relação de orientação, para manter o registro dos discentes do programa.
2. Como orientador, quero cadastrar as etapas e as *tasks* do plano de trabalho de um aluno, para organizar o acompanhamento do progresso.
3. Como aluno, quero registrar atualizações de progresso vinculadas a uma *task*, para refletir o andamento do meu plano.
4. Como coordenação, quero cadastrar tipos de atividade creditável com pontuação, limites e requisitos, para definir como cada atividade gera créditos.
5. Como aluno, quero registrar atividades creditáveis com comprovante, para que sejam validadas e contabilizadas nos meus créditos.
6. Como aluno, quero registrar uma produção indicando o veículo e uma observação, para que a relevância do veículo seja considerada na contabilização.
7. Como coordenação, quero validar ou rejeitar atividades registradas, para controlar a contabilização de créditos.
8. Como aluno, quero consultar meu checklist de integralização, para saber quais requisitos já cumpri, quais estão pendentes e quais estão em risco.
9. Como orientador, quero que o sistema infira a situação acadêmica de cada orientando (regular, em risco, qualificado, em fase de defesa, entre os estados definidos no Domínio), para priorizar minha atenção.
10. Como usuário, quero que toda operação sensível seja autorizada conforme meu papel, para que apenas quem tem permissão altere os dados.
11. Como coordenação, quero que o sistema mantenha um registro de auditoria e um histórico de alterações das entidades, para rastrear quem alterou o quê e quando.
12. Como usuário, quero receber alertas de pendências e prazos próximos do vencimento, para agir a tempo.
13. Como coordenação, quero gerar relatórios gerenciais (alunos em atraso, alunos por status e por orientador, tempo médio de integralização, produção por aluno e por professor), para acompanhar o andamento do programa.

---

# Regras Gerais de Implementação

1. O back-end e a lógica dos paradigmas devem ser implementados em Python, combinando os Paradigmas Lógico e Orientado a Aspectos no mesmo sistema.
2. O Paradigma Lógico deve ser realizado por um motor de inferência implementado do zero, sem bibliotecas externas de programação lógica.
3. O Paradigma Orientado a Aspectos deve ser realizado apenas com recursos nativos do Python, sem bibliotecas externas de orientação a aspectos.
4. A lógica de negócio das operações deve permanecer livre das preocupações transversais. Autorização, auditoria, histórico, validação de prazos e alertas devem ser aplicados por aspectos, não escritos manualmente dentro de cada operação.
5. As decisões sobre situações acadêmicas (aptidão, risco, validade de créditos, elegibilidade de atividades) devem ser expressas como regras declarativas resolvidas pelo motor de inferência, e não como cadeias de `if/else` espalhadas pelo código.
6. O sistema deve contar com uma interface gráfica que permita executar as operações do núcleo e visualizar, no mínimo, o checklist de integralização e a situação acadêmica inferida de um aluno.
7. O código deve seguir princípios de Clean Code: nomes descritivos, funções curtas, responsabilidades bem separadas e comentários significativos.

---

# Regras Específicas de Programação Lógica

1. Implemente um motor de inferência próprio capaz de representar fatos e regras, realizar unificação entre termos, aplicar substituições e resolver consultas.
2. Modele o conhecimento acadêmico como fatos e regras (cláusulas) processadas por esse motor. Os fatos vêm dos dados cadastrados (alunos, *tasks*, créditos, atividades creditáveis validadas). As regras expressam as políticas do programa.
3. Cubra, no mínimo, as seguintes inferências por meio de regras declarativas:

   a. Aptidão à defesa: um aluno está apto se possui créditos mínimos, proficiência, qualificação aprovada, ao menos uma produção (atividade creditável do tipo bibliográfico) validada e plano concluído.

   b. Validação de créditos: os créditos do aluno satisfazem os grupos obrigatórios (mínimo por grupo básico, mínimo por grupo específico, máximo por atividade creditável do tipo tecnológico).

   c. Situação acadêmica: inferir a situação do aluno dentre os estados definidos no Domínio, em especial distinguindo regular de em risco e identificando qualificado e em fase de defesa.

   d. Elegibilidade de atividade creditável: uma atividade creditável gera crédito se estiver dentro do período do curso, possuir comprovante, ter o tipo ativo e não exceder o limite por categoria.

   e. Pontuação de produção: a pontuação de uma produção pondera o nível de relevância do veículo, configurável a nível de programa.

4. As regras devem ser declarativas e configuráveis, de modo que mudar uma política signifique alterar regras ou fatos, e não reescrever o fluxo de controle do sistema.
5. Separe claramente a base de fatos, a base de regras e o mecanismo de resolução. O restante do sistema deve consultar o motor por meio de uma interface de consulta, sem conhecer os detalhes internos da resolução.

---

# Regras Específicas de Programação Orientada a Aspectos

1. Trate como aspectos as preocupações que atravessam várias operações do sistema. No mínimo, cinco aspectos: autorização por papel, auditoria das operações, histórico de alterações das entidades, validação de prazos e geração de alertas de pendências.
2. Implemente os aspectos usando exclusivamente mecanismos nativos do Python, como decoradores, metaclasses, descritores, `__init_subclass__` e o módulo `inspect`.
3. Deixe explícito, na documentação (essencial) e em comentários (quando for pertinente), como os conceitos de Orientação a Aspectos se manifestam no código: quais são os *join points* (pontos de interceptação), quais são os *advices* (comportamento aplicado antes, depois ou em torno da operação) e como ocorre o *weaving* (a aplicação dos aspectos sobre o código de negócio).
4. Um mesmo aspecto deve ser reutilizado em múltiplas operações sem duplicação de código. Adicionar uma nova operação ao sistema não deve exigir reescrever a lógica de autorização, auditoria ou histórico.
5. A ativação dos aspectos deve ser configurável, de modo que seja possível ligar ou desligar preocupações transversais sem alterar a lógica de negócio.

---

# Regras de Organização

Cada grupo deve criar um repositório privado no GitHub e adicionar os professores como colaboradores (usuários: `paulosevero` e `sequincozes`).

O desenvolvimento deve ser gerenciado usando a funcionalidade de Projetos do GitHub, com metodologia Kanban (ou similar), atendendo aos seguintes critérios:

- Issues devem ser usadas como tarefas do projeto.
- O quadro do projeto deve estar populado com todas as tarefas mapeadas para o desenvolvimento (até a entrega final), organizadas na coluna **Backlog**.
- A cada semana, o grupo deve remanejar as tarefas conforme o andamento do desenvolvimento, seguindo o fluxo:

```text
Backlog → Sprint Backlog → Em Progresso → Feito
```

com responsáveis atribuídos a cada tarefa.

> **IMPORTANTE:** A criação do repositório, o compartilhamento com os professores e a organização do projeto no GitHub devem ser realizados até dia **07/06/2026 às 23h59min**. Negligência no atendimento deste critério resultará em conceito **NOk** para o grupo inteiro na verificação semanal.
>
> A entrega final do projeto ocorre em **13/07/2026**.

---

# Stack de Tecnologia

- **Front-end:** React.
- **Back-end:** FastAPI.
- **Banco de dados:** Firebase.

---

# Dicas de Implementação

## Programação Lógica (motor de inferência)

1. Comece pelo motor isolado, com um conjunto pequeno de fatos e regras de teste, antes de conectá-lo ao domínio acadêmico. Garanta que unificação, substituição e aplicação de regras funcionam em consultas simples.
2. Represente termos lógicos com estruturas simples (por exemplo, tuplas e uma classe para variáveis) e mantenha a substituição como um dicionário de variável para valor.
3. Escreva cada regra de forma independente e nomeada, para conseguir testá-la isoladamente e ligar ou desligar políticas sem tocar no restante do código.
4. Teste cada inferência listada nas Regras Específicas de Programação Lógica com casos de aluno apto, em risco e inapto, garantindo que o resultado muda conforme os fatos.
5. Trate a relevância do veículo (evento ou revista) como um fato configurável a nível de programa, e não como valor fixo no código. Assim, a pontuação de uma mesma produção pode mudar conforme a relevância cadastrada e a observação registrada, sem alterar as regras.
6. Exponha o motor por uma única função de consulta e mantenha fatos, regras e resolução em módulos separados, para o restante do sistema não depender dos detalhes internos.

## Programação Orientada a Aspectos

1. Implemente um primeiro aspecto simples (auditoria via decorador) e só depois generalize para os demais. Cada aspecto deve valer para várias operações sem duplicação, de modo que adicionar uma operação nova não exija reescrever autorização, auditoria ou histórico.
2. Use decoradores para interceptar funções ou métodos individuais, e metaclasses ou `__init_subclass__` quando precisar aplicar um aspecto a todos os métodos de uma classe automaticamente. Use descritores quando o ponto de interceptação for o acesso a um atributo.
3. Use o módulo `inspect` para descobrir, em tempo de execução, informações sobre as operações interceptadas (nome, argumentos, assinatura), o que ajuda na auditoria, no histórico e na rastreabilidade.
4. Sugestões de aspectos e do que cada um intercepta:

   a. **Auditoria:** registra usuário, perfil, operação, data/hora, entidade afetada e valor anterior e novo, em operações como cadastro de plano, criação de *task*, envio de progresso, validação de atividade creditável e mudança de status.

   b. **Autorização por perfil:** antes da operação, verifica o papel (aluno registra apenas progresso próprio, orientador altera apenas planos dos próprios orientandos, coordenação valida atividades creditáveis e mantém checklist e tipos).

   c. **Notificações e alertas:** após a operação, dispara avisos (progresso registrado notifica o orientador, *task* próxima do vencimento alerta o aluno, atividade creditável validada ou rejeitada notifica o aluno).

   d. **Validação de prazos:** antes ou depois da operação, verifica *tasks* vencidas, plano atrasado, qualificação ou defesa próximas e checklist incompleto perto do prazo, alimentando a marcação de em risco.

   e. **Histórico e versionamento:** ao alterar plano, checklist ou tipo de atividade creditável, guarda a versão anterior, evidenciando que regras institucionais mudam com o tempo.

5. Deixe explícito, em comentários (onde for conveniente) e na documentação (obrigatoriamente), onde estão os *join points* (pontos interceptados), quais são os *advices* (comportamento antes, depois ou em torno da operação) e como ocorre o *weaving* (a aplicação dos aspectos sobre o código de negócio).

---

# Glossário

## Programação Lógica

- **Motor de inferência:** programa que responde consultas combinando fatos e regras para deduzir novas conclusões, em vez de seguir um passo a passo fixo escrito pelo programador.
- **Fato:** afirmação que o sistema considera verdadeira, derivada dos dados cadastrados, por exemplo "o aluno A concluiu a qualificação".
- **Regra (cláusula):** afirmação condicional que deduz algo novo a partir de outras condições, por exemplo "A está apto à defesa se A tem créditos mínimos e qualificação aprovada e produção validada".
- **Termo:** a unidade de informação manipulada pelo motor, podendo ser um valor concreto (constante) ou uma incógnita (variável).
- **Variável lógica:** incógnita dentro de um termo cujo valor o motor tenta descobrir ao responder uma consulta.
- **Unificação:** processo de comparar dois termos e descobrir quais valores tornam ambos iguais, por exemplo casar `apto(X)` com `apto(aluno_A)` descobrindo que `X = aluno_A`.
- **Substituição:** o conjunto de pares variável-valor encontrado pela unificação, mantido tipicamente como um dicionário de variável para valor.
- **Consulta:** pergunta feita ao motor, por exemplo "o aluno A está apto à defesa?", que o motor responde aplicando fatos e regras.
- **Aplicação direta de regras:** estratégia de resolução em que o motor verifica as condições de uma regra de forma direta (conjunção de condições), sem testar caminhos alternativos nem voltar atrás (sem *backtracking*).
- **Base de fatos e base de regras:** as duas coleções que o motor consulta, separadas do mecanismo que resolve as consultas.

## Programação Orientada a Aspectos

- **Programação orientada a aspectos:** abordagem que isola, em módulos próprios chamados aspectos, comportamentos que se repetem em muitas partes do sistema, mantendo a lógica de negócio limpa.
- **Preocupação transversal (cross-cutting concern):** comportamento necessário em várias operações diferentes, como autorização, auditoria, histórico e alertas, que cortaria o código todo se fosse escrito manualmente em cada lugar.
- **Aspecto:** o módulo que encapsula uma preocupação transversal e a aplica sobre as operações de negócio sem que elas precisem conhecê-la.
- **Separação de interesses:** princípio de manter cada responsabilidade em seu próprio lugar, de modo que a lógica de negócio não se misture com as preocupações transversais.
- **Join point (ponto de junção):** um ponto do programa onde um aspecto pode ser aplicado, por exemplo a chamada de um método ou o acesso a um atributo.
- **Advice:** o comportamento que o aspecto executa no *join point*, podendo rodar antes, depois ou em torno da operação original.
- **Weaving (tecelagem):** o ato de combinar os aspectos com a lógica de negócio, fazendo os *advices* serem de fato executados nos *join points* selecionados. Em Python, isso é feito por decoradores, metaclasses e mecanismos afins.

## Mecanismos nativos do Python usados como aspectos

- **Decorador:** função que envolve outra função ou método para acrescentar comportamento antes ou depois, sem alterar o código original.
- **Metaclasse:** classe que define como outras classes são criadas, permitindo aplicar um aspecto a todos os métodos de uma classe de uma só vez.
- **Descritor:** objeto que controla a leitura e a escrita de um atributo, servindo como ponto de interceptação no acesso a dados.
- **`__init_subclass__`:** gancho chamado automaticamente quando uma classe é definida a partir de outra, útil para aplicar aspectos a toda uma hierarquia de classes.
- **`inspect`:** módulo padrão que revela, em tempo de execução, informações sobre funções e classes (nome, argumentos, assinatura), úteis para auditoria e rastreabilidade.

---

**Última atualização:** terça-feira, 2 jun. 2026, 11:57
