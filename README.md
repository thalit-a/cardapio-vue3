
---

# 🍽️ Cardápio Virtual - Vue 3 + Tailwind + API Externa

Projeto desenvolvido durante um curso de Vue 3, com o objetivo de criar uma aplicação de **cardápio virtual interativo**, utilizando as melhores práticas do ecossistema moderno JavaScript.

---

## 🛠️ Tecnologias Utilizadas

- ⚙️ **Vue 3** – Framework JavaScript progressivo e reativo.
- 🎨 **Tailwind CSS v4** – Framework de estilos utilitário para uma UI moderna e responsiva.
- ⚡ **Vite** – Ferramenta de build super rápida.
- 🌐 **API Externa [DummyJSON](https://dummyjson.com/)** – Fonte de dados para as receitas e categorias de pratos.
- 🧠 **Composição com `<script setup>`** – Abordagem mais moderna do Vue 3.

---

## ✨ Funcionalidades

- 📋 Listagem de receitas com imagens, nomes e preços.
- 🍽️ Categorias de pratos organizadas por tipo de cozinha.
- 🔍 Visualização detalhada do produto ao clicar em um card.
- 🛒 Carrinho de compras funcional:
  - Adicionar itens
  - Remover itens
  - Exibir valor total
- ✅ Finalização de compra (simulada).
- 📱 Responsivo e adaptado para dispositivos móveis.

---

## 💻 Instalação e Execução

### 📦 Instalar dependências

```bash
npm install
```

### 🔥 Rodar em modo desenvolvimento

```bash
npm run dev
```

Acesse no navegador: [http://localhost:5173](http://localhost:5173)

### 🏗️ Gerar build para produção

```bash
npm run build
```

---

## ✅ Requisitos Recomendados

- [VS Code](https://code.visualstudio.com/)
- Extensão: [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
- Desativar a extensão Vetur se estiver ativa

---

## 📂 Organização do Projeto

- `src/components` → Componentes reutilizáveis (ex: DetalhesProduto, CarrinhoComponent)
- `src/assets` → Imagens e estilos
- `App.vue` → Estrutura principal do app

---

## 📦 API Utilizada

As receitas são obtidas da [DummyJSON Recipes API](https://dummyjson.com/recipes). Os dados são organizados por tipo de cozinha (`cuisine`) e exibidos dinamicamente.

---

## 🤝 Contribuição

Este projeto é educacional, mas sugestões, melhorias ou issues são sempre bem-vindas!

---