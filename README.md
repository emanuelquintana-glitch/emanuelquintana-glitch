<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emanuel Quintana Silva - GitHub Profile</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0a0e27 0%, #1a1f3a 50%, #0f1419 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #e0e6ed;
            overflow-x: hidden;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        /* Header con animación 3D */
        .header {
            position: relative;
            text-align: center;
            padding: 80px 20px;
            margin-bottom: 60px;
            perspective: 1000px;
        }

        .header-content {
            position: relative;
            z-index: 10;
            transform-style: preserve-3d;
            animation: floatHeader 6s ease-in-out infinite;
        }

        @keyframes floatHeader {
            0%, 100% { transform: translateY(0) rotateX(0deg); }
            50% { transform: translateY(-20px) rotateX(5deg); }
        }

        .title {
            font-size: 4.5rem;
            font-weight: 800;
            background: linear-gradient(45deg, #00d4ff, #7b2ff7, #ff006e, #00d4ff);
            background-size: 300% 300%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradientShift 8s ease infinite;
            text-shadow: 0 0 40px rgba(0, 212, 255, 0.3);
            letter-spacing: 2px;
            margin-bottom: 20px;
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .subtitle {
            font-size: 1.4rem;
            color: #8b9dc3;
            margin-bottom: 15px;
            font-weight: 300;
            letter-spacing: 1px;
        }

        .subtitle strong {
            color: #00d4ff;
            font-weight: 600;
        }

        /* Canvas 3D Background */
        #canvas3d {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            opacity: 0.4;
        }

        /* Cards con efecto de profundidad */
        .section {
            background: rgba(15, 20, 35, 0.8);
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 40px;
            position: relative;
            z-index: 10;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(0, 212, 255, 0.2);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .section:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 30px 80px rgba(0, 212, 255, 0.3);
        }

        .section-title {
            font-size: 2.2rem;
            color: #00d4ff;
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .section-title::before {
            content: '';
            width: 6px;
            height: 40px;
            background: linear-gradient(180deg, #00d4ff, #7b2ff7);
            border-radius: 3px;
            animation: pulse 2s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scaleY(1); }
            50% { opacity: 0.7; transform: scaleY(0.9); }
        }

        /* Tech Stack Grid */
        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .tech-item {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.1), rgba(123, 47, 247, 0.1));
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            border: 1px solid rgba(0, 212, 255, 0.3);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .tech-item::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(0, 212, 255, 0.3), transparent);
            transform: rotate(45deg);
            transition: all 0.5s ease;
        }

        .tech-item:hover::before {
            animation: shine 1.5s ease;
        }

        @keyframes shine {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        .tech-item:hover {
            transform: translateY(-8px) scale(1.05);
            box-shadow: 0 15px 40px rgba(0, 212, 255, 0.4);
        }

        .tech-name {
            font-size: 1.1rem;
            font-weight: 600;
            color: #e0e6ed;
            position: relative;
            z-index: 1;
        }

        /* Projects Grid */
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin-top: 30px;
        }

        .project-card {
            background: linear-gradient(135deg, rgba(20, 25, 45, 0.9), rgba(30, 35, 55, 0.9));
            border-radius: 15px;
            padding: 30px;
            border: 1px solid rgba(123, 47, 247, 0.3);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .project-card::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 212, 255, 0.1), transparent);
            transition: left 0.5s ease;
        }

        .project-card:hover::after {
            left: 100%;
        }

        .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 50px rgba(123, 47, 247, 0.4);
            border-color: rgba(0, 212, 255, 0.5);
        }

        .project-title {
            font-size: 1.5rem;
            color: #00d4ff;
            margin-bottom: 15px;
            font-weight: 700;
        }

        .project-desc {
            color: #a0aec0;
            line-height: 1.6;
            margin-bottom: 20px;
        }

        .project-link {
            display: inline-block;
            color: #7b2ff7;
            text-decoration: none;
            font-weight: 600;
            padding: 10px 20px;
            border: 2px solid #7b2ff7;
            border-radius: 8px;
            transition: all 0.3s ease;
        }

        .project-link:hover {
            background: #7b2ff7;
            color: white;
            transform: scale(1.05);
        }

        /* Stats Section */
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 25px;
            margin-top: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.15), rgba(123, 47, 247, 0.15));
            padding: 30px;
            border-radius: 15px;
            text-align: center;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border-radius: 15px;
            padding: 2px;
            background: linear-gradient(45deg, #00d4ff, #7b2ff7, #ff006e);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .stat-card:hover::before {
            opacity: 1;
        }

        .stat-number {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(45deg, #00d4ff, #7b2ff7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }

        .stat-label {
            font-size: 1rem;
            color: #8b9dc3;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Contact Section */
        .contact-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .contact-item {
            background: rgba(30, 35, 55, 0.5);
            padding: 25px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            gap: 15px;
            border: 1px solid rgba(0, 212, 255, 0.2);
            transition: all 0.3s ease;
        }

        .contact-item:hover {
            background: rgba(0, 212, 255, 0.1);
            border-color: #00d4ff;
            transform: translateX(10px);
        }

        .contact-icon {
            font-size: 1.5rem;
            color: #00d4ff;
        }

        .contact-text {
            color: #e0e6ed;
            word-break: break-all;
        }

        /* Wave Animation */
        .wave-container {
            position: relative;
            height: 150px;
            overflow: hidden;
            margin: 60px 0;
        }

        .wave {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 200%;
            height: 100%;
            background: linear-gradient(90deg, rgba(0, 212, 255, 0.3), rgba(123, 47, 247, 0.3));
            border-radius: 1000px 1000px 0 0;
            animation: wave 10s linear infinite;
        }

        .wave:nth-child(2) {
            opacity: 0.5;
            animation-duration: 15s;
            animation-direction: reverse;
        }

        @keyframes wave {
            0% { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 40px 20px;
            color: #8b9dc3;
            font-size: 0.9rem;
            position: relative;
            z-index: 10;
        }

        .footer-divider {
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, transparent, #00d4ff, transparent);
            margin: 20px auto;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .title {
                font-size: 2.5rem;
            }

            .section {
                padding: 25px;
            }

            .projects-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <canvas id="canvas3d"></canvas>

    <div class="container">
        <div class="header">
            <div class="header-content">
                <h1 class="title">EMANUEL QUINTANA SILVA</h1>
                <p class="subtitle">Economista en Formación | <strong>UPTC</strong></p>
                <p class="subtitle">Especialista en Econometría Computacional, R & Python</p>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">Sobre Mí</h2>
            <p style="font-size: 1.15rem; line-height: 1.8; color: #c4cfd9;">
                Economista en formación con una profunda pasión por la intersección entre economía, matemáticas y computación. 
                Mi enfoque se centra en la <strong style="color: #00d4ff;">Econometría Computacional</strong>, aprovechando el poder 
                de lenguajes como <strong style="color: #7b2ff7;">R</strong> y <strong style="color: #7b2ff7;">Python</strong> para 
                analizar datos complejos, desarrollar modelos estadísticos avanzados y generar insights significativos en Ciencias Sociales.
            </p>
        </div>

        <div class="section">
            <h2 class="section-title">Stack Tecnológico</h2>
            <div class="tech-grid">
                <div class="tech-item">
                    <div class="tech-name">R</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Python</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Econometría</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Estadística</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Machine Learning</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Data Science</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">LaTeX</div>
                </div>
                <div class="tech-item">
                    <div class="tech-name">Git</div>
                </div>
            </div>
        </div>

        <div class="wave-container">
            <div class="wave"></div>
            <div class="wave"></div>
        </div>

        <div class="section">
            <h2 class="section-title">Proyectos Destacados</h2>
            <div class="projects-grid">
                <div class="project-card">
                    <h3 class="project-title">Aeronautics Analysis</h3>
                    <p class="project-desc">
                        Análisis computacional aplicado a la aeronáutica, combinando modelos matemáticos 
                        con simulaciones estadísticas para estudiar fenómenos complejos en dinámica de fluidos.
                    </p>
                    <a href="https://github.com/emanuelquintana-glitch/Aeronautics_1.git" class="project-link" target="_blank">Ver Proyecto →</a>
                </div>

                <div class="project-card">
                    <h3 class="project-title">Apuntes Economía Matemática</h3>
                    <p class="project-desc">
                        Compilación exhaustiva de notas, teoremas y demostraciones en economía matemática, 
                        abarcando desde fundamentos hasta aplicaciones avanzadas en teoría económica.
                    </p>
                    <a href="https://github.com/emanuelquintana-glitch/Apuntes-Economia-Matematica.git" class="project-link" target="_blank">Ver Proyecto →</a>
                </div>

                <div class="project-card">
                    <h3 class="project-title">Teoría de Fuerzas Intermoleculares</h3>
                    <p class="project-desc">
                        Estudio computacional de interacciones moleculares utilizando métodos numéricos 
                        y simulaciones para modelar comportamientos físico-químicos complejos.
                    </p>
                    <a href="https://github.com/emanuelquintana-glitch/TEORIA_DE_FUERZAS_INTERMOLECULARES.git" class="project-link" target="_blank">Ver Proyecto →</a>
                </div>

                <div class="project-card">
                    <h3 class="project-title">Applied Computational Maths</h3>
                    <p class="project-desc">
                        Implementaciones avanzadas de algoritmos matemáticos y métodos computacionales 
                        aplicados a problemas de optimización, ecuaciones diferenciales y análisis numérico.
                    </p>
                    <a href="https://github.com/emanuelquintana-glitch/APPLIED_-_COMPUTATIONAL_MATHS.git" class="project-link" target="_blank">Ver Proyecto →</a>
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">GitHub Analytics</h2>
            <div class="stats-container">
                <div class="stat-card">
                    <div class="stat-number">3</div>
                    <div class="stat-label">Followers</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">77</div>
                    <div class="stat-label">Following</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">5+</div>
                    <div class="stat-label">Repositories</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">100+</div>
                    <div class="stat-label">Commits</div>
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">Contacto & Enlaces</h2>
            <div class="contact-grid">
                <div class="contact-item">
                    <span class="contact-icon">✉</span>
                    <span class="contact-text">emanuel.quintana@uptc.edu.co</span>
                </div>
                <div class="contact-item">
                    <span class="contact-icon">🔗</span>
                    <span class="contact-text">github.com/emanuelquintana-glitch</span>
                </div>
                <div class="contact-item">
                    <span class="contact-icon">🎓</span>
                    <a href="https://orcid.org/0009-0006-8419-2805" style="color: #00d4ff; text-decoration: none;">ORCID: 0009-0006-8419-2805</a>
                </div>
            </div>
        </div>

        <div class="footer">
            <div class="footer-divider"></div>
            <p>Desarrollado con pasión por la Econometría Computacional</p>
            <p style="margin-top: 10px;">© 2024 Emanuel Quintana Silva | UPTC</p>
        </div>
    </div>

    <script>
        // 3D Particle System
        const canvas = document.getElementById('canvas3d');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        class Particle {
            constructor() {
                this.reset();
            }

            reset() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.z = Math.random() * 1000;
                this.vz = Math.random() * 2 + 0.5;
            }

            update() {
                this.z -= this.vz;
                if (this.z <= 0) {
                    this.reset();
                    this.z = 1000;
                }
            }

            draw() {
                const scale = 1000 / (1000 + this.z);
                const x2d = (this.x - canvas.width / 2) * scale + canvas.width / 2;
                const y2d = (this.y - canvas.height / 2) * scale + canvas.height / 2;
                const size = (1 - this.z / 1000) * 3;

                const opacity = 1 - this.z / 1000;
                const hue = (this.z / 1000) * 60 + 180;

                ctx.fillStyle = `hsla(${hue}, 100%, 70%, ${opacity})`;
                ctx.beginPath();
                ctx.arc(x2d, y2d, size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        const particles = Array.from({ length: 150 }, () => new Particle());

        function animate() {
            ctx.fillStyle = 'rgba(10, 14, 39, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            particles.forEach(particle => {
                particle.update();
                particle.draw();
            });

            requestAnimationFrame(animate);
        }

        animate();

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // Parallax effect
        document.addEventListener('mousemove', (e) => {
            const moveX = (e.clientX - window.innerWidth / 2) * 0.01;
            const moveY = (e.clientY - window.innerHeight / 2) * 0.01;

            document.querySelectorAll('.section').forEach((section, index) => {
                section.style.transform = `translate(${moveX * (index + 1)}px, ${moveY * (index + 1)}px)`;
            });
        });
    </script>
</body>
</html>
