<script>
	import { onMount } from 'svelte';

	const protocols = [
		{
			number: '01',
			title: 'Строгий NDA',
			description:
				'Подписываем соглашение о неразглашении до начала обсуждения деталей проекта. Никаких утечек.'
		},
		{
			number: '02',
			title: 'Контроль съёмки',
			description:
				'Блокировка камер, изъятие телефонов (по запросу) и жесткий регламент работы технического персонала.'
		},
		{
			number: '03',
			title: 'Закрытые списки',
			description: 'Многоуровневая верификация гостей. Отсутствие случайных лиц на локации.'
		},
		{
			number: '04',
			title: 'Скрытая логистика',
			description:
				'Приватные трансферы, отдельные входы для VIP-персон и полная изоляция периметра.'
		}
	];

	const formats = [
		{
			title: 'Корпоративные события',
			description: 'Стратегические сессии и закрытые форумы для топ-менеджмента.',
			wide: true
		},
		{ title: 'Частные', description: 'Юбилеи и ужины вне чужих глаз.' },
		{ title: 'VIP & Protocol', description: 'Встречи первых лиц и делегаций с соблюдением протокола.' },
		{
			title: 'Архитектура "Под ключ"',
			description:
				'Полный цикл: от разработки концепции до технического продакшена (High-end звук и свет).',
			wide: true
		}
	];

	const archives = [
		{
			id: 'Case #042 • Swiss Alps',
			title: 'Private Summit',
			description: '3 дня. 40 гостей. Абсолютная изоляция. Сложная застройка в горной местности.'
		},
		{
			id: 'Case #089 • Dubai',
			title: 'Corporate Board',
			description:
				'Презентация стратегии для совета директоров. Технический продакшн высочайшего уровня.'
		},
		{
			id: 'Case #112 • Moscow',
			title: 'Closed Gala',
			description:
				'Событие для списка Forbes. Жесткий регламент доступа и запрет на мобильные устройства.'
		}
	];

	const stats = [
		{ value: 50, label: 'Мероприятий', suffix: '' },
		{ value: 7, label: 'Лет опыта', suffix: '+' },
		{ value: 100, label: 'NDA проектов', suffix: '%' },
		{ value: 85, label: 'Повторных клиентов', suffix: '%' }
	];

	const faqs = [
		{
			q: 'Вы подписываете NDA?',
			a: 'Да. NDA — это первый документ, который мы подписываем до обсуждения вводных данных, локации и формата мероприятия.'
		},
		{
			q: 'Как контролируется фото и видео?',
			a: 'Мы внедряем стикеры для камер, камеры хранения для техники и выделенную службу безопасности в зале.'
		},
		{
			q: 'Публикуете ли вы материалы?',
			a: 'Нет. Все права на медиаматериалы принадлежат клиенту. Любые публикации возможны только с письменного согласия.'
		}
	];

	onMount(() => {
		const cursor = document.getElementById('cursor');
		const hoverTargets = document.querySelectorAll('.hover-target, a, button, summary');
		const revealNodes = document.querySelectorAll('.reveal');
		const counterNodes = document.querySelectorAll('.counter');

		const onMove = (e) => {
			if (!cursor) return;
			cursor.style.left = `${e.clientX}px`;
			cursor.style.top = `${e.clientY}px`;
		};

		document.addEventListener('mousemove', onMove);

		hoverTargets.forEach((target) => {
			target.addEventListener('mouseenter', () => cursor?.classList.add('cursor-hover'));
			target.addEventListener('mouseleave', () => cursor?.classList.remove('cursor-hover'));
		});

		const revealObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) entry.target.classList.add('active');
				});
			},
			{ threshold: 0.1, rootMargin: '0px 0px -50px 0px' }
		);
		revealNodes.forEach((node) => revealObserver.observe(node));

		const counterObserver = new IntersectionObserver(
			(entries, observer) => {
				entries.forEach((entry) => {
					if (!entry.isIntersecting) return;
					const target = entry.target;
					const endValue = Number(target.getAttribute('data-target'));
					let startValue = 0;
					const duration = 2000;
					const increment = endValue / (duration / 16);

					const update = () => {
						startValue += increment;
						if (startValue < endValue) {
							target.textContent = String(Math.ceil(startValue));
							requestAnimationFrame(update);
						} else {
							target.textContent = String(endValue);
						}
					};
					update();
					observer.unobserve(target);
				});
			},
			{ threshold: 0.5 }
		);

		counterNodes.forEach((node) => counterObserver.observe(node));

		return () => {
			document.removeEventListener('mousemove', onMove);
			revealObserver.disconnect();
			counterObserver.disconnect();
		};
	});
