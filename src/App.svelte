<svelte:head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BROSCO Private Events | Конфиденциальные мероприятия</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet" />

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            gold: '#C9A961',
            dark: '#0A0A0A',
            'dark-light': '#141414',
            panel: '#1A1A1A'
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Playfair Display', 'serif']
          }
        }
      }
    };
  </script>
</svelte:head>

<div class="antialiased bg-dark text-white">
  <header class="fixed inset-x-0 top-0 z-50 border-b border-white/10 bg-dark/95 backdrop-blur-sm">
    <div class="mx-auto flex h-20 max-w-[1440px] items-center justify-between px-6 lg:px-8">
      <a href="#hero" class="flex items-center gap-3">
        <div class="flex h-10 w-10 items-center justify-center bg-white text-dark text-lg font-bold">B</div>
        <span class="text-sm font-semibold tracking-[0.2em] uppercase">Brosco <span class="text-gold">Private</span></span>
      </a>
      <nav class="hidden lg:flex items-center gap-8 text-[11px] uppercase tracking-[0.15em] text-white/50">
        <a href="#guarantees" class="hover:text-white transition">Гарантии</a>
        <a href="#services" class="hover:text-white transition">Форматы</a>
        <a href="#cases" class="hover:text-white transition">Кейсы</a>
        <a href="#approach" class="hover:text-white transition">Подход</a>
        <a href="#guests" class="hover:text-white transition">Гости</a>
        <a href="#faq" class="hover:text-white transition">FAQ</a>
      </nav>
      <a href="#contact" class="hidden md:flex border border-white/20 px-6 py-2 text-[10px] uppercase tracking-widest hover:border-gold hover:text-gold transition">Запросить NDA</a>
    </div>
  </header>

  <main>
    <section id="hero" class="relative min-h-screen flex items-center pt-20 overflow-hidden">
      <div class="absolute inset-0 z-0">
        <img src="/01-hero-background.png" class="w-full h-full object-cover" alt="Hero" />
        <div class="hero-overlay absolute inset-0"></div>
      </div>

      <div class="relative z-10 max-w-[1440px] mx-auto px-6 lg:px-8 w-full">
        <div class="max-w-4xl">
          <div class="flex items-center gap-3 mb-6 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold">
            <div class="w-2 h-2 rounded-full bg-gold"></div> Закрытые мероприятия
          </div>
          <h1 class="text-4xl md:text-6xl lg:text-7xl font-light uppercase tracking-tight leading-[1.1] mb-8">
            Организуем мероприятия, <br />о которых знают <span class="font-serif italic text-gold normal-case">только приглашенные</span>
          </h1>
          <p class="text-lg md:text-xl text-white/60 mb-12 max-w-2xl font-light">
            Частные, корпоративные и VIP-события под ключ — с полным контролем доступа, материалов и всех чувствительных деталей.
          </p>
          <div class="flex flex-col sm:flex-row gap-4">
            <a href="#contact" class="bg-white text-dark px-10 py-5 text-xs font-bold uppercase tracking-[0.15em] text-center hover:bg-gold transition">Обсудить мероприятие</a>
            <a href="#contact" class="border border-white/20 px-10 py-5 text-xs font-bold uppercase tracking-[0.15em] text-center hover:border-gold transition">Запросить NDA</a>
          </div>
        </div>
      </div>
    </section>

    <section id="guarantees" class="py-24 bg-dark-light border-y border-white/5">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="mb-16">
          <div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold">
            <div class="w-2 h-2 rounded-full bg-gold"></div> Гарантии
          </div>
          <h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight">Конфиденциальность в основе</h2>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div class="glass-panel p-8"><div class="text-gold text-3xl font-serif italic mb-6">01</div><h3 class="text-xl font-medium mb-3">NDA с командой</h3><p class="text-white/50 font-light text-sm">Все участники проекта работают по согласованным правилам конфиденциальности.</p></div>
          <div class="glass-panel p-8"><div class="text-gold text-3xl font-serif italic mb-6">02</div><h3 class="text-xl font-medium mb-3">Контроль съёмки</h3><p class="text-white/50 font-light text-sm">Заранее определяем, что можно снимать, хранить и публиковать.</p></div>
          <div class="glass-panel p-8"><div class="text-gold text-3xl font-serif italic mb-6">03</div><h3 class="text-xl font-medium mb-3">Доступ по спискам</h3><p class="text-white/50 font-light text-sm">На площадке действует персональный допуск для гостей и команды.</p></div>
          <div class="glass-panel p-8"><div class="text-gold text-3xl font-serif italic mb-6">04</div><h3 class="text-xl font-medium mb-3">Регламент материалов</h3><p class="text-white/50 font-light text-sm">Фото, видео и документы передаются и хранятся по утверждённому сценарию.</p></div>
        </div>
      </div>
    </section>

    <section id="services" class="py-24 bg-dark">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="grid lg:grid-cols-[1fr_1fr] gap-12 items-end mb-16">
          <div>
            <div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Услуги</div>
            <h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight">Форматы мероприятий</h2>
          </div>
          <div class="lg:border-l border-gold pl-6"><p class="text-white/60 text-lg font-light">От камерных встреч до статусных событий с полной координацией всех этапов.</p></div>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div class="glass-panel p-8 flex flex-col justify-between min-h-[280px]"><h3 class="text-xl font-medium uppercase tracking-tight mb-4 text-white">Корпоративные <br />события</h3><p class="text-sm text-white/50 font-light">Стратегические сессии, клиентские встречи, внутренние события и деловые ужины.</p></div>
          <div class="glass-panel p-8 flex flex-col justify-between min-h-[280px]"><h3 class="text-xl font-medium uppercase tracking-tight mb-4 text-white">Частные <br />мероприятия</h3><p class="text-sm text-white/50 font-light">Дни рождения, камерные ужины, family celebrations и private gatherings.</p></div>
          <div class="glass-panel p-8 flex flex-col justify-between min-h-[280px]"><h3 class="text-xl font-medium uppercase tracking-tight mb-4 text-white">VIP / Closed <br />Events</h3><p class="text-sm text-white/50 font-light">Приёмы, презентации, визиты специальных гостей и события с особым протоколом.</p></div>
          <div class="glass-panel p-8 flex flex-col justify-between min-h-[280px]"><h3 class="text-xl font-medium uppercase tracking-tight mb-4 text-gold">Проекты <br />Под ключ</h3><p class="text-sm text-white/50 font-light">Берём на себя концепцию, площадку, тайминг, подрядчиков и сопровождение проекта.</p></div>
        </div>
      </div>
    </section>

    <section id="cases" class="py-24 bg-dark-light border-y border-white/5">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="grid lg:grid-cols-[1fr_1fr] gap-12 items-start mb-16">
          <div>
            <div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Кейсы</div>
            <h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight">Закрытые кейсы</h2>
          </div>
          <div class="lg:border-l border-gold pl-6"><p class="text-white/60 text-lg font-light mb-6">Показываем формат, уровень сервиса и подход — без раскрытия клиентов.</p><a href="#contact" class="border border-gold text-gold px-8 py-3 text-[10px] uppercase tracking-widest hover:bg-gold hover:text-dark transition">Смотреть детали</a></div>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div class="glass-panel overflow-hidden image-hover-color group"><div class="h-64 overflow-hidden relative"><img src="/05-case-archive-1.png" class="w-full h-full object-cover" alt="Ужин" /></div><div class="p-6"><h3 class="text-lg font-medium mb-4 leading-tight">Закрытый ужин для собственников бизнеса</h3><div class="text-xs text-white/40 space-y-2 mb-6"><p>• 40 гостей</p><p>• Москва</p><p>• Полный контроль доступа</p></div><p class="text-xs text-white/60 border-t border-white/10 pt-4"><span class="text-gold">Итог:</span> доверительная атмосфера без лишнего внимания.</p></div></div>
          <div class="glass-panel overflow-hidden image-hover-color group"><div class="h-64 overflow-hidden relative"><img src="/06-case-archive-2.png" class="w-full h-full object-cover" alt="Камерное" /></div><div class="p-6"><h3 class="text-lg font-medium mb-4 leading-tight">Камерное частное событие</h3><div class="text-xs text-white/40 space-y-2 mb-6"><p>• 30 гостей</p><p>• Загородная резиденция</p><p>• Деликатное сопровождение</p></div><p class="text-xs text-white/60 border-t border-white/10 pt-4"><span class="text-gold">Итог:</span> уютный private-format с максимальной конфиденциальностью.</p></div></div>
          <div class="glass-panel overflow-hidden image-hover-color group"><div class="h-64 overflow-hidden relative"><img src="/02-corporate-format.png" class="w-full h-full object-cover" alt="Презентация" /></div><div class="p-6"><h3 class="text-lg font-medium mb-4 leading-tight">Презентация для партнёров и инвесторов</h3><div class="text-xs text-white/40 space-y-2 mb-6"><p>• 70 гостей</p><p>• Москва</p><p>• Работа по NDA</p></div><p class="text-xs text-white/60 border-t border-white/10 pt-4"><span class="text-gold">Итог:</span> точная координация и защищённая коммуникация.</p></div></div>
          <div class="glass-panel overflow-hidden image-hover-color group"><div class="h-64 overflow-hidden relative"><img src="/04-production-format.png" class="w-full h-full object-cover" alt="Сессия" /></div><div class="p-6"><h3 class="text-lg font-medium mb-4 leading-tight">Корпоративная стратегическая сессия</h3><div class="text-xs text-white/40 space-y-2 mb-6"><p>• 60 гостей</p><p>• Подмосковье</p><p>• Закрытый формат</p></div><p class="text-xs text-white/60 border-t border-white/10 pt-4"><span class="text-gold">Итог:</span> рабочая атмосфера без отвлечений с контролем сценария.</p></div></div>
        </div>
      </div>
    </section>

    <section id="approach" class="py-24 bg-dark">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="mb-16"><div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Подход</div><h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight mb-6">Всё остаётся внутри</h2><p class="text-white/60 text-lg font-light max-w-2xl">Мы выстраиваем проект так, чтобы защищать гостей, информацию, материалы и репутацию клиента.</p></div>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div class="glass-panel p-8"><h3 class="text-xl font-medium mb-4 text-white uppercase tracking-tight border-b border-gold pb-4 inline-block">Гости</h3><p class="text-sm text-white/50 font-light mt-4">Закрытые списки, деликатное сопровождение и контролируемый доступ на каждом этапе события.</p></div>
          <div class="glass-panel p-8"><h3 class="text-xl font-medium mb-4 text-white uppercase tracking-tight border-b border-gold pb-4 inline-block">Информация</h3><p class="text-sm text-white/50 font-light mt-4">Сценарии, тайминги и рабочие детали остаются строго внутри проектного контура.</p></div>
          <div class="glass-panel p-8"><h3 class="text-xl font-medium mb-4 text-white uppercase tracking-tight border-b border-gold pb-4 inline-block">Материалы</h3><p class="text-sm text-white/50 font-light mt-4">Фото, видео и документы не выходят в публичное поле без прямого согласования.</p></div>
          <div class="glass-panel p-8"><h3 class="text-xl font-medium mb-4 text-white uppercase tracking-tight border-b border-gold pb-4 inline-block">Репутация</h3><p class="text-sm text-white/50 font-light mt-4">Мы защищаем не только событие, но и доверие к вашему имени, бренду и кругу общения.</p></div>
        </div>
      </div>
    </section>

    <section class="py-20 border-y border-white/5 bg-dark-light">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="flex items-center gap-3 mb-10 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Доверие</div>
        <div class="grid grid-cols-2 md:grid-cols-5 gap-8 text-center md:text-left divide-x divide-white/10">
          <div class="px-4"><div class="text-4xl lg:text-5xl font-light text-white mb-2">50+</div><div class="text-[11px] uppercase tracking-widest text-white/50">мероприятий</div></div>
          <div class="px-4"><div class="text-4xl lg:text-5xl font-light text-white mb-2">7+</div><div class="text-[11px] uppercase tracking-widest text-white/50">лет опыта</div></div>
          <div class="px-4"><div class="text-4xl lg:text-5xl font-light text-gold mb-2">100%</div><div class="text-[11px] uppercase tracking-widest text-white/50">NDA-проектов</div></div>
          <div class="px-4"><div class="text-4xl lg:text-5xl font-light text-white mb-2">20+</div><div class="text-[11px] uppercase tracking-widest text-white/50">городов</div></div>
          <div class="px-4"><div class="text-4xl lg:text-5xl font-light text-white mb-2">85%</div><div class="text-[11px] uppercase tracking-widest text-white/50">повторных клиентов</div></div>
        </div>
      </div>
    </section>

    <section id="guests" class="py-24 bg-dark">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="mb-16"><div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Special Guests</div><h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight mb-6">Публичные гости</h2><p class="text-white/60 text-lg font-light max-w-2xl">Работаем с артистами, ведущими и статусными гостями в закрытом формате — без лишней публичности.</p></div>
        <div class="grid lg:grid-cols-2 gap-6">
          <div class="glass-panel overflow-hidden image-hover-color relative h-[400px] lg:h-auto"><img src="/05-case-archive-1.png" class="absolute inset-0 w-full h-full object-cover" alt="Артист" /><div class="absolute inset-0 bg-gradient-to-t from-dark via-dark/50 to-transparent"></div><div class="absolute bottom-0 p-8 z-10"><h3 class="text-2xl font-medium text-white mb-2">Артист федерального уровня</h3><p class="text-gold text-sm tracking-widest uppercase">Частное событие</p></div></div>
          <div class="grid sm:grid-cols-2 gap-6">
            <div class="glass-panel overflow-hidden image-hover-color relative h-[250px]"><img src="/06-case-archive-2.png" class="absolute inset-0 w-full h-full object-cover" alt="Хедлайнер" /><div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent"></div><div class="absolute bottom-0 p-6 z-10"><h3 class="text-lg font-medium text-white mb-1">Муз. хедлайнер</h3><p class="text-white/50 text-xs">VIP appearance</p></div></div>
            <div class="glass-panel overflow-hidden image-hover-color relative h-[250px]"><img src="/02-corporate-format.png" class="absolute inset-0 w-full h-full object-cover" alt="Ведущая" /><div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent"></div><div class="absolute bottom-0 p-6 z-10"><h3 class="text-lg font-medium text-white mb-1">Телеведущая</h3><p class="text-white/50 text-xs">Закрытый ужин</p></div></div>
            <div class="glass-panel overflow-hidden image-hover-color relative h-[250px]"><img src="/03-private-format.png" class="absolute inset-0 w-full h-full object-cover" alt="Персона" /><div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent"></div><div class="absolute bottom-0 p-6 z-10"><h3 class="text-lg font-medium text-white mb-1">Публичная персона</h3><p class="text-white/50 text-xs">Private event</p></div></div>
            <div class="glass-panel overflow-hidden image-hover-color relative h-[250px]"><img src="/04-production-format.png" class="absolute inset-0 w-full h-full object-cover" alt="Гость" /><div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent"></div><div class="absolute bottom-0 p-6 z-10"><h3 class="text-lg font-medium text-white mb-1">Специальный гость</h3><p class="text-white/50 text-xs">Closed event</p></div></div>
          </div>
        </div>
      </div>
    </section>

    <section id="reviews" class="py-24 bg-dark-light border-y border-white/5">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="mb-16"><div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> Отзывы</div><h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight mb-6">Что говорят клиенты</h2><p class="text-white/60 text-lg font-light max-w-2xl">Нас рекомендуют за точность, деликатность и контроль на каждом этапе.</p></div>
        <div class="grid md:grid-cols-3 gap-6">
          <div class="glass-panel p-10 relative"><div class="text-gold text-6xl font-serif leading-none absolute top-6 left-6 opacity-30">“</div><p class="text-white/80 font-light leading-relaxed relative z-10 pt-4 mb-8">Команда провела закрытый ужин без лишнего внимания и идеально выдержала весь сценарий. Всё было деликатно, спокойно и безупречно организовано.</p><div class="border-t border-white/10 pt-4"><p class="text-gold text-xs uppercase tracking-widest">Собственник инвестиционной компании</p></div></div>
          <div class="glass-panel p-10 relative"><div class="text-gold text-6xl font-serif leading-none absolute top-6 left-6 opacity-30">“</div><p class="text-white/80 font-light leading-relaxed relative z-10 pt-4 mb-8">Нам был важен не только уровень сервиса, но и приватность гостей. Проект реализовали точно, аккуратно и без лишней огласки.</p><div class="border-t border-white/10 pt-4"><p class="text-gold text-xs uppercase tracking-widest">Private client</p></div></div>
          <div class="glass-panel p-10 relative"><div class="text-gold text-6xl font-serif leading-none absolute top-6 left-6 opacity-30">“</div><p class="text-white/80 font-light leading-relaxed relative z-10 pt-4 mb-8">Редкий случай, когда подрядчик одинаково хорошо держит и эстетику события, и контроль всех чувствительных деталей.</p><div class="border-t border-white/10 pt-4"><p class="text-gold text-xs uppercase tracking-widest">Руководитель корпоративных коммуникаций</p></div></div>
        </div>
      </div>
    </section>

    <section id="faq" class="py-24 bg-dark">
      <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="grid lg:grid-cols-[1fr_1.5fr] gap-16">
          <div><div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> FAQ</div><h2 class="text-3xl md:text-5xl font-light uppercase tracking-tight mb-6">Важное <br />перед стартом</h2><p class="text-white/60 text-lg font-light mb-8">Коротко отвечаем на вопросы, которые чаще всего возникают перед запуском проекта.</p><a href="#contact" class="bg-white text-dark px-8 py-4 text-xs font-bold uppercase tracking-[0.15em] inline-block hover:bg-gold transition">Задать свой вопрос</a></div>
          <div class="space-y-4">
            <details class="glass-panel group" open><summary class="p-6 md:p-8 cursor-pointer flex justify-between items-center text-lg md:text-xl font-medium text-white hover:text-gold transition"><span class="flex items-center gap-4"><span class="text-gold font-serif italic text-sm">01</span> Подписываете ли вы NDA?</span><span class="text-gold text-2xl group-open:rotate-45 transition-transform">+</span></summary><div class="px-6 md:px-8 pb-8 text-white/50 font-light pl-[3.5rem]">Да. При необходимости фиксируем конфиденциальность документально ещё до старта обсуждения проекта.</div></details>
            <details class="glass-panel group"><summary class="p-6 md:p-8 cursor-pointer flex justify-between items-center text-lg md:text-xl font-medium text-white hover:text-gold transition"><span class="flex items-center gap-4"><span class="text-gold font-serif italic text-sm">02</span> Публикуете ли вы материалы?</span><span class="text-gold text-2xl group-open:rotate-45 transition-transform">+</span></summary><div class="px-6 md:px-8 pb-8 text-white/50 font-light pl-[3.5rem]">Нет, без отдельного согласования мы не публикуем фото, видео и детали проекта ни в каком виде.</div></details>
            <details class="glass-panel group"><summary class="p-6 md:p-8 cursor-pointer flex justify-between items-center text-lg md:text-xl font-medium text-white hover:text-gold transition"><span class="flex items-center gap-4"><span class="text-gold font-serif italic text-sm">03</span> Как контролируется фото и видео?</span><span class="text-gold text-2xl group-open:rotate-45 transition-transform">+</span></summary><div class="px-6 md:px-8 pb-8 text-white/50 font-light pl-[3.5rem]">Согласуем правила съёмки заранее, определяем жесткий доступ к материалам и контролируем публикации.</div></details>
            <details class="glass-panel group"><summary class="p-6 md:p-8 cursor-pointer flex justify-between items-center text-lg md:text-xl font-medium text-white hover:text-gold transition"><span class="flex items-center gap-4"><span class="text-gold font-serif italic text-sm">04</span> Можно ли провести событие без публичности?</span><span class="text-gold text-2xl group-open:rotate-45 transition-transform">+</span></summary><div class="px-6 md:px-8 pb-8 text-white/50 font-light pl-[3.5rem]">Да. Мы выстраиваем процесс так, чтобы мероприятие оставалось закрытым на всех 100% этапах.</div></details>
            <details class="glass-panel group"><summary class="p-6 md:p-8 cursor-pointer flex justify-between items-center text-lg md:text-xl font-medium text-white hover:text-gold transition"><span class="flex items-center gap-4"><span class="text-gold font-serif italic text-sm">05</span> Работаете ли вы с VIP-гостями?</span><span class="text-gold text-2xl group-open:rotate-45 transition-transform">+</span></summary><div class="px-6 md:px-8 pb-8 text-white/50 font-light pl-[3.5rem]">Да. Организуем деликатное сопровождение, доступ по спискам и жесткий контроль чувствительных зон.</div></details>
          </div>
        </div>
      </div>
    </section>

    <section id="contact" class="relative py-32 bg-dark-light border-y border-white/5 overflow-hidden">
      <img src="/07-contact-background.png" class="absolute inset-0 w-full h-full object-cover opacity-[0.08]" alt="Фон" />
      <div class="relative z-10 max-w-[1440px] mx-auto px-6 lg:px-8">
        <div class="grid lg:grid-cols-2 gap-16 items-start">
          <div>
            <div class="flex items-center gap-3 mb-4 text-gold text-[10px] uppercase tracking-[0.2em] font-semibold"><div class="w-2 h-2 rounded-full bg-gold"></div> CTA</div>
            <h2 class="text-4xl md:text-6xl font-light uppercase tracking-tight mb-8">Обсудим ваше <br />мероприятие</h2>
            <p class="text-white/60 text-xl font-light mb-12">Предложим формат, тайминг и безопасную организацию под вашу задачу.</p>
            <div class="space-y-6 text-xl tracking-wide font-light"><a href="tel:+79991234567" class="block hover:text-gold transition">+7 (999) 123-45-67</a><a href="mailto:events@brosco.studio" class="block hover:text-gold transition">events@brosco.studio</a><p class="text-white/40 text-sm mt-4">Москва, Россия</p></div>
          </div>

          <div class="glass-panel p-8 md:p-12">
            <form on:submit|preventDefault={() => alert('Конфиденциальный запрос отправлен.')}>
              <div class="grid gap-6 mb-8">
                <input type="text" placeholder="Ваше имя" class="w-full bg-[#111] border border-white/10 px-6 py-5 text-white outline-none focus:border-gold transition placeholder:text-white/30" required />
                <input type="text" placeholder="Телефон или Telegram" class="w-full bg-[#111] border border-white/10 px-6 py-5 text-white outline-none focus:border-gold transition placeholder:text-white/30" required />
                <textarea rows="4" placeholder="Кратко о задаче" class="w-full bg-[#111] border border-white/10 px-6 py-5 text-white outline-none focus:border-gold transition placeholder:text-white/30 resize-none"></textarea>
              </div>
              <button class="w-full bg-white text-dark py-5 text-xs font-bold uppercase tracking-[0.15em] hover:bg-gold transition">Получить предложение</button>
              <p class="text-center text-white/30 text-xs mt-6 italic">Первый контакт — полностью конфиденциальный</p>
            </form>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer class="py-16 bg-dark">
    <div class="max-w-[1440px] mx-auto px-6 lg:px-8">
      <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-12 mb-16">
        <div class="lg:col-span-1"><div class="text-xl font-medium tracking-tight mb-6">BROSCO PRIVATE EVENTS</div><p class="text-white/40 text-sm leading-relaxed mb-6">Организуем закрытые мероприятия под ключ. Конфиденциальность, точность и деликатное сопровождение.</p></div>
        <div><h4 class="text-gold text-[10px] uppercase tracking-widest font-semibold mb-6">Навигация</h4><ul class="space-y-4 text-white/60 text-sm"><li><a href="#hero" class="hover:text-white transition">Главная</a></li><li><a href="#services" class="hover:text-white transition">Форматы</a></li><li><a href="#cases" class="hover:text-white transition">Кейсы</a></li><li><a href="#approach" class="hover:text-white transition">Подход</a></li><li><a href="#faq" class="hover:text-white transition">FAQ</a></li></ul></div>
        <div><h4 class="text-gold text-[10px] uppercase tracking-widest font-semibold mb-6">Форматы</h4><ul class="space-y-4 text-white/60 text-sm"><li>Корпоративные события</li><li>Частные мероприятия</li><li>VIP / Closed Events</li><li>Под ключ</li></ul></div>
        <div><h4 class="text-gold text-[10px] uppercase tracking-widest font-semibold mb-6">Контакты</h4><ul class="space-y-4 text-white/60 text-sm"><li>+7 (999) 123-45-67</li><li>events@brosco.studio</li><li>Москва, Россия</li></ul></div>
      </div>
      <div class="border-t border-white/10 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-xs text-white/30"><div>© 2026 BROSCO Private Events. Все права защищены.</div><div class="flex gap-6"><a href="/privacy" class="hover:text-white transition">Политика конфиденциальности</a><a href="/data-processing" class="hover:text-white transition">Обработка данных</a></div></div>
    </div>
  </footer>
</div>

<style>
  :global(html) { scroll-behavior: smooth; }
  :global(body) { background-color: #0A0A0A; color: #ffffff; }
  .glass-panel { background: linear-gradient(180deg, rgba(255, 255, 255, 0.03), rgba(255, 255, 255, 0.01)); border: 1px solid rgba(255, 255, 255, 0.05); transition: all 0.4s ease; }
  .glass-panel:hover { border-color: rgba(201, 169, 97, 0.3); transform: translateY(-4px); }
  .hero-overlay { background: linear-gradient(180deg, rgba(10, 10, 10, 0.7) 0%, rgba(10, 10, 10, 0.5) 40%, rgba(10, 10, 10, 1) 100%); }
  .image-hover-color img { filter: grayscale(100%) brightness(0.6); transition: all 0.7s cubic-bezier(0.16, 1, 0.3, 1); }
  .image-hover-color:hover img { filter: grayscale(0%) brightness(0.9); transform: scale(1.05); }
  details > summary { list-style: none; }
  details > summary::-webkit-details-marker { display: none; }
</style>
