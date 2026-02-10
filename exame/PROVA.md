# TESTE DE MONGODB - SISTEMAS NOSQL

**Curso:** Pós-Graduação/MBA em Big Data  
**Disciplina:** Sistemas de Bancos de Dados NoSQL  
**Professor:** _________________________  
**Data:** ___/___/______  
**Duração:** 2 horas  

---

## IDENTIFICAÇÃO DO ALUNO

**Nome completo:** _______________________________________________  
**Matrícula:** ____________________  
**Email:** ________________________________________

---

## INSTRUÇÕES GERAIS

1. Este teste é **INDIVIDUAL** e deve ser realizado sem comunicação com outros alunos
2. Utilize o **MongoDB Compass** ou **Compass Shell** para resolver todas as questões
3. Você pode consultar a **documentação oficial do MongoDB** durante o teste
4. Para cada questão, forneça:
   - O comando/pipeline completo executado
   - Screenshot ou descrição do resultado obtido
   - Breve explicação da sua solução (quando solicitado)
5. Salve suas respostas no formato indicado no arquivo `template-resposta.md`
6. A clareza, organização e comentários no código serão considerados na avaliação
7. **Banco de dados utilizado:** `sample_mflix` (certifique-se de estar conectado)

---

## QUESTÕES

### QUESTÃO 1 (10 pontos) - Consulta Básica com Filtros

Encontre todos os filmes do gênero **"Drama"** lançados entre **2010 e 2015** que tenham uma classificação IMDB (`imdb.rating`) superior a **7.5**. 

**Requisitos:**
- Retorne apenas os campos: `title`, `year`, `imdb.rating` e `genres`
- Ordene os resultados por rating **decrescente**
- Limite os resultados aos 20 primeiros filmes

**Entregue:**
- [ ] Comando utilizado
- [ ] Quantidade de documentos encontrados
- [ ] Screenshot dos 5 primeiros resultados

---

### QUESTÃO 2 (10 pontos) - Agregação com Agrupamento

Calcule a quantidade total de filmes por país (campo `countries`). Mostre os **10 países** com maior produção cinematográfica.

**Requisitos:**
- Exiba o nome do país e a quantidade de filmes
- Considere que um filme pode ter múltiplos países
- Ordene pela quantidade de filmes de forma **decrescente**
- Ignore filmes sem informação de país

**Entregue:**
- [ ] Pipeline de agregação completa
- [ ] Lista dos 10 países com suas respectivas quantidades
- [ ] Screenshot do resultado

---

### QUESTÃO 3 (10 pontos) - Pipeline com $unwind e $group

Identifique os **5 atores** (campo `cast`) que mais aparecem em filmes da base. Para cada ator, mostre:
- Nome do ator
- Quantidade de filmes
- Média de rating (`imdb.rating`) dos filmes em que participou

**Requisitos:**
- Considere apenas filmes que tenham rating definido
- Arredonde a média de rating para 2 casas decimais
- Ordene pela quantidade de filmes de forma **decrescente**

**Entregue:**
- [ ] Pipeline completa com $unwind e $group
- [ ] Tabela com os 5 atores e suas estatísticas
- [ ] Screenshot do resultado

---

### QUESTÃO 4 (10 pontos) - Agregação com $lookup

Crie uma pipeline que combine dados das collections `movies` e `comments`. Para os **5 filmes com mais comentários**, mostre:
- Título do filme
- Ano de lançamento
- Quantidade de comentários
- Lista com nome e email dos **3 primeiros** usuários que comentaram

**Requisitos:**
- Use $lookup para relacionar as collections
- Ordene pelos filmes com mais comentários
- Limite o resultado aos 5 filmes

**Entregue:**
- [ ] Pipeline completa com $lookup
- [ ] Estrutura do documento resultante
- [ ] Screenshot mostrando pelo menos 2 filmes

---

### QUESTÃO 5 (10 pontos) - Análise Temporal

Analise a evolução da produção cinematográfica por década. Agrupe os filmes por década:
- 1980-1989
- 1990-1999
- 2000-2009
- 2010-2019

Para cada década, calcule:
- Quantidade total de filmes
- Rating médio do IMDB (arredondado para 2 casas decimais)
- Maior rating registrado

**Requisitos:**
- Use expressões condicionais ou bucket para agrupar por década
- Considere apenas filmes com rating definido
- Ordene cronologicamente (década mais antiga primeiro)

**Entregue:**
- [ ] Pipeline de agregação
- [ ] Tabela comparativa das décadas
- [ ] Breve análise: qual década teve melhor qualidade média?

---

### QUESTÃO 6 (10 pontos) - Filtros Complexos com Arrays

