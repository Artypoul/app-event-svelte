<script>
  import { onMount } from 'svelte';

  let navbar;
  let navInner;
  let mobileMenu;
  let menuOpen = false;
  let navbarHeight = 80;
  let contactForm;
  let submitBtn;
  let formSuccess;

  const closeMobileMenu = () => {
    menuOpen = false;
    document.body.style.overflow = '';
  };

  const openMobileMenu = () => {
    menuOpen = true;
    document.body.style.overflow = 'hidden';
  };

  function scrollToContact() {
    const contactSection = document.getElementById('contact');
    if (!contactSection) return;
    const offset = navbarHeight + 20;
    const elementPosition = contactSection.getBoundingClientRect().top;
    const offsetPosition = elementPosition + window.pageYOffset - offset;

    window.scrollTo({ top: offsetPosition, behavior: 'smooth' });
  }

  onMount(() => {
    window.lucide?.createIcons();

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

    window.addEventListener('scroll', handleNavScroll, { passive: true });

    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          revealObserver.unobserve(entry.target);
        }
      });
    }, {
      rootMargin: '0px 0px -60px 0px',
      threshold: 0.1
    });

    document.querySelectorAll('.reveal').forEach((el) => revealObserver.observe(el));

    const counterObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const counter = entry.target;
          const target = parseInt(counter.dataset.target);
          const suffix = counter.dataset.suffix || '';
          const duration = 2000;
          const startTime = performance.now();

          function updateCounter(currentTime) {
            const elapsed = currentTime - startTime;
            const progress = Math.min(elapsed / duration, 1);
            const eased = 1 - Math.pow(1 - progress, 3);
            const current = Math.round(eased * target);

            counter.textContent = current + suffix;

            if (progress < 1) {
              requestAnimationFrame(updateCounter);
            }
          }

          requestAnimationFrame(updateCounter);
          counterObserver.unobserve(counter);
        }
      });
    }, { threshold: 0.5 });

    document.querySelectorAll('.counter-value[data-target]').forEach((el) => counterObserver.observe(el));

    const onEsc = (e) => {
      if (e.key === 'Escape' && menuOpen) {
        closeMobileMenu();
      }
    };

    document.addEventListener('keydown', onEsc);

    const onSubmit = async (e) => {
      e.preventDefault();

      document.querySelectorAll('.error-message').forEach((msg) => msg.classList.add('hidden'));
      document.querySelectorAll('.form-input').forEach((input) => input.classList.remove('border-red-400'));

      let isValid = true;
      const nameInput = document.getElementById('name');
      const contactInput = document.getElementById('contact-info');

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

      const btnText = submitBtn.querySelector('.btn-text');
      const btnLoading = submitBtn.querySelector('.btn-loading');
      submitBtn.disabled = true;
      btnText.classList.add('hidden');
      btnLoading.classList.remove('hidden');

      await new Promise((resolve) => setTimeout(resolve, 1500));

      contactForm.classList.add('hidden');
      formSuccess.classList.remove('hidden');
      window.lucide?.createIcons();

      setTimeout(() => {
        contactForm.classList.remove('hidden');
        formSuccess.classList.add('hidden');
        contactForm.reset();
        submitBtn.disabled = false;
        btnText.classList.remove('hidden');
        btnLoading.classList.add('hidden');
      }, 5000);
    };

    contactForm?.addEventListener('submit', onSubmit);

    return () => {
      window.removeEventListener('scroll', handleNavScroll);
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
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/300.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/400.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/600.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/cormorant-garamond@5.0.8/400-italic.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/200.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/300.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/400.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/manrope@5.0.20/500.css">
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
</svelte:head>

<a href="#main-content" class="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 focus:z-[100] focus:bg-gold focus:text-black focus:px-4 focus:py-2 focus:rounded-md">Перейти к основному контенту</a>

<nav bind:this={navbar} class="fixed w-full z-50 top-0 transition-all duration-400 ease-out" aria-label="Основная навигация">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div bind:this={navInner} class="flex items-center justify-between h-20 transition-all duration-400">
      <a href="#main-content" class="relative z-50 text-xl sm:text-2xl font-serif font-semibold tracking-[0.2em] text-white uppercase flex-shrink-0">Closed<span class="text-gold">.</span>Events</a>

      <div class="hidden lg:flex items-center space-x-10">
        <a href="#confidentiality" class="text-xs uppercase tracking-[0.2em] text-gray-400 hover:text-gold">Конфиденциальность</a>
        <a href="#formats" class="text-xs uppercase tracking-[0.2em] text-gray-400 hover:text-gold">Форматы</a>
        <a href="#cases" class="text-xs uppercase tracking-[0.2em] text-gray-400 hover:text-gold">Кейсы</a>
        <a href="#faq" class="text-xs uppercase tracking-[0.2em] text-gray-400 hover:text-gold">FAQ</a>
      </div>

      <div class="hidden lg:block">
        <button on:click={scrollToContact} class="border border-white/20 px-7 py-2.5 text-[11px] uppercase tracking-[0.2em] text-white hover:bg-gold hover:border-gold hover:text-black transition-all duration-300">Обсудить проект</button>
      </div>

      <button class="lg:hidden relative z-50 w-10 h-10 flex items-center justify-center" on:click={() => (menuOpen ? closeMobileMenu() : openMobileMenu())} aria-label={menuOpen ? 'Закрыть меню' : 'Открыть меню'} aria-expanded={menuOpen}>
        <div class="flex flex-col items-center justify-center w-6 h-5 relative">
          <span class="nav-line absolute w-full h-px bg-white transition-all duration-300" class:line-1-open={menuOpen} style="top:0"></span>
          <span class="nav-line absolute w-full h-px bg-white transition-all duration-300" class:line-2-open={menuOpen} style="top:50%;transform:translateY(-50%)"></span>
          <span class="nav-line absolute w-full h-px bg-white transition-all duration-300" class:line-3-open={menuOpen} style="bottom:0"></span>
        </div>
      </button>
    </div>
  </div>

  <div bind:this={mobileMenu} class="mobile-menu fixed inset-0 z-40 bg-dark/98 backdrop-blur-xl lg:hidden" class:open={menuOpen}>
    <div class="flex flex-col items-center justify-center h-full space-y-8">
      <a href="#confidentiality" class="text-2xl font-serif text-white hover:text-gold" on:click={closeMobileMenu}>Конфиденциальность</a>
      <a href="#formats" class="text-2xl font-serif text-white hover:text-gold" on:click={closeMobileMenu}>Форматы</a>
      <a href="#cases" class="text-2xl font-serif text-white hover:text-gold" on:click={closeMobileMenu}>Кейсы</a>
      <a href="#faq" class="text-2xl font-serif text-white hover:text-gold" on:click={closeMobileMenu}>FAQ</a>
      <button on:click={() => { closeMobileMenu(); scrollToContact(); }} class="bg-gold text-black px-10 py-3 text-sm uppercase tracking-[0.2em] font-medium">Обсудить проект</button>
    </div>
  </div>
</nav>

<main id="main-content" class="font-sans antialiased">
  <header class="relative h-screen min-h-[700px] flex items-center justify-center overflow-hidden">
    <div class="absolute inset-0 z-0">
      <img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1ff567042-2eec-40d7-b49c-a8504b6a957a.png" alt="Атмосфера закрытого мероприятия" class="hero-image w-full h-full object-cover scale-110">
      <div class="absolute inset-0 bg-gradient-to-b from-dark/70 via-dark/40 to-dark"></div>
    </div>

    <div class="relative z-10 max-w-4xl mx-auto px-4 sm:px-6 text-center reveal">
      <p class="text-gold uppercase tracking-[0.35em] text-xs mb-8 font-medium">Private & Confidential</p>
      <h1 class="font-serif text-[2.5rem] sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl leading-[1.05] mb-8 text-white">Закрытые мероприятия <span class="block italic text-gray-300/80 text-[2rem] sm:text-4xl md:text-5xl lg:text-6xl xl:text-7xl mt-2">без огласки</span></h1>
      <p class="text-gray-400 text-base sm:text-lg md:text-xl max-w-2xl mx-auto mb-10">Организация событий премиум-класса, где ваша приватность является главным активом.</p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center items-center">
        <button on:click={scrollToContact} class="w-full sm:w-auto bg-gold text-black px-10 py-4 uppercase tracking-[0.2em] text-xs sm:text-sm font-medium">Обсудить мероприятие</button>
        <button class="w-full sm:w-auto border border-white/25 text-white px-10 py-4 uppercase tracking-[0.2em] text-xs sm:text-sm font-medium flex items-center justify-center gap-2"><i data-lucide="lock" class="w-4 h-4"></i>Запросить NDA</button>
      </div>
    </div>
  </header>

  <section id="confidentiality" class="py-20 sm:py-24 lg:py-28 bg-charcoal">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 lg:grid-cols-2 gap-12 lg:gap-16 items-center">
      <div class="reveal">
        <h2 class="font-serif text-3xl sm:text-4xl md:text-5xl mb-8 text-white">Конфиденциальность <span class="text-gold italic block">в основе всего</span></h2>
        <p class="text-gray-400 mb-8 leading-relaxed text-base sm:text-lg">Мы не просто обещаем молчание — мы встраиваем протоколы безопасности в каждый этап подготовки и проведения мероприятия.</p>
        <div class="space-y-6">
          <div class="flex items-start gap-4"><i data-lucide="file-signature" class="w-5 h-5 text-gold mt-1"></i><div><h4 class="text-white text-lg">Жесткий NDA</h4><p class="text-gray-500">Подписываем соглашение о неразглашении с каждым участником команды.</p></div></div>
          <div class="flex items-start gap-4"><i data-lucide="camera-off" class="w-5 h-5 text-gold mt-1"></i><div><h4 class="text-white text-lg">Контроль съёмки</h4><p class="text-gray-500">Запрет на смартфоны и контроль публикации материалов.</p></div></div>
          <div class="flex items-start gap-4"><i data-lucide="user-check" class="w-5 h-5 text-gold mt-1"></i><div><h4 class="text-white text-lg">Доступ по спискам</h4><p class="text-gray-500">Фейс-контроль и проверка списков гостей на входе.</p></div></div>
        </div>
      </div>
      <div class="reveal reveal-delay-200 relative">
        <img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1c90a0976-f4c6-45f1-a704-4a8900753e1e.png" alt="Щит безопасности" class="w-full h-[500px] object-cover">
      </div>
    </div>
  </section>

  <section id="formats" class="py-20 sm:py-24 lg:py-28 bg-dark">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-16 reveal"><span class="text-gold uppercase tracking-[0.3em] text-xs">Экспертиза</span><h2 class="font-serif text-3xl sm:text-4xl md:text-5xl mt-4 text-white">Форматы мероприятий</h2></div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div class="group relative h-[420px] overflow-hidden reveal"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/173402889-7605-45bb-84b9-6a7f27beb1fc.png" alt="Корпоративные закрытые события" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"><div class="absolute inset-0 bg-gradient-to-t from-black via-black/60 to-black/20"></div><div class="absolute bottom-0 p-8"><h3 class="font-serif text-2xl text-white mb-2">Корпоративные события</h3><p class="text-gray-400 text-sm">Закрытые встречи акционеров и стратегические сессии.</p></div></div>
        <div class="group relative h-[420px] overflow-hidden reveal"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/19ff57788-fc26-44ea-9dfb-2b5c41a5268b.png" alt="Частные закрытые мероприятия" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"><div class="absolute inset-0 bg-gradient-to-t from-black via-black/60 to-black/20"></div><div class="absolute bottom-0 p-8"><h3 class="font-serif text-2xl text-white mb-2">Частные мероприятия</h3><p class="text-gray-400 text-sm">Свадьбы и торжества в узком кругу.</p></div></div>
        <div class="group relative h-[420px] overflow-hidden reveal"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1032f2de6-7c8d-4e15-af56-47e8795cde9a.png" alt="VIP закрытые мероприятия" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"><div class="absolute inset-0 bg-gradient-to-t from-black via-black/60 to-black/20"></div><div class="absolute bottom-0 p-8"><h3 class="font-serif text-2xl text-white mb-2">VIP / Closed Events</h3><p class="text-gray-400 text-sm">Private gig и закрытые показы.</p></div></div>
        <div class="group relative h-[420px] overflow-hidden reveal"><img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1a0a26d6f-d974-45c8-a93c-363ba110453d.png" alt="Организация мероприятий под ключ" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"><div class="absolute inset-0 bg-gradient-to-t from-black via-black/60 to-black/20"></div><div class="absolute bottom-0 p-8"><h3 class="font-serif text-2xl text-white mb-2">Под ключ</h3><p class="text-gray-400 text-sm">Полная организация без вашего участия.</p></div></div>
      </div>
    </div>
  </section>

  <section id="cases" class="py-20 sm:py-24 lg:py-28 bg-charcoal border-y border-white/5">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="mb-16 reveal"><span class="text-gold uppercase tracking-[0.3em] text-xs">Опыт</span><h2 class="font-serif text-3xl sm:text-4xl md:text-5xl mt-4 text-white">Закрытые кейсы</h2></div>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <article class="bg-slate p-8 border border-white/5 reveal"><div class="text-xs text-gray-500 mb-5 uppercase tracking-[0.2em]">Корпоративный сектор</div><h3 class="font-serif text-2xl text-white mb-5">Саммит топ-менеджмента IT-гиганта</h3><ul class="space-y-3 text-sm text-gray-400 mb-6"><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Локация: частная резиденция</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>40 персон уровня C-Level</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Полное подавление сигналов связи</li></ul><p class="text-white/90 italic">"Идеальная тишина и безопасность."</p></article>
        <article class="bg-slate p-8 border border-white/5 reveal"><div class="text-xs text-gray-500 mb-5 uppercase tracking-[0.2em]">Private Party</div><h3 class="font-serif text-2xl text-white mb-5">Юбилей владельца холдинга</h3><ul class="space-y-3 text-sm text-gray-400 mb-6"><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Загородный клуб, полный выкуп</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Вылет артиста инкогнито</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Zero-photo policy для прессы</li></ul><p class="text-white/90 italic">"Гости чувствовали себя абсолютно свободно."</p></article>
        <article class="bg-slate p-8 border border-white/5 reveal"><div class="text-xs text-gray-500 mb-5 uppercase tracking-[0.2em]">Special Event</div><h3 class="font-serif text-2xl text-white mb-5">Закрытый показ коллекции</h3><ul class="space-y-3 text-sm text-gray-400 mb-6"><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Историческое здание в центре</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Контроль съёмки на входе</li><li class="flex gap-2"><i data-lucide="check" class="w-4 h-4 text-gold"></i>Персональные ассистенты для VIP</li></ul><p class="text-white/90 italic">"Высокий уровень сервиса и дискретности."</p></article>
      </div>
    </div>
  </section>

  <section class="py-16 sm:py-20 bg-gold text-black">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-10 text-center">
        <div><div class="text-4xl md:text-5xl font-serif font-bold mb-2 counter-value" data-target="50" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Мероприятий</div></div>
        <div><div class="text-4xl md:text-5xl font-serif font-bold mb-2 counter-value" data-target="7" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Лет опыта</div></div>
        <div><div class="text-4xl md:text-5xl font-serif font-bold mb-2">100%</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">NDA проектов</div></div>
        <div><div class="text-4xl md:text-5xl font-serif font-bold mb-2 counter-value" data-target="20" data-suffix="+">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Городов</div></div>
        <div class="col-span-2 sm:col-span-1"><div class="text-4xl md:text-5xl font-serif font-bold mb-2 counter-value" data-target="85" data-suffix="%">0</div><div class="text-xs uppercase tracking-[0.2em] opacity-70">Повторных клиентов</div></div>
      </div>
    </div>
  </section>

  <section id="faq" class="py-20 sm:py-24 lg:py-28 bg-charcoal border-t border-white/5">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
      <h2 class="font-serif text-3xl sm:text-4xl text-center text-white mb-14 reveal">Важное перед стартом</h2>
      <div class="space-y-4 reveal">
        <details class="group bg-slate border border-white/5"><summary class="flex justify-between items-center font-medium cursor-pointer list-none p-6 text-white">Подписываете ли вы NDA?<i data-lucide="chevron-down" class="w-5 h-5 text-gold"></i></summary><div class="px-6 pb-6 text-sm text-gray-400 border-t border-white/5 pt-4">Да, это стандарт нашей работы.</div></details>
        <details class="group bg-slate border border-white/5"><summary class="flex justify-between items-center font-medium cursor-pointer list-none p-6 text-white">Публикуете ли вы материалы в портфолио?<i data-lucide="chevron-down" class="w-5 h-5 text-gold"></i></summary><div class="px-6 pb-6 text-sm text-gray-400 border-t border-white/5 pt-4">Только с письменного разрешения клиента.</div></details>
        <details class="group bg-slate border border-white/5"><summary class="flex justify-between items-center font-medium cursor-pointer list-none p-6 text-white">Как контролируется фото и видео?<i data-lucide="chevron-down" class="w-5 h-5 text-gold"></i></summary><div class="px-6 pb-6 text-sm text-gray-400 border-t border-white/5 pt-4">Сбор телефонов на входе и контроль медиаматериалов.</div></details>
      </div>
    </div>
  </section>

  <section id="contact" class="py-20 sm:py-24 lg:py-28 bg-dark">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="glass-panel p-6 sm:p-8 md:p-12 reveal">
        <div class="text-center mb-10"><h2 class="font-serif text-3xl sm:text-4xl text-white mb-4">Обсудим ваше мероприятие</h2><p class="text-gray-400">Оставьте заявку. Мы свяжемся с вами через защищённый канал.</p></div>
        <form bind:this={contactForm} id="contact-form" class="space-y-6" novalidate>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
            <div><label for="name" class="text-xs uppercase tracking-[0.2em] text-gray-500">Имя *</label><input id="name" type="text" required autocomplete="name" class="form-input w-full bg-black/40 border border-white/10 p-4 text-white text-sm mt-2"><p class="error-message text-red-400 text-[11px] hidden">Введите ваше имя</p></div>
            <div><label for="contact-info" class="text-xs uppercase tracking-[0.2em] text-gray-500">Телефон / Telegram *</label><input id="contact-info" type="text" required autocomplete="tel" class="form-input w-full bg-black/40 border border-white/10 p-4 text-white text-sm mt-2"><p class="error-message text-red-400 text-[11px] hidden">Укажите способ связи</p></div>
          </div>
          <button bind:this={submitBtn} type="submit" id="submit-btn" class="w-full bg-gold text-black font-medium uppercase tracking-[0.2em] text-sm py-4 flex items-center justify-center gap-2"><span class="btn-text">Отправить запрос</span><span class="btn-loading hidden"><svg class="animate-spin h-4 w-4" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4" fill="none"></circle></svg></span></button>
        </form>
        <div bind:this={formSuccess} id="form-success" class="hidden text-center py-8"><i data-lucide="check-circle" class="w-8 h-8 text-gold mx-auto mb-4"></i><h3 class="font-serif text-2xl text-white mb-3">Заявка отправлена</h3></div>
      </div>
    </div>
  </section>
</main>

<footer class="bg-black py-12 sm:py-16 border-t border-white/10">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-10">
    <div><a href="#main-content" class="text-2xl font-serif font-semibold tracking-[0.2em] text-white uppercase block mb-5">Closed<span class="text-gold">.</span>Events</a><p class="text-gray-500 text-sm">Организация закрытых мероприятий премиум-класса. Конфиденциальность — наш главный продукт.</p></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Навигация</h4><ul class="space-y-3 text-sm text-gray-500"><li><a href="#confidentiality">Конфиденциальность</a></li><li><a href="#formats">Форматы</a></li><li><a href="#cases">Кейсы</a></li><li><a href="#faq">FAQ</a></li></ul></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Услуги</h4><ul class="space-y-3 text-sm text-gray-500"><li>Корпоративные события</li><li>Частные вечеринки</li><li>VIP логистика</li><li>Охрана и NDA</li></ul></div>
    <div><h4 class="text-white mb-6 uppercase text-xs tracking-[0.2em]">Контакты</h4><ul class="space-y-3 text-sm text-gray-500"><li>+7 (999) 000-00-00</li><li>private@closed.events</li><li>Москва, Сити</li></ul></div>
  </div>
</footer>

<style>
  :global(*) { box-sizing: border-box; -webkit-font-smoothing: antialiased; }
  :global(html) { scroll-behavior: smooth; scroll-padding-top: 80px; }
  :global(body) { margin: 0; background-color: #0a0a0a; color: #e5e5e5; overflow-x: hidden; }
  .bg-dark { background: #0a0a0a; }
  .bg-charcoal { background: #121212; }
  .bg-slate { background: #1c1c1c; }
  .text-gold { color: #d4af37; }
  .bg-gold { background: #d4af37; }
  .font-serif { font-family: 'Cormorant Garamond', Georgia, serif; }
  .font-sans { font-family: 'Manrope', -apple-system, sans-serif; }
  .mobile-menu { transform: translateX(100%); transition: transform .4s cubic-bezier(.16,1,.3,1); }
  .mobile-menu.open { transform: translateX(0); }
  .line-1-open { transform: rotate(45deg) translate(5px, 5px); }
  .line-2-open { opacity: 0; }
  .line-3-open { transform: rotate(-45deg) translate(7px, -6px); }
  :global(.bg-dark-nav) { background: rgba(10,10,10,.95); backdrop-filter: blur(12px); box-shadow: 0 10px 30px rgba(0,0,0,.25); }
  :global(.h-20) { height: 5rem; }
  :global(.h-16) { height: 4rem; }
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity .8s cubic-bezier(.16,1,.3,1), transform .8s cubic-bezier(.16,1,.3,1); }
  :global(.reveal.is-visible) { opacity: 1; transform: translateY(0); }
  .glass-panel { background: rgba(28, 28, 28, 0.65); backdrop-filter: blur(16px); border: 1px solid rgba(255, 255, 255, 0.06); }
  .form-input:focus { outline: 1px solid rgba(212,175,55,.4); border-color: #d4af37; }
</style>