</script>

<div class="app">
	<div class="noise-overlay"></div>
	<div id="cursor"></div>

	<nav class="top-nav">
		<div class="logo">Planeta</div>
		<a href="#contact" class="hover-target nav-link">Запросить доступ</a>
	</nav>

	<section class="hero section">
		<div class="hero-content">
			<h1 class="hero-title reveal active">Закрытые мероприятия <br /><span>без огласки</span></h1>
			<p class="hero-text reveal active">
				Организация премиальных событий для тех, кто ценит абсолютную приватность и
				безупречный уровень исполнения.
			</p>
			<div class="hero-actions reveal active">
				<a href="#contact" class="hover-target btn btn-primary">Обсудить проект</a>
				<a href="#faq" class="hover-target btn btn-outline">Запросить NDA</a>
			</div>
		</div>
		<div class="hero-line"></div>
	</section>

	<section class="section section-protocols">
		<div class="container protocol-grid">
			{#each protocols as item, idx}
				<article class="panel reveal" style={`transition-delay:${idx * 0.1}s`}>
					<div class="panel-number">{item.number}</div>
					<h3>{item.title}</h3>
					<p>{item.description}</p>
				</article>
			{/each}
		</div>
	</section>

	<section class="section container formats">
		<h2 class="section-title reveal">Форматы</h2>
		<div class="formats-grid">
			{#each formats as item, idx}
				<article class={`panel format-card reveal ${item.wide ? 'wide' : ''}`} style={`transition-delay:${idx * 0.1}s`}>
					<h3>{item.title}</h3>
					<p>{item.description}</p>
				</article>
			{/each}
		</div>
	</section>

	<section class="section section-archive">
		<div class="container archive-head reveal">
			<h2 class="section-title">Архив</h2>
			<span>Client names redacted</span>
		</div>
		<div class="archive-track">
			{#each archives as item}
				<article class="panel archive-card">
					<div class="archive-overlay"></div>
					<div class="archive-content">
						<p>{item.id}</p>
						<h3>{item.title}</h3>
						<span>{item.description}</span>
					</div>
				</article>
			{/each}
		</div>
	</section>

	<section class="section statement reveal">
		<h2 class="hero-title">Всё остаётся <br /><span>внутри.</span></h2>
		<p>
			Мы защищаем вашу репутацию, информацию и покой гостей. То, что происходит на наших
			событиях, принадлежит только вам.
		</p>
	</section>

	<section class="section section-stats">
		<div class="container stats-grid">
			{#each stats as item, idx}
				<div class="reveal" style={`transition-delay:${idx * 0.1}s`}>
					<div class="stat-value">
						<span class="counter" data-target={item.value}>0</span>{item.suffix}
					</div>
					<div class="stat-label">{item.label}</div>
				</div>
			{/each}
		</div>
	</section>

	<section class="section container reveal">
		<div class="panel status-card">
			<div class="status-glow"></div>
			<div class="status-main">
				<h2>Особый статус</h2>
				<p>
					Мы умеем работать со статусными персонами, Special Guests и топ-артистами в условиях
					повышенного внимания.
				</p>
			</div>
			<div class="status-list">
				<p>• VIP Logistics</p>
				<p>• Rider Management</p>
				<p>• Security Protocol</p>
			</div>
		</div>
	</section>

	<section class="section section-reviews">
		<div class="container">
			<h2 class="section-title reveal">Репутация</h2>
			<div class="reviews-list">
				<blockquote class="reveal">
					<p>
						«Идеальная точность. Технический продакшн работает как швейцарские часы, а о самом
						факте мероприятия не знает никто за пределами зала».
					</p>
					<cite>— CEO, Tech Corporation</cite>
				</blockquote>
				<blockquote class="reveal">
					<p>
						«Поразительная деликатность команды. Они невидимы, но контролируют каждую секунду
						события».
					</p>
					<cite>— Private Client</cite>
				</blockquote>
			</div>
		</div>
	</section>

	<section id="faq" class="section container reveal">
		<h2 class="section-title">Протокол работы</h2>
		<div class="faq-list">
			{#each faqs as item}
				<details class="panel">
					<summary class="hover-target">{item.q}<span>+</span></summary>
					<div>{item.a}</div>
				</details>
			{/each}
		</div>
	</section>

	<section id="contact" class="section section-contact">
		<div class="contact-glow"></div>
		<div class="contact-content reveal">
			<h2 class="section-title">Инициировать проект</h2>
			<p>Оставьте контакты для защищенной связи. Ваш запрос строго конфиденциален.</p>
			<form class="contact-form" on:submit|preventDefault>
				<input type="text" placeholder="Имя / Должность" required />
				<input type="text" placeholder="Удобный мессенджер (Telegram / WhatsApp)" required />
				<button type="submit" class="hover-target btn btn-primary">Отправить запрос</button>
			</form>
		</div>
	</section>

	<footer class="footer">
		<div class="container footer-grid">
			<div class="logo">Planeta</div>
			<div class="footer-links">
				<a href="/services" class="hover-target">Услуги</a>
				<a href="#faq" class="hover-target">FAQ</a>
				<a href="/nda-policy" class="hover-target">NDA Policy</a>
			</div>
			<div>© 2026 Planeta. Silence is the new gold.</div>
		</div>
	</footer>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&family=Syncopate:wght@400;700&display=swap');

	:global(html) {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		background: #000;
		color: #fff;
		font-family: Inter, sans-serif;
		overflow-x: hidden;
		cursor: none;
	}

	.app {
		--bg: #000;
		--surface: #0a0a0a;
		--border: rgba(255, 255, 255, 0.1);
		--text-muted: rgba(255, 255, 255, 0.5);
		position: relative;
	}

	.container {
		max-width: 1280px;
		margin: 0 auto;
		padding: 0 24px;
	}

	.section {
		padding: 96px 0;
	}

	.noise-overlay {
		position: fixed;
		inset: 0;
		z-index: 50;
		pointer-events: none;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
		opacity: 0.03;
		mix-blend-mode: overlay;
	}

	#cursor {
		width: 8px;
		height: 8px;
		background: #fff;
		border-radius: 50%;
		position: fixed;
		pointer-events: none;
		z-index: 9999;
		mix-blend-mode: difference;
		transform: translate(-50%, -50%);
		transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1), background 0.2s ease;
	}

	.cursor-hover {
		transform: translate(-50%, -50%) scale(5) !important;
		background: rgba(255, 255, 255, 0.5) !important;
	}

	.top-nav {
		position: fixed;
		inset: 0 0 auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 24px 40px;
		z-index: 60;
		mix-blend-mode: difference;
	}

	.logo,
	.section-title,
	h3,
	summary,
	.stat-value {
		font-family: Syncopate, sans-serif;
		text-transform: uppercase;
	}

	.logo {
		font-size: clamp(20px, 2vw, 32px);
	}

	.nav-link {
		font-size: 11px;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: #fff;
		text-decoration: none;
		opacity: 0.7;
	}

	.hero {
		min-height: 100vh;
		display: grid;
		place-items: center;
		padding-inline: 24px;
	}

	.hero-content {
		max-width: 980px;
		text-align: center;
	}

	.hero-title {
		font-family: Syncopate, sans-serif;
		font-size: clamp(38px, 7vw, 92px);
		line-height: 1.1;
		text-transform: uppercase;
		margin: 0;
	}

	.hero-title span {
		opacity: 0.4;
	}

	.hero-text,
	.statement p,
	.contact-content p {
		max-width: 720px;
		margin: 24px auto 0;
		font-size: clamp(14px, 1.3vw, 18px);
		line-height: 1.7;
		color: var(--text-muted);
	}

	.hero-actions {
		margin-top: 40px;
		display: flex;
		gap: 16px;
		justify-content: center;
		flex-wrap: wrap;
	}

	.btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: 16px 32px;
		text-decoration: none;
		font-size: 12px;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		border: 1px solid var(--border);
		background: transparent;
		color: #fff;
	}

	.btn-primary {
		background: #fff;
		color: #000;
		border-color: #fff;
	}

	.btn-outline:hover,
	.btn-primary:hover {
		transform: translateY(-2px);
	}

	.hero-line {
		position: absolute;
		bottom: 40px;
		left: 50%;
		width: 1px;
		height: 64px;
		background: linear-gradient(180deg, rgba(255, 255, 255, 0.3) 0%, transparent 100%);
	}

	.section-protocols,
	.section-stats,
	.section-reviews {
		border-top: 1px solid var(--border);
	}

	.protocol-grid {
		display: grid;
		grid-template-columns: repeat(4, minmax(0, 1fr));
		gap: 1px;
		background: var(--border);
	}

	.panel {
		background: var(--surface);
		border: 1px solid var(--border);
		padding: 36px;
		transition: border-color 0.4s ease;
	}

	.panel:hover {
		border-color: rgba(255, 255, 255, 0.3);
	}

	.panel-number {
		font-family: Syncopate, sans-serif;
		font-size: 12px;
		opacity: 0.5;
		margin-bottom: 16px;
	}

	.panel h3 {
		font-size: 14px;
		margin: 0 0 16px;
	}

	.panel p,
	.panel span,
	.archive-head span,
	.stat-label,
	.footer {
		font-size: 12px;
		font-weight: 300;
		color: var(--text-muted);
		line-height: 1.7;
	}

	.formats {
		max-width: 1280px;
	}

	.section-title {
		text-align: center;
		font-size: clamp(28px, 4vw, 54px);
		margin: 0 0 48px;
	}

	.formats-grid {
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 16px;
	}

	.format-card {
		min-height: 280px;
		display: flex;
		flex-direction: column;
		justify-content: flex-end;
	}

	.format-card.wide {
		grid-column: span 2;
	}

	.section-archive,
	.section-contact {
		background: #050505;
		border-top: 1px solid var(--border);
		border-bottom: 1px solid var(--border);
	}

	.archive-head {
		display: flex;
		justify-content: space-between;
		align-items: end;
		margin-bottom: 40px;
	}

	.archive-track {
		display: flex;
		gap: 24px;
		overflow-x: auto;
		padding: 0 24px 20px;
		scroll-snap-type: x mandatory;
	}

	.archive-card {
		position: relative;
		min-width: min(85vw, 600px);
		height: 500px;
		scroll-snap-align: center;
		overflow: hidden;
	}

	.archive-overlay {
		position: absolute;
		inset: 0;
		background: rgba(255, 255, 255, 0.05);
		opacity: 0;
		transition: opacity 0.7s;
	}

	.archive-card:hover .archive-overlay {
		opacity: 1;
	}

	.archive-content {
		position: absolute;
		left: 0;
		right: 0;
		bottom: 0;
		padding: 32px;
		background: linear-gradient(180deg, transparent 0%, rgba(0, 0, 0, 0.85) 65%);
	}

	.archive-content p {
		font-family: Syncopate, sans-serif;
		font-size: 10px;
		margin: 0 0 8px;
		letter-spacing: 0.14em;
		text-transform: uppercase;
	}

	.archive-content h3 {
		font-size: 18px;
		margin: 0 0 8px;
	}

	.statement {
		text-align: center;
	}

	.stats-grid {
		display: grid;
		grid-template-columns: repeat(4, minmax(0, 1fr));
		gap: 24px;
		text-align: center;
	}

	.stat-value {
		font-size: clamp(40px, 5vw, 74px);
	}

	.stat-label {
		margin-top: 10px;
		text-transform: uppercase;
		letter-spacing: 0.2em;
	}

	.status-card {
		position: relative;
		overflow: hidden;
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 24px;
	}

	.status-glow {
		position: absolute;
		inset: 0;
		background: radial-gradient(ellipse at center, rgba(255, 255, 255, 0.06), #000 70%);
	}

	.status-main,
	.status-list {
		position: relative;
		z-index: 1;
	}

	.status-main h2 {
		font-family: Syncopate, sans-serif;
		text-transform: uppercase;
		font-size: clamp(24px, 3vw, 42px);
		margin: 0 0 16px;
	}

	.status-list {
		font-family: Syncopate, sans-serif;
		font-size: 10px;
		text-transform: uppercase;
		letter-spacing: 0.2em;
		opacity: 0.6;
	}

	.reviews-list {
		display: grid;
		gap: 48px;
		max-width: 900px;
		margin: 0 auto;
	}

	blockquote {
		margin: 0;
		padding-left: 24px;
		border-left: 1px solid rgba(255, 255, 255, 0.2);
	}

	blockquote p {
		font-size: clamp(18px, 2.2vw, 30px);
		font-style: italic;
		line-height: 1.5;
		margin: 0 0 14px;
	}

	cite {
		font-family: Syncopate, sans-serif;
		text-transform: uppercase;
		font-size: 10px;
		opacity: 0.4;
	}

	.faq-list {
		display: grid;
		gap: 16px;
	}

	details > summary {
		list-style: none;
		cursor: none;
		display: flex;
		justify-content: space-between;
		align-items: center;
		font-size: 14px;
		padding: 20px;
	}

	details > summary::-webkit-details-marker {
		display: none;
	}

	details[open] summary ~ * {
		animation: sweep 0.5s ease-in-out;
	}

	@keyframes sweep {
		0% {
			opacity: 0;
			transform: translateY(-10px);
		}
		100% {
			opacity: 1;
			transform: translateY(0);
		}
	}

	details div {
		padding: 0 20px 20px;
	}

	.section-contact {
		position: relative;
		text-align: center;
	}

	.contact-glow {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: min(800px, 90vw);
		height: min(800px, 90vw);
		background: rgba(255, 255, 255, 0.05);
		border-radius: 50%;
		filter: blur(100px);
		pointer-events: none;
	}

	.contact-content {
		position: relative;
		z-index: 1;
		max-width: 760px;
		margin: 0 auto;
		padding-inline: 24px;
	}

	.contact-form {
		display: grid;
		gap: 16px;
		margin-top: 28px;
	}

	input {
		width: 100%;
		background: transparent;
		border: 0;
		border-bottom: 1px solid rgba(255, 255, 255, 0.2);
		padding: 16px;
		color: #fff;
		font-size: 14px;
	}

	input:focus {
		outline: none;
		border-color: #fff;
	}

	.footer {
		padding: 40px 0;
		border-top: 1px solid var(--border);
	}

	.footer-grid {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 16px;
	}

	.footer-links {
		display: flex;
		gap: 24px;
	}

	a {
		color: inherit;
	}

	.reveal {
		opacity: 0;
		transform: translateY(30px);
		transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.reveal.active {
		opacity: 1;
		transform: translateY(0);
	}

	@media (max-width: 1024px) {
		:global(body) {
			cursor: auto;
		}

		#cursor {
			display: none;
		}

		details > summary {
			cursor: pointer;
		}

		.top-nav {
			padding: 18px 16px;
		}

		.section {
			padding: 72px 0;
		}

		.protocol-grid,
		.stats-grid,
		.formats-grid {
			grid-template-columns: 1fr;
		}

		.format-card.wide {
			grid-column: auto;
		}

		.status-card,
		.footer-grid {
			flex-direction: column;
			align-items: flex-start;
		}

		.footer-links {
			display: none;
		}
	}
</style>
