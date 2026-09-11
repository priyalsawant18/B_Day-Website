<doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#4b2630">
  <meta name="description" content="A personal birthday memory experience.">
  <title>For You ✨ | A Little Celebration...✨</title>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@500;600;700&family=DM+Sans:wght@400;500;600;700&family=Caveat:wght@500;600&display=swap" rel="stylesheet">

  <style>
    /* ============================================================
       MASTER STYLESHEET
       ============================================================ */
    :root {
      --burgundy: #4b2630;
      --burgundy-dark: #29161c;
      --terracotta: #a65f4f;
      --terracotta-light: #c48270;
      --dusty-rose: #c9958d;
      --cream: #f6eee2;
      --cream-dark: #eadcca;
      --beige: #d9c4aa;
      --sage: #87917b;
      --charcoal: #292526;
      --brown: #654d42;
      --gold: #c8a96b;
      --white: #fffaf3;
      --shadow: 0 20px 60px rgba(41, 22, 28, .16);
      --serif: "Cormorant Garamond", Georgia, serif;
      --sans: "DM Sans", Arial, sans-serif;
      --hand: "Caveat", cursive;
      --radius: 22px;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body { background: var(--cream); color: var(--charcoal); font-family: var(--sans); overflow-x: hidden; }
    button, a { font: inherit; }
    button { border: 0; cursor: pointer; }
    img { max-width: 100%; display: block; }

    .grain {
      position: fixed; inset: 0; z-index: 100; pointer-events: none; opacity: .055;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.7'/%3E%3C/svg%3E");
    }        

    .floating-particles { position: fixed; inset: 0; pointer-events: none; z-index: 1; }
    .particle {
      position: absolute; width: 4px; height: 4px; border-radius: 50%; background: var(--gold); opacity: .4; animation: floatParticle linear infinite;
    }
    @keyframes floatParticle {
      from { transform: translateY(110vh); }
      to { transform: translateY(-10vh); }
    }

    /* NAVIGATION */
    .site-header {
      position: fixed; top: 0; left: 0; width: 100%; height: 72px;
      display: flex; align-items: center; justify-content: space-between; padding: 0 5vw; z-index: 90;
      transition: background .10s ease, backdrop-filter .10s ease;
    }
    .site-header.scrolled { background: rgba(246, 238, 226, .82); backdrop-filter: blur(18px); }
    .logo { width: 38px; height: 38px; display: grid; place-items: center; color: var(--gold); text-decoration: none; border: 1px solid rgba(200, 169, 107, .5); border-radius: 50%; }
    .desktop-nav { display: flex; gap: 24px; }
    .desktop-nav a { color: inherit; text-decoration: none; font-size: 10px; letter-spacing: .12em; font-weight: 700; opacity: .65; transition: opacity .10s ease; }
    .desktop-nav a:hover { opacity: 1; }
    .music-btn, .menu-btn { width: 40px; height: 40px; display: grid; place-items: center; border-radius: 50%; background: rgba(255,255,255,.15); color: inherit; }
    .menu-btn { display: none; }

    .mobile-menu {
      position: fixed; inset: 0; background: var(--burgundy-dark); color: var(--cream); z-index: 200;
      display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 26px;
      transform: translateX(100%); transition: transform .5s cubic-bezier(.77,0,.18,1);
    }
    .mobile-menu.open { transform: translateX(0); }
    .mobile-menu a { color: var(--cream); text-decoration: none; font-size: 15px; letter-spacing: .15em; }
    .close-menu { position: absolute; top: 25px; right: 25px; background: none; color: var(--cream); font-size: 35px; }

    /* CHAPTERS */
    .chapter { position: relative; min-height: 100vh; padding: 130px 8vw; overflow: hidden; }
    .eyebrow { display: block; text-transform: uppercase; letter-spacing: .18em; font-size: 10px; font-weight: 700; opacity: .65; }
    .section-number { display: inline-block; font-size: 11px; letter-spacing: .15em; color: var(--gold); margin-bottom: 12px; }
    .section-heading { display: flex; gap: 30px; align-items: flex-start; margin-bottom: 80px; }
    .section-heading h2 { font-family: var(--serif); font-size: clamp(48px, 7vw, 100px); line-height: .85; font-weight: 600; }
    .section-heading.centered { display: block; text-align: center; }

    .reveal { opacity: 0; transform: translateY(35px); transition: opacity .8s ease, transform .8s cubic-bezier(.2,.7,.2,1); }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    .primary-btn {
      display: inline-flex; align-items: center; justify-content: center; gap: 15px; padding: 16px 25px;
      border-radius: 100px; background: var(--cream); color: var(--burgundy); font-weight: 700; box-shadow: var(--shadow);
      transition: transform .25s ease, box-shadow .25s ease;
    }
    .primary-btn:hover { transform: translateY(-3px); box-shadow: 0 25px 60px rgba(41,22,28,.22); }

    /* INTRO */
    .intro {
      min-height: 100svh; display: grid; place-items: center; text-align: center;
      background: radial-gradient(circle at 30% 20%, rgba(200,169,107,.16), transparent 30%), linear-gradient(135deg, var(--burgundy-dark), var(--burgundy), var(--terracotta));
      color: var(--cream);
    }
    .intro-inner { max-width: 850px; }
    .intro-title { font-family: var(--serif); font-size: clamp(60px, 11vw, 150px); line-height: .8; margin: 28px 0; font-weight: 500; }
    .intro-title span { color: var(--dusty-rose); }
    .intro-subtitle { font-size: clamp(16px, 2vw, 22px); margin-bottom: 8px; }
    .marathi-line { color: var(--beige); margin-bottom: 35px; }
    .intro-reveal { max-height: 0; overflow: hidden; opacity: 0; transition: max-height 1s ease, opacity .8s ease; }
    .intro-reveal.show { max-height: 250px; opacity: 1; margin-top: 45px; }
    .intro-reveal p { font-family: var(--serif); font-size: 30px; margin-bottom: 10px; }
    .intro-reveal strong { color: var(--dusty-rose); font-size: 18px; }
    .reveal-line { width: 1px; height: 60px; background: var(--gold); margin: auto auto 20px; }
   
    /* QUESTION SECTION */
    .question-section { background: var(--cream); display: flex; flex-direction: column; justify-content: center; }
    .question-card { max-width: 900px; margin: 0 auto; padding: clamp(30px,6vw,70px); background: var(--white); border-radius: var(--radius); box-shadow: var(--shadow); text-align: center; }
    .question-text { font-family: var(--serif); font-size: clamp(32px,5vw,60px); margin-bottom: 40px; }
    .answer-buttons { display: grid; grid-template-columns: repeat(2,1fr); gap: 12px; }
    .answer-btn { padding: 18px; border: 1px solid var(--cream-dark); background: var(--cream); border-radius: 14px; transition: transform .2s ease, background .2s ease; }
    .answer-btn:hover { transform: translateY(-3px); background: var(--dusty-rose); }
    .question-response { min-height: 30px; margin-top: 30px; font-family: var(--hand); font-size: 28px; color: var(--terracotta); }
    .final-question-reveal { text-align: center; max-width: 650px; margin: 70px auto 0; opacity: 0; transform: translateY(20px); transition: .8s ease; }
    .final-question-reveal.show { opacity: 1; transform: translateY(0); }
    .large-statement { font-family: var(--serif); font-size: 65px; color: var(--burgundy); }
    .final-question-reveal p { margin: 10px 0; }
    .mini-confetti-icon { font-size: 35px; margin-top: 20px; color: var(--gold); }

    /* FLIP CARDS */
    .why-section { background: linear-gradient(135deg, var(--cream), var(--dusty-rose)); }
    .flip-grid { max-width: 1100px; margin: auto; display: grid; grid-template-columns: repeat(2,1fr); gap: 25px; }
    .flip-card { min-height: 350px; perspective: 1200px; cursor: pointer; }
    .flip-inner { position: relative; width: 100%; height: 100%; min-height: 350px; transition: transform .7s cubic-bezier(.2,.8,.2,1); transform-style: preserve-3d; }
    .flip-card.flipped .flip-inner { transform: rotateY(180deg); }
    .flip-front, .flip-back { position: absolute; inset: 0; backface-visibility: hidden; border-radius: var(--radius); padding: 35px; box-shadow: var(--shadow); }
    .flip-front { background: var(--burgundy); color: var(--cream); display: flex; flex-direction: column; justify-content: space-between; }
    .flip-front span { color: var(--gold); }
    .flip-front h2 { font-family: var(--serif); font-size: 38px; line-height: .9; }
    .flip-front small { opacity: .6; }
    .flip-back { background: var(--cream); color: var(--charcoal); transform: rotateY(180deg); display: grid; place-items: center; text-align: center; }
    .flip-back p { font-family: var(--serif); font-size: 28px; line-height: 1.10; }
    .final-card { grid-column: span 2; }

   /* ================================
   MEMORIES / TIMELINE
================================ */

.memories-section {
    background: var(--charcoal);
    color: var(--cream);
}

.timeline {
    position: relative;
    max-width: 900px;
    margin: auto;
    padding-bottom: 20px;
}

/* Timeline vertical line */
.timeline::before {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    left: 20px;
    width: 1px;
    background: rgba(255, 255, 255, 0.18);
}

/* Each memory */
.timeline-item {
    position: relative;
    padding-left: 70px;
    margin-bottom: 100px;
}

/* Timeline dot */
.timeline-dot {
    position: absolute;
    left: 13px;
    top: 10px;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: var(--gold);
    box-shadow: 0 0 0 7px rgba(200, 169, 107, 0.12);
}

/* Date / small label */
.memory-label {
    font-size: 10px;
    letter-spacing: 0.18em;
    color: var(--gold);
    text-transform: uppercase;
}

/* Memory title */
.timeline-content h3 {
    font-family: var(--serif);
    font-size: clamp(35px, 5vw, 60px);
    font-weight: 500;
    margin: 10px 0 30px;
}

/* Photo frame */
.timeline-photo {
    max-width: 600px;
    background: var(--brown);
    padding: 10px;
    transform: rotate(-1deg);
    box-shadow: 0 30px 70px rgba(0, 0, 0, 0.35);
    overflow: hidden;
}

/* Alternate photo angle */
.timeline-item:nth-child(even) .timeline-photo {
    transform: rotate(1.5deg);
}

/* Actual image */
.timeline-photo img {
    display: block;
    width: 100%;
    aspect-ratio: 4 / 3;
    object-fit: cover;
}

/* Optional memory description */
.memory-description {
    max-width: 600px;
    margin-top: 18px;
    color: rgba(255, 255, 255, 0.72);
    line-height: 1.7;
    font-size: 15px;
}

/* Loading message */
.timeline-loading {
    padding-left: 70px;
    color: rgba(255, 255, 255, 0.55);
    font-size: 14px;
}

/* Empty state */
.timeline-empty {
    padding-left: 70px;
    color: rgba(255, 255, 255, 0.55);
    font-size: 14px;
}

/* Mobile */
@media (max-width: 600px) {

    .timeline-item {
        padding-left: 55px;
        margin-bottom: 70px;
    }

    .timeline::before {
        left: 15px;
    }

    .timeline-dot {
        left: 8px;
        width: 14px;
        height: 14px;
    }

    .timeline-content h3 {
        font-size: 36px;
    }

    .timeline-photo {
        max-width: 100%;
    }

    .timeline-loading,
    .timeline-empty {
        padding-left: 55px;
    }
}

    /* GALLERY */
    .gallery-section { background: var(--cream); }
    .gallery-intro { max-width: 1000px; margin: 0 auto 50px; display: grid; grid-template-columns: repeat(2,1fr); gap: 20px; }
    .gallery-category { display: flex; gap: 18px; align-items: center; padding: 25px; border: 1px solid var(--cream-dark); border-radius: 18px; }
    .category-icon { font-size: 30px; }
    .gallery-category h3 { margin-bottom: 5px; }
    .gallery-category p { opacity: .65; font-size: 14px; }
    .gallery-filters { display: flex; justify-content: center; flex-wrap: wrap; gap: 8px; margin-bottom: 40px; }
    .filter-btn { padding: 10px 17px; border-radius: 100px; background: transparent; border: 1px solid var(--cream-dark); font-size: 11px; letter-spacing: .08em; }
    .filter-btn.active { background: var(--burgundy); color: var(--cream); }
    .masonry-gallery { columns: 4 220px; column-gap: 18px; max-width: 1200px; margin: auto; }
    .gallery-item { display: inline-block; width: 100%; margin-bottom: 18px; break-inside: avoid; cursor: pointer; transition: transform .3s ease, opacity .3s ease; }
    .gallery-item:hover { transform: translateY(-6px) rotate(.5deg); }
    .polaroid { background: var(--white); padding: 10px 10px 25px; box-shadow: 0 15px 35px rgba(41,22,28,.12); }
    .polaroid img { width: 100%; aspect-ratio: auto; object-fit: cover; }
    .polaroid-caption { padding: 12px 4px 0; font-family: var(--hand); font-size: 21px; color: var(--brown); }
    .gallery-tag { display: inline-block; font-size: 8px; letter-spacing: .12em; margin-top: 5px; opacity: .55; }

    /* PERSONALITY */
    .personality-section { background: radial-gradient(circle at 80% 30%, rgba(200,169,107,.2), transparent 30%), var(--burgundy); color: var(--cream); }
    .personality-layout { min-height: 70vh; max-width: 1100px; margin: auto; display: grid; grid-template-columns: 1fr 1fr; align-items: center; gap: 80px; }
    .personality-copy h2 { font-family: var(--serif); font-size: clamp(55px,7vw,100px); line-height: .8; margin: 20px 0 30px; }
    .personality-copy p { max-width: 450px; opacity: .7; }
    .character-card { position: relative; background: var(--cream); color: var(--charcoal); padding: 30px; border-radius: 25px; box-shadow: 0 35px 80px rgba(0,0,0,.3); overflow: hidden; }
    .character-card-top { display: flex; justify-content: space-between; font-size: 9px; letter-spacing: .15em; opacity: .5; margin-bottom: 35px; }
    .trait-list { display: grid; gap: 10px; }
    .trait { display: flex; align-items: center; gap: 12px; padding: 13px; background: rgba(137,145,123,.1); border-radius: 10px; }
    .character-note { margin-top: 30px; display: flex; justify-content: space-between; font-size: 10px; }
    .character-note strong { color: var(--terracotta); }

    /* TRAVEL */
    .travel-section { background: var(--sage); color: var(--charcoal); display: grid; place-items: center; text-align: center; }
    .travel-background-map { position: absolute; inset: 0; opacity: .08; background-image: radial-gradient(circle, var(--charcoal) 1px, transparent 1px); background-size: 35px 35px; }
    .travel-content { position: relative; z-index: 2; }
    .travel-content h2 { font-family: var(--serif); font-size: clamp(65px,10vw,130px); line-height: .8; margin: 20px 0; }
    .travel-content > p { font-family: var(--hand); font-size: 28px; }
    .passport { width: min(430px,90vw); height: 270px; margin: 45px auto; position: relative; perspective: 1200px; cursor: pointer; }
    .passport-cover, .passport-page { position: absolute; inset: 0; border-radius: 16px; box-shadow: var(--shadow); transition: transform .8s cubic-bezier(.2,.8,.2,1); }
    .passport-cover { background: var(--burgundy); color: var(--cream); display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 10px; transform-origin: left; z-index: 2; }
    .passport.open .passport-cover { transform: rotateY(-125deg); }
    .passport-symbol { font-size: 45px; color: var(--gold); }
    .passport-cover strong { letter-spacing: .25em; }
    .passport-cover small { opacity: .10; }
    .passport-page { background: var(--cream); padding: 30px; display: flex; flex-direction: column; justify-content: center; gap: 10px; }
    .passport-stamp { position: absolute; top: 20px; right: 20px; width: 55px; height: 55px; display: grid; place-items: center; border: 1px solid var(--terracotta); border-radius: 50%; color: var(--terracotta); transform: rotate(15deg); }
    .map-pin { position: absolute; color: var(--gold); animation: pinFloat 3s ease-in-out infinite; }
    .pin-one { top: 25%; left: 20%; }
    .pin-two { top: 60%; right: 20%; animation-delay: 1s; }
    .pin-three { bottom: 15%; left: 35%; animation-delay: 1.8s; }
    @keyframes pinFloat { 50% { transform: translateY(-12px); } }

    /* SURPRISE */
    .surprise-section { background: var(--cream-dark); text-align: center; display: grid; place-items: center; }
    .surprise-content h2 { font-family: var(--serif); font-size: clamp(60px,8vw,110px); line-height: .8; margin: 20px 0; }
    .envelope-wrapper { width: 380px; height: 200px; margin: 50px auto 30px; perspective: 900px; }
    .envelope { position: relative; width: 100%; height: 100%; transform-style: preserve-3d; transition: transform .6s; }
    .envelope-back { position: absolute; inset: 0; background: var(--burgundy); border-radius: 5px; }
    .envelope.open .envelope-flap { transform: rotateX(180deg); }
    .surprise-letter { max-height: 0; overflow: hidden; opacity: 0; transition: max-height .8s ease, opacity .8s ease; margin-top: 20px; background: var(--white); padding: 0 30px; border-radius: 12px; box-shadow: var(--shadow); }
    .surprise-letter.show { max-height: 500px; opacity: 1; padding: 30px; }
    .handwritten { font-family: var(--hand); font-size: 26px; color: var(--terracotta); display: block; margin-bottom: 10px; }
    .letter-sign { display: block; margin-top: 15px; font-family: var(--serif); color: var(--burgundy); font-weight: bold; }

    /* FINALE */
    .finale-section { background: var(--burgundy-dark); color: var(--cream); text-align: center; display: grid; place-items: center; }
    .finale-content h2 { font-family: var(--serif); font-size: clamp(70px,12vw,140px); line-height: .85; margin: 20px 0; }
    .finale-content h2 span { color: var(--dusty-rose); }
    .final-message { max-width: 650px; margin: 40px auto; font-size: 18px; line-height: 1.6; opacity: .85; display: grid; gap: 20px; }
    .final-message .highlight { font-family: var(--serif); font-size: 28px; color: var(--gold); }
    .next-chapter { margin-top: 40px; font-size: 12px; letter-spacing: .2em; text-transform: uppercase; opacity: .6; display: flex; align-items: center; justify-content: center; gap: 10px; }

    /* LIGHTBOX */
    .lightbox { position: fixed; inset: 0; background: rgba(0,0,0,.9); z-index: 1000; display: none; align-items: center; justify-content: center; padding: 40px; }
    .lightbox.open { display: flex; }
    .lightbox-content { max-width: 800px; text-align: center; color: var(--white); }
    .lightbox-content img { max-height: 70vh; margin: 0 auto 15px; border-radius: 8px; }
    .lightbox-close { position: absolute; top: 30px; right: 30px; background: none; color: var(--white); font-size: 35px; }

    /* CONFETTI */
    .confetti-container { position: fixed; inset: 0; pointer-events: none; z-index: 999; overflow: hidden; }
    .confetti { position: absolute; top: -20px; animation: fallConfetti 3s linear forwards; }
    @keyframes fallConfetti {
      to { transform: translateY(105vh) rotate(360deg); opacity: 0; }
    }

    @media (max-width: 768px) {
      .desktop-nav { display: none; }
      .menu-btn { display: grid; }
      .flip-grid, .gallery-intro, .personality-layout, .answer-buttons { grid-template-columns: 1fr; }
      .final-card { grid-column: span 1; }
    }
  </style>
</head>

<body>
  <div class="grain"></div>
  <div class="floating-particles" id="particles"></div>
  <div class="confetti-container" id="confettiContainer"></div>

  <!-- HEADER -->
  <header class="site-header" id="siteHeader">
    <a href="#intro" class="logo">✨</a>
    <nav class="desktop-nav">
      <a href="#intro">01 WELCOME</a>
      <a href="#why">03 REASON</a>
      <a href="#memories">04 MEMORIES</a>
      <a href="#you">06 FOR YOU</a>
      <a href="#travel">07 DESTINY</a>
      <a href="#surprise">08 SURPRISE</a>
      <a href="#unkown">09 UNKNOWN</a>
      <a href="#finale">10 ONCE AGAIN</a>
    </nav>
    <button class="music-btn" id="musicBtn" aria-label="Toggle music">♫</button>
    <button class="menu-btn" id="menuBtn" aria-label="Open menu">☰</button>
  </header>

  <!-- MOBILE MENU -->
  <div class="mobile-menu" id="mobileMenu">
    <button class="close-menu" id="closeMenu">×</button>
    <a href="#intro">01 WELCOME</a>
    <a href="#why">03 REASON</a>
    <a href="#memories">04 MEMORIES</a>
    <a href="#you">06 FOR YOU</a>
    <a href="#travel">07 DESTINY</a>
    <a href="#surprise">08 SURPRISE</a>
    <a href="#unknown">09 UNKNOWN</a>
    <a href="#finale">10 ONCE AGAIN</a>
  </div>

<audio id="birthdayAudio" loop preload="auto">
  <source src="birthday-song.mp3" type="audio/mpeg">
</audio>

<button onclick="toggleMusic()" id="musicButton">
  🎵 Play Music for YOUR SPECIAL DAY!
</button>

<script>
const audio = document.getElementById("birthdayAudio");
const button = document.getElementById("musicButton");

function toggleMusic() {
  if (audio.paused) {
    audio.play();
    button.textContent = "⏸ Pause Music";
  } else {
    audio.pause();
    button.textContent = "🎵 Play Music";
  }
}
</script>

  <main>
    <!-- PAGE 1 — INTRO -->
    <section class="chapter intro" id="intro">
      <div class="intro-inner">
        <span class="eyebrow reveal">...Made something JUST for YOU...</span>
        <h1 class="intro-title reveal">Oye...<span> जरा थांब...</span></h1>
        <p class="intro-subtitle reveal">This isn't just another birthday wish...</p>
        <p class="marathi-line reveal">Because आजचा दिवस थोडा वेगळा आहे...</p>
        <button class="primary-btn reveal" id="enterStory">Enter the story <span>→</span></button>
        <div class="intro-reveal" id="introReveal">
           <p>Because for me, today "someone" important was born.</p>
          <strong>आणि हो... तो “someone” म्हणजे तूच आहेस, बरं का!:)</strong>
        </div>
      </div>
    </section>

    <!-- PAGE 2 — QUESTION -->
    <section class="chapter question-section" id="question">
      <div class="section-heading reveal">
        <span class="section-number">02</span>
        <div>
          <span class="eyebrow">Let's start easy</span>
          <h3>एक विचारू...</h3>
        </div>
      </div>
      <div class="question-card reveal">
        <p class="question-text">Why do you think birthdays deserve to be celebrated?</p>
        <div class="answer-buttons">
          <button class="answer-btn" data-response="Okay, not the cake but You are the 'Main Character' of the day!" . 🍰">Because cake exists 🍰</button>
          <button class="answer-btn" data-response="Fair enough. For getting old by 1 year, Respect. 😌">Because you survived another year.</button>
          <button class="answer-btn" data-response=" Absolutely right, now we're getting somewhere close... 👀">Because it's YOUR day?</button>
          <button class="answer-btn" data-response="Honestly, Incorrect!"> No idea...👀</button>
        </div>
        <div class="question-response" id="questionResponse"></div>
      </div>
      <div class="final-question-reveal" id="finalQuestionReveal">
        <p class="large-statement">Exactly.</p>
        <p>आजचा दिवस important आहे,“कारण काही तारखा फक्त calendar वर नसतात...</p>
        <p><strong>तर त्या मनात ही कायमच्या आठवणीत राहतात..."</strong></p>
        <div class="mini-confetti-icon">✦</div>
      </div>
    </section>

    <!-- PAGE 3 — WHY -->
    <section class="chapter why-section" id="why">
      <div class="section-heading centered reveal">
        <span class="section-number">03</span>
        <span class="eyebrow">unofficial reasons <br> </span>
        <h3>आज दिवस enjoy करण्यासाठी<br> <br>काही reasons...</h3>
      </div>
      <div class="flip-grid">
        <article class="flip-card reveal">
          <div class="flip-inner">
            <div class="flip-front"><span>01</span><h3>Another year completed.</h3><small>Tap to flip ↻</small></div>
            <div class="flip-back"><p>एक वर्ष म्हणजे फक्त age वाढणं नाही...तर तो experiences, lessons आणि memories चा एक पूर्ण chapter असतो...</p></div>
          </div>
        </article>
        <article class="flip-card reveal">
          <div class="flip-inner">
            <div class="flip-front"><span>02</span><h3>People remember you.</h3><small>Tap to flip ↻</small></div>
            <div class="flip-back"><p>कदाचित सगळे सांगत नसतील... पण तू अनेक लोकांच्या आयुष्यात एक जागा बनवली आहेस.</p></div>
          </div>
        </article>
        <article class="flip-card reveal">
          <div class="flip-inner">
            <div class="flip-front"><span>03</span><h3>More places are waiting.</h3><small>Tap to flip ↻</small></div>
            <div class="flip-back"><p>अजून कितीतरी journeys, नवीन places, नवीन stories बाकी आहेत.</p></div>
          </div>
        </article>
        <article class="flip-card reveal">
          <div class="flip-inner">
            <div class="flip-front"><span>04</span><h3>Your next chapter hasn't happened yet.</h3><small>Tap to flip ↻</small></div>
            <div class="flip-back"><p>म्हणून आजचा दिवस फक्त celebrate करायचा नाही... तर पुढचं chapter enjoy करायला सुरुवात करायची.</p></div>
          </div>
        </article>
        <article class="flip-card final-card reveal">
          <div class="flip-inner">
            <div class="flip-front"><span>★</span><h3>Because you deserve one day that's simply about YOU.</h3><small>Tap to flip ↻</small></div>
            <div class="flip-back"><p>आज explanations नकोत. आज फक्त enjoy करायचं. :)</p></div>
          </div>
        </article>
      </div>
    </section>

    <!-- PAGE 4 — MEMORIES -->
    <section class="memories-section" id="memories">

    <div class="section-heading">
        <span class="memory-label">MEMORIES</span>
        <h2>A little collection of moments</h2>
    </div>
     <div class="timeline" id="timeline">

        <div class="timeline-loading">
            Loading memories...
        </div>

    </div>
 </section>

    <!-- PAGE 5 — GALLERY -->
    <section class="chapter gallery-section" id="gallery">
      <div class="section-heading centered reveal">
        <span class="section-number">05</span>
        <span class="eyebrow">The archive</span>
        <h2>Somewhere between<br>photos & memories.</h2>
      </div>
      <div class="gallery-filters reveal">
        <button class="filter-btn active" data-filter="all">ALL</button>
        <button class="filter-btn" data-filter="acknowledged">KNOWN 📸</button>
        <button class="filter-btn" data-filter="candid">CANDID 👀</button>
        <button class="filter-btn" data-filter="travel">TRAVEL ✈️</button>
      </div>
      <div class="masonry-gallery" id="galleryGrid"></div>
    </section>

    <!-- PAGE 6 — PERSONALITY -->
    <section class="chapter personality-section" id="you">
      <div class="personality-layout">
        <div class="personality-copy reveal">
          <span class="section-number">06</span>
          <span class="eyebrow">Absolutely unofficial research</span>
          <h2>Based on<br>absolutely unofficial<br>research...</h2>
          <p>काही observations आहेत. Scientific आहेत की नाहीत, ते मात्र सांगता येणार नाही. 😌</p>
        </div>
        <div class="character-card reveal">
          <div class="character-card-top">
            <span>PERSONALITY FILE</span>
            <span>NO. 001</span>
          </div>
          <div class="trait-list" id="traitList"></div>
          <div class="character-note">
            <span>VERIFIED BY:</span>
            <strong>Absolutely nobody.</strong>
          </div>
        </div>
      </div>
    </section>

    <!-- PAGE 7 — TRAVEL -->
    <section class="chapter travel-section" id="travel">
      <div class="travel-background-map"></div>
      <div class="travel-content reveal">
        <span class="section-number">07</span>
        <span class="eyebrow">Boarding pass to the future</span>
        <h2>Next destination?</h2>
        <p>अजून कितीतरी places बाकी आहेत.</p>
        <div class="passport" id="passportBtn">
          <div class="passport-cover">
            <span class="passport-symbol">✦</span>
            <strong>PASSPORT</strong>
            <small>MEMORIES & ADVENTURES</small>
          </div>
          <div class="passport-page">
            <div class="passport-stamp">✈</div>
            <span>DESTINATION</span>
            <strong id="destinationText">?</strong>
            <small>Wherever the next good memory happens.</small>
          </div>
        </div>
        <button class="primary-btn" style="margin-top:20px;">Open the passport ✈️</button>
      </div>
      <div class="map-pin pin-one">✦</div>
      <div class="map-pin pin-two">✦</div>
      <div class="map-pin pin-three">✦</div>
    </section>

    <!-- PAGE 8 — SURPRISE -->
    <section class="chapter surprise-section" id="surprise">
      <div class="surprise-content reveal">
        <span class="section-number">08</span>
        <span class="eyebrow">Almost there...</span>
        <h2>एक शेवटची गोष्ट<br>बाकी आहे...</h2>
        <div class="envelope-wrapper">
          <div class="envelope" id="envelope">
            <div class="envelope-back"></div>
            <div class="envelope-front"></div>
            <div class="envelope-flap" id="envelopeFlap"></div>
          </div>
        </div>
        <button class="primary-btn" id="openSurprise">Open it 🎁</button>
        <div class="surprise-letter" id="surpriseLetter">
          <span class="handwritten">A little note...</span>
          <p>Some people make ordinary days a little more memorable simply by being themselves.</p>
          <p>आज तुझ्यासाठी एक छोटासा reminder — तू celebrate करण्यासारखा आहेस.</p>
          <span class="letter-sign">✦ Happy Birthday ✦</span>
        </div>
      </div>
    </section>

    <!-- PAGE 9 — FINALE -->
    <section class="chapter finale-section" id="finale">
      <div class="finale-content reveal">
        <span class="eyebrow">And finally...</span>
        <h2>HAPPY<br><span>BIRTHDAY!</span></h2>
        <div class="final-message">
          <p>आजचा दिवस फक्त birthday म्हणून नाही, तर तुझ्या story चा आणखी एक chapter म्हणून celebrate कर.</p>
          <p class="highlight"ो आज थोडं थांब... स्वतःसाठी enjoy कर.</p>
          <p>Happy Birthday. Keep travelling. Keep growing. Keep making memories. :) </p>
        </div>
        <div class="next-chapter"><span>Here’s to your next chapter.</span><strong>✨</strong></div>
      </div>
    </section>
  </main>

