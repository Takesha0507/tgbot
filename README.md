<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ContentTracker - Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/3.2.1/anime.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.4.3/dist/echarts.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/js/splide.min.js"></script>
    <link href="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/css/splide.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #1a1a1a;
            --bg-secondary: #2d2d2d;
            --bg-dark: #0d0d0d;
            --text-primary: #ffffff;
            --text-secondary: #e0e0e0;
            --accent-gold: #f4c430;
            --success: #4caf50;
            --warning: #ff9800;
        }
        
        body {
            background: linear-gradient(135deg, var(--bg-dark) 0%, var(--bg-primary) 100%);
            font-family: 'Inter', sans-serif;
            color: var(--text-primary);
            min-height: 100vh;
        }
        
        .hero-title {
            font-family: 'Playfair Display', serif;
            background: linear-gradient(135deg, var(--accent-gold) 0%, var(--text-primary) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .card-hover {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .card-hover:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 20px 40px rgba(244, 196, 48, 0.2);
        }
        
        .progress-ring {
            transform: rotate(-90deg);
        }
        
        .floating-particles {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }
        
        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: var(--accent-gold);
            border-radius: 50%;
            opacity: 0.6;
        }
        
        .notification-badge {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .gradient-text {
            background: linear-gradient(135deg, var(--accent-gold), #fff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .backdrop-blur {
            backdrop-filter: blur(10px);
        }
        
        .nav-link {
            position: relative;
            transition: all 0.3s ease;
        }
        
        .nav-link:hover {
            color: var(--accent-gold);
        }
        
        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 2px;
            background: var(--accent-gold);
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 bg-black bg-opacity-80 backdrop-blur border-b border-gray-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center">
                    <h1 class="text-2xl font-bold gradient-text">ContentTracker</h1>
                </div>
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-8">
                        <a href="index.html" class="nav-link active text-white hover:text-yellow-400 px-3 py-2 text-sm font-medium">Dashboard</a>
                        <a href="catalog.html" class="nav-link text-gray-300 hover:text-yellow-400 px-3 py-2 text-sm font-medium">Catalog</a>
                        <a href="bookmarks.html" class="nav-link text-gray-300 hover:text-yellow-400 px-3 py-2 text-sm font-medium">Bookmarks</a>
                    </div>
                </div>
                <div class="flex items-center">
                    <button class="relative p-2 text-gray-400 hover:text-white">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-5 5-5-5h5v-5a7.5 7.5 0 1 0-15 0v5h5l-5 5-5-5h5V7a12 12 0 0 1 24 0v10z"/>
                        </svg>
                        <span class="notification-badge absolute -top-1 -right-1 h-3 w-3 bg-red-500 rounded-full"></span>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative pt-20 pb-12 overflow-hidden">
        <div class="floating-particles" id="particles"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="text-center">
                <h1 class="hero-title text-5xl md:text-7xl font-bold mb-6">
                    Track Your
                    <span class="block">Entertainment</span>
                </h1>
                <p class="text-xl text-gray-300 mb-8 max-w-2xl mx-auto">
                    Never lose track of your favorite shows and movies. Keep your entertainment journey organized and discover what's next.
                </p>
                <div class="flex flex-col sm:flex-row gap-4 justify-center">
                    <button onclick="showContinueWatching()" class="bg-yellow-500 hover:bg-yellow-600 text-black font-semibold px-8 py-3 rounded-lg transition-all duration-300 transform hover:scale-105">
                        Continue Watching
                    </button>
                    <button onclick="window.location.href='catalog.html'" class="border border-yellow-500 text-yellow-500 hover:bg-yellow-500 hover:text-black font-semibold px-8 py-3 rounded-lg transition-all duration-300">
                        Discover New Content
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Stats Overview -->
    <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <div class="w-12 h-12 bg-yellow-500 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 4V2a1 1 0 011-1h8a1 1 0 011 1v2m-9 0h10m-10 0a2 2 0 00-2 2v14a2 2 0 002 2h10a2 2 0 002-2V6a2 2 0 00-2-2M9 12l2 2 4-4"/>
                                </svg>
                            </div>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-400">Total Watched</p>
                            <p class="text-2xl font-bold text-white" id="totalWatched">47</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <div class="w-12 h-12 bg-green-500 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                                </svg>
                            </div>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-400">Hours Watched</p>
                            <p class="text-2xl font-bold text-white" id="hoursWatched">342</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <div class="w-12 h-12 bg-orange-500 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                                </svg>
                            </div>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-400">In Progress</p>
                            <p class="text-2xl font-bold text-white" id="inProgress">12</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <div class="w-12 h-12 bg-blue-500 rounded-lg flex items-center justify-center">
                                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                                </svg>
                            </div>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-400">New Episodes</p>
                            <p class="text-2xl font-bold text-white" id="newEpisodes">5</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Continue Watching -->
    <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl font-bold mb-8 gradient-text">Continue Watching</h2>
            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-2xl p-8 card-hover">
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="lg:col-span-1">
                        <img src="https://kimi-web-img.moonshot.cn/img/m.media-amazon.com/9d36a5c3da8c86f6fc500537cf75368cdc162c91.jpg" 
                             alt="Stranger Things" 
                             class="w-full h-80 object-cover rounded-xl">
                    </div>
                    <div class="lg:col-span-2">
                        <h3 class="text-3xl font-bold mb-2">Stranger Things</h3>
                        <p class="text-gray-400 mb-4">Season 4, Episode 7</p>
                        <p class="text-gray-300 mb-6">
                            When a young boy vanishes, a small town uncovers a mystery involving secret experiments, terrifying supernatural forces and one strange little girl.
                        </p>
                        
                        <div class="mb-6">
                            <div class="flex justify-between text-sm text-gray-400 mb-2">
                                <span>Progress</span>
                                <span>67%</span>
                            </div>
                            <div class="w-full bg-gray-700 rounded-full h-2">
                                <div class="bg-yellow-500 h-2 rounded-full" style="width: 67%"></div>
                            </div>
                        </div>
                        
                        <div class="flex flex-col sm:flex-row gap-4">
                            <button onclick="updateProgress()" class="bg-yellow-500 hover:bg-yellow-600 text-black font-semibold px-6 py-3 rounded-lg transition-all duration-300">
                                Update Progress
                            </button>
                            <button onclick="window.location.href='details.html'" class="border border-gray-600 text-gray-300 hover:border-yellow-500 hover:text-yellow-500 font-semibold px-6 py-3 rounded-lg transition-all duration-300">
                                View Details
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Latest Releases Carousel -->
    <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl font-bold mb-8 gradient-text">Latest Releases</h2>
            <div class="splide" id="latest-releases">
                <div class="splide__track">
                    <ul class="splide__list">
                        <li class="splide__slide">
                            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl overflow-hidden card-hover">
                                <img src="https://kimi-web-img.moonshot.cn/img/cached.imagescaler.hbpl.co.uk/3451ddd00a1e0ccb76508e9603daf0726a6b05ee.jpg" 
                                     alt="The Batman" class="w-full h-64 object-cover">
                                <div class="p-4">
                                    <h3 class="font-bold mb-2">The Batman</h3>
                                    <p class="text-gray-400 text-sm">2024 • Action</p>
                                </div>
                            </div>
                        </li>
                        <li class="splide__slide">
                            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl overflow-hidden card-hover">
                                <img src="https://kimi-web-img.moonshot.cn/img/s3.ifanr.com/b51333f1fbcac696b6c04010a3fb0b2b953d7fe3.jpg" 
                                     alt="Spider-Man" class="w-full h-64 object-cover">
                                <div class="p-4">
                                    <h3 class="font-bold mb-2">Spider-Man: No Way Home</h3>
                                    <p class="text-gray-400 text-sm">2024 • Action</p>
                                </div>
                            </div>
                        </li>
                        <li class="splide__slide">
                            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl overflow-hidden card-hover">
                                <img src="https://kimi-web-img.moonshot.cn/img/assets.mubicdn.net/293f2d06bcf90daf2a87e2ad1dc2db3bf6a427cf.jpg" 
                                     alt="Dune" class="w-full h-64 object-cover">
                                <div class="p-4">
                                    <h3 class="font-bold mb-2">Dune: Part Two</h3>
                                    <p class="text-gray-400 text-sm">2024 • Sci-Fi</p>
                                </div>
                            </div>
                        </li>
                        <li class="splide__slide">
                            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl overflow-hidden card-hover">
                                <img src="https://kimi-web-img.moonshot.cn/img/static1.thegamerimages.com/a896e69fe2f27c3493c5b2ca2a1655e89fbfe92f.jpg" 
                                     alt="Oppenheimer" class="w-full h-64 object-cover">
                                <div class="p-4">
                                    <h3 class="font-bold mb-2">Oppenheimer</h3>
                                    <p class="text-gray-400 text-sm">2024 • Drama</p>
                                </div>
                            </div>
                        </li>
                        <li class="splide__slide">
                            <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl overflow-hidden card-hover">
                                <img src="https://kimi-web-img.moonshot.cn/img/images.lifestyleasia.com/b8d3d35f685da0c2b3b9fc0ab9587e5d82259a74.jpg" 
                                     alt="Wednesday" class="w-full h-64 object-cover">
                                <div class="p-4">
                                    <h3 class="font-bold mb-2">Wednesday</h3>
                                    <p class="text-gray-400 text-sm">2024 • Comedy</p>
                                </div>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- Progress Chart -->
    <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <h3 class="text-xl font-bold mb-4 gradient-text">Watching Progress</h3>
                    <div id="progressChart" style="height: 300px;"></div>
                </div>
                <div class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover">
                    <h3 class="text-xl font-bold mb-4 gradient-text">Genre Distribution</h3>
                    <div id="genreChart" style="height: 300px;"></div>
                </div>
            </div>
        </div>
    </section>

    <!-- Quick Actions -->
    <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-3xl font-bold mb-8 gradient-text">Quick Actions</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <button onclick="window.location.href='catalog.html'" class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover text-left">
                    <div class="w-12 h-12 bg-blue-500 rounded-lg flex items-center justify-center mb-4">
                        <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
                        </svg>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Search Content</h3>
                    <p class="text-gray-400">Find new movies and shows to add to your watchlist</p>
                </button>
                
                <button onclick="window.location.href='bookmarks.html'" class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover text-left">
                    <div class="w-12 h-12 bg-green-500 rounded-lg flex items-center justify-center mb-4">
                        <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"/>
                        </svg>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Manage Bookmarks</h3>
                    <p class="text-gray-400">View and organize your saved content</p>
                </button>
                
                <button onclick="showNotifications()" class="bg-gray-900 bg-opacity-50 backdrop-blur rounded-xl p-6 card-hover text-left">
                    <div class="w-12 h-12 bg-orange-500 rounded-lg flex items-center justify-center mb-4">
                        <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-5 5-5-5h5v-5a7.5 7.5 0 1 0-15 0v5h5l-5 5-5-5h5V7a12 12 0 0 1 24 0v10z"/>
                        </svg>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">View Notifications</h3>
                    <p class="text-gray-400">Check for new episodes and updates</p>
                </button>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-black bg-opacity-80 backdrop-blur border-t border-gray-800 py-8">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center">
                <p class="text-gray-400">&copy; 2024 ContentTracker. Track your entertainment journey.</p>
            </div>
        </div>
    </footer>

    <!-- Modal -->
    <div id="modal" class="fixed inset-0 bg-black bg-opacity-50 backdrop-blur hidden z-50 flex items-center justify-center">
        <div class="bg-gray-900 rounded-xl p-8 max-w-md w-full mx-4 transform scale-95 opacity-0 transition-all duration-300" id="modalContent">
            <h3 class="text-xl font-bold mb-4 gradient-text" id="modalTitle">Update Progress</h3>
            <p class="text-gray-300 mb-6" id="modalText">Mark episode as watched?</p>
            <div class="flex gap-4">
                <button onclick="closeModal()" class="flex-1 border border-gray-600 text-gray-300 hover:border-yellow-500 hover:text-yellow-500 px-4 py-2 rounded-lg transition-all duration-300">
                    Cancel
                </button>
                <button onclick="confirmUpdate()" class="flex-1 bg-yellow-500 hover:bg-yellow-600 text-black font-semibold px-4 py-2 rounded-lg transition-all duration-300">
                    Confirm
                </button>
            </div>
        </div>
    </div>

    <script src="main.js"></script>
</body>
</html>
