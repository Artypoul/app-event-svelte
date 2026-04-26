<script>
	import { onMount } from 'svelte';

	const protocols = [
		{
			id: '01',
			title: 'Immediate NDA',
			description:
				'Соглашение о неразглашении подписывается до первой встречи. Ваши данные защищены мгновенно.'
		},
		{
			id: '02',
			title: 'Signal Blocker',
			description:
				'Техническое отключение камер, блокировка сигналов и изъятие устройств по запросу клиента.'
		},
		{
			id: '03',
			title: 'Vetted Staff',
			description:
				'Персонал проходит многоуровневую проверку безопасности и жесткий инструктаж.'
		},
		{
			id: '04',
			title: 'Zero Trace',
			description:
				'Полное удаление цифрового следа события: отсутствие геолокации, фотоотчетов и упоминаний.'
		}
	];

	const expertise = [
		{
			title: 'Corporate Worlds',
			description: 'Стратегические сессии и закрытые форумы для тех, кто управляет рынками.',
			image:
				'https://images.unsplash.com/photo-1582213726895-3b03697e88d8?q=80&w=1000&auto=format&fit=crop'
		},
		{
			title: 'Private Realms',
			description: 'Юбилеи и ужины в кругу доверенных лиц, скрытые от посторонних глаз.',
			image:
				'https://images.unsplash.com/photo-1549416878-b9ca95e26903?q=80&w=1000&auto=format&fit=crop'
		},
		{
			title: 'High-End Production',
			description: 'Собственный парк оборудования. Звук и свет уровня мировых звезд.',
			image:
				'https://images.unsplash.com/photo-1598463349603-99b38f8303f5?q=80&w=1000&auto=format&fit=crop',
			highlight: true
		}
	];

	const counters = [
		{ value: 70, label: 'Events', gold: true },
		{ value: 8, label: 'Years' },
		{ value: 100, label: 'NDA Strict' },
		{ value: 90, label: 'Returning' }
	];

	onMount(() => {
		const cursor = document.getElementById('cursor');
		const hoverTargets = document.querySelectorAll('.hover-target, a, button, summary');
		const revealElements = document.querySelectorAll('.reveal');
		const counterElements = document.querySelectorAll('.counter');

		const onMove = (event) => {
			if (!cursor) return;
			cursor.style.left = `${event.clientX}px`;
			cursor.style.top = `${event.clientY}px`;
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
			{ threshold: 0.15, rootMargin: '0px 0px -50px 0px' }
		);

		revealElements.forEach((el) => revealObserver.observe(el));

		const counterObserver = new IntersectionObserver(
			(entries, observer) => {
				entries.forEach((entry) => {
					if (!entry.isIntersecting) return;
					const node = entry.target;
					const end = Number(node.getAttribute('data-target') || 0);
					let current = 0;
					const duration = 2500;
					const increment = end / (duration / 16);

					const tick = () => {
						current += increment;
						if (current < end) {
							node.textContent = String(Math.ceil(current));
							requestAnimationFrame(tick);
						} else {
							node.textContent = `${end}+`;
						}
					};

					tick();
					observer.unobserve(node);
				});
			},
			{ threshold: 0.7 }
		);

		counterElements.forEach((el) => counterObserver.observe(el));

		return () => {
			document.removeEventListener('mousemove', onMove);
			revealObserver.disconnect();
			counterObserver.disconnect();
		};
	});
</script>

