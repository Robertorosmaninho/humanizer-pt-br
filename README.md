# Humanizer pt-BR

Skill portátil para remover marcas recorrentes de texto gerado por IA e reescrever o conteúdo em português brasileiro natural. A adaptação preserva sentido, cobertura, registro e voz autoral. Não é uma tradução palavra por palavra do Humanizer em inglês: os critérios foram revistos para a sintaxe, a ortografia, os registros e a variação do português do Brasil.

O runtime é apenas o arquivo `SKILL.md`, em Markdown. Qualquer agente capaz de carregar instruções de skill pode usá-lo.

## Instalação

### Skills CLI

```bash
npx skills add Robertorosmaninho/humanizer-pt-br
```

Para atualizar uma instalação existente:

```bash
npx skills update humanizer-pt-br
```

Para instalar em todos os agentes configurados:

```bash
npx skills add Robertorosmaninho/humanizer-pt-br --agent '*'
```

Para escolher um agente:

```bash
npx skills add Robertorosmaninho/humanizer-pt-br --agent <nome-do-agente>
```

### Plugin do Claude Code

```text
/plugin marketplace add Robertorosmaninho/humanizer-pt-br
/plugin install humanizer-pt-br@humanizer-pt-br
```

O comando da skill passa a ser `/humanizer-pt-br:humanizer-pt-br`.

### Instalação manual

```bash
git clone https://github.com/Robertorosmaninho/humanizer-pt-br.git /caminho/para/skills/humanizer-pt-br
```

Ou copie apenas o runtime:

```bash
mkdir -p /caminho/para/skills/humanizer-pt-br
cp SKILL.md /caminho/para/skills/humanizer-pt-br/
```

## Uso

Invoque a skill conforme o mecanismo do seu agente:

```text
/humanizer-pt-br

[cole aqui o texto em português brasileiro]
```

Também funciona como pedido direto:

```text
Humanize este texto em português brasileiro: [texto]
```

### Calibração de voz

Forneça dois ou três parágrafos escritos pela própria pessoa quando quiser preservar seu ritmo, vocabulário, pontuação, regionalismos e escolhas como `tu`/`você` ou `nós`/`a gente`:

```text
Use esta amostra para calibrar minha voz:
[amostra]

Agora humanize este texto:
[texto]
```

A skill não injeta `pra`, `né`, gírias ou diminutivos para fingir espontaneidade. Ela também não europeíza colocação pronominal nem uniformiza variedades regionais sem pedido.

## Como a adaptação pt-BR funciona

A versão mantém a arquitetura original de 33 padrões, além do ciclo rascunho, auditoria e versão final. Cinco regras exigiram mudanças estruturais, não tradução literal:

- o gerúndio é legítimo em pt-BR; o padrão 3 mira gerúndios que fingem análise;
- sujeito oculto, oração impessoal e `se` são naturais; o padrão 13 mira passiva burocrática, nominalização e apagamento relevante do agente;
- travessões são comuns em diálogos e na prosa brasileira; o padrão 14 corta o excesso parentético, não todo travessão;
- aspas tipográficas não são um sinal útil; o padrão 19 agora detecta calques e sintaxe traduzida do inglês;
- hífen não é uma preferência estilística em português; o padrão 26 aplica a ortografia brasileira e remove compostos artificiais importados do inglês.

O texto só deve ser marcado quando houver um conjunto de sinais. Uma palavra formal, um travessão, um emoji ou uma frase curta isolada não provam uso de IA.

## 33 padrões detectados

### Conteúdo

| # | Padrão | Antes | Depois |
|---|---|---|---|
| 1 | **Importância e legado inflados** | "representou um marco decisivo na evolução cultural" | Dizer o que abriu, mudou ou passou a atender |
| 2 | **Notoriedade sem contexto** | Lista de jornais, canais e seguidores | Citar uma declaração ou fato relevante |
| 3 | **Gerúndios de análise superficial** | "refletindo... simbolizando... destacando..." | Informar agente, causa ou fonte |
| 4 | **Linguagem promocional** | "experiência única no coração da serra" | Descrever localização e características verificáveis |
| 5 | **Atribuições vagas** | "especialistas acreditam" | Nomear a fonte; sem fonte, retirar a alegação ou explicitar a lacuna |
| 6 | **Desafios e perspectivas formulaicos** | "apesar dos desafios, segue rumo a um futuro promissor" | Explicar problemas, datas e ações concretas |

### Linguagem e gramática

