<script>
  import { onMount } from 'svelte';

  let navbar;
  let navInner;
  let menuOpen = false;
  let navbarHeight = 80;

  let contactForm;
  let formSuccess;
  let submitBtn;
  let btnText;
  let btnLoading;
  let scrollTick = false;

  const navLinks = [
    { href: '#confidentiality', title: 'Конфиденциальность' },
    { href: '#formats', title: 'Форматы' },
    { href: '#cases', title: 'Кейсы' },
    { href: '#faq', title: 'FAQ' }
  ];

  const formatCards = [
    {
      title: 'Корпоративные события',
      text: 'Закрытые встречи акционеров, стратегические сессии, юбилеи компаний.',
      image: 'https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/173402889-7605-45bb-84b9-6a7f27beb1fc.png'
    },
    {
      title: 'Частные мероприятия',
      text: 'Свадьбы, дни рождения, семейные торжества в узком кругу.',
      image: 'https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/19ff57788-fc26-44ea-9dfb-2b5c41a5268b.png'
    },
    {
      title: 'VIP / Closed Events',
      text: 'Вечеринки для избранных, концерты private gig, закрытые показы.',
      image: 'https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1032f2de6-7c8d-4e15-af56-47e8795cde9a.png'
    },
    {
      title: 'Под ключ',
      text: 'Полная организация логистики, охраны и контента без вашего участия.',
      image: 'https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1a0a26d6f-d974-45c8-a93c-363ba110453d.png'
    }
  ];

  const cases = [
    {
      type: 'Корпоративный сектор',
      title: 'Саммит топ-менеджмента IT-гиганта',
      points: ['Локация: частная резиденция', '40 персон уровня C-Level', 'Полное подавление сигналов связи'],
      quote: 'Идеальная тишина и безопасность.'
    },
    {
      type: 'Private Party',
      title: 'Юбилей владельца холдинга',
      points: ['Загородный клуб, полный выкуп', 'Вылет артиста инкогнито', 'Zero-photo policy для прессы'],
      quote: 'Гости чувствовали себя абсолютно свободно.'
    },
    {
      type: 'Special Event',
      title: 'Закрытый показ коллекции',
      points: ['Историческое здание в центре', 'Контроль съёмки на входе', 'Персональные ассистенты для VIP'],
      quote: 'Высокий уровень сервиса и дискретности.'
    }
  ];

  const faqs = [
    ['Подписываете ли вы NDA?', 'Да, это стандарт нашей работы. Подписываем двустороннее соглашение до старта проекта.'],
    ['Публикуете ли вы материалы в портфолио?', 'Только с письменного разрешения клиента. Чаще используем слепые кейсы или не публикуем вовсе.'],
    ['Как контролируется фото и видео?', 'Сбор телефонов на входе, проверенные фотографы и удаление метаданных.'],
    ['Можно ли провести событие полностью без публичности?', 'Да. Используем частные владения, скрытую логистику и звукоизоляцию.'],
    ['Работаете ли вы с VIP-гостями?', 'Да. Отдельные входы, личная охрана и соблюдение приватности.']
  ];

  function scrollToContact() {
    const contactSection = document.getElementById('contact');
    const offset = navbarHeight + 20;
    const elementPosition = contactSection.getBoundingClientRect().top;
    window.scrollTo({ top: elementPosition + window.pageYOffset - offset, behavior: 'smooth' });
  }

  onMount(() => {
    const handleNavScroll = () => {
      const currentScroll = window.pageYOffset;
      if (currentScroll > 60) {
        navbar.classList.add('bg-dark-nav');
        navInner.classList.remove('h-20');
        navInner.classList.add('h-16');
        navbarHeight = 64;
      } else {
        navbar.classList.remove('bg-dark-nav');
        navInner.classList.add('h-20');
        navInner.classList.remove('h-16');
        navbarHeight = 80;
      }
    };

    const onScroll = () => {
      if (scrollTick) return;
      scrollTick = true;
      requestAnimationFrame(() => {
        handleNavScroll();
        scrollTick = false;
      });
    };

    window.addEventListener('scroll', onScroll, { passive: true });

    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          revealObserver.unobserve(entry.target);
        }
      });
    }, { rootMargin: '0px 0px -60px 0px', threshold: 0.1 });

    document.querySelectorAll('.reveal').forEach((el) => revealObserver.observe(el));

    const counterObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return;
        const counter = entry.target;
        const target = parseInt(counter.dataset.target);
        const suffix = counter.dataset.suffix || '';
        const duration = 2000;
        const startTime = performance.now();

        const updateCounter = (currentTime) => {
          const progress = Math.min((currentTime - startTime) / duration, 1);
          const eased = 1 - Math.pow(1 - progress, 3);
          counter.textContent = Math.round(eased * target) + suffix;
          if (progress < 1) requestAnimationFrame(updateCounter);
        };

        requestAnimationFrame(updateCounter);
        counterObserver.unobserve(counter);
      });
    }, { threshold: 0.5 });

    document.querySelectorAll('.counter-value[data-target]').forEach((el) => counterObserver.observe(el));

    const onEsc = (e) => e.key === 'Escape' && menuOpen && (menuOpen = false);
    document.addEventListener('keydown', onEsc);

    const onSubmit = async (e) => {
      e.preventDefault();
      document.querySelectorAll('.error-message').forEach((msg) => msg.classList.add('hidden'));
      document.querySelectorAll('.form-input').forEach((input) => input.classList.remove('border-red-400'));

      const nameInput = document.getElementById('name');
      const contactInput = document.getElementById('contact-info');
      let isValid = true;

      if (!nameInput.value.trim()) {
        nameInput.classList.add('border-red-400');
        nameInput.parentElement.querySelector('.error-message').classList.remove('hidden');
        isValid = false;
      }
      if (!contactInput.value.trim()) {
        contactInput.classList.add('border-red-400');
        contactInput.parentElement.querySelector('.error-message').classList.remove('hidden');
        isValid = false;
      }
      if (!isValid) return;

      submitBtn.disabled = true;
      btnText.classList.add('hidden');
      btnLoading.classList.remove('hidden');
      await new Promise((resolve) => setTimeout(resolve, 1000));

      contactForm.classList.add('hidden');
      formSuccess.classList.remove('hidden');

      setTimeout(() => {
        contactForm.classList.remove('hidden');
        formSuccess.classList.add('hidden');
        contactForm.reset();
        submitBtn.disabled = false;
        btnText.classList.remove('hidden');
        btnLoading.classList.add('hidden');
      }, 4000);
    };

    contactForm?.addEventListener('submit', onSubmit);
    document.querySelectorAll('.form-input').forEach((input) => {
      input.addEventListener('input', () => {
        input.classList.remove('border-red-400');
        input.parentElement.querySelector('.error-message')?.classList.add('hidden');
      });
    });

    return () => {
      window.removeEventListener('scroll', onScroll);
      document.removeEventListener('keydown', onEsc);
      revealObserver.disconnect();
      counterObserver.disconnect();
      contactForm?.removeEventListener('submit', onSubmit);
      document.body.style.overflow = '';
    };
  });
