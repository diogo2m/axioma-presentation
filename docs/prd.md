# PRD — AXIOMA Apresentação

> Axioma é um sistema acadêmico para monitoramento de trajetória acadêmica construidp com **FastAPI**, **React + TypeScript**, **Firebase** e **Clean Architecture**. O projeto aplica múltiplos paradigmas de programação, especialmente programação logica e programação orientada a aspectos.
>
> Contexto consolidado: [CLAUDE.md](../CLAUDE.md), [CONTEXT.md](../CONTEXT.md), [docs/adr](adr).

## Objetivo

Criar uma apresentação de slides robusta para apresentação para professor. Deve durar 10 minutos.

## User Stories (software desenvolvido, não da apresentação)

1. Como coordenação, quero cadastrar alunos, orientadores e a relação de orientação, para manter o registro dos discentes do programa.
2. Como orientador, quero cadastrar as etapas e as _tasks_ do plano de trabalho de um aluno, para organizar o acompanhamento do progresso.
3. Como aluno, quero registrar atualizações de progresso vinculadas a uma _task_, para refletir o andamento do meu plano.
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

## Implementation Decisions

### Decision #1: Motor de Inferência Lógica Construído do Zero

- Motor próprio de lógica de predicados implementado em Python puro (sem bibliotecas externas), com suporte a termos (Atom, Compound, Variable), unificação e resolução SLD.
- Base de conhecimento configurável contendo fatos acadêmicos e regras declarativas para resolver aptidão à defesa, validade de créditos, situação acadêmica e elegibilidade de atividades.
- Abstração por meio de uma interface simples de consulta (`inference_port`), mantendo o núcleo de inferência isolado do restante do sistema.

### Decision #2: Programação Orientada a Aspectos Nativa

- Interceptação de preocupações transversais (Autorização por papel, Auditoria, Histórico de alterações, Validação de prazos e Alertas/Notificações) usando decoradores, metaclasses (`__init_subclass__`) e descritores nativos do Python.
- Uso do módulo padrão `inspect` para reflexão em tempo de execução para extrair assinaturas e argumentos dos métodos interceptados.
- Ativação configurável de aspectos, permitindo ligar/desligar aspectos por ambiente ou contexto sem alterar a lógica de negócios da aplicação.

### Decision #3: Clean Architecture e DDD em Sete Camadas

- Divisão clara de responsabilidades com fronteiras bem definidas: React/TypeScript -> Services -> FastAPI Routers -> Aspect Layer -> Application Use Cases -> Domain Core & Inference Engine -> Infrastructure adapters (Firebase/Firestore Repositories).
- Inversão de dependências rigorosa (setas apontando sempre para dentro), onde o domínio central e o motor lógico não conhecem camadas externas ou banco de dados.

### Configuração (`AxiomaPresentationSettings`)

Dataclass com configurações de estilo e tecnologias definidos em JSON.

## Further Notes

- A apresentação deve detalhar a colaboração prática entre Lógica e Aspectos: como um aspecto (ex: submissão de atividade creditável) intercepta o fluxo de negócios e consulta o motor de inferência lógica para reavaliar o checklist de integralização e o status do discente.
- O estilo visual dos diagramas de arquitetura e sequência nos slides deve seguir o padrão simplificado do ByteByteGo para garantir legibilidade técnica instantânea.
