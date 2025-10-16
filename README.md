<html lang="en"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UMWTV - International Film Company</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Three.js -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <!-- GSAP for animations -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.4/ScrollTrigger.min.js"></script>
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Poppins:wght@300;400;600&display=swap');
        
        :root {
            --primary-color: #0a2463;
            --secondary-color: #e6af2e;
            --accent-color: #3e92cc;
            --dark-color: #1e1e24;
            --light-color: #f8f8f8;
        }
        
        html {
            scroll-behavior: smooth;
        }
        
        .container-full {
            width: 100%;
            padding-right: 1rem;
            padding-left: 1rem;
            margin-right: auto;
            margin-left: auto;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            color: var(--light-color);
            background-color: var(--dark-color);
            overflow-x: hidden;
        }
        
        h1, h2, h3, h4 {
            font-family: 'Playfair Display', serif;
        }
        
        .hero-section {
            position: relative;
            height: 100vh;
            overflow: hidden;
        }
        
        #hero-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        
        .hero-content {
            position: relative;
            z-index: 1;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 20px;
        }
        
        .logo {
            max-width: 80%;
            max-height: 300px;
            margin-bottom: 2rem;
            filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.5));
        }
        
        .section-title {
            position: relative;
            display: inline-block;
            margin-bottom: 2rem;
            font-size: 2.5rem;
            color: var(--secondary-color);
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 60px;
            height: 3px;
            background-color: var(--secondary-color);
        }
        
        .film-card {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            height: 400px;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        
        .film-card:hover {
            transform: scale(1.03);
        }
        
        .film-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }
        
        .film-card:hover img {
            transform: scale(1.1);
        }
        
        .film-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
            padding: 2rem 1.5rem;
            transform: translateY(70px);
            transition: transform 0.3s ease;
        }
        
        .film-card:hover .film-overlay {
            transform: translateY(0);
        }
        
        .film-title {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
            color: var(--secondary-color);
        }
        
        .film-description {
            font-size: 0.9rem;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .film-card:hover .film-description {
            opacity: 1;
        }
        
        .about-section {
            background-color: var(--primary-color);
            padding: 6rem 0;
        }
        
        .team-member {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            height: 400px;
            cursor: pointer;
        }
        
        .team-member img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }
        
        .team-member:hover img {
            transform: scale(1.1);
        }
        
        .team-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
            padding: 2rem 1.5rem;
        }
        
        .team-name {
            font-size: 1.5rem;
            color: var(--secondary-color);
        }
        
        .team-role {
            font-size: 0.9rem;
        }
        
        .recommendation-section {
            background-color: var(--dark-color);
            padding: 6rem 0;
        }
        
        .recommendation-card {
            background-color: rgba(255, 255, 255, 0.05);
            border-radius: 8px;
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .recommendation-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
        }
        
        .recommendation-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }
        
        .recommendation-content {
            padding: 1.5rem;
        }
        
        .recommendation-title {
            font-size: 1.2rem;
            color: var(--secondary-color);
            margin-bottom: 0.5rem;
        }
        
        .genre-filter {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-bottom: 2rem;
        }
        
        .genre-btn {
            background-color: transparent;
            border: 1px solid var(--secondary-color);
            color: var(--secondary-color);
            padding: 0.5rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        
        .genre-btn:hover, .genre-btn.active {
            background-color: var(--secondary-color);
            color: var(--primary-color);
        }
        
        .footer {
            background-color: var(--primary-color);
            padding: 4rem 0 2rem;
        }
        
        .social-icon {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.1);
            color: var(--light-color);
            margin-right: 0.5rem;
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        
        .social-icon:hover {
            background-color: var(--secondary-color);
            color: var(--primary-color);
        }
        
        .copyright {
            margin-top: 2rem;
            padding-top: 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
            color: rgba(255, 255, 255, 0.7);
        }
        
        /* Loading animation */
        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--primary-color);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }
        
        .loader.hidden {
            opacity: 0;
            visibility: hidden;
        }
        
        .loader-icon {
            width: 50px;
            height: 50px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--secondary-color);
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        /* Mobile menu */
        .mobile-menu-btn {
            display: none;
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
            width: 40px;
            height: 40px;
            background-color: rgba(10, 36, 99, 0.8);
            border: none;
            border-radius: 50%;
            color: var(--light-color);
            cursor: pointer;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }
        
        .mobile-menu {
            position: fixed;
            top: 0;
            right: -100%;
            width: 80%;
            height: 100%;
            background-color: var(--primary-color);
            z-index: 999;
            padding: 2rem;
            transition: right 0.3s ease;
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.3);
        }
        
        .mobile-menu.active {
            right: 0;
        }
        
        .mobile-menu-close {
            position: absolute;
            top: 20px;
            right: 20px;
            background: none;
            border: none;
            color: var(--light-color);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        .mobile-menu ul {
            list-style: none;
            padding: 0;
            margin-top: 60px;
        }
        
        .mobile-menu ul li {
            margin-bottom: 1.5rem;
        }
        
        .mobile-menu ul li a {
            color: var(--light-color);
            text-decoration: none;
            font-size: 1.2rem;
            transition: color 0.3s ease;
        }
        
        .mobile-menu ul li a:hover {
            color: var(--secondary-color);
        }
        
        /* Responsive styles */
        @media (max-width: 768px) {
            .desktop-nav {
                display: none;
            }
            
            .mobile-menu-btn {
                display: block;
            }
            
            .section-title {
                font-size: 2rem;
            }
            
            .film-card, .team-member {
                height: 300px;
            }
        }
        
        @media (max-width: 640px) {
            .logo {
                max-height: 200px;
            }
            
            .section-title {
                font-size: 1.5rem;
            }
            
            .film-card, .team-member {
                height: 250px;
            }
        }
        
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: var(--dark-color);
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--primary-color);
            border-radius: 4px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: var(--secondary-color);
        }
        
        /* Certification cards */
        .certification-card {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .certification-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .certification-card img {
            width: 100%;
            height: auto;
            display: block;
            transition: transform 0.3s ease;
        }
        
        .certification-card:hover img {
            transform: scale(1.05);
        }
    </style>
</head>
<body>
    <!-- Loading animation -->
    <div class="loader">
        <div class="loader-icon"></div>
    </div>
    
    <!-- Mobile menu button -->
    <button class="mobile-menu-btn">
        <i class="fas fa-bars"></i>
    </button>
    
    <!-- Mobile menu -->
    <div class="mobile-menu">
        <button class="mobile-menu-close">
            <i class="fas fa-times"></i>
        </button>
        <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#films">Our Films</a></li>
            <li><a href="#about">About Us</a></li>
            <li><a href="#certifications">Certifications</a></li>
            <li><a href="#partners">Partners</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </div>
    
    <!-- Desktop navigation -->
    <nav class="desktop-nav fixed top-0 left-0 w-full bg-opacity-90 bg(--primary-color) z-50 backdrop-blur-sm">
        <div class="container-full px-4 py-3 flex justify-between items-center">
            <div class="flex items-center">
                <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/2e09836336b447b28d9fae66a0b6cd46~tplv-a9rns2rl98-image.image?rcl=2025101500063919681A116B0DB5771CF5&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761062799&amp;x-signature=DgCT3ys106nYNet%2BFbRzYIZFTAM%3D" alt="UMWTV Logo" class="h-12" style="border-radius: 30px;">
                <h1 class="ml-3 text-2xl font-bold text-white">UMWTV</h1>
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#home" class="text-white hover:text-yellow-400 transition-colors">Home</a>
                <a href="#services" class="text-white hover:text-yellow-400 transition-colors">Our Services</a>
                <a href="#about" class="text-white hover:text-yellow-400 transition-colors">About Us</a>
                <a href="#certifications" class="text-white hover:text-yellow-400 transition-colors">Our certificates</a>
                <a href="#partners" class="text-white hover:text-yellow-400 transition-colors">Partners</a>
                <a href="#contact" class="text-white hover:text-yellow-400 transition-colors">Contact</a>
            </div>
        </div>
    </nav>
    
    <!-- Hero section -->
    <section id="home" class="hero-section">
        <canvas id="hero-canvas"></canvas>
        <div class="hero-content">
            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/c99761f184d9407e8bbae9a83cc16463~tplv-a9rns2rl98-image.image?rcl=20251015000609D0EFD97F091BED706543&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761062769&amp;x-signature=QmN5hvMy5YQlKfjRW5z%2Fvi%2F3%2FrM%3D" alt="UMWTV Logo" class="logo" style="border: 1px solid rgba(0, 0, 0, 0.08); border-radius: 5px;">
            <h1 class="text-4xl md:text-6xl font-bold mb-4">UMWTV South Africa Film Company</h1>
            <p class="text-xl md:text-2xl mb-8 max-w-3xl">Creating cinematic masterpieces that captivate audiences worldwide</p>
            <a href="#services" class="bg-yellow-500 hover:bg-yellow-600 text-primary-color font-bold py-3 px-8 rounded-full transition-colors duration-300 transform hover:scale-105">
                Explore Our Services
            </a>
        </div>
    </section>
    
    <!-- Services section -->
    <section id="services" class="py-20 bg-gray-900">
        <div class="container-full px-4">
            <h2 class="section-title">Our Services</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <!-- Service 1 -->
                <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
                    <div class="text-yellow-500 text-4xl mb-4">
                        <i class="fas fa-bullhorn"></i>
                    </div>
                    <h3 class="text-2xl mb-4 text-white">Multi-channel Creative Strategy</h3>
                    <p class="text-gray-300">We design campaigns that combine video, social media, and digital media to maximize impact and reach.</p>
                </div>
                
                <!-- Service 2 -->
                <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
                    <div class="text-yellow-500 text-4xl mb-4">
                        <i class="fas fa-mobile-alt"></i>
                    </div>
                    <h3 class="text-2xl mb-4 text-white">Interactive Content Optimization</h3>
                    <p class="text-gray-300">Through the UMWTV app, we convert user interactions into greater exposure and awareness for film companies.</p>
                </div>
                
                <!-- Service 3 -->
                <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
                    <div class="text-yellow-500 text-4xl mb-4">
                        <i class="fas fa-chart-line"></i>
                    </div>
                    <h3 class="text-2xl mb-4 text-white">Market Research and Analysis</h3>
                    <p class="text-gray-300">We study local and global audiences to adapt each message to their cultural and business context.</p>
                </div>
                
                <!-- Service 4 -->
                <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300">
                    <div class="text-yellow-500 text-4xl mb-4">
                        <i class="fas fa-hands-helping"></i>
                    </div>
                    <h3 class="text-2xl mb-4 text-white">Community Impact Programs</h3>
                    <p class="text-gray-300">We integrate social responsibility into every project, creating value for both brands and society.</p>
                </div>
            </div>
            
            <!-- New English Content -->
            <div class="mt-16">
                <h3 class="text-3xl mb-6 text-yellow-400 text-center">True innovation stems from experience.</h3>
                <p class="text-xl text-center mb-12 max-w-3xl mx-auto text-gray-300">We expand your business through creativity, efficiency, and a global approach, connecting film and television companies with audiences around the world.</p>
                
                <!-- Service Features -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-16">
                    <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center">
                        <div class="text-yellow-500 text-3xl mb-3">
                            <i class="fas fa-globe"></i>
                        </div>
                        <h4 class="text-xl mb-2 text-white">Strategies adapted to each market</h4>
                    </div>
                    
                    <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center">
                        <div class="text-yellow-500 text-3xl mb-3">
                            <i class="fas fa-microchip"></i>
                        </div>
                        <h4 class="text-xl mb-2 text-white">Technology that boosts visibility</h4>
                    </div>
                    
                    <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center">
                        <div class="text-yellow-500 text-3xl mb-3">
                            <i class="fas fa-users"></i>
                        </div>
                        <h4 class="text-xl mb-2 text-white">A multicultural team with a global perspective</h4>
                    </div>
                    
                    <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center">
                        <div class="text-yellow-500 text-3xl mb-3">
                            <i class="fas fa-chart-bar"></i>
                        </div>
                        <h4 class="text-xl mb-2 text-white">Dedicated to measurable results</h4>
                    </div>
                </div>
                
                <!-- Service Benefits -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-16">
                    <!-- Benefit 1 -->
                    <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300 flex flex-col">
                        <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/d9003e90307043d7bde29e062f47d20a~tplv-a9rns2rl98-image.image?rcl=20251015061233F223FF4949DCD485FADA&amp;rk3s=8e244e95&amp;rrcfp=f06b921b&amp;x-expires=1763071976&amp;x-signature=uFid2%2FxnSj8Ju4FLFhMTAQsF06M%3D" alt="Boosting film and television exposure" class="w-full h-48 object-cover rounded-lg mb-4">
                        <div class="text-yellow-500 text-4xl mb-4">
                            <i class="fas fa-film"></i>
                        </div>
                        <h3 class="text-2xl mb-4 text-white">Boosting film and television exposure</h3>
                        <p class="text-gray-300">We help film and television companies raise awareness through creative and effective campaigns.</p>
                    </div>
                    
                    <!-- Benefit 2 -->
                    <div class="bg-gray-800 p-8 rounded-lg shadow-lg hover:shadow-xl transition-shadow duration-300 flex flex-col">
                        <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/4f0483ee4530475f95832666e45005e9~tplv-a9rns2rl98-image.image?rcl=20251015061233F223FF4949DCD485FADA&amp;rk3s=8e244e95&amp;rrcfp=f06b921b&amp;x-expires=1763071990&amp;x-signature=766EQNpXBQX1kCuk9sLnWO7Z3BU%3D" alt="Creating Connections" class="w-full h-48 object-cover rounded-lg mb-4">
                        <div class="text-yellow-500 text-4xl mb-4">
                            <i class="fas fa-globe-asia"></i>
                        </div>
                        <h3 class="text-2xl mb-4 text-white">Creating Connections</h3>
                        <p class="text-gray-300">We connect companies with global audiences through digital experiences.</p>
                    </div>
                    
                    <!-- Benefit 3 -->
                    <div class="bg-gray-800 p-8 rounded-lg shadow shadow-lg hover:shadow-xl transition-shadow duration-300 flex flex-col">
                        <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/6398644f29c24db4aed03b11b444a5be~tplv-a9rns2rl98-image.image?rcl=20251015061233F223FF4949DCD485FADA&amp;rk3s=8e244e95&amp;rrcfp=f06b921b&amp;x-expires=1763072007&amp;x-signature=iPCIkTnCwbuTIlItoL9n6jpWnr0%3D" alt="Excellent Results" class="w-full h-48 object-cover rounded-lg mb-4">
                        <div class="text-yellow-500 text-4xl mb-4">
                            <i class="fas fa-trophy"></i>
                        </div>
                        <h3 class="text-2xl mb-4 text-white">Excellent Results</h3>
                        <p class="text-gray-300">Every project is executed with precision, commitment, and international standards.</p>
                    </div>
                </div>
                
                <!-- UMWTV App Section -->
                <div class="mt-16">
                    <h3 class="text-3xl mb-8 text-yellow-400 text-center">How the UMWTV App Works</h3>
                    <p class="text-xl text-center mb-12 max-w-3xl mx-auto text-gray-300">Our platform transforms digital engagement into tangible results for film and television. The entire process is simple, transparent, and efficient:</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                        <!-- Step 1 -->
                        <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center hover:shadow-xl transition-shadow duration-300 flex flex-col">
                            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/879c4fb39d504801807107e79848b5e9~tplv-a9rns2rl98-image.image?rcl=202510160239215BF9D6E67046D325FC07&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1763145595&x-signature=hDCwU7gnUVDIM1YTgvNUM2QOKcs%3D" alt="Publish and Promote" class="w-full h-48 object-cover rounded-lg mb-4">
                            <div class="text-yellow-500 text-5xl mb-4">
                                <i class="fas fa-upload"></i>
                            </div>
                            <h4 class="text-xl mb-3 text-white">Publish and Promote</h4>
                            <p class="text-gray-300">Film and television companies publish their film and television ads on the UMWTV app.</p>
                        </div>
                        
                        <!-- Step 2 -->
                        <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center hover:shadow-xl transition-shadow duration-300 flex flex-col">
                            <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/41e2cb12e06e4e8f92a476988807b4ac~tplv-a9rns2rl98-image.image?rcl=202510160239215BF9D6E67046D325FC07&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1763145609&x-signature=F6%2BhF44I7gzjDBIePS1hbyu5U3s%3D" alt="User Engagement" class="w-full h-48 object-cover rounded-lg mb-4">
                            <div class="text-yellow-500 text-5xl mb-4">
                                <i class="fas fa-users"></i>
                            </div>
                            <h4 class="text-xl mb-3 text-white">User Engagement</h4>
                            <p class="text-gray-300">Online users earn revenue by watching videos through the UMWTV platform.</p>
                        </div>
                        
                        <!-- Step 3 -->
                        <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center hover:shadow-xl transition-shadow duration-300 flex flex-col">
                            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/4226e9fc114a41e7b285b49660b63f98~tplv-a9rns2rl98-image.image?rcl=202510160239215BF9D6E67046D325FC07&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1763145636&x-signature=SS37qvKSBcNJ8c59gUvwDYS7RT8%3D" alt="Increase Exposure" class="w-full h-48 object-cover rounded-lg mb-4">
                            <div class="text-yellow-500 text-5xl mb-4">
                                <i class="fas fa-chart-line"></i>
                            </div>
                            <h4 class="text-xl mb-3 text-white">Increase Exposure</h4>
                            <p class="text-gray-300">Every interaction increases film and television company visibility and recognition.</p>
                        </div>
                        
                        <!-- Step 4 -->
                        <div class="bg-gray-800 p-6 rounded-lg shadow-lg text-center hover:shadow-xl transition-shadow duration-300 flex flex-col">
                            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/7f19b5e5a7764b938d64f4b67da4555a~tplv-a9rns2rl98-image.image?rcl=202510160239215BF9D6E67046D325FC07&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1763145652&x-signature=DorEUlZVZYKf2lg2fKyV4Eq4crU%3D" alt="Shared Rewards" class="w-full h-48 object-cover rounded-lg mb-4">
                            <div class="text-yellow-500 text-5xl mb-4">
                                <i class="fas fa-hand-holding-usd"></i>
                            </div>
                            <h4 class="text-xl mb-3 text-white">Shared Rewards</h4>
                            <p class="text-gray-300">UMWTV collects fees from film and television companies and distributes 70% to 80% of the revenue to participants.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- South African Community Contributions -->
    <section class="py-16 bg-gray-900">
        <div class="container-full px-4">
            <h2 class="section-title">What contributions has UMWTV made to the local area?</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-12">
                <!-- Job Creation and Economic Growth -->
                <div class="bg-gray-800 rounded-lg overflow-hidden shadow-xl transform transition duration-500 hover:scale-105">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/24bd2876e03644f58dc4e461b20a4182~tplv-a9rns2rl98-image.image?rcl=2025101602004944D7CB78E54D0DED062C&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156050&amp;x-signature=AzODGQEYsiBBzA4a3UoE4PUxXs4%3D" alt="Job Creation and Economic Growth" class="w-full h-64 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-bold text-yellow-500 mb-3">Creating jobs and economic growth in South Africa</h3>
                        <p class="text-gray-300">In the next five years, UMWTV will create millions of jobs and provide a stable income for every employed person in South Africa.</p>
                    </div>
                </div>
                
                <!-- Community Care and Education -->
                <div class="bg-gray-800 rounded-lg overflow-hidden shadow-xl transform transition duration-500 hover:scale-105">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/da22edb1f09c482ebe7b9176c32ce32a~tplv-a9rns2rl98-image.image?rcl=2025101504134259DB6995B687567A55B1&amp;rk3s=8e244e95&amp;rrcfp=f06b921b&amp;x-expires=1763064865&amp;x-signature=4hMh7%2FJ%2FujOathDOGx2ZWwG8AxQ%3D" alt="Community Care and Education" class="w-full h-64 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-bold text-yellow-500 mb-3">Community Care and Education</h3>
                        <p class="text-gray-300">Providing assistance to vulnerable groups (including low-income families, orphans, and people with disabilities), and providing scholarships and knowledge-sharing programs to improve educational opportunities.</p>
                        <p class="text-gray-300 mt-3">Healthcare and Infrastructure: Providing medical assistance and improving essential public infrastructure to enhance the quality of life in local communities.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- About section -->
    <section id="about" class="about-section">
        <div class="container-full px-4">
            <h2 class="section-title">About UMWTV</h2>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center mb-16">
                <div>
                    <h3 class="text-2xl mb-4 text-yellow-400">Our Story</h3>
                    <p class="mb-4">Universal McCann Worldwide (UMW) is a media company providing innovative and forward-thinking communications and promotion solutions. Founded in 1999 and headquartered in New York, UMW employs 10,800 full-time employees in 256 offices across 33 countries. The company operates globally, with a network of offices in the United States, the Americas, Europe, the Middle East and Africa, and Asia Pacific.</p>
                    <p class="mb-4">UMWTV, a subsidiary of Universal McCann, is renowned for its creativity and efficiency. Its services include advertising creative, media, public relations, recruitment marketing, and more.</p>
                    <p>UMWTV has long-standing strategic partnerships with world-renowned film studios such as Paramount, Warner Bros., 20th Century Fox, Universal Pictures, Walt Disney Studios, DreamWorks Pictures, and MGM Studios, providing these companies with global exhibition and broadcast promotion services.</p>
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/3c1c89576f754f2a8a19b0a8297a2557~tplv-a9rns2rl98-image.image?rcl=20251016020246D4524EEEA9F96F410C1D&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156166&amp;x-signature=uUBdFF0xMNw%2F%2BzFUrHuy8QwWBd8%3D" alt="Film Set" class="rounded-lg shadow-lg">
                    <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/a00470d8fec1400482e380c53d676647~tplv-a9rns2rl98-image.image?rcl=20251016020128EDCF13777D5F6627FC5A&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156092&amp;x-signature=Z0uKVCVgjQpwXZgN1Gwt%2BegCA7Y%3D" alt="Film Set" class="rounded-lg shadow-lg">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/2af760acfbf24968a6160bc1509f0625~tplv-a9rns2rl98-image.image?rcl=202510160201571F9D924D38F10C597EED&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156120&amp;x-signature=bM58xoid6P7wct%2BWarCvS68zQHw%3D" alt="Film Set" class="rounded-lg shadow-lg">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/acf39b1554e642b3a9ae6b07ec3430a8~tplv-a9rns2rl98-image.image?rcl=20251016020145767509D253E5F20CDABD&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156106&amp;x-signature=RHNGJ9%2BHduqvEqjiN%2FrJmxMOeZU%3D" alt="Film Set" class="rounded-lg shadow-lg">
                </div>
            </div>
            
            <h3 class="text-2xl mb-8 text-yellow-400">Our Team</h3>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Team Member 1 -->
                <div class="team-member">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/782e766349a3ca1ae1e4c45c958363f~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765641521&amp;x-signature=8WHxTgzyTI5YEEIOu9HxYeZ1%2BCg%3D" alt="Team Member">
                    <div class="team-overlay">
                        <h4 class="team-name">Michael Chen</h4>
                        <p class="team-role">Founder &amp; CEO</p>
                    </div>
                </div>
                
                <!-- Team Member 2 -->
                <div class="team-member">
                    <img src="https://p3-doubao-search-sign.byteimg.com/tos-cn-i-qvj2lq49k0/aa94e77d36af4054836b1157c67650cd~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765641521&amp;x-signature=CEU%2FeTOUhUdUGd4stm0tuyFLBtw%3D" alt="Team Member">
                    <div class="team-overlay">
                        <h4 class="team-name">Sarah Johnson</h4>
                        <p class="team-role">Head of Production</p>
                    </div>
                </div>
                
                <!-- Team Member 3 -->
                <div class="team-member">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/f3e3c59f6db5e42dcdb3d6d95863df9e~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765641521&amp;x-signature=mm0WQOca6tZf44JMTEELqU%2FwvvE%3D" alt="Team Member">
                    <div class="team-overlay">
                        <h4 class="team-name">David Rodriguez</h4>
                        <p class="team-role">Lead Director</p>
                    </div>
                </div>
                
                <!-- Team Member 4 -->
                <div class="team-member">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/3526444a50d6d663c5085c3924990890~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765641521&amp;x-signature=U7fN8JDI1Tkussr654w4%2F09v9z4%3D" alt="Team Member">
                    <div class="team-overlay">
                        <h4 class="team-name">Emma Thompson</h4>
                        <p class="team-role">Head of Screenwriting</p>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Certifications section -->
    <section id="certifications" class="py-20 bg-gray-900">
        <div class="container-full px-4">
            <h2 class="section-title">Company Certifications</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Certification 1 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/a86b78a8173f4e3984a6eafa84998ca6~tplv-a9rns2rl98-image.image?rcl=20251016021559D3E7F59F73CB294CA79D&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156960&amp;x-signature=UVSR%2Fc45dA8vBnNjBpV5aCaKU1A%3D" alt="International Certification of Film Company">
                </div>
                
                <!-- Certification 2 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/dbe730a0af8d46748d06c3d080febd52~tplv-a9rns2rl98-image.image?rcl=20251016021617E8E3F8575958DB2C48C5&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156984&amp;x-signature=0vxfaQGUCQTyNQxFsJ0GtbDEzM8%3D" alt="Film Production Quality Award">
                </div>
                
                <!-- Certification 3 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/525f296949e44f21a85297ffcd015847~tplv-a9rns2rl98-image.image?rcl=2025101602163384C331570DA445FCC8C5&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761156993&amp;x-signature=r211VbGkHfOC%2BXM2HlWi8RKR8Js%3D" alt="International Film Association Membership">
                </div>
                
                <!-- Certification 4 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/51596036f6954031b9c2c9e43e5c8878~tplv-a9rns2rl98-image.image?rcl=20251016021701D9A5B9EC5D176AEF3CD1&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761157021&amp;x-signature=6XCB9x1T5c4dNTHhxG%2FP2QDcLq4%3D" alt="Film Distribution License">
                </div>
                
                <!-- Certification 5 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/9ef218d068ba413788f6ad1b97f2e3dc~tplv-a9rns2rl98-image.image?rcl=202510160216516F403607801B22F51CF4&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761157012&amp;x-signature=zsCoj2hcjHmUYE8Mo1VaQyLblgs%3D" alt="Excellence in Film Production Award">
                </div>
                
                <!-- Certification 6 -->
                <div class="certification-card">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/41ae682640994690ad9b7b1f23da6701~tplv-a9rns2rl98-image.image?rcl=20251016021644694373B292EA6836A649&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761157004&amp;x-signature=1kgoXqwvy7FKmRx%2BQe8OidxRZhU%3D" alt="Best Film Award">
                </div>
            </div>
            
            <div class="mt-12 p-6 bg-gray-800 rounded-lg">
                <p class="text-gray-300 text-center">UMWTV has been fully legally certified and supported by the South African government. It provides guaranteed income for every employee. UMWTV is worthy of the trust of every member.</p>
            </div>
        </div>
    </section>
    
    <!-- Contact section -->
    <section id="contact" class="py-20 bg-gray-800">
        <div class="container-full px-4">
            <h2 class="section-title">Contact Us</h2>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <div>
                    <h3 class="text-2xl mb-4 text-yellow-400">Get in Touch</h3>
                    <p class="mb-6">Whether you're interested in collaborating with us, have questions about our projects, or want to learn more about our company, we'd love to hear from you.</p>
                    
                    <div class="space-y-4">
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">Headquarters</h4>
                                <p>123 Film Boulevard, Hollywood, CA 90028</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">London Office</h4>
                                <p>456 Cinema Lane, Soho, London W1D 3BQ</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">Tokyo Office</h4>
                                <p>789 Entertainment Street, Shibuya, Toko 150-0002</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">Paris Office</h4>
                                <p>321 Film Avenue, Champs-Élysées, Paris&nbsp;</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">Email</h4>
                                <p>info@umwtv.com</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start">
                            <div class="flex-shrink-0 w-10 h-10 bg-yellow-500 rounded-full flex items-center justify-center text-primary-color">
                                <i class="fas fa-phone-alt"></i>
                            </div>
                            <div class="ml-4">
                                <h4 class="text-lg font-semibold">Phone</h4>
                                <p>+1 (555) 123-4567</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-8">
                        <h4 class="text-lg font-semibold mb-4">Follow Us</h4>
                        <div class="flex space-x-4">
                            <a href="#" class="social-icon">
                                <i class="fab fa-facebook-f"></i>
                            </a>
                            <a href="#" class="social-icon">
                                <i class="fab fa-twitter"></i>
                            </a>
                            <a href="#" class="social-icon">
                                <i class="fab fa-instagram"></i>
                            </a>
                            <a href="#" class="social-icon">
                                <i class="fab fa-linkedin-in"></i>
                            </a>
                            <a href="#" class="social-icon">
                                <i class="fab fa-youtube"></i>
                            </a>
                        </div>
                    </div>
                </div>
                
                <div>
                    <h3 class="text-2xl mb-4 text-yellow-400">Send Us a Message</h3>
                    <form id="contact-form">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                            <div>
                                <label for="name" class="block text-sm font-medium mb-2">Name</label>
                                <input type="text" id="name" name="name" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-md focus:outline-none focus:ring-2 focus:ring-yellow-500 text-white">
                            </div>
                            
                            <div>
                                <label for="email" class="block text-sm font-medium mb-2">Email</label>
                                <input type="email" id="email" name="email" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-md focus:outline-none focus:ring-2 focus:ring-yellow-500 text-white">
                            </div>
                        </div>
                        
                        <div class="mb-6">
                            <label for="subject" class="block text-sm font-medium mb-2">Subject</label>
                            <input type="text" id="subject" name="subject" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-md focus:outline-none focus:ring-2 focus:ring-yellow-500 text-white">
                        </div>
                        
                        <div class="mb-6">
                            <label for="message" class="block text-sm font-medium mb-2">Message</label>
                            <textarea id="message" name="message" rows="5" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-md focus:outline-none focus:ring-2 focus:ring-yellow-500 text-white"></textarea>
                        </div>
                        
                        <button type="submit" class="w-full bg-yellow-500 hover:bg-yellow-600 text-primary-color font-bold py-3 px-8 rounded-md transition-colors duration-300">
                            Send Message
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Partners section -->
    <section id="partners" class="py-16 bg-gray-900">
        <div class="container-full px-4">
            <h2 class="section-title text-center mx-auto">Our Partners</h2>
            <p class="text-center mb-12 max-w-3xl mx-auto">We are proud to collaborate with some of the most prestigious film studios in the world.</p>
            
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-8">
                <!-- Paramount -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/657684f8b6e2882db23a1801d101797f~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765643262&amp;x-signature=Ug3hrZLC0v3Yi2wlPAkVMxwWpuw%3D" alt="Paramount" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
                
                <!-- Warner Bros -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p11-doubao-search-sign.byteimg.com/labis/caeda919a46aaae163dc5b2d7d15ecbb~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765644408&amp;x-signature=gdwi%2FH1B57NPvAuCQVJ0O3Uy8iU%3D" alt="Warner Bros" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
                
                <!-- 20th Century Fox -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p3-doubao-search-sign.byteimg.com/labis/2093cf3ba566ca729eb445546e5d672a~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765643262&amp;x-signature=2994GGBpInk8eLVDevU82JoW%2Br0%3D" alt="20th Century Fox" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
                
                <!-- Universal -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p26-doubao-search-sign.byteimg.com/labis/323ee67116e7c031ccab40ce37832663~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765643262&amp;x-signature=etlJebBOPo%2B%2FjJ5aIHC%2BO67xkyQ%3D" alt="Universal" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
                
                <!-- Disney -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p11-doubao-search-sign.byteimg.com/labis/ad223ff7ce64f9fb83321f54af8b8545~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765643262&amp;x-signature=6BIknYVGWaOr1sOSBXgqnKngXuI%3D" alt="Disney" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
                
                <!-- DreamWorks -->
                <div class="flex items-center justify-center p-4 bg-gray-800 rounded-lg hover:bg-gray-700 transition-colors duration-300">
                    <img src="https://p3-doubao-search-sign.byteimg.com/pgc-image/2b111e711eba4cb58e53d3053201b64e~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&amp;x-expires=1765643262&amp;x-signature=YpXjF6yZDLSR5VFI%2FCHO5i28b2Q%3D" alt="DreamWorks" class="max-h-16 filter grayscale hover:grayscale-0 transition-all duration-300">
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="container-full px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/code_assistant/4732b3acff5c46fc8877d2098ee6b62a~tplv-a9rns2rl98-image.image?rcl=202510150050058F4C09FFD9CB197A2B49&amp;rk3s=8e244e95&amp;rrcfp=e75484ac&amp;x-expires=1761065406&amp;x-signature=2Q2ew5o8IQg06Fvap1y8rfLZbGE%3D" alt="UMWTV Logo" class="h-16 mb-4" style="border-radius: 5px;">
                    <p class="text-gray-400">Creating cinematic masterpieces that captivate audiences worldwide.</p>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold mb-4">Quick Links</h4>
                    <ul class="space-y-2">
                        <li><a href="#home" class="text-gray-400 hover:text-yellow-400 transition-colors">Home</a></li>
                        <li><a href="#services" class="text-gray-400 hover:text-yellow-400 transition-colors">Our Services</a></li>
                        <li><a href="#about" class="text-gray-400 hover:text-yellow-400 transition-colors">About Us</a></li>
                        <li><a href="#certifications" class="text-gray-400 hover:text-yellow-400 transition-colors">Certifications</a></li>
                        <li><a href="#partners" class="text-gray-400 hover:text-yellow-400 transition-colors">Partners</a></li>
                        <li><a href="#contact" class="text-gray-400 hover:text-yellow-400 transition-colors">Contact</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold mb-4">Our Services</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-400 hover:text-yellow-400 transition-colors">Film Production</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-yellow-400 transition-colors">Distribution</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-yellow-400 transition-colors">Post-Production</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-yellow-400 transition-colors">Talent Management</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-yellow-400 transition-colors">Film Financing</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold mb-4">Newsletter</h4>
                    <p class="text-gray-400 mb-4">Subscribe to our newsletter for the latest updates on our projects and releases.</p>
                    <form class="flex">
                        <input type="email" placeholder="Your email" class="px-4 py-2 bg-gray-700 border border-gray-600 rounded-l-md focus:outline-none focus:ring-2 focus:ring-yellow-500 text-white flex-grow">
                        <button type="submit" class="bg-yellow-500 hover:bg-yellow-600 text-primary-color font-bold px-4 py-2 rounded-r-md transition-colors duration-300">
                            Subscribe
                        </button>
                    </form>
                </div>
            </div>
            
            <div class="copyright text-center mb-6">
                <p>© 2025 UMWTV International Film Company. All rights reserved.</p>
            </div>
            
            <div class="text-center">
                <a href="https://umw-tv.com/xml/index.html#/login" class="inline-block bg-yellow-500 hover:bg-yellow-600 text-primary-color font-bold py-3 px-8 rounded-md transition-colors duration-300">UMWTV official website</a>
            </div>
        </div>
    </footer>
    
    <script>
        
        
        // Initialize Three.js scene
        function initThreeScene() {
            const canvas = document.getElementById('hero-canvas');
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            
            const renderer = new THREE.WebGLRenderer({
                canvas: canvas,
                alpha: true,
                antialias: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(window.devicePixelRatio);
            
            // Create particles
            const particlesGeometry = new THREE.BufferGeometry();
            const particlesCount = 1500;
            
            const posArray = new Float32Array(particlesCount * 3);
            
            for (let i = 0; i < particlesCount * 3; i++) {
                posArray[i] = (Math.random() - 0.5) * 10;
            }
            
            particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
            
            // Materials
            const particlesMaterial = new THREE.PointsMaterial({
                size: 0.02,
                color: 0xe6af2e,
                transparent: true,
                opacity: 0.8
            });
            
            // Mesh
            const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
            scene.add(particlesMesh);
            
            // Camera position
            camera.position.z = 5;
            
            // Animation
            function animate() {
                requestAnimationFrame(animate);
                
                particlesMesh.rotation.y += 0.001;
                particlesMesh.rotation.x += 0.0005;
                
                renderer.render(scene, camera);
            }
            
            animate();
            
            // Handle resize
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
            
            // Handle mouse movement for parallax effect
            document.addEventListener('mousemove', (event) => {
                const mouseX = (event.clientX / window.innerWidth) * 2 - 1;
                const mouseY = -(event.clientY / window.innerHeight) * 2 + 1;
                
                gsap.to(particlesMesh.rotation, {
                    x: mouseY * 0.1,
                    y: mouseX * 0.1,
                    duration: 2
                });
            });
        }
        
        // Initialize the page
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize Three.js scene
            initThreeScene();
            
            // Load user preferences from localStorage
            const savedPreferences = localStorage.getItem('umwtvPreferences');
            if (savedPreferences) {
                userPreferences = JSON.parse(savedPreferences);
            }
            

            
            // Genre filter functionality
            const genreButtons = document.querySelectorAll('.genre-btn');
            const filmCards = document.querySelectorAll('.film-card');
            
            genreButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // Remove active class from all buttons
                    genreButtons.forEach(btn => btn.classList.remove('active'));
                    
                    // Add active class to clicked button
                    button.classList.add('active');
                    
                    const selectedGenre = button.getAttribute('data-genre');
                    
                    // Filter films
                    filmCards.forEach(card => {
                        if (selectedGenre === 'all' || card.getAttribute('data-genre') === selectedGenre) {
                            card.style.display = 'block';
                        } else {
                            card.style.display = 'none';
                        }
                    });
                });
            });
            
            // Track film card interactions for AI recommendations
            filmCards.forEach(card => {
                card.addEventListener('click', () => {
                    const genre = card.getAttribute('data-genre');
                    userPreferences[genre] += 1;
                    // Store preferences in localStorage
                    localStorage.setItem('umwtvPreferences', JSON.stringify(userPreferences));
                    
                    // Get film title from overlay
                    const title = card.querySelector('.film-title').textContent;
                    
                    // Show feedback
                    showFeedback(`You liked ${title}! We'll recommend more ${genre} films.`);
                });
            });
            
            // Mobile menu functionality
            const mobileMenuBtn = document.querySelector('.mobile-menu-btn');
            const mobileMenu = document.querySelector('.mobile-menu');
            const mobileMenuClose = document.querySelector('.mobile-menu-close');
            const mobileMenuLinks = document.querySelectorAll('.mobile-menu ul li a');
            
            mobileMenuBtn.addEventListener('click', () => {
                mobileMenu.classList.add('active');
            });
            
            mobileMenuClose.addEventListener('click', () => {
                mobileMenu.classList.remove('active');
            });
            
            mobileMenuLinks.forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.remove('active');
                });
            });
            
            // Contact form submission
            const contactForm = document.getElementById('contact-form');
            
            contactForm.addEventListener('submit', (event) => {
                event.preventDefault();
                
                // Get form values
                const name = document.getElementById('name').value;
                const email = document.getElementById('email').value;
                const subject = document.getElementById('subject').value;
                const message = document.getElementById('message').value;
                
                // Validate form
                if (!name || !email || !subject || !message) {
                    alert('Please fill in all fields');
                    return;
                }
                
                // Simulate form submission
                alert(`Thank you, ${name}! We've received your message and will get back to you soon.`);
                
                // Reset form
                contactForm.reset();
            });
            
            // Newsletter form submission
            const newsletterForm = document.querySelector('.footer form');
            
            newsletterForm.addEventListener('submit', (event) => {
                event.preventDefault();
                
                // Get email value
                const email = newsletterForm.querySelector('input[type="email"]').value;
                
                // Validate email
                if (!email) {
                    alert('Please enter your email');
                    return;
                }
                
                // Simulate subscription
                alert(`Thank you for subscribing with ${email}!`);
                
                // Reset form
                newsletterForm.reset();
            });
            
            // Hide loading animation after page loads
            const loader = document.querySelector('.loader');
            
            window.addEventListener('load', () => {
                loader.classList.add('hidden');
            });
            
            // GSAP animations
            // Animate hero content
            gsap.from('.hero-content img', {
                opacity: 0,
                y: 50,
                duration: 1.5,
                delay: 0.5
            });
            
            gsap.from('.hero-content h1', {
                opacity: 0,
                y: 30,
                duration: 1.5,
                delay: 0.8
            });
            
            gsap.from('.hero-content p', {
                opacity: 0,
                y: 20,
                duration: 1.5,
                delay: 1.1
            });
            
            gsap.from('.hero-content a', {
                opacity: 0,
                y: 20,
                duration: 1.5,
                delay: 1.4
            });
            
            // Scroll animations
            gsap.registerPlugin(ScrollTrigger);
            
            // Animate section titles
            gsap.utils.toArray('.section-title').forEach(title => {
                gsap.from(title, {
                    scrollTrigger: {
                        trigger: title,
                        start: 'top 80%'
                    },
                    opacity: 0,
                    y: 50,
                    duration: 1
                });
            });
            
            // Animate film cards
            gsap.utils.toArray('.film-card').forEach((card, i) => {
                gsap.from(card, {
                    scrollTrigger: {
                        trigger: card,
                        start: 'top 80%'
                    },
                    opacity: 0,
                    y: 50,
                    duration: 0.8,
                    delay: i * 0.1
                });
            });
            
            // Animate about content
            gsap.from('.about-section p', {
                scrollTrigger: {
                    trigger: '.about-section',
                    start: 'top 80%'
                },
                opacity: 0,
                y: 30,
                duration: 1,
                stagger: 0.2
            });
            
            // Animate team members
            gsap.utils.toArray('.team-member').forEach((member, i) => {
                gsap.from(member, {
                    scrollTrigger: {
                        trigger: member,
                        start: 'top 80%'
                    },
                    opacity: 0,
                    y: 50,
                    duration: 0.8,
                    delay: i * 0.1
                });
            });
            
            // Animate recommendation cards
            gsap.utils.toArray('.recommendation-card').forEach((card, i) => {
                gsap.from(card, {
                    scrollTrigger: {
                        trigger: card,
                        start: 'top 80%'
                    },
                    opacity: 0,
                    y: 50,
                    duration: 0.8,
                    delay: i * 0.1
                });
            });
            
            // Animate contact form
            gsap.from('#contact-form', {
                scrollTrigger: {
                    trigger: '#contact-form',
                    start: 'top 80%'
                },
                opacity: 0,
                x: 50,
                duration: 1
            });
            
            // Animate contact info
            gsap.from('.contact-info', {
                scrollTrigger: {
                    trigger: '.contact-info',
                    start: 'top 80%'
                },
                opacity: 0,
                x: -50,
                duration: 1
            });
            
            // Animate partner logos
            gsap.utils.toArray('#partners img').forEach((logo, i) => {
                gsap.from(logo, {
                    scrollTrigger: {
                        trigger: '#partners',
                        start: 'top 80%'
                    },
                    opacity: 0,
                    y: 30,
                    duration: 0.8,
                    delay: i * 0.1
                });
            });
        });
    </script>


</body></html>
