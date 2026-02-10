# GUIA DE USO DO MONGODB COMPASS

## 📱 Sobre o MongoDB Compass

MongoDB Compass é a interface gráfica oficial do MongoDB que permite explorar e interagir com seus dados de forma visual e intuitiva. É a ferramenta recomendada para este teste.

---

## 🚀 Instalação

### Download
- Acesse: https://www.mongodb.com/try/download/compass
- Selecione seu sistema operacional
- Faça o download da versão mais recente
- Execute o instalador

### Sistemas Suportados
- Windows 10/11
- macOS 10.14+
- Ubuntu 20.04+
- Red Hat Enterprise Linux 8+

---

## 🔗 Conectando ao Banco de Dados

### Passo 1: Abrir o Compass
- Inicie o MongoDB Compass
- Você verá a tela de conexão

### Passo 2: String de Conexão
String de Conexão disponibilizada no Grupo WhatsApp

```
mongodb+srv://usuario:senha@cluster.mongodb.net/sample_mflix
```

### Passo 3: Conectar
1. Cole a string de conexão no campo apropriado
2. Clique em "Connect"
3. Aguarde a conexão ser estabelecida

### Verificação
Após conectar, você deve ver:
- Lista de databases no painel esquerdo
- Database `sample_mflix` disponível
- Collections: movies, comments, users, theaters, sessions

---

## 🗂️ Navegando pela Interface

### Painel Esquerdo - Databases e Collections
```
📁 sample_mflix
  ├── 📄 comments      (~50,000 docs)
  ├── 📄 movies        (~23,000 docs)
  ├── 📄 sessions      (~vários docs)
  ├── 📄 theaters      (~vários docs)
  └── 📄 users         (~vários docs)
```

### Área Central - Visualização de Dados
- **Documents**: Ver documentos da collection
- **Aggregations**: Criar pipelines de agregação
- **Schema**: Ver estrutura dos dados
- **Indexes**: Ver e criar índices
- **Validation**: Regras de validação

---

## 🔍 Explorando Dados - Aba Documents

### Visualizar Documentos
1. Clique em uma collection (ex: `movies`)
2. Veja os documentos em formato JSON
3. Use as setas para navegar entre documentos

### Filtrar Documentos
Na barra "Filter", você pode usar queries MongoDB:

```javascript
// Exemplos de filtros
{ year: 2010 }
{ "imdb.rating": { $gt: 8.0 } }
{ genres: "Drama" }
```

### Projeção (Selecionar Campos)
Na opção "Project":
```javascript
{ title: 1, year: 1, "imdb.rating": 1, _id: 0 }
```

### Ordenação
Na opção "Sort":
```javascript
{ "imdb.rating": -1 }  // Decrescente
{ year: 1 }            // Crescente
```

---

## 🔧 Usando Aggregation Builder

### Abrir Aggregation Builder
1. Selecione a collection
2. Clique na aba **"Aggregations"**
3. Você verá um pipeline vazio

### Adicionar Estágios
1. Clique em **"Add Stage"**
2. Selecione o operador (ex: $match, $group, $project)
3. Digite o código JSON no editor
4. Veja o preview dos resultados

### Exemplo Visual de Pipeline

```
Stage 1: $match
┌─────────────────────────────┐
│ { year: { $gte: 2010 } }   │
└─────────────────────────────┘
        ↓
Stage 2: $group
┌─────────────────────────────┐
│ {                           │
│   _id: "$genres",           │
│   count: { $sum: 1 }        │
│ }                           │
└─────────────────────────────┘
        ↓
Stage 3: $sort
┌─────────────────────────────┐
│ { count: -1 }               │
└─────────────────────────────┘
```

### Recursos Úteis
- **Preview**: Veja os resultados de cada estágio
- **Collapse/Expand**: Ocultar estágios para focar em um específico
- **Enable/Disable**: Ativar/desativar estágios temporariamente
- **Comments**: Adicionar comentários aos estágios

---

## 💻 Usando o Compass Shell (MongoSH)

### Abrir o Shell
1. Clique no ícone `>_MONGOSH` no rodapé do Compass
2. Uma janela de terminal será aberta dentro do Compass

### Comandos Básicos

```javascript
// Verificar database atual
db

// Mudar para sample_mflix
use sample_mflix

// Listar collections
show collections

// Contar documentos
db.movies.countDocuments()

// Query simples
db.movies.find({ year: 2010 })

// Query com pretty print
db.movies.find({ year: 2010 }).pretty()

// Aggregation
db.movies.aggregate([
  { $match: { year: 2010 } },
  { $count: "total" }
])
```

### Dicas do Shell
- Use `↑` e `↓` para navegar no histórico de comandos
- Use `Tab` para autocompletar
- Use `.help()` para ajuda: `db.movies.find.help()`
- Use `.limit(10)` para limitar resultados durante testes