<!-- 🎂 MAKE A WISH CAKE -->
<div class="wish-cake">
  <h2>Make a Wish ✨</h2>

  <div class="cake">
    <div class="candles">
      <span class="candle"><i>🔥</i></span>
      <span class="candle"><i>🔥</i></span>
      <span class="candle"><i>🔥</i></span>
    </div>

    <div class="cake-top"></div>
    <div class="cake-body"></div>
  </div>

  <button onclick="blowCandles()">💨 Blow the Candles</button>

  <p id="wishResult"></p>
</div>

<style>
.wish-cake {
  text-align: center;
  padding: 40px 20px;
  font-family: Georgia, serif;
}

.wish-cake h2 {
  font-size: 32px;
  margin-bottom: 35px;
}

.cake {
  position: relative;
  width: 220px;
  height: 180px;
  margin: auto;
}

/* Candles */
.candles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 28px;
  z-index: 2;
}

.candle {
  width: 15px;
  height: 55px;
  background: #f5a6c0;
  border-radius: 4px;
  position: relative;
}

.candle i {
  position: absolute;
  top: -30px;
  left: -5px;
  font-size: 24px;
  font-style: normal;
}

/* Cake */
.cake-top {
  position: absolute;
  top: 55px;
  left: 10px;
  width: 200px;
  height: 45px;
  background: #ffc1d6;
  border-radius: 50%;
}

