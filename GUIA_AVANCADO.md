# 🎨 GUIA AVANÇADO DE CUSTOMIZAÇÃO

## 1. Adicionar Novos Pratos em Massa

```javascript
// src/data/menu.js

// Array de pratos a adicionar
const novoPratos = [
  {
    id: 21,
    name: "Strogonoff Premium",
    description: "Strogonoff de carne premium com cogumelos, creme de leite e arroz cremoso",
    price: 75.90,
    category: "Pratos Principais",
    image: "https://images.unsplash.com/..."
  },
  // Adicione mais...
];

// Adicionar ao array existente
export const menuData = {
  mainCourses: [...menuData.mainCourses, ...novoPratos],
  // ...
};
```

---

## 2. Customizar Cores do Site

### Opção A: Alterar Palette Completa
```javascript
// tailwind.config.js

export default {
  theme: {
    extend: {
      colors: {
        primary: {
          dark: '#0a0a0a',      // Preto
          light: '#1a1a1a',     // Cinza escuro
        },
        accent: {
          gold: '#d4af37',      // Dourado
          orange: '#ff8c42',    // Laranja
          light: '#ffa500',     // Laranja claro
        },
      },
    },
  },
}
```

### Opção B: Cores Específicas por Elemento
```css
/* src/styles/global.css */

.btn-primary {
  @apply px-8 py-3 bg-accent-gold text-primary-dark;
  background: linear-gradient(135deg, #d4af37 0%, #ffa500 100%);
}
```

---

## 3. Adicionar Nova Página

### Passo 1: Criar o componente
```javascript
// src/pages/Reservas.jsx

import React from 'react';
import { motion } from 'framer-motion';

export const Reservas = () => {
  return (
    <section id="reservas" className="py-20 bg-primary-dark">
      <div className="max-w-7xl mx-auto px-4">
        <motion.h1
          initial={{ opacity: 0 }}
          whileInView={{ opacity: 1 }}
          className="text-5xl font-serif font-bold text-accent-gold"
        >
          Fazer Reserva
        </motion.h1>
        {/* Conteúdo */}
      </div>
    </section>
  );
};

export default Reservas;
```

### Passo 2: Importar em App.jsx
```javascript
// src/App.jsx

import Reservas from './pages/Reservas';

export const App = () => {
  return (
    <main>
      <Home />
      <Menu />
      <Reservas />  {/* Nova página */}
      <About />
      <Contact />
    </main>
  );
};
```

### Passo 3: Adicionar ao Navbar
```javascript
// src/components/Navbar.jsx

const navItems = [
  { label: 'Home', id: 'home' },
  { label: 'Cardápio', id: 'menu' },
  { label: 'Reservas', id: 'reservas' },  // Nova
  { label: 'Sobre', id: 'about' },
  { label: 'Contato', id: 'contact' },
];
```

---

## 4. Integrar Formulário de Contato Real

### Opção 1: FormSubmit.co (Gratuito)
```javascript
// src/pages/Contact.jsx

const handleSubmit = (e) => {
  e.preventDefault();
  
  const form = e.target;
  form.action = "https://formsubmit.co/seu@email.com";
  form.submit();
};

// No form:
<form onSubmit={handleSubmit} method="POST">
  <input type="email" name="email" required />
  {/* ... */}
</form>
```

### Opção 2: Emailjs (Recomendado)
```bash
npm install @emailjs/browser
```

```javascript
import emailjs from '@emailjs/browser';

const handleSubmit = async (e) => {
  e.preventDefault();
  
  await emailjs.sendForm(
    'service_id',
    'template_id',
    e.target,
    'public_key'
  );
};
```

---

## 5. Adicionar Sistema de Categorias Dinâmicas

```javascript
// src/data/menu.js

export const categories = [
  { id: 'main', name: 'Pratos Principais', icon: '🥩' },
  { id: 'burger', name: 'Hambúrgueres', icon: '🍔' },
  { id: 'portions', name: 'Porções', icon: '🍟' },
  { id: 'drinks', name: 'Bebidas', icon: '🍷' },
  { id: 'desserts', name: 'Sobremesas', icon: '🍰' },
];

// Componente dinâmico:
{categories.map(cat => (
  <MenuSection
    key={cat.id}
    title={cat.name}
    icon={cat.icon}
    dishes={menuData[`${cat.id}Courses`]}
  />
))}
```

---

## 6. Adicionar Google Analytics

```html
<!-- index.html -->

<head>
  <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-XXXXXXX');
  </script>
</head>
```

---

## 7. Adicionar Notificações de Pedido

```javascript
// src/hooks/useNotification.js

import { useState } from 'react';

export const useNotification = () => {
  const [notification, setNotification] = useState(null);

  const showNotification = (message, type = 'success') => {
    setNotification({ message, type });
    setTimeout(() => setNotification(null), 3000);
  };

  return { notification, showNotification };
};

// Usar:
const { showNotification } = useNotification();
const handleOrder = () => {
  showNotification('Pedido enviado com sucesso!', 'success');
};
```

---

## 8. Adicionar Carrossel de Imagens

```bash
npm install swiper
```

```javascript
// src/components/ImageCarousel.jsx

import { Swiper, SwiperSlide } from 'swiper/react';
import 'swiper/css';

export const ImageCarousel = ({ images }) => {
  return (
    <Swiper slidesPerView={1} autoplay>
      {images.map((img, idx) => (
        <SwiperSlide key={idx}>
          <img src={img} alt="Imagem" />
        </SwiperSlide>
      ))}
    </Swiper>
  );
};
```

