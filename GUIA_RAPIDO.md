# 🚀 GUIA RÁPIDO - Sabor da Vila Website

## ⚡ Começar em 3 Passos

### 1️⃣ Instalar Dependências
```bash
cd sabor-da-vila
npm install
```

### 2️⃣ Iniciar o Servidor
```bash
npm run dev
```

### 3️⃣ Acessar no Navegador
```
http://localhost:5173
```

---

## 📋 O Que Está Incluído

### ✅ Páginas Completas
- **Home** - Banner hero profissional
- **Cardápio** - 5 categorias com 20+ pratos
- **Sobre** - História, valores e equipe
- **Contato** - Formulário + mapa + horários

### ✅ Componentes Reutilizáveis
- Navbar responsiva com menu mobile
- Card de pratos com imagem e preço
- Botão flutuante WhatsApp
- Footer profissional
- Seções de categoria do menu

### ✅ Funcionalidades
- ✨ Animações suaves com Framer Motion
- 📱 100% responsivo (mobile + desktop)
- 🟢 Integração WhatsApp automática
- 🎨 Design escuro premium com dourado/laranja
- ⚡ Performance otimizada

---

## 🎨 Personalizar para Seu Restaurante

### Passo 1: Editar Informações Básicas
Arquivo: `src/data/menu.js`

```javascript
export const restaurantInfo = {
  name: "Seu Restaurante",
  tagline: "Sua frase especial",
  phone: "+55 (11) XXXXX-XXXX",
  whatsapp: "55119XXXXXXX",
  address: "Seu endereço aqui",
  hours: {
    weekday: "11:00 - 23:00",
    weekend: "12:00 - 00:00"
  }
};
```

### Passo 2: Adicionar Seus Pratos
Edite as arrays no mesmo arquivo:
```javascript
{
  id: 1,
  name: "Nome do Prato",
  description: "Descrição detalhada",
  price: 49.90,
  category: "Pratos Principais",
  image: "https://link-da-imagem.com/img.jpg"
}
```

### Passo 3: Atualizar Imagens
- Substitua URLs das imagens Unsplash pelas suas próprias
- Use serviço como: Cloudinary, AWS S3, ou hospedagem própria

### Passo 4: Customizar Cores (Opcional)
Arquivo: `tailwind.config.js`
```javascript
colors: {
  accent: {
    gold: '#d4af37',      // Mude para sua cor
    orange: '#ff8c42',    // Mude para sua cor
  }
}
```

---

## 📦 Estrutura de Pastas Explicada

```
src/
├── components/        # Botões, cards, navbar, footer
├── pages/            # Home, Menu, About, Contact
├── data/             # Cardápio em JSON
├── hooks/            # Lógica reutilizável (WhatsApp)
├── styles/           # CSS global
├── App.jsx           # Componente raiz
└── main.jsx          # Entrada da app
```

---

## 🌍 Deploy (Publicar na Internet)

### Opção 1: Netlify (Recomendado - Grátis)
1. Faça `npm run build`
2. Vá para https://netlify.com
3. Faça upload da pasta `dist`
4. Pronto! Site online em minutos

### Opção 2: Vercel
1. Conecte seu GitHub
2. Vercel detecta Vite automaticamente
3. Deploy automático a cada push

### Opção 3: GitHub Pages
1. Configure `vite.config.js`
2. Faça push para GitHub
3. Ative GitHub Pages nas configurações

---

## 🔗 Links do WhatsApp Automático

O site já vem com integração WhatsApp pronta:
- ✅ Botão flutuante no canto inferior direito
- ✅ Botão "Pedir" em cada prato
- ✅ Link no navbar mobile
- ✅ Mensagem pré-formatada automática

Basta atualizar o número em `src/data/menu.js`!

---

## 📱 Testar Responsividade

### No Chrome/Firefox:
1. Abra `F12` (DevTools)
2. Clique no ícone de telefone/tablet
3. Teste diferentes tamanhos

O site é 100% responsivo:
- ✅ Mobile (360px - 768px)
- ✅ Tablet (768px - 1024px)
- ✅ Desktop (1024px+)

---

## 🎬 Animações e Efeitos

Site inclui:
- Fade-in automático ao scroll
- Hover effects nos cards
- Scroll suave
- Animações de entrada
- Transições elegantes

Powered by Framer Motion ✨

---

## 🛠️ Comandos Úteis

```bash
# Desenvolvimento
npm run dev          # Inicia servidor local

# Produção
npm run build        # Cria versão otimizada
npm run preview      # Visualiza build

# Verificar código
npm run lint         # (Opcional) Verifica erros
```

---

## 📋 Checklist de Customização

- [ ] Alterar nome do restaurante
- [ ] Atualizar número de WhatsApp
- [ ] Substituir pratos do cardápio
- [ ] Adicionar suas fotos/imagens
- [ ] Atualizar endereço e horários
- [ ] Mudar cores (se desejar)
- [ ] Testar no celular
- [ ] Fazer deploy online
- [ ] Compartilhar link com clientes

---

## ❓ Perguntas Frequentes

**P: Como adiciono mais pratos?**
R: Edite `src/data/menu.js` e adicione novo objeto à array

**P: Posso mudar as cores?**
R: Sim! Edite `tailwind.config.js` na seção de cores

**P: Como mudo as imagens?**
R: Substitua as URLs das imagens pelo Unsplash pelas suas próprias

**P: O formulário de contato funciona?**
R: Não (requer backend). Atualize com sua solução preferred

**P: Posso usar meu próprio domínio?**
R: Sim, ao fazer deploy em Netlify/Vercel, você conecta seu domínio

---

## 🚀 Próximos Passos

1. **Customize o site** com suas informações
2. **Teste em mobile** para garantir responsividade
3. **Faça deploy** em Netlify ou Vercel
4. **Compartilhe o link** com seus clientes
5. **Monitore com Google Analytics** (opcional)

---

## 💡 Dicas Profissionais

✅ Use imagens de alta qualidade (mínimo 1000px)
✅ Mantenha descrições dos pratos atrativas
✅ Atualize preços regularmente
✅ Teste links WhatsApp antes de publicar
✅ Use favicon customizado (seu logo)
✅ Configure Google Analytics para métricas

---

## 📞 Suporte Rápido

**Problema: npm install não funciona**
```bash
npm cache clean --force
npm install
```

**Problema: Porta 5173 já em uso**
```bash
# Use outra porta
npm run dev -- --port 3000
```

**Problema: Imagens não carregam**
- Verifique se URLs estão corretas
- Teste com imagens do Unsplash primeiro
- Verifique permissões CORS

---

## 📊 Estrutura Profissional Incluída

✅ Código limpo nível sênior
✅ Componentes reutilizáveis
✅ Sem código duplicado
✅ Performance otimizada
✅ Mobile-first design
✅ Acessibilidade (a11y)
✅ SEO friendly
✅ Pronto para vendas comerciais

---

## 🎓 Aprender Mais

- **React**: https://react.dev
- **TailwindCSS**: https://tailwindcss.com
- **Vite**: https://vitejs.dev
- **Framer Motion**: https://www.framer.com/motion/

---

**Desenvolvido com ❤️ para sua loja de alimentos**

Aproveite o site! 🍽️✨
