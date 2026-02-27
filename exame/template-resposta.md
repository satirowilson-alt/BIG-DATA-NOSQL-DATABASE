# RESPOSTAS - TESTE DE MONGODB

## IDENTIFICAÇÃO

**Nome completo:** _____________________________________________  
**Matrícula:** ____________________  
**Email:** ________________________________________  
**Data:** ___/___/______

---

## QUESTÃO 1 - Consulta Básica com Filtros

### Comando Utilizado
```javascript
// Cole aqui seu comando find()
find com filtros + projection + sort + limit
db.movies.find(
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
.limit(20)

Quantidade de documentos encontrados (no shell):
db.movies.countDocuments({
  genres: "Drama",
  year: { $gte: 2010, $lte: 2015 },
  "imdb.rating": { $gt: 7.5 }
})

Código para print dos 5 primeiros
db.movies.find(
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
.limit(5)

```

### Resultado Obtido
- **Quantidade de documentos encontrados:** 352
- **5 primeiros filmes (título e rating):**
  1. title: 'Most Likely to Succeed',  rating: 8.9
  2. title: 'Drishyam',  rating: 8.9
  3. title: 'Killswitch', rating: 8.8
  4. title: 'Kaakkaa Muttai', rating: 8.8
  5. title: 'The Great Alone', rating: 8.7

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao01.png]_



### Observações (opcional)


---

## QUESTÃO 2 - Agregação com Agrupamento

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([


])
```

### Resultado Obtido

| Posição | País | Quantidade de Filmes |
|---------|------|----------------------|
| 1º | | |
| 2º | | |
| 3º | | |
| 4º | | |
| 5º | | |
| 6º | | |
| 7º | | |
| 8º | | |
| 9º | | |
| 10º | | |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao02.png]_

### Observações (opcional)


---

## QUESTÃO 3 - Pipeline com $unwind e $group

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([


])
```

### Resultado Obtido

| Posição | Ator | Qtd Filmes | Rating Médio |
|---------|------|------------|--------------|
| 1º | | | |
| 2º | | | |
| 3º | | | |
| 4º | | | |
| 5º | | | |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao03.png]_

### Observações (opcional)


---

## QUESTÃO 4 - Agregação com $lookup

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline com $lookup
db.movies.aggregate([


])
```

### Resultado Obtido

**Filme 1:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

**Filme 2:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao04.png]_

### Observações (opcional)

---

## QUESTÃO 5 - Agregação com Múltiplos Estágios

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline completa
db.movies.aggregate([


])
```

### Resultado Obtido

| Gênero | Qtd Filmes | Rating Médio |
|--------|------------|--------------|
| | | |
| | | |
| | | |
| | | |

### Explicação
**Por que esses gêneros são considerados subestimados?**


### Screenshot
_[Anexar screenshot ou indicar arquivo: questao07.png]_

---
