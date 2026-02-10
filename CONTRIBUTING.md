# Contribuindo com o Projeto

Obrigado por considerar contribuir com o MongoDB NoSQL Exam! Este documento fornece diretrizes para contribuições.

## 🤝 Como Contribuir

### Reportando Bugs

Se você encontrou um erro no teste, gabarito ou documentação:

1. Verifique se o bug já foi reportado nas [Issues](../../issues)
2. Se não, crie uma nova issue incluindo:
   - Descrição clara do problema
   - Passos para reproduzir
   - Comportamento esperado vs. atual
   - Screenshots (se aplicável)
   - Versão do MongoDB/Compass utilizada

### Sugerindo Melhorias

Para sugerir novas questões ou melhorias:

1. Abra uma issue com a tag `enhancement`
2. Descreva sua sugestão detalhadamente
3. Explique por que seria útil
4. Forneça exemplos se possível

### Pull Requests

1. **Fork** o repositório
2. Crie uma **branch** para sua feature (`git checkout -b feature/NovaQuestao`)
3. **Commit** suas mudanças (`git commit -m 'Adiciona nova questão sobre indexes'`)
4. **Push** para a branch (`git push origin feature/NovaQuestao`)
5. Abra um **Pull Request**

## 📝 Diretrizes para Questões

### Criando Novas Questões

Ao criar uma nova questão:

- ✅ Deve usar o banco sample_mflix
- ✅ Deve ter objetivo claro e específico
- ✅ Deve incluir requisitos explícitos
- ✅ Deve ter gabarito completo com soluções
- ✅ Deve documentar erros comuns
- ✅ Deve ter pontuação definida (geralmente 10 pontos)

### Estrutura de Arquivo de Gabarito

```javascript
// ============================================================================
// GABARITO - QUESTÃO X
// Título Descritivo
// ============================================================================

// OBJETIVO:
// Descrição clara do que a questão avalia

// SOLUÇÃO COMPLETA
// Código comentado

// RESULTADO ESPERADO
// O que o aluno deve obter

// CRITÉRIOS DE AVALIAÇÃO
// Como pontuar (4+4+2)

// ERROS COMUNS DOS ALUNOS
// Lista de erros típicos

// VARIAÇÕES ACEITAS
// Soluções alternativas válidas
```

## 🎯 Áreas que Precisam de Ajuda

- [ ] Tradução do material para inglês
- [ ] Questões sobre geoespacial ($geoNear, $geoWithin)
- [ ] Questões sobre text search
- [ ] Questões sobre indexes e performance
- [ ] Vídeos tutoriais
- [ ] Material de estudo preparatório
- [ ] Scripts de correção automatizada

## 💻 Configuração do Ambiente de Desenvolvimento

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/mongodb-nosql-exam.git

# Navegue até o diretório
cd mongodb-nosql-exam

# Configure o MongoDB
# Certifique-se de ter sample_mflix carregado

# Teste as queries
mongosh < scripts/setup-database.js
```

## ✅ Checklist para Pull Requests

- [ ] Código testado no MongoDB Compass
- [ ] Documentação atualizada
- [ ] Comentários adequados no código
- [ ] Gabarito completo se for nova questão
- [ ] CHANGELOG.md atualizado
- [ ] Sem erros de sintaxe
- [ ] Segue o estilo do projeto

## 📜 Código de Conduta

### Nossa Promessa

Este projeto é dedicado a fornecer uma experiência livre de assédio para todos, independentemente de:
- Idade, tamanho corporal, deficiência
- Etnia, identidade e expressão de gênero
- Nível de experiência, nacionalidade
- Aparência pessoal, raça, religião
- Identidade e orientação sexual

### Comportamento Esperado

- Linguagem acolhedora e inclusiva
- Respeito a pontos de vista e experiências diferentes
- Aceitar críticas construtivas graciosamente
- Focar no que é melhor para a comunidade
- Mostrar empatia com outros membros

### Comportamento Inaceitável

- Linguagem ou imagens sexualizadas
- Trolling, comentários insultuosos/depreciativos
- Assédio público ou privado
- Publicar informações privadas de outros
- Outras condutas inapropriadas em contexto profissional

## 🏆 Reconhecimento

Contribuidores serão listados no README.md e receberão crédito apropriado.

### Contribuidores Atuais

- Seu Nome Aqui! (seja o primeiro a contribuir)

## 📧 Contato

Para questões sobre contribuições:
- Abra uma issue
- Ou entre em contato com os mantenedores

## 📄 Licença

Ao contribuir, você concorda que suas contribuições serão licenciadas sob a mesma licença MIT do projeto.

---

**Obrigado por contribuir! 🚀**

Sua ajuda torna este recurso melhor para professores e alunos de MongoDB.
