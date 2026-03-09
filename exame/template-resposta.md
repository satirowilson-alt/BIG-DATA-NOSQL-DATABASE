# RESPOSTAS - TESTE DE MONGODB

## IDENTIFICAÇÃO

**Nome completo:** WILSON SÁTIRO DE SOUZA FILHO  
**Matrícula:** 2428632  
**Email:** satirowilson@gmail.com  
**Data:** ___/___/______

---

## QUESTÃO 1 - Consulta Básica com Filtros

### Comando Utilizado
```javascript
// Cole aqui seu comando find(db.movies.find(
  {
    genres: "Drama",
    year: { $gte: 2010, $lte: 2015 },
    "imdb.rating": { $gt: 7.5 }
  },
  {
    _id: 0,
    title: 1,
    year: 1,
    "imdb.rating": 1,
    genres: 1
  }
)
.sort({ "imdb.rating": -1 })
.limit(20))


```

### Resultado Obtido
- **Quantidade de documentos encontrados:** 352
- **5 primeiros filmes (título e rating):**
  1. title: 'Drishyam',  rating: 8.9
  2. title: 'Most Likely to Succeed',  rating: 8.9
  3. title: 'Kaakkaa Muttai', rating: 8.8
  4. title: 'Killswitch', rating: 8.8
  5. title: 'The Great Alone', rating: 8.7

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao01.png]_



### Observações (opcional)
A consulta utilizou filtro por gênero, intervalo de anos e classificação IMDb, com projeção dos campos solicitados, ordenação decrescente por rating e limitação aos 20 primeiros resultados.

---

## QUESTÃO 2 - Agregação com Agrupamento

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
[
{
$match: {
countries: { $exists: true, $type: "array", $ne: [] }
}
},
{
$unwind: "$countries"
},
{
$match: {
countries: { $ne: null, $ne: "" }
}
},
{
$group: {
_id: "$countries",
quantidadeFilmes: { $sum: 1 }
}
},
{
$sort: { quantidadeFilmes: -1 }
},
{
$limit: 10
},
{
$project: {
_id: 0,
pais: "$_id",
quantidadeFilmes: 1
}
}
]
```

### Resultado Obtido

| Posição | País | Quantidade de Filmes |
|---------|------|----------------------|
| 1º | USA | 10921 |
| 2º | UK | 2652 |
| 3º | FRANCE | 2647 |
| 4º | GERMANY | 1494 |
| 5º | CANADA | 1260 |
| 6º | ITALY | 1217 |
| 7º | JAPAN | 786 |
| 8º | SPAIN | 675 |
| 9º | INDIA | 564 |
| 10º | AUSTRALIA | 470 |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao02.png]_

### Observações (opcional)
O pipeline considera apenas filmes com informação válida no campo countries, utiliza $unwind para separar os países dos filmes com múltiplas nacionalidades, agrupa os registros por país, ordena pela quantidade de filmes em ordem decrescente e limita o resultado aos 10 países com maior produção.

---

## QUESTÃO 3 - Pipeline com $unwind e $group

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([
db.movies.aggregate([
  { $match: { "imdb.rating": { $ne: null } } },
  { $unwind: "$cast" },
  {
    $group: {
      _id: "$cast",
      quantidadeFilmes: { $sum: 1 },
      mediaRating: { $avg: "$imdb.rating" }
    }
  },
  {
    $project: {
      _id: 0,
      ator: "$_id",
      quantidadeFilmes: 1,
      mediaRating: { $round: ["$mediaRating", 2] }
    }
  },
  { $sort: { quantidadeFilmes: -1 } },
  { $limit: 5 }
])

])
```

### Resultado Obtido

| Posição | Ator | Qtd Filmes | Rating Médio |
|---------|------|------------|--------------|
| 1º | Gèrard Depardieu | 67 | 6.69 |
| 2º | Robert De Niro | 58 | 6.96 |
| 3º | Michael Caine | 51 | 6.71 |
| 4º | Bruce Willis | 49 | 6.41 |
| 5º | Samuel L. Jackson | 48 | 6.4 |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao03.png]_

### Observações (opcional)


---

## QUESTÃO 4 - Agregação com $lookup

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline com $lookup
db.movies.aggregate([[
{
$group: {
_id: "$movie_id",
quantidadeComentarios: { $sum: 1 },
primeiros3Usuarios: {
$push: {
name: "$name",
email: "$email"
}
}
}
},
{
$project: {
quantidadeComentarios: 1,
primeiros3Usuarios: { $slice: ["$primeiros3Usuarios", 3] }
}
},
{
$sort: { quantidadeComentarios: -1 }
},
{
$limit: 5
},
{
$lookup: {
from: "movies",
localField: "_id",
foreignField: "_id",
as: "filme"
}
},
{
$unwind: "$filme"
},
{
$project: {
_id: 0,
title: "$filme.title",
year: "$filme.year",
quantidadeComentarios: 1,
primeiros3Usuarios: 1
}
}
]


])
```

### Resultado Obtido

**Filme 1:**
- Título: The Taking of Pelham 1 2 3
- Ano: 2009
- Quantidade de comentários: 161
- Primeiros 3 usuários:
  1. Nome: Alliser Thorne | Email: owen_teale@gameofthron.es
  2. Nome: Amy Ramirez | Email: amy_ramirez@fakegmail.com
  3. Nome: Amy Ramirez | Email: amy_ramirez@fakegmail.com

**Filme 2:**
- Título: About a Boy
- Ano: 2002
- Quantidade de comentários: 158
- Primeiros 3 usuários:
  1. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com
  2. Nome: Anthony Cline | Email: anthony_cline@fakegmail.com
  3. Nome: Anthony Smith | Email: anthony_smith@fakegmail.com

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao04.png]_

### Observações (opcional)

---

## QUESTÃO 5 - Agregação com Múltiplos Estágios

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline completa
db.movies.aggregate([[
{
$match: {
"imdb.rating": { $ne: null },
genres: { $exists: true, $ne: [] }
}
},
{
$unwind: "$genres"
},
{
$match: {
genres: { $ne: null, $ne: "" }
}
},
{
$group: {
_id: "$genres",
quantidadeFilmes: { $sum: 1 },
mediaRating: { $avg: "$imdb.rating" }
}
},
{
$match: {
quantidadeFilmes: { $gte: 10, $lte: 50 },
mediaRating: { $gt: 7.0 }
}
},
{
$project: {
_id: 0,
genero: "$_id",
quantidadeFilmes: 1,
mediaRating: { $round: ["$mediaRating", 2] }
}
},
{
$sort: { mediaRating: -1 }
}
]


])
```

### Resultado Obtido

| Gênero | Qtd Filmes | Rating Médio |
| News   |    44      | 7.25         |
| | | |
| | | |
| | | |
| | | |

### Explicação
**Por que esses gêneros são considerados subestimados?**
O gênero "News" pode ser considerado subestimado porque possui uma quantidade relativamente pequena de filmes na base analisada (44 filmes), mas apresenta uma classificação média elevada (7.25). Isso indica que, embora haja poucas produções nesse gênero, os filmes tendem a ter boa qualidade segundo as avaliações do IMDb.

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao07.png]_

---