| # | Padrão | Antes | Depois |
|---|---|---|---|
| 7 | **Vocabulário de IA acumulado** | "solução robusta que potencializa a jornada" | Explicar o que o sistema faz |
| 8 | **Fuga de ser, estar e ter** | "configura-se como", "atua como", "conta com" | "é", "está", "tem" quando forem mais claros |
| 9 | **Paralelismos negativos e slogans** | "não é só X, é Y", "sem achismo" | Afirmar o ponto diretamente |
| 10 | **Regra de três** | "inovação, inspiração e conexão" | Usar a quantidade real de itens |
| 11 | **Rodízio de sinônimos** | "pesquisadora, cientista, especialista, acadêmica" | Repetir o termo mais claro |
| 12 | **Falsos intervalos** | "do samba à arquitetura, passando pela culinária" | Listar tópicos sem escala inventada |
| 13 | **Passiva burocrática e agente apagado** | "foi realizada a análise" | "a equipe analisou" quando o agente importar |

### Estilo

| # | Padrão | Antes | Depois |
|---|---|---|---|
| 14 | **Travessões parentéticos em excesso** | Vários apartes entre travessões | Reestruturar; preservar diálogo e usos autorais |
| 15 | **Negrito em série** | "**OKRs**, **KPIs**, **metas**" | Destacar apenas o que precisa de ênfase |
| 16 | **Listas com minitítulos** | "**Desempenho:** O desempenho..." | Prosa, tabela ou lista sem repetição |
| 17 | **Maiúsculas de título** | "Negociações Estratégicas e Parcerias Globais" | "Negociações estratégicas e parcerias globais" |
| 18 | **Emojis decorativos** | "🚀 Lançamento; ✅ Próximos passos" | Remover quando não fizerem parte da voz |
| 19 | **Calques do inglês** | "endereçar dores e entregar experiência sem fricção" | Usar colocação e regência naturais em pt-BR |

### Comunicação

| # | Padrão | Antes | Depois |
|---|---|---|---|
| 20 | **Restos de conversa com chatbot** | "Espero que ajude. Quer que eu continue?" | Retirar do conteúdo |
| 21 | **Corte de conhecimento e especulação** | "há poucos dados; provavelmente cresceu..." | Dizer apenas o que as fontes informam |
| 22 | **Tom bajulador** | "Excelente pergunta! Você está certíssimo!" | Responder diretamente |

### Enchimento e cadência

| # | Padrão | Antes | Depois |
|---|---|---|---|
| 23 | **Enchimento e metadiscurso** | "é importante destacar que" | Começar pela informação |
| 24 | **Atenuação excessiva** | "poderia potencialmente talvez" | "pode" ou a ressalva necessária |
| 25 | **Conclusão positiva genérica** | "futuro promissor e novos patamares" | Informar próximo passo, prazo ou fato |
| 26 | **Hifenização importada** | "centrado-no-cliente", "tempo-real" | "centrado no cliente", "tempo real" |
| 27 | **Falsa autoridade** | "a verdadeira questão", "em sua essência" | Apresentar o argumento sem cerimônia |
| 28 | **Anúncio da explicação** | "vamos mergulhar", "a seguir veremos" | Começar pela explicação |
| 29 | **Cabeçalho repetido** | `## Desempenho` + "Desempenho é fundamental" | Deixar o título cumprir sua função |
| 30 | **Texto ancorado no diff** | "esta função foi adicionada para substituir" | Descrever o comportamento atual |
| 31 | **Drama em frases curtas** | "Sem medo. Sem ruído. Sem concessões." | Variar o ritmo e apresentar fatos |
| 32 | **Fórmula de aforismo** | "simetria é a linguagem da confiança" | Explicar a relação concreta |
| 33 | **Falsa intimidade retórica** | "Sinceramente? A verdade é a seguinte..." | Dizer a observação diretamente |

## Exemplo

**Antes:**

> Passei cinco dias inesquecíveis em Salvador e preciso dizer: essa cidade roubou meu coração! Banhada pela Baía de Todos-os-Santos, Salvador se apresenta como um testemunho vibrante da rica história brasileira, onde tradição, cultura e modernidade se entrelaçam de forma única.
>
> Nenhuma visita estaria completa sem conhecer o icônico Pelourinho e mergulhar em sua energia contagiante. E a comida? Simplesmente divina. Cada acarajé representa uma celebração de sabores, destacando a diversidade cultural que torna a Bahia tão singular.
>
> Eu voltaria? Com certeza! Salvador não é apenas um destino, mas um lugar para sentir, viver e amar. Prepare-se para uma experiência que ficará para sempre no coração. ✨

**Depois:**

> Passei cinco dias em Salvador em janeiro e voltei com duas certezas: gostei muito da cidade e escolhi a pior semana possível para descobrir que não lido bem com calor. Eu sabia que faria calor, claro. Só não tinha entendido que, às dez da manhã, minha camisa já pareceria ter atravessado uma tempestade.
>
> Fiquei perto do centro histórico, o que ajudou em parte. Também significou subir ladeiras todos os dias e aprender rápido quais trajetos valiam um carro. O Pelourinho estava tão cheio na primeira tarde que mal consegui prestar atenção nos prédios. Voltei cedo dois dias depois. Com as lojas ainda abrindo e menos gente disputando a calçada, o lugar finalmente fez sentido para mim.
>
> Comi acarajé duas vezes. O primeiro exigiu quarenta minutos de fila e chegou morno. O segundo veio de um tabuleiro perto do hotel, sem placa famosa nem discurso, e estava muito melhor. Foi uma boa lembrança de que roteiro gastronômico também erra.
>
> Eu voltaria, de preferência num mês menos quente e com mais dois dias livres. Não porque a cidade tenha "roubado meu coração", mas porque saí com a sensação incômoda de ter entendido só uma parte dela.