---

## 📊 Exportando Resultados

### Exportar de Aggregation Builder
1. Monte sua pipeline
2. Clique em "..." (três pontos) no topo
3. Selecione **"Export to Language"**
4. Escolha **"JavaScript"**
5. Copie o código gerado

### Exportar Documentos
1. Na aba Documents, filtre os dados desejados
2. Clique em "..." (três pontos)
3. Selecione **"Export Collection"**
4. Escolha formato: JSON, CSV

---

## 📸 Capturando Screenshots

### Windows
- **Ferramenta de Captura**: `Win + Shift + S`
- **Print Screen**: `PrtScn` (tela toda)
- **Snipping Tool**: Busque no menu Iniciar

### macOS
- **Área selecionada**: `Cmd + Shift + 4`
- **Tela toda**: `Cmd + Shift + 3`
- **Janela específica**: `Cmd + Shift + 4`, depois `Space`

### Linux
- **Print Screen**: Captura tela
- **Shift + Print Screen**: Captura área
- **Flameshot**: `flameshot gui` (se instalado)

### Dicas para Screenshots
- Inclua a query/pipeline no screenshot
- Certifique-se que os resultados estejam visíveis
- Mostre pelo menos 3-5 documentos de resultado
- Não precisa mostrar TODOS os resultados, apenas exemplos

---

## 🐛 Troubleshooting

### Problema: Não consigo conectar
**Soluções:**
- Verifique se a string de conexão está correta
- Confirme usuário e senha
- Verifique sua conexão com a internet (se Atlas)
- Confirme se o MongoDB está rodando (se local)

### Problema: Pipeline não executa
**Soluções:**
- Verifique vírgulas e chaves
- Use um validador JSON online
- Teste cada estágio individualmente
- Leia a mensagem de erro com atenção

### Problema: Resultado vazio
**Soluções:**
- Verifique se os filtros estão corretos
- Teste sem filtros primeiro
- Use `.countDocuments()` para ver se há dados
- Verifique se está na collection correta

### Problema: Compass está lento
**Soluções:**
- Limite resultados com `.limit(100)`
- Feche outras abas/aplicações
- Use filtros para reduzir dados carregados
- Reinicie o Compass

---

## ⚡ Atalhos de Teclado

| Atalho | Ação |
|--------|------|
| `Ctrl/Cmd + K` | Abrir Command Palette |
| `Ctrl/Cmd + F` | Buscar em documentos |
| `Ctrl/Cmd + Shift + F` | Buscar em toda database |
| `Ctrl/Cmd + T` | Nova aba |
| `Ctrl/Cmd + W` | Fechar aba |
| `F5` | Atualizar view |

---

## 💡 Dicas para o Teste

### Antes de Começar
1. ✅ Conecte ao banco e explore as collections
2. ✅ Veja exemplos de documentos com `findOne()`
3. ✅ Teste queries simples antes de fazer pipelines complexas
4. ✅ Mantenha a documentação do MongoDB aberta

### Durante o Teste
1. 💡 Teste cada estágio da pipeline individualmente
2. 💡 Use `.limit(5)` enquanto desenvolve para economizar tempo
3. 💡 Copie e salve seus códigos em um arquivo de texto
4. 💡 Faça screenshots à medida que resolve as questões

### Boas Práticas
- **Comente seu código** quando a lógica for complexa
- **Indente corretamente** para facilitar leitura
- **Use nomes descritivos** para campos calculados
- **Teste antes de finalizar** - execute tudo novamente

### Se Encontrar Dificuldades
1. Releia a questão com calma
2. Divida o problema em partes menores
3. Consulte a documentação oficial
4. Tente uma abordagem mais simples primeiro
5. Deixe para depois e volte com mente fresca

---

## 📚 Recursos Adicionais

### Documentação Oficial
- MongoDB Manual: https://docs.mongodb.com/manual/
- Aggregation Operators: https://docs.mongodb.com/manual/reference/operator/aggregation/
- Query Operators: https://docs.mongodb.com/manual/reference/operator/query/

### Tutoriais Compass
- Compass Docs: https://docs.mongodb.com/compass/
- Video Tutorials: Canal oficial MongoDB no YouTube

### Prática
- MongoDB University: https://university.mongodb.com/
- Exercises: https://www.mongodb.com/docs/manual/tutorial/

---

## ✅ Checklist Final

Antes de entregar o teste:

- [ ] Todos os comandos foram testados e executam
- [ ] Screenshots foram capturados
- [ ] Códigos foram salvos em arquivo de texto
- [ ] Resultados fazem sentido logicamente
- [ ] Formatação está legível
- [ ] Nome e matrícula estão no arquivo

---

**Boa prova! Você consegue! 🚀**

Lembre-se: MongoDB é sobre explorar dados de forma flexível. Seja criativo, mas também seja preciso!