Encontre filmes que tenham **Tom Hanks E Robin Wright** no elenco (campo `cast`) **simultaneamente**.

**Requisitos:**
- Retorne: título, ano, elenco completo e rating
- Use operadores apropriados para busca em arrays
- Ordene por ano de lançamento

**Entregue:**
- [ ] Query utilizada
- [ ] Quantidade de filmes encontrados
- [ ] Lista completa dos filmes (título e ano)
- [ ] Screenshot de pelo menos 1 filme completo

---

### QUESTÃO 7 (10 pontos) - Agregação com Múltiplos Estágios

Crie uma pipeline que identifique os gêneros mais **"subestimados"** - aqueles que têm poucos filmes mas alta qualidade.

**Critérios:**
- Gêneros com **no mínimo 10 filmes** e **no máximo 50 filmes**
- Rating médio superior a **7.0**
- Mostre: gênero, quantidade de filmes e rating médio (2 casas decimais)
- Ordene pelo rating médio **decrescente**

**Requisitos:**
- Use $unwind para separar os gêneros
- Aplique filtros apropriados
- Use $match em múltiplos estágios se necessário

**Entregue:**
- [ ] Pipeline completa
- [ ] Lista de gêneros subestimados
- [ ] Explicação: por que esses gêneros são considerados subestimados?

---

### QUESTÃO 8 (10 pontos) - Análise de Comentários

Usando a collection `comments`, identifique os **5 usuários mais ativos** (que fizeram mais comentários).

Para cada usuário, mostre:
- Nome do usuário (`name`)
- Email
- Total de comentários
- Data do primeiro comentário
- Data do último comentário

**Requisitos:**
- Agrupe por email do usuário
- Use operadores de agregação para min/max de datas
- Ordene pela quantidade de comentários (decrescente)

**Entregue:**
- [ ] Pipeline de agregação
- [ ] Tabela com os 5 usuários mais ativos
- [ ] Screenshot do resultado

---

### QUESTÃO 9 (10 pontos) - Pipeline com Expressões Condicionais

Classifique os filmes em categorias baseadas no rating IMDB:
- **"Excelente"**: rating >= 8.0
- **"Bom"**: rating >= 6.0 e < 8.0
- **"Regular"**: rating >= 4.0 e < 6.0
- **"Fraco"**: rating < 4.0

**Requisitos:**
- Mostre quantos filmes existem em cada categoria
- Calcule o rating médio de cada categoria (2 casas decimais)
- Considere apenas filmes que tenham rating definido
- Use $switch ou $cond para classificação

**Entregue:**
- [ ] Pipeline com expressões condicionais
- [ ] Tabela com as 4 categorias e suas estatísticas
- [ ] Screenshot do resultado
- [ ] Qual categoria tem mais filmes?

---

### QUESTÃO 10 (10 pontos) - Pipeline Avançada Combinada

Crie uma análise que mostre, para cada **diretor que tenha dirigido pelo menos 5 filmes**:
- Nome do diretor
- Quantidade de filmes dirigidos
- Rating médio dos seus filmes (2 casas decimais)
- Seu filme com **maior rating** (título e rating)
- Gêneros mais frequentes nos seus filmes (**top 3**)

**Requisitos:**
- Use $unwind para diretores
- Filtre diretores com mínimo de 5 filmes
- Ordene pelos diretores com maior rating médio
- Limite aos 10 melhores diretores

**Entregue:**
- [ ] Pipeline completa (pode ser complexa, comente as etapas)
- [ ] Lista dos 5 primeiros diretores
- [ ] Screenshot de pelo menos 2 diretores com detalhes completos
- [ ] Breve explicação da estratégia utilizada

---

## CRITÉRIOS DE AVALIAÇÃO

Para cada questão será avaliado:

| Critério | Pontos | Descrição |
|----------|--------|-----------|
| **Sintaxe e Execução** | 4 | Query/pipeline sintaticamente correta e executável |
| **Resultado Correto** | 4 | Resposta atende aos requisitos e está correta |
| **Organização** | 2 | Código legível, bem formatado e comentado |

**Pontuação Final:** Soma das 10 questões = **100 pontos**

---

## ENTREGA

1. Preencha o arquivo `template-resposta.md` com todas as suas respostas
2. Inclua screenshots solicitados em cada questão
3. Formato de entrega: arquivo `.md` ou `.pdf` com nome: `MONGODB_SeuNome_Matricula`
4. Prazo: conforme instruções do professor

---

**BOA PROVA! 🚀**

**Lembre-se:** MongoDB é sobre encontrar padrões nos dados. Analise, experimente e documente seu raciocínio!
