<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jay's Animated GitHub Profile</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;800&family=Inter:wght@300;400;500;600;700;800&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --neon-cyan: #00ffbf;
            --neon-purple: #bf00ff;
            --neon-pink: #ff006b;
            --dark-bg: #0a0a0f;
            --card-bg: rgba(15, 15, 25, 0.8);
            --glass-bg: rgba(255, 255, 255, 0.05);
            --text-primary: #ffffff;
            --text-secondary: #a0a0a0;
        }

        body {
            background: var(--dark-bg);
            color: var(--text-primary);
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* Animated Background */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                        radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.3) 0%, transparent 50%),
                        radial-gradient(circle at 40% 40%, rgba(120, 199, 198, 0.3) 0%, transparent 50%);
            animation: bgFloat 20s ease-in-out infinite;
        }

        @keyframes bgFloat {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.1) rotate(180deg); }
        }

        /* Floating Particles */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: var(--neon-cyan);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
            box-shadow: 0 0 20px var(--neon-cyan);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); opacity: 0; }
            50% { transform: translateY(-100px) rotate(180deg); opacity: 1; }
        }

        /* Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        /* Header Section */
        .header {
            text-align: center;
            padding: 80px 0;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(0, 255, 191, 0.2) 0%, transparent 70%);
            border-radius: 50%;
            animation: pulse 4s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.3; }
            50% { transform: translate(-50%, -50%) scale(1.2); opacity: 0.1; }
        }

        .profile-title {
            font-size: clamp(3rem, 8vw, 6rem);
            font-weight: 800;
            background: linear-gradient(45deg, var(--neon-cyan), var(--neon-purple), var(--neon-pink));
            background-size: 200% 200%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradientShift 3s ease-in-out infinite;
            margin-bottom: 20px;
            text-shadow: 0 0 30px rgba(0, 255, 191, 0.5);
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .typing-animation {
            font-family: 'JetBrains Mono', monospace;
            font-size: clamp(1.2rem, 3vw, 2rem);
            color: var(--neon-cyan);
            margin-bottom: 40px;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Glass Card Effect */
        .glass-card {
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 40px;
            margin: 40px 0;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .glass-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(0, 255, 191, 0.1), transparent);
            transform: rotate(-45deg);
            animation: shimmer 3s linear infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%) translateY(-100%) rotate(-45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(-45deg); }
        }

        .glass-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 255, 191, 0.2);
            border-color: rgba(0, 255, 191, 0.3);
        }

        /* About Section */
        .about {
            position: relative;
            z-index: 2;
        }

        .section-title {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 30px;
            background: linear-gradient(135deg, var(--neon-cyan), var(--neon-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .section-icon {
            font-size: 2rem;
            color: var(--neon-cyan);
            animation: bounce 2s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        /* Tech Stack */
        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .tech-item {
            background: var(--glass-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .tech-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 191, 0.2), transparent);
            transition: left 0.5s;
        }

        .tech-item:hover::before {
            left: 100%;
        }

        .tech-item:hover {
            transform: scale(1.05);
            border-color: var(--neon-cyan);
            box-shadow: 0 10px 25px rgba(0, 255, 191, 0.3);
        }

        .tech-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
            color: var(--neon-cyan);
        }

        /* Projects Section */
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin: 40px 0;
        }

        .project-card {
            background: var(--glass-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 30px;
            position: relative;
            overflow: hidden;
            transition: all 0.4s ease;
        }

        .project-card::after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 3px;
            height: 100%;
            background: linear-gradient(to bottom, var(--neon-cyan), var(--neon-purple));
            transform: scaleY(0);
            transition: transform 0.3s ease;
        }

        .project-card:hover::after {
            transform: scaleY(1);
        }

        .project-card:hover {
            transform: translateY(-5px);
            border-color: rgba(0, 255, 191, 0.5);
            box-shadow: 0 15px 35px rgba(0, 255, 191, 0.2);
        }

        .project-title {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--neon-cyan);
            margin-bottom: 15px;
        }

        .project-description {
            color: var(--text-secondary);
            margin-bottom: 20px;
            line-height: 1.6;
        }

        .project-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .tag {
            background: rgba(0, 255, 191, 0.1);
            color: var(--neon-cyan);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            border: 1px solid rgba(0, 255, 191, 0.3);
            transition: all 0.3s ease;
        }

        .tag:hover {
            background: rgba(0, 255, 191, 0.2);
            transform: scale(1.05);
        }

        /* Social Links */
        .social-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 40px 0;
        }

        .social-link {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: var(--glass-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--neon-cyan);
            font-size: 1.5rem;
            text-decoration: none;
            transition: all 0.3s ease;
            position: relative;
        }

        .social-link::before {
            content: '';
            position: absolute;
            inset: -2px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--neon-cyan), var(--neon-purple));
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .social-link:hover::before {
            opacity: 1;
        }

        .social-link:hover {
            transform: scale(1.1) rotate(360deg);
            box-shadow: 0 0 25px rgba(0, 255, 191, 0.5);
        }

        /* Stats Section */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 40px 0;
        }

        .stat-card {
            background: var(--glass-bg);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--neon-cyan);
            margin-bottom: 10px;
            font-family: 'JetBrains Mono', monospace;
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .glass-card {
                padding: 20px;
                margin: 20px 0;
            }
            
            .tech-grid {
                grid-template-columns: repeat(auto-fit, minmax(60px, 1fr));
                gap: 15px;
            }
            
            .projects-grid {
                grid-template-columns: 1fr;
            }
            
            .social-links {
                gap: 20px;
            }
        }

        /* Scroll Animations */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s ease;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Cursor Trail */
        .cursor-trail {
            position: fixed;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: radial-gradient(circle, var(--neon-cyan), transparent);
            pointer-events: none;
            z-index: 9999;
            mix-blend-mode: screen;
            animation: trailFade 0.5s ease-out forwards;
        }

        @keyframes trailFade {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(0); opacity: 0; }
        }
    </style>
