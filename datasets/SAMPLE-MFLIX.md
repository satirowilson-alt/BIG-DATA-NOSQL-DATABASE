# SAMPLE_MFLIX DATABASE

## 📚 Visão Geral

O `sample_mflix` é um banco de dados de exemplo fornecido pelo MongoDB que simula um serviço de streaming de filmes, similar ao Netflix. É ideal para aprendizado e testes de queries NoSQL.

---

## 🗂️ Estrutura do Banco de Dados

### Collections Principais

```
sample_mflix/
├── 📄 movies        (~23,000 documentos)
├── 📄 comments      (~50,000 documentos)
├── 📄 users         (~185 documentos)
├── 📄 theaters      (~1,500 documentos)
└── 📄 sessions      (sessões de usuário)
```

---

## 🎬 Collection: movies

Contém informações sobre filmes, incluindo metadados, elenco, avaliações e prêmios.

### Estrutura de Documento

```javascript
{
  _id: ObjectId("573a1390f29313caabcd4135"),
  title: "The Great Train Robbery",
  year: 1903,
  runtime: 11,
  released: ISODate("1903-12-01T00:00:00.000Z"),
  
  // Informações de exibição
  rated: "TV-G",              // Classificação etária
  plot: "A group of bandits...",
  fullplot: "Extended plot description...",
  
  // Arrays de categorização
  genres: ["Action", "Western", "Crime"],
  directors: ["Edwin S. Porter"],
  writers: ["Scott Marble (story)", "Edwin S. Porter"],
  cast: ["A.C. Abadie", "Gilbert M. 'Broncho Billy' Anderson"],
  countries: ["USA"],
  languages: ["English"],
  
  // Avaliações
  imdb: {
    rating: 7.4,
    votes: 9847,
    id: 439
  },
  
  tomatoes: {
    viewer: {
      rating: 3.7,
      numReviews: 2559,
      meter: 75
    },
    fresh: 6,
    critic: {
      rating: 7.6,
      numReviews: 6,
      meter: 100
    },
    rotten: 0,
    lastUpdated: ISODate("2015-08-08T19:16:10.000Z")
  },
  
  // Metadados adicionais
  poster: "url_to_poster.jpg",
  num_mflix_comments: 0,
  
  // Prêmios
  awards: {
    wins: 1,
    nominations: 0,
    text: "1 win."
  },
  
  type: "movie",
  lastupdated: "2015-08-26 00:03:50.133000000"
}
```

### Campos Importantes

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `title` | String | Título do filme |
| `year` | Number | Ano de lançamento |
| `runtime` | Number | Duração em minutos |
| `genres` | Array | Gêneros (Drama, Action, etc.) |
| `directors` | Array | Lista de diretores |
| `cast` | Array | Elenco principal |
| `countries` | Array | Países de produção |
| `imdb.rating` | Number | Nota IMDB (0-10) |
| `imdb.votes` | Number | Quantidade de votos |
| `tomatoes.viewer.rating` | Number | Nota Rotten Tomatoes |

### Estatísticas

```javascript
// Total de documentos
db.movies.countDocuments()
// ~23,000

// Filmes com rating IMDB
db.movies.countDocuments({ "imdb.rating": { $exists: true } })
// ~21,000

// Filmes por década
db.movies.aggregate([
  { $bucket: {
      groupBy: "$year",
      boundaries: [1900, 1950, 1980, 1990, 2000, 2010, 2020],
      default: "Outros",
      output: { count: { $sum: 1 } }
    }
  }
])
```

### Gêneros Mais Comuns

1. Drama - ~13,000 filmes
2. Comedy - ~8,000 filmes
3. Romance - ~4,500 filmes
4. Thriller - ~4,000 filmes
5. Action - ~3,500 filmes

---

## 💬 Collection: comments

Comentários de usuários sobre filmes.

### Estrutura de Documento

```javascript
{
  _id: ObjectId("5a9427648b0beebeb69579cc"),
  name: "Andrea Le",
  email: "andrea_le@fakegmail.com",
  movie_id: ObjectId("573a1390f29313caabcd4135"),
  text: "Rem officiis eaque repellendus amet...",
  date: ISODate("2012-03-26T23:20:16.000Z")
}
```

### Campos

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `name` | String | Nome do usuário |
| `email` | String | Email do usuário |
| `movie_id` | ObjectId | Referência ao filme |
| `text` | String | Texto do comentário |
| `date` | ISODate | Data/hora do comentário |

### Estatísticas

```javascript
// Total de comentários
db.comments.countDocuments()
// ~50,000

// Comentários por filme (top 5)
db.comments.aggregate([
  { $group: { _id: "$movie_id", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 5 }
])

// Usuários mais ativos
db.comments.aggregate([
  { $group: { _id: "$email", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 }
])
```

---

## 👤 Collection: users

Informações de usuários da plataforma.

### Estrutura de Documento

```javascript
{
  _id: ObjectId("59b99db4cfa9a34dcd7885b6"),
  name: "Ned Stark",
  email: "sean_bean@gameofthron.es",
  password: "$2b$12$UREFwsRUoyF0CRqGNK0LzO0HM/jLhgUCNNIJ9RJAqMUQ74crlJ1Vu"
}
```

### Campos

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `name` | String | Nome completo |
| `email` | String | Email (usado como login) |
| `password` | String | Hash da senha (bcrypt) |

---

## 🎭 Collection: theaters

Informações sobre cinemas.

### Estrutura de Documento

