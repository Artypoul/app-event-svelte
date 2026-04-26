<script>
  import { onMount } from 'svelte';

  let menuOpen = false;
  let shrinkNav = false;

  const toContact = () => {
    document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth', block: 'start' });
  };

  onMount(() => {
    const onScroll = () => (shrinkNav = window.scrollY > 50);
    window.addEventListener('scroll', onScroll, { passive: true });
    return () => window.removeEventListener('scroll', onScroll);
  });
</script>

<svelte:head>
  <title>Closed Events | Закрытые мероприятия</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<a href="#main" class="skip-link">Перейти к основному контенту</a>

<header class="nav" class:shrink={shrinkNav}>
  <div class="container nav-inner">
    <a class="logo" href="#main">Closed<span>.Events</span></a>
    <nav class="desktop-nav">
      <a href="#confidentiality">Конфиденциальность</a>
      <a href="#formats">Форматы</a>
      <a href="#cases">Кейсы</a>
      <a href="#faq">FAQ</a>
    </nav>
    <button class="cta" on:click={toContact}>Обсудить проект</button>
    <button class="menu-btn" on:click={() => (menuOpen = !menuOpen)}>{menuOpen ? '✕' : '☰'}</button>
  </div>
</header>

{#if menuOpen}
  <div class="mobile-menu">
    <a href="#confidentiality" on:click={() => (menuOpen = false)}>Конфиденциальность</a>
    <a href="#formats" on:click={() => (menuOpen = false)}>Форматы</a>
    <a href="#cases" on:click={() => (menuOpen = false)}>Кейсы</a>
    <a href="#faq" on:click={() => (menuOpen = false)}>FAQ</a>
  </div>
{/if}

<main id="main">
  <section class="hero">
    <img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1ff567042-2eec-40d7-b49c-a8504b6a957a.png" alt="Закрытое мероприятие" />
    <div class="overlay"></div>
    <div class="hero-content container">
      <p class="eyebrow">Private & Confidential</p>
      <h1>Закрытые мероприятия <span>без огласки</span></h1>
      <p>Организация событий премиум-класса с фокусом на приватность.</p>
      <div class="actions">
        <button on:click={toContact}>Обсудить мероприятие</button>
        <button class="ghost">Запросить NDA</button>
      </div>
    </div>
  </section>

  <section id="confidentiality" class="section dark">
    <div class="container two-col">
      <div>
        <h2>Конфиденциальность в основе всего</h2>
        <p>Протоколы безопасности встроены в каждый этап подготовки и проведения.</p>
        <ul>
          <li>Жесткий NDA с командой и подрядчиками</li>
          <li>Контроль съемки и распространения материалов</li>
          <li>Доступ гостей по спискам</li>
        </ul>
      </div>
      <img src="https://image.qwenlm.ai/public_source/66673185-31fc-400c-9758-01d949190730/1c90a0976-f4c6-45f1-a704-4a8900753e1e.png" alt="Конфиденциальность" />
    </div>
  </section>

  <section id="formats" class="section">
    <div class="container">
      <h2>Форматы мероприятий</h2>
      <div class="cards">
        <article><h3>Корпоративные события</h3></article>
        <article><h3>Частные мероприятия</h3></article>
        <article><h3>VIP / Closed Events</h3></article>
        <article><h3>Под ключ</h3></article>
      </div>
    </div>
  </section>

  <section id="cases" class="section dark">
    <div class="container">
      <h2>Закрытые кейсы</h2>
      <div class="cases">
        <article>Саммит топ-менеджмента IT-гиганта</article>
        <article>Юбилей владельца холдинга</article>
        <article>Закрытый показ коллекции</article>
      </div>
    </div>
  </section>

  <section id="faq" class="section">
    <div class="container narrow">
      <h2>FAQ</h2>
      <details><summary>Подписываете ли вы NDA?</summary><p>Да, это стандарт нашей работы.</p></details>
      <details><summary>Публикуете ли вы материалы в портфолио?</summary><p>Только по письменному разрешению клиента.</p></details>
    </div>
  </section>

  <section id="contact" class="section dark">
    <div class="container narrow panel">
      <h2>Обсудим ваше мероприятие</h2>
      <form>
        <input placeholder="Имя" required />
        <input placeholder="Телефон / Telegram" required />
        <button type="submit">Отправить запрос</button>
      </form>
    </div>
  </section>
</main>

<style>
  :global(body){margin:0;background:#0a0a0a;color:#eee;font-family:system-ui,sans-serif}
  .container{max-width:1200px;margin:0 auto;padding:0 20px}
  .skip-link{position:absolute;left:-9999px}.skip-link:focus{left:10px;top:10px;background:#d4af37;color:#000;padding:8px}
  .nav{position:fixed;top:0;left:0;right:0;z-index:50;background:transparent;transition:.3s}
  .nav.shrink{background:rgba(10,10,10,.92);backdrop-filter:blur(8px)}
  .nav-inner{display:flex;align-items:center;gap:20px;height:80px}
  .logo{color:#fff;text-decoration:none;font-size:28px}.logo span{color:#d4af37}
  .desktop-nav{display:flex;gap:24px}.desktop-nav a{color:#bbb;text-decoration:none}
  .cta{margin-left:auto}.menu-btn{display:none}
  .mobile-menu{position:fixed;inset:80px 0 auto 0;background:#121212;padding:20px;display:grid;gap:14px;z-index:40}
  .hero{position:relative;height:100vh;min-height:680px;display:flex;align-items:center}
  .hero img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
  .overlay{position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,0,.75),rgba(0,0,0,.4),#0a0a0a)}
  .hero-content{position:relative;z-index:2;text-align:center}
  .eyebrow{letter-spacing:.3em;color:#d4af37;text-transform:uppercase}
  h1{font-size:64px;margin:10px 0} h1 span{display:block;font-style:italic;color:#d0d0d0}
  .actions{display:flex;gap:12px;justify-content:center}.ghost{background:transparent;color:#fff;border:1px solid #777}
  .section{padding:90px 0}.dark{background:#121212}
  .two-col{display:grid;grid-template-columns:1fr 1fr;gap:30px;align-items:center}.two-col img{width:100%;height:450px;object-fit:cover}
  .cards,.cases{display:grid;grid-template-columns:repeat(4,1fr);gap:16px}.cases{grid-template-columns:repeat(3,1fr)}
  article{background:#1c1c1c;padding:24px}
  .narrow{max-width:760px}.panel{background:#1c1c1c;padding:30px;border:1px solid #2c2c2c}
  form{display:grid;gap:12px}input,button{padding:12px}
  @media (max-width:900px){.desktop-nav,.cta{display:none}.menu-btn{display:block;margin-left:auto}.two-col,.cards,.cases{grid-template-columns:1fr}h1{font-size:40px}}
</style>