---

## 9. Otimizar Imagens

```javascript
// Usar Cloudinary para otimização automática
const optimizeImage = (url, width = 500, height = 500) => {
  return `https://res.cloudinary.com/seu-cloud/image/fetch/w_${width},h_${height},c_fill,f_auto,q_auto/${url}`;
};

// Usar:
<img src={optimizeImage(dish.image, 500, 500)} />
```

---

## 10. Dark/Light Mode

```javascript
// src/hooks/useTheme.js

import { useState, useEffect } from 'react';

export const useTheme = () => {
  const [theme, setTheme] = useState('dark');

  const toggleTheme = () => {
    const newTheme = theme === 'dark' ? 'light' : 'dark';
    setTheme(newTheme);
    document.documentElement.setAttribute('data-theme', newTheme);
  };

  return { theme, toggleTheme };
};
```

---

## 11. Adicionar Busca no Cardápio

```javascript
// src/hooks/useSearch.js

import { useState, useMemo } from 'react';

export const useSearch = (dishes) => {
  const [search, setSearch] = useState('');

  const results = useMemo(() => {
    return dishes.filter(dish =>
      dish.name.toLowerCase().includes(search.toLowerCase()) ||
      dish.description.toLowerCase().includes(search.toLowerCase())
    );
  }, [search, dishes]);

  return { search, setSearch, results };
};

// Componente:
const { search, setSearch, results } = useSearch(menuData.mainCourses);

<input
  value={search}
  onChange={(e) => setSearch(e.target.value)}
  placeholder="Buscar pratos..."
/>

{results.map(dish => <DishCard key={dish.id} dish={dish} />)}
```

---

## 12. Sistema de Filtros Avançado

```javascript
// src/components/MenuFilter.jsx

import { motion } from 'framer-motion';
import { useState } from 'react';

export const MenuFilter = ({ categories, onFilter }) => {
  const [selected, setSelected] = useState('all');

  const handleFilter = (category) => {
    setSelected(category);
    onFilter(category);
  };

  return (
    <div className="flex gap-4 justify-center flex-wrap mb-12">
      <motion.button
        onClick={() => handleFilter('all')}
        className={`px-6 py-2 rounded-lg transition-all ${
          selected === 'all'
            ? 'bg-accent-gold text-primary-dark'
            : 'border-2 border-accent-gold text-accent-gold'
        }`}
      >
        Todos
      </motion.button>

      {categories.map(cat => (
        <motion.button
          key={cat.id}
          onClick={() => handleFilter(cat.id)}
          className={`px-6 py-2 rounded-lg transition-all ${
            selected === cat.id
              ? 'bg-accent-gold text-primary-dark'
              : 'border-2 border-accent-gold text-accent-gold'
          }`}
        >
          {cat.name}
        </motion.button>
      ))}
    </div>
  );
};
```

---

## 13. Performance: Lazy Loading de Imagens

```javascript
// Usar imagen nativa do HTML
<img
  src={dish.image}
  loading="lazy"
  alt={dish.name}
/>

// Ou com biblioteca:
npm install react-lazyload

import LazyLoad from 'react-lazyload';

<LazyLoad height={200}>
  <img src={dish.image} alt={dish.name} />
</LazyLoad>
```

---

## 14. SEO: Meta Tags Dinâmicas

```javascript
// src/hooks/useSEO.js

import { useEffect } from 'react';

export const useSEO = ({ title, description, image, url }) => {
  useEffect(() => {
    document.title = title;
    document.querySelector('meta[name="description"]')?.setAttribute('content', description);
    document.querySelector('meta[property="og:title"]')?.setAttribute('content', title);
    document.querySelector('meta[property="og:description"]')?.setAttribute('content', description);
  }, [title, description, image, url]);
};

// Usar em cada página:
useSEO({
  title: 'Cardápio - Sabor da Vila',
  description: 'Confira nosso cardápio completo',
});
```

---

## 15. Sistema de Cupons/Promoções

```javascript
// src/data/menu.js

export const promotions = [
  {
    id: 1,
    code: 'BEMVINDO10',
    discount: 10,
    description: 'Desconto de 10% para primeiro pedido',
    active: true
  },
  // Mais cupons...
];

// Componente:
const validateCoupon = (code) => {
  return promotions.find(p => p.code === code && p.active);
};
```

---

## 📋 Checklist de Customização Avançada

- [ ] Adicionar mais pratos
- [ ] Integrar formulário real
- [ ] Setup Google Analytics
- [ ] Otimizar imagens
- [ ] Adicionar busca
- [ ] Sistema de filtros
- [ ] Cupons de promoção
- [ ] Dark mode (opcional)
- [ ] Notificações
- [ ] SEO meta tags

---

## 🚀 Dicas Finais de Performance

```javascript
// Lazy load componentes
const Menu = React.lazy(() => import('./pages/Menu'));

// Suspense fallback
<Suspense fallback={<LoadingSpinner />}>
  <Menu />
</Suspense>

// Memoizar componentes pesados
const MenuSection = React.memo(({ dishes }) => {
  return <div>{dishes.map(...)}</div>;
});
```

---

**Continue customizando e criando! 🎨✨**
