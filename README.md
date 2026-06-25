<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AutoCaption Pro - AI Subtitle Generator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .gradient-text {
            background: linear-gradient(to right, #3b82f6, #8b5cf6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
    </style>
</head>
<body class="bg-gray-900 text-white font-sans antialiased selection:bg-blue-500 selection:text-white">

    <!-- Navigation -->
    <nav class="border-b border-gray-800 p-4">
        <div class="max-w-6xl mx-auto flex justify-between items-center">
            <h1 class="text-2xl font-bold tracking-tighter">AutoCaption<span class="text-blue-500">Pro</span></h1>
            <button class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg font-semibold text-sm transition">Login / Signup</button>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="text-center py-16 px-4">
        <h2 class="text-4xl md:text-6xl font-extrabold mb-4">Generate Viral Subtitles <br><span class="gradient-text">in Seconds.</span></h2>
        <p class="text-gray-400 text-lg mb-8 max-w-2xl mx-auto">Upload your video and let AI automatically generate accurate, styled captions like your favorite creators.</p>
    </header>

    <!-- Main App UI -->
    <main class="max-w-4xl mx-auto px-4 pb-20">
        
        <!-- Video Upload Box -->
        <div class="bg-gray-800 border-2 border-dashed border-gray-600 rounded-2xl p-10 text-center hover:border-blue-500 transition cursor-pointer mb-8" id="uploadBox">
            <svg class="w-16 h-16 mx-auto text-gray-400 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path></svg>
            <h3 class="text-xl font-semibold mb-2">Click to Upload Video</h3>
            <p class="text-gray-500 text-sm">MP4, MOV or WebM (Max 50MB)</p>
            <input type="file" class="hidden" id="fileInput" accept="video/*">
        </div>

        <!-- Caption Style Selector -->
        <div class="mb-8">
            <h3 class="text-lg font-semibold mb-4 border-l-4 border-blue-500 pl-3">Choose Caption Style</h3>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                
                <div class="bg-gray-800 p-4 rounded-xl border border-gray-700 hover:border-blue-400 cursor-pointer text-center group">
                    <div class="bg-gray-900 h-16 rounded mb-2 flex items-center justify-center">
                        <span class="font-bold text-yellow-400 uppercase text-lg group-hover:scale-110 transition">BOLD</span>
                    </div>
                    <p class="text-sm font-medium">Hormozi Style</p>
                </div>

                <div class="bg-gray-800 p-4 rounded-xl border border-gray-700 hover:border-blue-400 cursor-pointer text-center group">
                    <div class="bg-gray-900 h-16 rounded mb-2 flex items-center justify-center">
                        <span class="font-black text-cyan-400 text-xl" style="text-shadow: 2px 2px 0 #000, -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000;">BEAST</span>
                    </div>
                    <p class="text-sm font-medium">MrBeast Style</p>
                </div>

                <div class="bg-gray-800 p-4 rounded-xl border border-blue-500 cursor-pointer text-center ring-2 ring-blue-500 ring-opacity-50 group">
                    <div class="bg-gray-900 h-16 rounded mb-2 flex items-center justify-center">
                        <span class="font-serif text-white tracking-widest text-sm opacity-90">Cinematic</span>
                    </div>
                    <p class="text-sm font-medium">Anime / Movie</p>
                </div>

                <div class="bg-gray-800 p-4 rounded-xl border border-gray-700 hover:border-blue-400 cursor-pointer text-center group">
                    <div class="bg-gray-900 h-16 rounded mb-2 flex items-center justify-center">
                        <span class="font-mono text-green-400 text-sm bg-black/50 px-2 py-1 rounded">Karaoke_</span>
                    </div>
                    <p class="text-sm font-medium">Podcast Type</p>
                </div>

            </div>
        </div>

        <!-- Generate Button & Progress -->
        <div class="text-center">
            <button id="generateBtn" class="bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-500 hover:to-purple-500 text-white text-lg font-bold py-4 px-12 rounded-full shadow-lg transform transition hover:scale-105 w-full md:w-auto">
                Generate Subtitles ⚡
            </button>
            
            <!-- Simulated Progress Bar (Hidden by default) -->
            <div id="progressArea" class="hidden mt-6 max-w-md mx-auto">
                <div class="flex justify-between text-sm text-gray-400 mb-2">
                    <span>Processing AI...</span>
                    <span>45%</span>
                </div>
                <div class="w-full bg-gray-700 rounded-full h-2.5">
                    <div class="bg-blue-500 h-2.5 rounded-full" style="width: 45%"></div>
                </div>
            </div>
        </div>

    </main>

    <!-- Simple JavaScript for UI interaction -->
    <script>
        const uploadBox = document.getElementById('uploadBox');
        const fileInput = document.getElementById('fileInput');
        const generateBtn = document.getElementById('generateBtn');
        const progressArea = document.getElementById('progressArea');

        uploadBox.addEventListener('click', () => {
            fileInput.click();
        });

        generateBtn.addEventListener('click', () => {
            generateBtn.classList.add('hidden');
            progressArea.classList.remove('hidden');
            
            // Simulating a loading process
            let progress = 45;
            const interval = setInterval(() => {
                progress += 5;
                progressArea.querySelector('span:last-child').innerText = progress + '%';
                progressArea.querySelector('.bg-blue-500').style.width = progress + '%';
                
                if(progress >= 100) {
                    clearInterval(interval);
                    progressArea.querySelector('span:first-child').innerText = 'Subtitles Generated!';
                }
            }, 500);
        });
    </script>
</body>
</html>