<div class="page noise">
	<div id="cursor"></div>

	<nav class="top-nav">
		<div class="logo">Planeta</div>
		<a href="#contact" class="hover-target nav-link">Initiate Protocol</a>
	</nav>

	<section class="hero">
		<img
			src="https://images.unsplash.com/photo-1517457373958-b7bdd4587205?q=80&w=2560&auto=format&fit=crop"
			alt="Hero Background"
			class="hero-bg"
		/>
		<div class="hero-overlay"></div>
		<div class="hero-content">
			<h1 class="reveal-text">
				Closed Events <br /><span>Without a Trace</span>
			</h1>
			<p class="hero-subtitle reveal">Absolute discretion for private and corporate gatherings.</p>
			<div class="hero-actions reveal">
				<a href="#contact" class="btn btn-light hover-target">Обсудить</a>
				<a href="#faq" class="btn btn-outline hover-target">Запросить NDA</a>
			</div>
		</div>
	</section>

	<section class="protocols">
		<div class="protocol-grid">
			{#each protocols as item, idx}
				<article class="protocol-card glow-border reveal" style={`transition-delay:${idx * 0.1}s`}>
					<h3>Protocol {item.id}</h3>
					<h4>{item.title}</h4>
					<p>{item.description}</p>
				</article>
			{/each}
		</div>
	</section>

	<section class="expertise-section">
		<h2 class="section-title reveal">Areas of Expertise</h2>
		<div class="expertise-grid">
			{#each expertise as item, idx}
				<article class="expertise-card glow-border reveal" style={`transition-delay:${idx * 0.2}s`}>
					<img src={item.image} alt={item.title} class="premium-img" />
					<div class="card-overlay"></div>
					<div class="card-content">
						<h3 class:gold={item.highlight}>{item.title}</h3>
						<p>{item.description}</p>
					</div>
				</article>
			{/each}
		</div>
	</section>

	<section class="quote-section reveal">
		<h2>Great Events <br /><span>Require Silence.</span></h2>
	</section>

	<section class="counter-section">
		<div class="counter-grid">
			{#each counters as item, idx}
				<div class="counter-item reveal" style={`transition-delay:${idx * 0.1}s`}>
					<div class={`counter font-sync ${item.gold ? 'gold' : ''}`} data-target={item.value}>0</div>
					<div class="counter-label">{item.label}</div>
				</div>
			{/each}
		</div>
	</section>

	<section id="faq" class="faq-section reveal">
		<h2 class="section-title">Operation Protocol</h2>
		<details class="glow-border">
			<summary class="hover-target">Do you provide Immediate NDA?<span>+</span></summary>
			<div>Yes. Agreement is signed before the first detailed discussion.</div>
		</details>
		<details class="glow-border">
			<summary class="hover-target">How is device usage managed?<span>+</span></summary>
			<div>Camera stickers, secure storage lockers, and on-site monitoring.</div>
		</details>
	</section>

	<section id="contact" class="contact-section">
		<img
			src="https://images.unsplash.com/photo-1599675308696-65103a8df45d?q=80&w=2000&auto=format&fit=crop"
			alt="Contact"
			class="contact-bg"
		/>
		<div class="contact-overlay"></div>
		<div class="contact-content reveal">
			<h2>Initiate <span>Dial</span></h2>
			<p>Secure channel activation.</p>
			<form class="contact-form" on:submit|preventDefault>
				<input type="text" placeholder="Identity / Position" required />
				<input type="text" placeholder="Secure Messenger (Telegram / Signal)" required />
				<button class="btn btn-light hover-target" type="submit">Request Secure Call</button>
			</form>
		</div>
	</section>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Inter:wght@200;300;400;600&family=Syncopate:wght@400;700&display=swap');

	:global(html) {
		scroll-behavior: smooth;
	}

	:global(body) {
		margin: 0;
		font-family: Inter, sans-serif;
		background: #000;
		color: #fff;
		overflow-x: hidden;
		cursor: none;
	}

	.page {
		--gold: #c5a059;
		--border: rgba(255, 255, 255, 0.08);
		position: relative;
		background: #000;
	}

	.noise::before {
		content: '';
		position: fixed;
		inset: 0;
		background: url('https://grainy-gradients.vercel.app/noise.svg');
		opacity: 0.04;
		pointer-events: none;
		z-index: 50;
	}

	#cursor {
		width: 10px;
		height: 10px;
		background: #fff;
		border-radius: 50%;
		position: fixed;
		pointer-events: none;
		z-index: 9999;
		mix-blend-mode: difference;
		transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
		transform: translate(-50%, -50%);
	}

	.cursor-hover {
		transform: translate(-50%, -50%) scale(6) !important;
		background: rgba(255, 255, 255, 0.2) !important;
	}

	.top-nav {
		position: fixed;
		inset: 0 0 auto 0;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 24px 32px;
		z-index: 60;
		mix-blend-mode: difference;
	}

	.logo,
	.font-sync {
		font-family: Syncopate, sans-serif;
	}

	.logo {
		font-size: 28px;
		text-transform: uppercase;
	}

	.nav-link {
		font-size: 11px;
		letter-spacing: 0.3em;
		text-transform: uppercase;
		text-decoration: none;
		color: #fff;
		opacity: 0.75;
	}

	section {
		position: relative;
	}

	.hero {
		height: 100vh;
		display: grid;
		place-items: center;
		text-align: center;
		padding: 24px;
		overflow: hidden;
	}

	.hero-bg,
	.contact-bg {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.hero-bg {
		filter: brightness(0.2);
	}

	.hero-overlay,
	.contact-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(180deg, #000 0%, transparent 45%, #000 100%);
	}

	.hero-content {
		position: relative;
		z-index: 1;
		max-width: 980px;
	}

	h1 {
		font-family: Syncopate, sans-serif;
		font-size: clamp(40px, 7vw, 112px);
		text-transform: uppercase;
		line-height: 1.1;
		margin: 0;
	}

	h1 span,
	.quote-section span,
	.contact-content h2 span,
	.gold {
		color: var(--gold);
	}

	.hero-subtitle {
		margin: 24px auto 40px;
		max-width: 620px;
		font-size: 14px;
		color: rgba(255, 255, 255, 0.6);
	}

	.hero-actions {
		display: flex;
		justify-content: center;
		gap: 16px;
		flex-wrap: wrap;
	}

	.btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		text-decoration: none;
		padding: 18px 32px;
		font-size: 11px;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.2em;
		border: 1px solid transparent;
	}

	.btn-light {
		background: #fff;
		color: #000;
	}

	.btn-outline {
		border-color: rgba(255, 255, 255, 0.2);
		color: #fff;
	}

	.protocols,
	.counter-section,
	.faq-section {
		padding: 96px 24px;
		background: #080808;
		border-top: 1px solid rgba(255, 255, 255, 0.05);
	}

	.protocol-grid,
	.counter-grid {
		max-width: 1280px;
		margin: 0 auto;
		display: grid;
		grid-template-columns: repeat(4, minmax(0, 1fr));
		gap: 1px;
		background: rgba(255, 255, 255, 0.05);
	}

	.protocol-card {
		background: #000;
		padding: 48px;
	}

	.protocol-card h3 {
		font-family: Syncopate, sans-serif;
		font-size: 12px;
		letter-spacing: 0.14em;
		text-transform: uppercase;
		color: var(--gold);
		margin: 0 0 16px;
	}

	.protocol-card h4 {
		font-size: 28px;
		font-weight: 300;
		margin: 0 0 14px;
	}

	.protocol-card p,
	.card-content p,
	.counter-label,
	.faq-section div {
		font-size: 12px;
		line-height: 1.8;
		color: rgba(255, 255, 255, 0.55);
	}

	.expertise-section {
		max-width: 1280px;
		margin: 0 auto;
		padding: 120px 24px;
	}

	.section-title {
		font-family: Syncopate, sans-serif;
		text-align: center;
		text-transform: uppercase;
		font-size: clamp(28px, 4vw, 52px);
		margin: 0 0 64px;
	}

	.expertise-grid {
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 20px;
	}

	.expertise-card {
		position: relative;
		min-height: 560px;
		overflow: hidden;
	}

	.premium-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		filter: grayscale(100%) brightness(50%) contrast(120%);
		transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.expertise-card:hover .premium-img {
		filter: grayscale(0%) brightness(70%) contrast(100%);
		transform: scale(1.05);
	}

	.card-overlay {
		position: absolute;
		inset: 0;
		background: linear-gradient(0deg, rgba(0, 0, 0, 0.92) 0%, rgba(0, 0, 0, 0.35) 100%);
	}

	.card-content {
		position: absolute;
		z-index: 1;
		left: 32px;
		right: 32px;
		bottom: 32px;
	}

	.card-content h3 {
		font-family: Syncopate, sans-serif;
		font-size: 24px;
		text-transform: uppercase;
		margin: 0 0 12px;
	}

	.quote-section {
		padding: 180px 24px;
		text-align: center;
	}

	.quote-section h2,
	.contact-content h2 {
		font-family: Syncopate, sans-serif;
		text-transform: uppercase;
		font-size: clamp(36px, 5vw, 82px);
		line-height: 1.15;
		margin: 0;
	}

	.counter-item {
		background: #000;
		padding: 36px 12px;
		text-align: center;
	}

	.counter {
		font-size: clamp(42px, 6vw, 88px);
		margin-bottom: 8px;
	}

	.counter-label {
		text-transform: uppercase;
		letter-spacing: 0.24em;
	}

	.faq-section {
		max-width: 980px;
		margin: 0 auto;
		background: transparent;
	}

	details {
		background: #000;
		border: 1px solid var(--border);
		margin-bottom: 12px;
	}

	summary {
		list-style: none;
		padding: 26px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		text-transform: uppercase;
		font-family: Syncopate, sans-serif;
		font-size: 14px;
		cursor: none;
	}

	details div {
		padding: 0 26px 26px;
	}

	.contact-section {
		padding: 160px 24px;
		border-top: 1px solid rgba(255, 255, 255, 0.05);
		overflow: hidden;
	}

	.contact-bg {
		filter: brightness(0.1);
	}

	.contact-content {
		position: relative;
		z-index: 1;
		text-align: center;
		max-width: 700px;
		margin: 0 auto;
	}

	.contact-content p {
		font-size: 12px;
		letter-spacing: 0.04em;
		color: rgba(255, 255, 255, 0.6);
		margin: 20px auto 40px;
	}

	.contact-form {
		display: grid;
		gap: 16px;
	}

	input {
		background: transparent;
		border: 0;
		border-bottom: 1px solid rgba(255, 255, 255, 0.12);
		color: #fff;
		padding: 18px;
		font-size: 12px;
		text-transform: uppercase;
		letter-spacing: 0.14em;
	}

	input:focus {
		outline: none;
		border-color: var(--gold);
	}

	.reveal {
		opacity: 0;
		transform: translateY(40px);
		transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.reveal.active {
		opacity: 1;
		transform: translateY(0);
	}

	@keyframes textReveal {
		to {
			clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
			transform: translateY(0);
		}
	}

	.reveal-text {
		clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0 100%);
		transform: translateY(30px);
		animation: textReveal 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
	}

	.glow-border {
		border: 1px solid var(--border);
		transition: border-color 0.5s ease;
	}

	.glow-border:hover {
		border-color: rgba(197, 160, 89, 0.5);
	}

	@media (max-width: 1024px) {
		:global(body) {
			cursor: auto;
		}

		#cursor {
			display: none;
		}

		.top-nav {
			padding: 20px 16px;
		}

		.protocol-grid,
		.counter-grid,
		.expertise-grid {
			grid-template-columns: 1fr;
		}

		.protocol-card,
		.counter-item,
		.expertise-card {
			min-height: auto;
		}

		summary {
			cursor: pointer;
		}
	}
</style>