</head>
<body>
    <!-- Animated Background -->
    <div class="bg-animation"></div>
    
    <!-- Floating Particles -->
    <div class="particles" id="particles"></div>

    <div class="container">
        <!-- Header Section -->
        <header class="header">
            <h1 class="profile-title">👋 Hey there! I'm Jay</h1>
            <div class="typing-animation" id="typing-text"></div>
        </header>

        <!-- About Section -->
        <section class="about glass-card fade-in">
            <h2 class="section-title">
                <span class="section-icon">👨‍💻</span>
                About Me
            </h2>
            <p>Hi, I'm <strong>Jay</strong>, a passionate full-stack web developer from <strong>Maharashtra, India</strong>. I specialize in building responsive, scalable, and delightful web applications. Always eager to learn, experiment, and ship meaningful tech.</p>
            
            <div style="margin: 30px 0;">
                <p>🌱 Currently learning <strong>AI integrations</strong> and <strong>backend APIs</strong></p>
                <p>🔭 Working on <strong>AI-powered productivity apps</strong></p>
                <p>🧠 Exploring <strong>Digital Twin systems</strong></p>
                <p>📫 Reach me at: <a href="mailto:jaybontawar33@gmail.com" style="color: var(--neon-cyan);">jaybontawar33@gmail.com</a></p>
            </div>
        </section>

        <!-- Social Links -->
        <section class="fade-in">
            <h2 class="section-title">
                <span class="section-icon">🌐</span>
                Connect with Me
            </h2>
            <div class="social-links">
                <a href="https://linkedin.com/in/jay-bontawar" class="social-link" title="LinkedIn">💼</a>
                <a href="mailto:jaybontawar33@gmail.com" class="social-link" title="Email">✉️</a>
                <a href="https://github.com/jay26027894" class="social-link" title="GitHub">🐙</a>
            </div>
        </section>

        <!-- Tech Stack -->
        <section class="glass-card fade-in">
            <h2 class="section-title">
                <span class="section-icon">💻</span>
                Tech Stack
            </h2>
            <div class="tech-grid">
                <div class="tech-item">
                    <div class="tech-icon">⚛️</div>
                    <div>React</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🎨</div>
                    <div>Tailwind</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🟨</div>
                    <div>JavaScript</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🌐</div>
                    <div>HTML</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🎭</div>
                    <div>CSS</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🔥</div>
                    <div>Firebase</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">⚡</div>
                    <div>Vite</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🍃</div>
                    <div>MongoDB</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🎯</div>
                    <div>Figma</div>
                </div>
                <div class="tech-item">
                    <div class="tech-icon">🌿</div>
                    <div>Git</div>
                </div>
            </div>
        </section>

        <!-- Projects Section -->
        <section class="fade-in">
            <h2 class="section-title">
                <span class="section-icon">🚀</span>
                Featured Projects
            </h2>
            <div class="projects-grid">
                <div class="project-card">
                    <h3 class="project-title">🔹 DigiTwin (AI Productivity Hub)</h3>
                    <p class="project-description">Personalized productivity assistant with AI task planner, habit tracker, and journaling.</p>
                    <div class="project-tags">
                        <span class="tag">React</span>
                        <span class="tag">MongoDB</span>
                        <span class="tag">TailwindCSS</span>
                        <span class="tag">AI</span>
                    </div>
                </div>
                
                <div class="project-card">
                    <h3 class="project-title">🔹 CaptionCraft</h3>
                    <p class="project-description">Create aesthetic AI-generated Instagram captions with emojis & mood tones.</p>
                    <div class="project-tags">
                        <span class="tag">Gemini AI</span>
                        <span class="tag">Vite</span>
                        <span class="tag">JavaScript</span>
                    </div>
                </div>
                
                <div class="project-card">
                    <h3 class="project-title">🔹 NewsNest</h3>
                    <p class="project-description">Smart news site with filters for World, Politics, Tech, and more.</p>
                    <div class="project-tags">
                        <span class="tag">React</span>
                        <span class="tag">NewsAPI</span>
                        <span class="tag">GNews</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- GitHub Stats -->
        <section class="glass-card fade-in">
            <h2 class="section-title">
                <span class="section-icon">📊</span>
                GitHub Stats
            </h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number" id="commits">500+</div>
                    <div class="stat-label">Commits</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="projects">25+</div>
                    <div class="stat-label">Projects</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="languages">10+</div>
                    <div class="stat-label">Languages</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="contributions">1000+</div>
                    <div class="stat-label">Contributions</div>
                </div>
            </div>
        </section>

        <!-- Visitor Counter -->
        <section class="glass-card fade-in" style="text-align: center;">
            <h2 class="section-title">
                <span class="section-icon">🧭</span>
                Visitor Counter
            </h2>
            <div class="stat-number" id="visitor-count">42,069</div>
            <div class="stat-label">Profile Visits</div>
        </section>
    </div>

    <script>
        // Typing Animation
        const typingTexts = [
            "Web Developer 💻",
            "React + Tailwind Enthusiast 🤗",
            "Love clean UI and modern UX 💖",
            "Building cool projects everyday 🚀",
            "AI Integration Explorer 🤖",
            "Full-Stack Developer 🌟"
        ];
        
        let textIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typingElement = document.getElementById('typing-text');
        
        function typeAnimation() {
            const currentText = typingTexts[textIndex];
            
            if (isDeleting) {
                typingElement.textContent = currentText.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typingElement.textContent = currentText.substring(0, charIndex + 1);
                charIndex++;
            }
            
            let typeSpeed = isDeleting ? 50 : 100;
            
            if (!isDeleting && charIndex === currentText.length) {
                typeSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                textIndex = (textIndex + 1) % typingTexts.length;
                typeSpeed = 200;
            }
            
            setTimeout(typeAnimation, typeSpeed);
        }
        
        typeAnimation();

        // Floating Particles
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.top = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 6 + 's';
                particle.style.animationDuration = (Math.random() * 3 + 3) + 's';
                particlesContainer.appendChild(particle);
            }
        }
        
        createParticles();

        // Scroll Animation
        function animateOnScroll() {
            const elements = document.querySelectorAll('.fade-in');
            
            elements.forEach(element => {
                const elementTop = element.getBoundingClientRect().top;
                const elementVisible = 150;
                
                if (elementTop < window.innerHeight - elementVisible) {
                    element.classList.add('visible');
                }
            });
        }
        
        window.addEventListener('scroll', animateOnScroll);
        animateOnScroll(); // Initial check

        // Cursor Trail Effect
        let mouseX = 0;
        let mouseY = 0;
        
        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            
            const trail = document.createElement('div');
            trail.className = 'cursor-trail';
            trail.style.left = mouseX - 10 + 'px';
            trail.style.top = mouseY - 10 + 'px';
            document.body.appendChild(trail);
            
            setTimeout(() => {
                document.body.removeChild(trail);
            }, 500);
        });

        // Animated Counter
        function animateCounter(element, target, duration = 2000) {
            const start = 0;
            const startTime = performance.now();
            
            function updateCounter(currentTime) {
                const elapsed = currentTime - startTime;
                const progress = Math.min(elapsed / duration, 1);
                
                const current = Math.floor(progress * target);
                element.textContent = current.toLocaleString() + '+';
                
                if (progress < 1) {
                    requestAnimationFrame(updateCounter);
                }
            }
            
            requestAnimationFrame(updateCounter);
        }

        // Animate stats when visible
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const element = entry.target;
                    const id = element.id;
                    
                    switch(id) {
                        case 'commits':
                            animateCounter(element, 500);
                            break;
                        case 'projects':
                            animateCounter(element, 25);
                            break;
                        case 'languages':
                            animateCounter(element, 10);
                            break;
                        case 'contributions':
                            animateCounter(element, 1000);
                            break;
                        case 'visitor-count':
                            animateCounter(element, 42069);
                            break;
                    }
                    
                    observer.unobserve(element);
                }
            });
        });

        // Observe stat numbers
        document.querySelectorAll('.stat-number').forEach(el => {
            observer.observe(el);
        });

        // Add dynamic glow effects to tech items
        document.querySelectorAll('.tech-item').forEach(item => {
            item.addEventListener('mouseenter', () => {
                const colors = ['#00ffbf', '#bf00ff', '#ff006b', '#667eea'];
                const randomColor = colors[Math.floor(Math.random() * colors.length)];
                item.style.boxShadow = `0 10px 25px ${randomColor}40`;
            });
            
            item.addEventListener('mouseleave', () => {
                item.style.boxShadow = '';
            });
        });

        // Add parallax effect to cards
        document.addEventListener('mousemove', (e) => {
            const cards = document.querySelectorAll('.glass-card, .project-card');
            const x = e.clientX / window.innerWidth;
            const y = e.clientY / window.innerHeight;
            
            cards.forEach((card, index) => {
                const speed = (index + 1) * 0.5;
                const xPos = (x - 0.5) * speed;
                const yPos = (y - 0.5) * speed;
                
                card.style.transform = `translate(${xPos}px, ${yPos}px)`;
            });
        });
    </script>
</body>
</html>