```javascript
{
  _id: ObjectId("59a47286cfa9a3a73e51e72c"),
  theaterId: 104,
  location: {
    address: {
      street1: "5000 W 147th St",
      city: "Hawthorne",
      state: "CA",
      zipcode: "90250"
    },
    geo: {
      type: "Point",
      coordinates: [-118.36559, 33.897167]
    }
  }
}
```

### Campos

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `theaterId` | Number | ID único do cinema |
| `location.address` | Object | Endereço completo |
| `location.geo` | GeoJSON | Coordenadas geográficas |

---

## 🔗 Relacionamentos

### movies ↔ comments

```javascript
// Relacionamento 1:N (One-to-Many)
// Um filme pode ter muitos comentários

// Join usando $lookup
db.movies.aggregate([
  {
    $lookup: {
      from: "comments",
      localField: "_id",        // Campo em movies
      foreignField: "movie_id", // Campo em comments
      as: "comentarios"
    }
  }
])
```

### comments ↔ users

```javascript
// Relacionamento N:1 (Many-to-One)
// Muitos comentários pertencem a um usuário

// Join por email
db.comments.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "email",
      foreignField: "email",
      as: "usuario"
    }
  }
])
```

---

## 📊 Queries de Exemplo

### Filmes Mais Bem Avaliados

```javascript
db.movies.find(
  { 
    "imdb.rating": { $exists: true },
    "imdb.votes": { $gte: 1000 }
  },
  {
    title: 1,
    year: 1,
    "imdb.rating": 1
  }
).sort({ "imdb.rating": -1 }).limit(10)
```

### Atores Mais Prolíficos

```javascript
db.movies.aggregate([
  { $unwind: "$cast" },
  { 
    $group: { 
      _id: "$cast", 
      filmes: { $sum: 1 },
      avgRating: { $avg: "$imdb.rating" }
    } 
  },
  { $sort: { filmes: -1 } },
  { $limit: 20 }
])
```

### Evolução dos Gêneros por Década

```javascript
db.movies.aggregate([
  { $match: { year: { $gte: 1980 } } },
  { $unwind: "$genres" },
  {
    $bucket: {
      groupBy: "$year",
      boundaries: [1980, 1990, 2000, 2010, 2020],
      output: {
        generos: { $push: "$genres" },
        count: { $sum: 1 }
      }
    }
  },
  { $unwind: "$generos" },
  {
    $group: {
      _id: { decada: "$_id", genero: "$generos" },
      quantidade: { $sum: 1 }
    }
  },
  { $sort: { "_id.decada": 1, quantidade: -1 } }
])
```

### Filmes com Mais Comentários

```javascript
db.movies.aggregate([
  {
    $lookup: {
      from: "comments",
      localField: "_id",
      foreignField: "movie_id",
      as: "comentarios"
    }
  },
  {
    $project: {
      title: 1,
      year: 1,
      qtdComentarios: { $size: "$comentarios" }
    }
  },
  { $sort: { qtdComentarios: -1 } },
  { $limit: 10 }
])
```

---

## 🎯 Índices Existentes

### movies
```javascript
db.movies.getIndexes()

// Índices principais:
// - _id (padrão)
// - cast_text_fullplot_text_genres_text_title_text (text search)
```

### comments
```javascript
db.comments.getIndexes()

// Índices principais:
// - _id (padrão)
// - movie_id (para lookups)
```

---

## 💡 Dicas de Performance

### Use Projeções
```javascript
// ❌ Ruim - retorna documento completo
db.movies.find({ year: 2010 })

// ✅ Bom - retorna apenas campos necessários
db.movies.find(
  { year: 2010 },
  { title: 1, year: 1, "imdb.rating": 1 }
)
```

### Limite Resultados Durante Desenvolvimento
```javascript
// Use .limit() para testar queries
db.movies.find({ year: 2010 }).limit(10)
```

### Filtre Antes de Unwind
```javascript
// ❌ Ineficiente
db.movies.aggregate([
  { $unwind: "$cast" },
  { $match: { year: 2010 } }  // Filtra depois de unwind
])

// ✅ Eficiente
db.movies.aggregate([
  { $match: { year: 2010 } },  // Filtra antes de unwind
  { $unwind: "$cast" }
])
```

---

## 🔍 Campos Úteis para Análises

### Análises Temporais
- `year` - Ano de lançamento
- `released` - Data completa de lançamento
- `comments.date` - Data dos comentários

### Análises de Qualidade
- `imdb.rating` - Avaliação IMDB
- `imdb.votes` - Popularidade
- `tomatoes.viewer.rating` - Avaliação do público
- `awards.wins` - Prêmios ganhos

### Análises Categóricas
- `genres` - Gêneros (array)
- `countries` - Países de produção
- `languages` - Idiomas
- `directors` - Diretores
- `cast` - Elenco

### Análises Geográficas
- `theaters.location.geo` - Coordenadas (GeoJSON)
- `countries` - Países

---

## 📖 Recursos Adicionais

- **MongoDB Sample Datasets**: https://docs.atlas.mongodb.com/sample-data/
- **Aggregation Framework**: https://docs.mongodb.com/manual/aggregation/
- **Array Operators**: https://docs.mongodb.com/manual/reference/operator/query-array/

---

**Dataset ideal para aprender:**
- ✅ Dados realistas e interessantes
- ✅ Múltiplas collections com relacionamentos
- ✅ Diversos tipos de campos (strings, numbers, arrays, objetos)
- ✅ Ideal para praticar aggregations complexas