.cake-body {
  position: absolute;
  top: 75px;
  left: 10px;
  width: 200px;
  height: 70px;
  background: #f49ab5;
  border-radius: 0 0 15px 15px;
}

/* Button */
.wish-cake button {
  margin-top: 20px;
  padding: 12px 24px;
  border: none;
  border-radius: 25px;
  background: #ff7096;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

.wish-cake button:hover {
  transform: scale(1.05);
}

#wishResult {
  font-size: 18px;
  font-weight: bold;
  margin-top: 18px;
}
</style>

<script>
function blowCandles() {
  document.querySelectorAll(".candle i").forEach(flame => {
    flame.style.display = "none";
  });

  document.getElementById("wishResult").textContent =
    "✨ Wish made! May it come true! 🎉";
}
</script>

  <!-- LIGHTBOX -->
  <div class="lightbox" id="lightbox">
    <button class="lightbox-close" id="lightboxClose">×</button>
    <div class="lightbox-content">
      <img id="lightboxImage" src="" alt="">
      <p id="lightboxCaption" style="font-family: var(--hand); font-size: 24px;"></p>
    </div>
  </div>

  <script>
    /* ============================================================
       JAVASCRIPT LOGIC
       ============================================================ */
    const musicFile = "audio/birthday.mp3";

    const memories = [
      { category: "acknowledged", image: "https://picsum.photos/400/500?random=3", caption: "One of those good moments.", favourite: true },
      { category: "travel", image: "https://picsum.photos/500/400?random=4", caption: "Another place, another story. ✈️", favourite: false },
      { category: "candid", image: "https://picsum.photos/400/400?random=5", caption: "You probably don't remember this one. 😌", favourite: false },
      { category: "acknowledged", image: "https://picsum.photos/450/500?random=6", caption: "एक जुना moment...", favourite: true },
      { category: "favourite", image: "https://picsum.photos/400/600?random=7", caption: "One of my favourite frames.", favourite: true }
    ];

    const personalityTraits = [
      "✈️|Traveller",
      "💼|Professional mode ON",
      "😌|Calm / composed",
      "📸|Occasionally caught on camera",
      "😂|Unexpectedly funny",
      "🧭|Always another place to explore"
    ];

    document.addEventListener("DOMContentLoaded", () => {
      setupParticles();
      setupRevealAnimations();
      setupNavigation();
      setupIntro();
      setupQuestion();
      setupFlipCards();
      setupGallery();
      setupLightbox();
      setupPassport();
      setupSurprise();
      setupPersonality();
    });

    function setupParticles() {
      const container = document.getElementById("particles");
      if (!container) return;
      for (let i = 0; i < 20; i++) {
        const particle = document.createElement("span");
        particle.className = "particle";
        particle.style.left = Math.random() * 100 + "%";
        particle.style.animationDuration = (8 + Math.random() * 15) + "s";
        particle.style.animationDelay = Math.random() * 10 + "s";
        container.appendChild(particle);
      }
    }

    function setupRevealAnimations() {
      const elements = document.querySelectorAll(".reveal");
      const observer = new IntersectionObserver(entries => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add("visible");
            observer.unobserve(entry.target);
          }
        });
      }, { threshold: .12 });
      elements.forEach(element => observer.observe(element));
    }

    function setupNavigation() {
      const header = document.getElementById("siteHeader");
      const menuBtn = document.getElementById("menuBtn");
      const closeMenu = document.getElementById("closeMenu");
      const mobileMenu = document.getElementById("mobileMenu");

      window.addEventListener("scroll", () => {
        if (window.scrollY > 50) header.classList.add("scrolled");
        else header.classList.remove("scrolled");
      });

      menuBtn.addEventListener("click", () => mobileMenu.classList.add("open"));
      closeMenu.addEventListener("click", () => mobileMenu.classList.remove("open"));
      mobileMenu.querySelectorAll("a").forEach(link => {
        link.addEventListener("click", () => mobileMenu.classList.remove("open"));
      });
    }

    function setupIntro() {
      const button = document.getElementById("enterStory");
      const reveal = document.getElementById("introReveal");
      button.addEventListener("click", () => {
        reveal.classList.add("show");
        setTimeout(() => {
          document.getElementById("question").scrollIntoView({ behavior: "smooth" });
        }, 1800);
      });
    }

    const musicBtn = document.getElementById("musicBtn");
    const music = document.getElementById("birthdayMusic");
    let musicPlaying = false;
    musicBtn.addEventListener("click", async () => {
      try {
        if (!musicPlaying) {
          await music.play();
          musicPlaying = true;
        } else {
          music.pause();
          musicPlaying = false;
        }
      } catch (e) {
        alert("Make sure an audio file is present or check browser permissions.");
      }
    });

    function setupQuestion() {
      const buttons = document.querySelectorAll(".answer-btn");
      const response = document.getElementById("questionResponse");
      const finalReveal = document.getElementById("finalQuestionReveal");
      buttons.forEach(button => {
        button.addEventListener("click", () => {
          response.textContent = button.dataset.response;
          finalReveal.classList.add("show");
          createConfetti(25);
        });
      });
    }

    function setupFlipCards() {
      document.querySelectorAll(".flip-card").forEach(card => {
        card.addEventListener("click", () => card.classList.toggle("flipped"));
      });
    }

    let currentGallery = [];
    let currentLightboxIndex = 0;

    function setupGallery() {
      renderGallery("all");
      document.querySelectorAll(".filter-btn").forEach(button => {
        button.addEventListener("click", () => {
          document.querySelectorAll(".filter-btn").forEach(btn => btn.classList.remove("active"));
          button.classList.add("active");
          renderGallery(button.dataset.filter);
        });
      });
    }

    function renderGallery(filter) {
      const grid = document.getElementById("galleryGrid");
      if (!grid) return;
      if (filter === "all") currentGallery = memories;
      else currentGallery = memories.filter(m => m.category === filter);

      grid.innerHTML = "";
      currentGallery.forEach((memory, index) => {
        const item = document.createElement("article");
        item.className = "gallery-item";
        item.innerHTML = `
          <div class="polaroid">
            <img src="${memory.image}" alt="${memory.caption}" loading="lazy">
            <div class="polaroid-caption">${memory.caption}</div>
            <span class="gallery-tag">${memory.category.toUpperCase()}</span>
          </div>
        `;
        item.addEventListener("click", () => openLightbox(index));
        grid.appendChild(item);
      });
    }

    function setupLightbox() {
      const lightbox = document.getElementById("lightbox");
      document.getElementById("lightboxClose").addEventListener("click", () => lightbox.classList.remove("open"));
    }

    function openLightbox(index) {
      currentLightboxIndex = index;
      const memory = currentGallery[currentLightboxIndex];
      document.getElementById("lightboxImage").src = memory.image;
      document.getElementById("lightboxCaption").textContent = memory.caption;
      document.getElementById("lightbox").classList.add("open");
    }

    function setupPassport() {
      const passport = document.getElementById("passportBtn");
      const destination = document.getElementById("destinationText");
      passport.addEventListener("click", () => {
        passport.classList.toggle("open");
        if (passport.classList.contains("open")) {
          destination.textContent = "WHEREVER.";
          createConfetti(15);
        } else {
          destination.textContent = "?";
        }
      });
    }

    function setupSurprise() {
      const button = document.getElementById("openSurprise");
      const envelope = document.getElementById("envelope");
      const letter = document.getElementById("surpriseLetter");
      button.addEventListener("click", () => {
        envelope.classList.add("open");
        letter.classList.add("show");
        button.textContent = "✨ Opened";
        createConfetti(50);
      });
    }

    function setupPersonality() {
      const list = document.getElementById("traitList");
      if (!list) return;
      list.innerHTML = "";
      personalityTraits.forEach(trait => {
        const [icon, text] = trait.split("|");
        const element = document.createElement("div");
        element.className = "trait";
        element.innerHTML = `<span>${icon}</span><span>${text}</span>`;
        list.appendChild(element);
      });
    }

    function createConfetti(amount = 30) {
      const container = document.getElementById("confettiContainer");
      const symbols = ["✦", "•", "◆", "✧", "★"];
      for (let i = 0; i < amount; i++) {
        const piece = document.span = document.createElement("span");
        piece.className = "confetti";
        piece.textContent = symbols[Math.floor(Math.random() * symbols.length)];
        piece.style.left = Math.random() * 100 + "%";
        piece.style.fontSize = (8 + Math.random() * 15) + "px";
        piece.style.color = ["#c8a96b", "#c9958d", "#f6eee2", "#a65f4f"][Math.floor(Math.random() * 4)];
        container.appendChild(piece);
        setTimeout(() => piece.remove(), 3500);
      }
    }
  </script>
</body>
</html>
