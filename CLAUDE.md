# AXIOMA Apresentação

Instruções específicas para esta apresentação. Sobrepõem-se às globais em caso de conflito.

## Contexto

- **Domínio**: solução para gestão de atividades de discentes de pós-graduação.
- **Status**: solução fechada, implementada em versão estável. Disponível em [axioma](axioma/).
- **Paradismas**: Paradigmas Lógico + Orientado a Aspectos.
- **Última revisão**: 2026-07-10.

A apresentação é baseada no que foi desenvolvido ao longo do semestre no repositório do [AXIOMA](https://github.com/ed-dferreira/axioma/) (cópia em `axioma/`). Entretanto, algumas informações podem estar sendo implicitamente tomadas baseado no conteúdo do [enunciado](docs/enunciado/projeto_enunciado.md). O estilo de apresentação é fortemente similar a [ByteByteGo](https://bytebytego.com/), entretanto a estética _per se_ (cores, curvas, formas, tipografia) devem ser baseadas na [logo](docs/img/logo.png).

## Papel do Claude

- Entender o projeto desenvolvido de forma progressiva de acordo com que os slides se tornam mais aprofundados na implementação técnica.
- Desenvolver uma estilização única e memorável, similarmente ao que foi feito em [beautiful-html-templates](beautiful-html-templates/)
- Implementar e refinar o sistema TAILOR seguindo as decisões já tomadas (ver CONTEXT.md e README.md).
- Aderir estritamente ao escopo registrado: não introduzir conceitos ou features inexistentes, não trocar estilização, não adicionar elementos complexos com difícil manutenção no HTML/CSS etc.
- Quando uma decisão de design não estiver em CONTEXT.md ou README.md, **perguntar antes de implementar**. Não inferir silenciosamente.

## Stack e convenções de código

- **Stack da Apresentação**: HTML5 estático, Vanilla JS (gerenciamento de palco e teclado), Tailwind CSS (via CDN para layouts rápidos, posicionamento e micro-animações) e CSS customizado para o padrão `cobalt-grid`.
- **Animações**: Transições dinâmicas de slide-in/out e fade-in suaves usando as classes utilitárias de transição do Tailwind CSS combinadas com regras de animação nativas.
- **Convenções**:
  - Idioma: PT-BR em discussões, documentação e conteúdo dos slides; EN-US em variáveis de controle de código, funções e estilos.
  - Formatação: Manter o código limpo, sem dependências de compilação JS externas.

## Pontos de referência no repositório

- [README.md](README.md) — escopo e arquitetura.
- [CONTEXT.md](CONTEXT.md) — glossário canônico.
- [DESIGN.md](DESIGN.md) — glossário contendo as informações de estilo.
- [docs/prd.md](docs/prd.md) — PRD da apresentação de AXIOMA.
- [docs/adr/](docs/adr/) — decisões que divergem do design original.
- [docs/enunciado](docs/enunciado) — Contém informações do projeto [projeto_enunciado](docs/enunciado/projeto_enunciado.md), diretrizes de como a implementação deve ser feita e quais atributos são necessários de serem feitos. Além disso, possui informações adicionais da forma de [avaliação das entregas](docs/enunciado/plano_de_ensino.md).
- [axioma](axioma) — Solução feita. Estender, não modificar (adicionar `arrival_step` em `Application` é trivial e segue padrão de outros projetos do diretório).

## Invariantes (não negociar sem perguntar)

1. **Controle de slides**: Frente e traz com arrow cases, cíclico, quando termina o último slide, volta para a capa.
2. **Download em PDF**: Possibilidade de salvar a apresentação em PDF.

## Decisões em aberto a serem confirmadas durante a implementação

- **Visualização de Código**: Trechos de código curtos mostrando unificação e aspectos AOP serão exibidos em cards estilizados que simulam IDEs com a cor azul cobalto dominante.
- **Diagramas de Integração**: Fluxos de dados estilo ByteByteGo ilustrando como os Aspectos interceptam ações e consultam o motor de inferência lógica serão desenhados com elementos CSS/SVG responsivos.
- **Layout das Grades**: O visual de papel milimetrado (`cobalt-grid`) será o plano de fundo em todos os slides da apresentação, com linhas tênues em azul cobalto.

## Convenções

- Idioma: PT-BR em discussão e documentação; EN-US em código (variáveis, funções, comentários, docstrings).
- Documentação técnica: `README.md` (humano), `CLAUDE.md` (agente), `CONTEXT.md` (glossário), `docs/adr/*.md` (decisões).
- Após escrever ou editar qualquer `.md`, rodar `prettier -w` no arquivo.

## Não fazer

- Não usar frameworks pesados de apresentação JS (como Reveal.js ou Impress.js) que interfiram nos estilos e grids minimalistas do template `cobalt-grid`.
- Não depender do servidor backend FastAPI ativo para rodar a apresentação; todos os fluxos e dados das demonstrações devem ser estáticos ou simulados no front-end da apresentação.
- Não introduzir fontes de texto externas ao escopo do template `cobalt-grid` (Newsreader, Hanken Grotesk, DM Mono) para garantir a coerência visual acadêmica.
