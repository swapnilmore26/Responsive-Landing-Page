# Responsive-Landing-Page
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Interactive Fixed Navigation Menu</title>
  <style>
    :root{
      --nav-height: 72px;
      --nav-bg: rgba(255,255,255,0.85);
      --nav-bg-scrolled: rgba(20,20,40,0.95);
      --accent: #0ea5a4;
      --text: #111827;
      --muted: #6b7280;
      --transition: 260ms cubic-bezier(.2,.9,.3,1);
    }

    *{box-sizing:border-box;margin:0;padding:0;scroll-behavior:smooth;}
    html,body{height:100%;font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,'Helvetica Neue',Arial;background:linear-gradient(180deg,#e0f7fa,#ffffff);}

    /* NAVIGATION BAR */
    .site-nav{
      position:fixed;top:0;left:0;right:0;height:var(--nav-height);
      display:flex;align-items:center;justify-content:space-between;
      padding:0 2rem;z-index:9999;background:var(--nav-bg);
      backdrop-filter:blur(8px);
      box-shadow:0 2px 6px rgba(0,0,0,0.1);
      transition:background var(--transition),box-shadow var(--transition),height var(--transition),padding var(--transition);
    }

    .site-nav.scrolled{
      background:var(--nav-bg-scrolled);
      box-shadow:0 4px 20px rgba(0,0,0,0.4);
      height:60px; padding:0 1rem;
    }

    .brand{
      display:flex;align-items:center;gap:.75rem;text-decoration:none;color:var(--text);
      font-size:1.4rem;font-weight:700;text-transform:uppercase;
    }
    .brand .logo{
      width:50px;height:50px;border-radius:50%;background:linear-gradient(135deg,var(--accent),#3b82f6);
      display:grid;place-items:center;color:#fff;font-weight:800;font-size:20px;transition:transform var(--transition);
    }
    .site-nav.scrolled .brand .logo{transform:scale(0.85);}

    /* NAV LINKS */
    .nav-links{display:flex;gap:1rem;align-items:center;}
    .nav-links a{
      text-decoration:none;color:var(--text);padding:0.5rem 1rem;border-radius:8px;font-weight:600;
      position:relative;transition:color var(--transition),background var(--transition),transform var(--transition);
    }

    .nav-links a::after{
      content:'';position:absolute;bottom:0;left:0;width:0%;height:3px;background:var(--accent);border-radius:2px;transition:width var(--transition);
    }

    .nav-links a:hover::after{width:100%;}
    .nav-links a:hover{color:var(--accent);transform:translateY(-3px);}

    .nav-links a.active{
      color:#fff;background:linear-gradient(90deg,var(--accent),#06b6d4);
      box-shadow:0 0 10px rgba(14,165,164,0.4);
    }

    /* BUTTON CTA */
    .nav-cta{
      border:2px solid var(--accent);color:var(--accent);font-weight:700;
    }
    .nav-cta:hover{
      background:var(--accent);color:white;box-shadow:0 0 20px rgba(14,165,164,0.4);
    }

    /* HAMBURGER MENU */
    .hamburger{display:none;background:transparent;border:none;cursor:pointer;}

    @media (max-width:820px){
      .nav-links{display:none;flex-direction:column;position:absolute;top:var(--nav-height);left:0;right:0;background:var(--nav-bg);padding:1rem;}
      .nav-links.open{display:flex;}
      .hamburger{display:block;}
    }

    /* PAGE CONTENT */
    main{padding-top:calc(var(--nav-height) + 20px);}
    section{min-height:100vh;padding:4rem 2rem;display:flex;flex-direction:column;justify-content:center;align-items:center;opacity:0;transform:translateY(40px);transition:all 0.8s ease-out;}
    section.visible{opacity:1;transform:translateY(0);}
    section:nth-child(odd){background:#e0f2fe;}
    section:nth-child(even){background:#f9fafb;}

    h1{font-size:2.5rem;margin-bottom:1rem;color:var(--text);animation:fadeIn 1.5s ease-in-out;}
    p{font-size:1.2rem;color:var(--muted);max-width:600px;text-align:center;animation:fadeInUp 2s ease-in-out;}

    footer{
      text-align:center;padding:2rem;background:#0f172a;color:white;font-weight:600;
      animation:fadeInUp 2s ease-in-out;
    }

    /* ANIMATIONS */
    @keyframes fadeIn {
      0% {opacity:0;transform:translateY(-20px);}
      100% {opacity:1;transform:translateY(0);}
    }

    @keyframes fadeInUp {
      0% {opacity:0;transform:translateY(30px);}
      100% {opacity:1;transform:translateY(0);}
    }
  </style>
</head>
<body>
  <header class="site-nav" id="siteNav">
    <a class="brand" href="#home">
      <span class="logo">IN</span>
      InkNav
    </a>

    <nav>
      <button class="hamburger" id="hamburgerBtn">☰</button>
      <div class="nav-links" id="navLinks">
        <a href="#home">Home</a>
        <a href="#about">About</a>
        <a href="#services">Services</a>
        <a href="#portfolio">Portfolio</a>
        <a href="#contact" class="nav-cta">Contact</a>
      </div>
    </nav>
  </header>

  <main>
    <section id="home"><h1>Welcome Home</h1><p>This is a stylish navigation example with scroll, hover, and active effects.</p></section>
    <section id="about"><h1>About Us</h1><p>More enhanced styles and background color changes on each section.</p></section>
    <section id="services"><h1>Our Services</h1><p>We provide top-quality solutions with animations as you scroll.</p></section>
    <section id="portfolio"><h1>Portfolio</h1><p>Explore our work samples and achievements, enhanced with fade-in animations.</p></section>
    <section id="contact"><h1>Contact Us</h1><p>Feel free to get in touch for projects or collaboration.</p></section>
  </main>

  <footer>
    © 2025 InkNav. All rights reserved.
  </footer>

  <script>
    const nav = document.getElementById('siteNav');
    const hamburger = document.getElementById('hamburgerBtn');
    const navLinks = document.getElementById('navLinks');
    const links = navLinks.querySelectorAll('a');

    hamburger.addEventListener('click',()=>{
      navLinks.classList.toggle('open');
    });

    window.addEventListener('scroll',()=>{
      if(window.scrollY > 50){nav.classList.add('scrolled');}
      else{nav.classList.remove('scrolled');}
    });

    const sections = document.querySelectorAll('section');
    const observer = new IntersectionObserver((entries)=>{
      entries.forEach(entry=>{
        if(entry.isIntersecting){
          entry.target.classList.add('visible');
          links.forEach(l=>l.classList.remove('active'));
          document.querySelector(`.nav-links a[href='#${entry.target.id}']`).classList.add('active');
        }
      });
    },{threshold:0.3});

    sections.forEach(sec=>observer.observe(sec));
  </script>
</body>
</html>