O exemplo completo, com o rascunho e a auditoria intermediária, está em `SKILL.md`.

## Base linguística e licenças

| Fonte | Uso nesta adaptação | Observação |
|---|---|---|
| [VOLP, Academia Brasileira de Letras](https://www.academia.org.br/nossa-lingua/vocabulario-ortografico) | Autoridade de grafia e classe gramatical | A edição digital 2025-2026 informa mais de 380 mil entradas e atenção à variedade brasileira |
| [VERO/LibreOffice pt-BR](https://github.com/LibreOffice/dictionaries/tree/master/pt_BR) | Léxico Hunspell para conferência ortográfica | Dicionário livre sob LGPLv3/MPL; usado como ferramenta de pesquisa, não incluído no runtime Markdown |
| [PortiLexicon-UD, NILC/ICMC-USP](https://portilexicon.icmc.usp.br/) | Formas, lemas, classes e traços morfológicos | Mais de 1,2 milhão de entradas; CC BY 4.0 |
| [Corpus Carolina, USP](https://sites.usp.br/corpuscarolina/corpus/) | Uso contemporâneo em contexto e contraste de gêneros | Cada documento tem procedência e licença próprias; o cabeçalho do corpus usa CC BY-NC-SA 4.0 |
| [Portal Domínio Público, MEC](https://dominiopublico.mec.gov.br/) | Ritmo literário e história do português brasileiro | Obras antigas não servem, sozinhas, como modelo de prosa contemporânea |
| [Agência Brasil](https://agenciabrasil.ebc.com.br/sobre) | Referência pontual de prosa jornalística atual | A política vigente permite reprodução jornalística com crédito e pede contato para usos comerciais; o conteúdo não foi incorporado ao repositório |

O dicionário VERO usado na pesquisa tem 312.368 entradas de base e regras Hunspell de flexão. Ele ficou fora do repositório porque o produto deve continuar portátil e inteiramente baseado em Markdown. Ortografia, frequência e naturalidade são problemas diferentes: o VOLP e o VERO confirmam formas; o PortiLexicon descreve morfologia; corpora mostram uso; a decisão editorial ainda depende de contexto e registro.

## Referências

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), taxonomia de partida
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup), projeto que mantém o guia
- [Humanizer original](https://github.com/blader/humanizer), base da arquitetura, do fluxo e da numeração inicial

## Histórico de versões

- **3.0.0** - Primeira adaptação integral para português brasileiro. Preserva os 33 números, mas reescreve instruções, listas e exemplos em pt-BR; adiciona calibração de variedade e registro; impede a fabricação de oralidade; adapta gerúndios e passivas; deixa de proibir travessões legítimos; substitui a regra de aspas curvas por calques do inglês; troca a regra inglesa de compostos pela hifenização brasileira; e exige que atribuições vagas sejam resolvidas ou assumidas como lacuna, nunca apenas repetidas após a auditoria. A mudança é estrutural porque uma tradução literal produziria correções erradas em sujeito oculto, colocação pronominal, pontuação e compostos.
- **2.8.2** - Versão-base em inglês: novo exemplo completo em primeira pessoa, mantendo tema, perspectiva e extensão aproximada.
- **2.8.1** - Documentação de instalação entre agentes, empacotamento opcional para Claude Code e proteção contra falsos positivos em texto citado.
- **2.8.0** - Padrões 31 a 33 para punchlines fabricadas, fórmulas de aforismo e aberturas retóricas. Total: 33 padrões.
- **2.7.0** - Padrão 30, corte rígido de travessões na versão inglesa e ampliação do preenchimento especulativo. Total: 30 padrões.
- **2.6.0** - Consolidação do fluxo e limitação da orientação de personalidade aos gêneros adequados. Sem mudança na contagem.
- **2.5.1** - Regra de voz passiva e fragmentos sem sujeito. Total: 29 padrões.
- **2.5.0** - Novos padrões de autoridade persuasiva, metadiscurso e cabeçalhos fragmentados.
- **2.4.0** - Calibração opcional pela amostra de voz do usuário.
- **2.3.0** - Regra inglesa de compostos hifenizados.
- **2.2.0** - Auditoria "ainda parece IA" e segunda reescrita.
- **2.1.1** - Correção do exemplo de aspas curvas e retas.
- **2.1.0** - Exemplos antes/depois para os 24 padrões então existentes.
- **2.0.0** - Reescrita com base no guia da Wikipédia.
- **1.0.0** - Lançamento inicial.

## Licença

MIT