</script>

<svelte:head>
  <title>Closed Events | Закрытые мероприятия</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/300.css" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/400.css" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/600.css" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/400-italic.css" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/300.css" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/400.css" />
  <script src="https://cdn.tailwindcss.com"></script>
</svelte:head>

<a href="#main-content" class="sr-only focus-link">Перейти к основному контенту</a>
<nav bind:this={navbar} class="fixed w-full z-50 top-0 transition-all duration-400">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div bind:this={navInner} class="flex items-center justify-between h-20 transition-all duration-400">
      <a href="#main-content" class="text-xl sm:text-2xl font-serif font-semibold tracking-[0.2em] text-white uppercase">Closed<span class="text-gold">.</span>Events</a>
      <div class="hidden lg:flex items-center space-x-10">
        {#each navLinks as link}
          <a href={link.href} class="text-xs uppercase tracking-[0.2em] text-gray-400 hover:text-gold">{link.title}</a>
        {/each}
      </div>
      <button class="hidden lg:block border border-white/20 px-7 py-2.5 text-[11px] uppercase tracking-[0.2em] text-white" on:click={scrollToContact}>Обсудить проект</button>
      <button
        class="lg:hidden text-white"
        on:click={() => {
          menuOpen = !menuOpen;
          document.body.style.overflow = menuOpen ? 'hidden' : '';
        }}
        aria-label="Открыть меню"
        aria-expanded={menuOpen}
      >
        <span class="w-6 h-6">{menuOpen ? "✕" : "☰"}</span>
      </button>
    </div>
  </div>
  <div class="mobile-menu fixed inset-0 z-40 bg-black/95 backdrop-blur-xl lg:hidden" class:open={menuOpen}>
    <div class="flex flex-col items-center justify-center h-full space-y-8">
      {#each navLinks as link}
        <a href={link.href} class="text-2xl font-serif text-white hover:text-gold" on:click={() => { menuOpen = false; document.body.style.overflow = ''; }}>{link.title}</a>
      {/each}
      <button on:click={() => { menuOpen = false; document.body.style.overflow = ''; scrollToContact(); }} class="bg-gold text-black px-10 py-3 text-sm uppercase tracking-[0.2em]">Обсудить проект</button>
    </div>
  </div>
</nav>

<main id="main-content" class="font-sans bg-dark text-gray-200">
  <header class="relative h-screen min-h-[700px] flex items-center justify-center overflow-hidden">
    <img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1ff567042-2eec-40d7-b49c-a8504b6a957a.png" class="hero-image absolute inset-0 w-full h-full object-cover" alt="hero" />
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-black/30 to-black"></div>
    <div class="relative z-10 max-w-4xl mx-auto px-6 text-center reveal">
      <p class="text-gold uppercase tracking-[0.35em] text-xs mb-8">Private & Confidential</p>
      <h1 class="font-serif text-5xl md:text-7xl text-white leading-[1.05] mb-6">Закрытые мероприятия <span class="block italic text-gray-300">без огласки</span></h1>
      <p class="text-gray-400 text-lg max-w-2xl mx-auto mb-10">Организация событий премиум-класса, где ваша приватность является главным активом.</p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center"><button on:click={scrollToContact} class="bg-gold text-black px-10 py-4 uppercase tracking-[0.2em] text-xs">Обсудить мероприятие</button><button class="border border-white/25 text-white px-10 py-4 uppercase tracking-[0.2em] text-xs flex items-center gap-2"><span class="w-4 h-4">🔒</span>Запросить NDA</button></div>
    </div>
  </header>

  <section id="confidentiality" class="py-24 bg-charcoal">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid lg:grid-cols-2 gap-16 items-center">
      <div class="reveal">
        <h2 class="font-serif text-4xl md:text-5xl text-white mb-8">Конфиденциальность <span class="text-gold italic block">в основе всего</span></h2>
        <p class="text-gray-400 mb-10 text-lg">Мы встраиваем протоколы безопасности в каждый этап подготовки и проведения мероприятия.</p>
        <div class="space-y-6">
          <div class="flex gap-4"><span class="w-5 h-5 text-gold mt-1">✍️</span><div><h4 class="text-white">Жесткий NDA</h4><p class="text-gray-500">С каждым членом команды и подрядчиком.</p></div></div>
          <div class="flex gap-4"><span class="w-5 h-5 text-gold mt-1">📵</span><div><h4 class="text-white">Контроль съёмки</h4><p class="text-gray-500">Запрет на смартфоны и контроль публикаций.</p></div></div>
          <div class="flex gap-4"><span class="w-5 h-5 text-gold mt-1">✅</span><div><h4 class="text-white">Доступ по спискам</h4><p class="text-gray-500">Фейс-контроль и проверка гостей на входе.</p></div></div>
        </div>
      </div>
      <div class="reveal"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1c90a0976-f4c6-45f1-a704-4a8900753e1e.png" alt="confidential" class="w-full h-[500px] object-cover" /></div>
    </div>
  </section>

  <section id="formats" class="py-24 bg-dark">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16 reveal"><span class="text-gold uppercase tracking-[0.3em] text-xs">Экспертиза</span><h2 class="font-serif text-4xl md:text-5xl mt-4 text-white">Форматы мероприятий</h2></div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        {#each formatCards as card}
          <article class="group relative h-[420px] overflow-hidden reveal">
            <img src={card.image} alt={card.title} class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
            <div class="absolute inset-0 bg-gradient-to-t from-black via-black/60 to-black/20"></div>
            <div class="absolute bottom-0 left-0 right-0 p-8"><h3 class="font-serif text-2xl text-white mb-2">{card.title}</h3><p class="text-gray-400 text-sm">{card.text}</p></div>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <section id="cases" class="py-24 bg-charcoal border-y border-white/5">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="mb-16 reveal"><span class="text-gold uppercase tracking-[0.3em] text-xs">Опыт</span><h2 class="font-serif text-4xl md:text-5xl mt-4 text-white">Закрытые кейсы</h2></div>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        {#each cases as c}
          <article class="bg-slate p-8 border border-white/5 reveal">
            <div class="text-xs text-gray-500 mb-5 uppercase tracking-[0.2em]">{c.type}</div>
            <h3 class="font-serif text-2xl text-white mb-5">{c.title}</h3>
            <ul class="space-y-3 text-sm text-gray-400 mb-6">
              {#each c.points as p}<li class="flex gap-2"><span class="w-4 h-4 text-gold mt-0.5">✓</span><span>{p}</span></li>{/each}
            </ul>
            <p class="text-white/90 italic">“{c.quote}”</p>
          </article>
        {/each}
      </div>
    </div>
  </section>

  <section class="py-24 bg-dark">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid lg:grid-cols-2 gap-16 items-center">
      <div class="reveal"><h2 class="font-serif text-4xl md:text-5xl text-white mb-8">Всё остаётся <span class="text-gold block">внутри</span></h2><p class="text-gray-400 text-lg mb-10">Что происходит на мероприятии, остается только в памяти участников.</p></div>
      <div class="reveal flex items-center justify-center"><div class="w-64 h-64 rounded-full border border-gold/30 flex items-center justify-center"><span class="w-14 h-14 text-gold">🛡️</span></div></div>
    </div>
  </section>

  <section class="py-16 sm:py-20 bg-gold text-black">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-8 text-center">
        <div><div class="text-4xl font-serif font-bold mb-2 counter-value" data-target="50" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Мероприятий</div></div>
        <div><div class="text-4xl font-serif font-bold mb-2 counter-value" data-target="7" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Лет опыта</div></div>
        <div><div class="text-4xl font-serif font-bold mb-2">100%</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">NDA проектов</div></div>
        <div><div class="text-4xl font-serif font-bold mb-2 counter-value" data-target="20" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Городов</div></div>
        <div class="col-span-2 sm:col-span-1"><div class="text-4xl font-serif font-bold mb-2 counter-value" data-target="85" data-suffix="%">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Повторных клиентов</div></div>
      </div>
    </div>
  </section>

  <section class="py-24 bg-charcoal">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16 reveal"><h2 class="font-serif text-4xl md:text-5xl text-white mb-5">Работа со статусными гостями</h2><p class="text-gray-400 max-w-2xl mx-auto text-lg">Мы знаем специфику работы с публичными персонами, политиками и звёздами шоу-бизнеса.</p></div>
      <div class="grid lg:grid-cols-3 gap-6">
        <div class="lg:col-span-2 relative overflow-hidden"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/16d75ab75-af4f-40bb-8aec-d9bdf3a7418c.png" alt="vip" class="w-full h-[500px] object-cover" /></div>
        <div class="space-y-5"><div class="bg-slate p-6 border-l-2 border-gold"><h4 class="text-white font-serif text-xl mb-2">Инкогнито</h4><p class="text-gray-400 text-sm">Заселение в отель под вымышленными именами.</p></div><div class="bg-slate p-6 border-l-2 border-gold"><h4 class="text-white font-serif text-xl mb-2">Anti-Paparazzi</h4><p class="text-gray-400 text-sm">Блокировка несанкционированной съёмки.</p></div><div class="bg-slate p-6 border-l-2 border-gold"><h4 class="text-white font-serif text-xl mb-2">Личные райдеры</h4><p class="text-gray-400 text-sm">Точное соблюдение индивидуальных требований.</p></div></div>
      </div>
    </div>
  </section>

  <section class="py-24 bg-dark">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="font-serif text-4xl text-center text-white mb-16">Что говорят клиенты</h2>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div class="bg-charcoal p-8"><p class="text-gray-300 italic">«Единственное агентство, которое реально понимает значение слова секретность.»</p></div>
        <div class="bg-charcoal p-8"><p class="text-gray-300 italic">«Деликатность персонала на высшем уровне.»</p></div>
        <div class="bg-charcoal p-8"><p class="text-gray-300 italic">«Полный контроль над ситуацией.»</p></div>
      </div>
    </div>
  </section>

  <section id="faq" class="py-24 bg-charcoal border-t border-white/5">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="font-serif text-4xl text-center text-white mb-14 reveal">Важное перед стартом</h2>
      <div class="space-y-4 reveal">
        {#each faqs as row}
          <details class="group bg-slate border border-white/5">
            <summary class="flex justify-between items-center font-medium cursor-pointer list-none p-6 text-white"><span>{row[0]}</span><span class="w-5 h-5 text-gold">⌄</span></summary>
            <div class="px-6 pb-6 text-sm text-gray-400 border-t border-white/5 pt-4">{row[1]}</div>
          </details>
        {/each}
      </div>
    </div>
  </section>

  <section id="contact" class="py-24 bg-dark">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="glass-panel p-8 md:p-12 reveal">
        <div class="text-center mb-10"><h2 class="font-serif text-4xl text-white mb-4">Обсудим ваше мероприятие</h2><p class="text-gray-400">Оставьте заявку. Мы свяжемся через защищённый канал.</p></div>
        <form bind:this={contactForm} class="space-y-6" novalidate aria-label="Форма заявки на мероприятие">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
            <div><label for="name" class="text-xs uppercase tracking-[0.2em] text-gray-500">Имя *</label><input id="name" type="text" required autocomplete="name" class="form-input w-full bg-black/40 border border-white/10 p-4 text-white text-sm mt-2" /><p class="error-message text-red-400 text-[11px] hidden">Введите ваше имя</p></div>
            <div><label for="contact-info" class="text-xs uppercase tracking-[0.2em] text-gray-500">Телефон / Telegram *</label><input id="contact-info" type="text" required autocomplete="tel" class="form-input w-full bg-black/40 border border-white/10 p-4 text-white text-sm mt-2" /><p class="error-message text-red-400 text-[11px] hidden">Укажите способ связи</p></div>
          </div>
          <button bind:this={submitBtn} type="submit" class="w-full bg-gold text-black font-medium uppercase tracking-[0.2em] text-sm py-4 flex items-center justify-center gap-2"><span bind:this={btnText}>Отправить запрос</span><span bind:this={btnLoading} class="hidden"><svg class="animate-spin h-4 w-4" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" fill="none"></circle></svg></span></button>
        </form>
        <div bind:this={formSuccess} class="hidden text-center py-8"><span class="w-8 h-8 text-gold mx-auto mb-4">✓</span><h3 class="font-serif text-2xl text-white mb-3">Заявка отправлена</h3></div>
      </div>
    </div>
  </section>
</main>

<footer class="bg-black py-12 sm:py-16 border-t border-white/10">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-10">
    <div><a href="#main-content" class="text-2xl font-serif font-semibold tracking-[0.2em] text-white uppercase block mb-5">Closed<span class="text-gold">.</span>Events</a><p class="text-gray-500 text-sm">Организация закрытых мероприятий премиум-класса.</p></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Навигация</h4><ul class="space-y-3 text-sm text-gray-500">{#each navLinks as l}<li><a href={l.href}>{l.title}</a></li>{/each}</ul></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Услуги</h4><ul class="space-y-3 text-sm text-gray-500"><li>Корпоративные события</li><li>Частные вечеринки</li><li>VIP логистика</li><li>Охрана и NDA</li></ul></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Контакты</h4><ul class="space-y-3 text-sm text-gray-500"><li>+7 (999) 000-00-00</li><li>private@closed.events</li><li>Москва, Сити</li></ul></div>
  </div>
</footer>

<style>
  :global(*) { box-sizing: border-box; }
  :global(html) { scroll-behavior: smooth; scroll-padding-top: 80px; }
  :global(body) { margin: 0; background: #0a0a0a; color: #e5e5e5; overflow-x: hidden; }
  .text-gold { color: #d4af37; }
  .bg-dark { background: #0a0a0a; }
  .bg-charcoal { background: #121212; }
  .bg-slate { background: #1c1c1c; }
  .bg-gold { background: #d4af37; }
  .font-serif { font-family: 'Cormorant Garamond', Georgia, serif; }
  .font-sans { font-family: 'Manrope', -apple-system, sans-serif; }
  .mobile-menu { transform: translateX(100%); transition: transform .4s cubic-bezier(.16,1,.3,1); }
  .mobile-menu.open { transform: translateX(0); }
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity .8s cubic-bezier(.16,1,.3,1), transform .8s cubic-bezier(.16,1,.3,1); }
  :global(.reveal.is-visible) { opacity: 1; transform: translateY(0); }
  :global(.bg-dark-nav) { background: rgba(10,10,10,.95); backdrop-filter: blur(12px); box-shadow: 0 10px 20px rgba(0,0,0,.2); }
  :global(.h-20) { height: 5rem; }
  :global(.h-16) { height: 4rem; }
  .glass-panel { background: rgba(28, 28, 28, 0.65); backdrop-filter: blur(16px); border: 1px solid rgba(255, 255, 255, 0.06); }
  .form-input:focus { outline: 1px solid rgba(212,175,55,.4); border-color: #d4af37; }
  .focus-link:focus { position: fixed; top: 1rem; left: 1rem; z-index: 100; background: #d4af37; color: #000; padding: .5rem 1rem; }
  .w-4, .w-5, .w-6, .w-8, .w-14 { display:inline-flex; align-items:center; justify-content:center; }
</style>
