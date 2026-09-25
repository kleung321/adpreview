<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Google Ads Performance Max - Asset Studio & Client Preview</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Inter, Roboto, Google Sans -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;500;600;700&family=Inter:wght@400;500;600;700&family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            google: ['"Google Sans"', 'Roboto', 'sans-serif'],
            roboto: ['Roboto', 'sans-serif'],
          },
          colors: {
            google: {
              blue: '#1a73e8',
              'blue-hover': '#1557b0',
              'blue-light': '#e8f0fe',
              green: '#1e8e3e',
              'green-light': '#e6f4ea',
              red: '#d93025',
              'red-light': '#fce8e6',
              yellow: '#f9ab00',
              'yellow-light': '#fef7e0',
              gray: '#5f6368',
              border: '#dadce0',
              bg: '#f8f9fa',
              darkbg: '#202124'
            }
          }
        }
      }
    }
  </script>

  <style>
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background-color: #cbd5e1;
      border-radius: 9999px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: transparent;
    }
    .serp-link:hover {
      text-decoration: underline;
    }
    @media print {
      .no-print { display: none !important; }
      .print-only { display: block !important; }
      body { background: white !important; overflow: visible !important; height: auto !important; }
      #previewViewport { overflow: visible !important; height: auto !important; }
    }
  </style>
</head>
<body class="bg-[#f0f3f6] text-gray-800 font-sans antialiased h-screen flex flex-col overflow-hidden select-none">

  <!-- TOP HEADER -->
  <header class="bg-white border-b border-gray-200 px-4 py-2 flex items-center justify-between z-30 flex-shrink-0">
    <div class="flex items-center gap-3">
      <div class="flex items-center gap-2">
        <svg class="w-6 h-6" viewBox="0 0 24 24">
          <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
          <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
          <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/>
          <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.52 6.16-4.52z"/>
        </svg>
        <span class="text-base md:text-lg font-google font-semibold text-gray-800 tracking-tight">Google Ads</span>
        <span class="text-xs px-2 py-0.5 bg-blue-50 text-blue-700 font-medium rounded-full border border-blue-200">Performance Max Studio</span>
      </div>
      <div class="h-4 w-px bg-gray-300 hidden md:block"></div>
      <span class="text-xs md:text-sm font-medium text-gray-600 truncate max-w-[180px] sm:max-w-xs md:max-w-md" id="headerCampaignName">
        Asset Group: <span id="headerBrandSpan" class="text-gray-900 font-semibold">Your Brand</span>
      </span>
    </div>

    <!-- Header Actions -->
    <div class="flex items-center gap-2">
      <!-- Quick Demos -->
      <div class="hidden lg:flex items-center gap-1 text-xs text-gray-500 mr-2 border-r border-gray-200 pr-3">
        <span class="text-[11px] text-gray-400">Load Template:</span>
        <button onclick="loadTemplate('clean')" class="px-2 py-1 text-xs font-medium text-gray-700 bg-gray-100 hover:bg-gray-200 rounded transition">Generic Clean</button>
        <button onclick="loadTemplate('saas')" class="px-2 py-1 text-xs font-medium text-blue-700 bg-blue-50 hover:bg-blue-100 rounded transition">SaaS Tech</button>
        <button onclick="loadTemplate('retail')" class="px-2 py-1 text-xs font-medium text-emerald-700 bg-emerald-50 hover:bg-emerald-100 rounded transition">Ecommerce / Travel</button>
        <button onclick="resetToEmpty()" class="px-2 py-1 text-xs font-medium text-red-600 hover:bg-red-50 rounded transition" title="Clear all fields">Clear All</button>
      </div>

      <!-- Live Presentation Session Button -->
      <button onclick="togglePresentationMode(true)" class="flex items-center gap-1.5 px-3 py-1.5 text-xs font-semibold text-white bg-blue-600 hover:bg-blue-700 rounded-md transition shadow-xs">
        <i data-lucide="monitor-play" class="w-3.5 h-3.5"></i>
        <span>Client Presentation Mode</span>
      </button>

      <button onclick="openExportModal()" class="flex items-center gap-1.5 px-3 py-1.5 text-xs font-medium text-gray-700 bg-white border border-gray-300 hover:bg-gray-50 rounded-md transition shadow-xs">
        <i data-lucide="share-2" class="w-3.5 h-3.5 text-gray-500"></i>
        <span class="hidden sm:inline">Export / Sign-off</span>
      </button>
    </div>
  </header>

  <!-- WORKSPACE BODY (Split Screen or Full Presentation) -->
  <div class="flex-1 flex overflow-hidden relative">

    <!-- LEFT COLUMN: ASSET INPUT EDITOR (45% Width) -->
    <div id="editorPanel" class="w-full lg:w-[46%] xl:w-[44%] bg-white border-r border-gray-200 flex flex-col h-full overflow-hidden transition-all duration-300">
      
      <!-- Panel Header with Ad Strength Score -->
      <div class="px-5 py-3 border-b border-gray-200 bg-gray-50/80 flex items-center justify-between flex-shrink-0">
        <div>
          <h2 class="text-xs font-bold uppercase tracking-wider text-gray-700 flex items-center gap-2">
            <span>Asset Builder</span>
            <span class="text-[11px] font-normal text-gray-500 capitalize">• PMax Official Spec</span>
          </h2>
          <p class="text-[11px] text-gray-500">Enter copy & creatives to preview omnichannel ads</p>
        </div>

        <!-- Google Ad Strength Meter Widget -->
        <div class="flex items-center gap-2.5 bg-white px-3 py-1.5 rounded-lg border border-gray-200 shadow-2xs">
          <div class="relative w-7 h-7 flex items-center justify-center">
            <svg class="w-7 h-7 transform -rotate-90">
              <circle cx="14" cy="14" r="11" stroke="#e5e7eb" stroke-width="3" fill="transparent"></circle>
              <circle id="strengthCircle" cx="14" cy="14" r="11" stroke="#1e8e3e" stroke-width="3" fill="transparent" stroke-dasharray="69.1" stroke-dashoffset="15"></circle>
            </svg>
            <i data-lucide="check" id="strengthIcon" class="w-3.5 h-3.5 text-green-600 absolute"></i>
          </div>
          <div>
            <div class="text-[9px] text-gray-400 uppercase tracking-wider font-semibold">Ad Strength</div>
            <div id="strengthText" class="text-xs font-bold text-green-700">Excellent</div>
          </div>
        </div>
      </div>

      <!-- Scrollable Form Inputs -->
      <div class="flex-1 overflow-y-auto p-5 space-y-5 custom-scrollbar text-xs select-text">

        <!-- 1. Identity & URLs -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3.5">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
              <i data-lucide="globe" class="w-3.5 h-3.5 text-blue-600"></i> Core Business Identity & URLs
            </span>
          </div>

          <!-- Business Name -->
          <div>
            <div class="flex justify-between items-center mb-1">
              <label class="font-medium text-gray-700">Business Name <span class="text-red-500">*</span></label>
              <span id="counter-businessName" class="font-mono text-gray-400">0 / 25</span>
            </div>
            <input type="text" id="input-businessName" maxlength="25"
              placeholder="e.g. Acme Corp"
              class="w-full px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md focus:ring-1 focus:ring-blue-500 focus:border-blue-500 outline-none"
              oninput="handleScalarInput('businessName', 25)">
          </div>

          <!-- Final URL -->
          <div>
            <div class="flex justify-between items-center mb-1">
              <label class="font-medium text-gray-700">Final Landing Page URL <span class="text-red-500">*</span></label>
            </div>
            <input type="url" id="input-finalUrl"
              placeholder="https://www.acme.com/offer"
              class="w-full px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md focus:ring-1 focus:ring-blue-500 outline-none"
              oninput="handleScalarInput('finalUrl', 200)">
          </div>

          <!-- Display Path 1 & 2 -->
          <div class="grid grid-cols-2 gap-3">
            <div>
              <div class="flex justify-between items-center mb-1">
                <label class="font-medium text-gray-700">Display Path 1</label>
                <span id="counter-path1" class="font-mono text-gray-400">0 / 15</span>
              </div>
              <div class="flex items-center border border-gray-300 rounded-md bg-white overflow-hidden">
                <span class="px-2 text-gray-400 bg-gray-50 border-r border-gray-200">/</span>
                <input type="text" id="input-path1" maxlength="15" placeholder="Special-Offer"
                  class="w-full px-2 py-1.5 text-xs border-0 outline-none"
                  oninput="handleScalarInput('path1', 15)">
              </div>
            </div>
            <div>
              <div class="flex justify-between items-center mb-1">
                <label class="font-medium text-gray-700">Display Path 2</label>
                <span id="counter-path2" class="font-mono text-gray-400">0 / 15</span>
              </div>
              <div class="flex items-center border border-gray-300 rounded-md bg-white overflow-hidden">
                <span class="px-2 text-gray-400 bg-gray-50 border-r border-gray-200">/</span>
                <input type="text" id="input-path2" maxlength="15" placeholder="Official"
                  class="w-full px-2 py-1.5 text-xs border-0 outline-none"
                  oninput="handleScalarInput('path2', 15)">
              </div>
            </div>
          </div>

          <!-- CTA dropdown -->
          <div>
            <label class="font-medium text-gray-700 block mb-1">Call to Action (CTA)</label>
            <select id="input-cta" class="w-full px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md focus:ring-1 focus:ring-blue-500 outline-none" onchange="handleScalarInput('cta', 30)">
              <option value="Learn more">Learn more</option>
              <option value="Shop now">Shop now</option>
              <option value="Sign up">Sign up</option>
              <option value="Get quote">Get quote</option>
              <option value="Book now">Book now</option>
              <option value="Subscribe">Subscribe</option>
              <option value="Contact us">Contact us</option>
              <option value="Download">Download</option>
            </select>
          </div>
        </div>

        <!-- 2. Headlines (Up to 15, max 30 chars each) -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <div>
              <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
                <i data-lucide="type" class="w-3.5 h-3.5 text-blue-600"></i> Headlines (Up to 30 Chars)
              </span>
              <p class="text-[10px] text-gray-500">Google rotates up to 3 headlines dynamically in Search & Display</p>
            </div>
            <button onclick="addHeadline()" class="text-[11px] font-semibold text-blue-600 hover:text-blue-800 flex items-center gap-1">
              <i data-lucide="plus" class="w-3 h-3"></i> Add (Max 15)
            </button>
          </div>

          <div id="headlinesContainer" class="space-y-2">
            <!-- Injected dynamically -->
          </div>
        </div>

        <!-- 3. Long Headlines (Up to 5, max 90 chars each) -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <div>
              <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
                <i data-lucide="align-left" class="w-3.5 h-3.5 text-blue-600"></i> Long Headlines (Up to 90 Chars)
              </span>
              <p class="text-[10px] text-gray-500">Appears on larger YouTube, Discover & GDN banner slots</p>
            </div>
            <button onclick="addLongHeadline()" class="text-[11px] font-semibold text-blue-600 hover:text-blue-800 flex items-center gap-1">
              <i data-lucide="plus" class="w-3 h-3"></i> Add (Max 5)
            </button>
          </div>

          <div id="longHeadlinesContainer" class="space-y-2">
            <!-- Injected dynamically -->
          </div>
        </div>

        <!-- 4. Descriptions (1 Short 60 char, up to 4 Long 90 chars) -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <div>
              <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
                <i data-lucide="file-text" class="w-3.5 h-3.5 text-blue-600"></i> Descriptions
              </span>
              <p class="text-[10px] text-gray-500">Provide 1 short (60c) and up to 4 detailed descriptions (90c)</p>
            </div>
            <button onclick="addDescription()" class="text-[11px] font-semibold text-blue-600 hover:text-blue-800 flex items-center gap-1">
              <i data-lucide="plus" class="w-3 h-3"></i> Add (Max 4)
            </button>
          </div>

          <!-- Short Description (60 chars) -->
          <div class="p-2.5 bg-white rounded-lg border border-gray-200">
            <div class="flex justify-between items-center mb-1">
              <span class="font-medium text-gray-700">Short Description (Max 60 Chars)</span>
              <span id="counter-shortDesc" class="font-mono text-gray-400">0 / 60</span>
            </div>
            <input type="text" id="input-shortDesc" maxlength="60"
              placeholder="e.g. Elevate your everyday routine with verified expert solutions."
              class="w-full px-3 py-1.5 text-xs bg-gray-50 border border-gray-300 rounded focus:bg-white outline-none"
              oninput="handleScalarInput('shortDesc', 60)">
          </div>

          <div id="descriptionsContainer" class="space-y-2">
            <!-- Injected dynamically -->
          </div>
        </div>

        <!-- 5. Creative Assets (Images, Logo, Video) -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3.5">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
              <i data-lucide="image" class="w-3.5 h-3.5 text-blue-600"></i> Visual Media Assets
            </span>
            <span class="text-[10px] text-gray-500">Landscape (1.91:1) & Logo (1:1)</span>
          </div>

          <!-- Marketing Hero Image -->
          <div>
            <label class="font-medium text-gray-700 block mb-1">Marketing Hero Landscape (1200 x 628)</label>
            <div class="flex gap-2">
              <input type="text" id="input-heroImage" placeholder="https://image-url..."
                class="flex-1 px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md outline-none"
                oninput="handleScalarInput('heroImage', 300)">
              <label class="px-2.5 py-1.5 bg-gray-100 hover:bg-gray-200 border border-gray-300 rounded-md cursor-pointer font-medium text-gray-700 flex items-center gap-1 flex-shrink-0">
                <i data-lucide="upload" class="w-3 h-3"></i>
                <span>Upload</span>
                <input type="file" accept="image/*" class="hidden" onchange="handleFileUpload(event, 'heroImage')">
              </label>
            </div>
          </div>

          <!-- Brand Logo Square -->
          <div>
            <label class="font-medium text-gray-700 block mb-1">Brand Square Logo (1:1)</label>
            <div class="flex gap-2 items-center">
              <div class="w-8 h-8 rounded border border-gray-300 bg-white p-0.5 flex items-center justify-center overflow-hidden flex-shrink-0">
                <img id="formLogoThumb" src="" class="w-full h-full object-contain" alt="Logo">
              </div>
              <input type="text" id="input-logoImage" placeholder="https://logo-url..."
                class="flex-1 px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md outline-none"
                oninput="handleScalarInput('logoImage', 300)">
              <label class="px-2.5 py-1.5 bg-gray-100 hover:bg-gray-200 border border-gray-300 rounded-md cursor-pointer font-medium text-gray-700 flex items-center gap-1 flex-shrink-0">
                <i data-lucide="upload" class="w-3 h-3"></i>
                <span>Upload</span>
                <input type="file" accept="image/*" class="hidden" onchange="handleFileUpload(event, 'logoImage')">
              </label>
            </div>
          </div>

          <!-- YouTube Video Thumbnail/Video Asset -->
          <div>
            <label class="font-medium text-gray-700 block mb-1">YouTube Video Asset (Preview Thumbnail)</label>
            <input type="text" id="input-videoThumbnail" placeholder="https://video-preview-image..."
              class="w-full px-3 py-1.5 text-xs bg-white border border-gray-300 rounded-md outline-none"
              oninput="handleScalarInput('videoThumbnail', 300)">
          </div>
        </div>

        <!-- 6. Sitelinks Extensions (Max 4) -->
        <div class="bg-gray-50/70 rounded-xl p-4 border border-gray-200 space-y-3">
          <div class="flex items-center justify-between pb-1 border-b border-gray-200">
            <div>
              <span class="font-semibold text-gray-800 uppercase tracking-wide text-[11px] flex items-center gap-1.5">
                <i data-lucide="link-2" class="w-3.5 h-3.5 text-blue-600"></i> Sitelinks Extensions (Up to 4)
              </span>
              <p class="text-[10px] text-gray-500">Expands Search real estate with deep-link navigation</p>
            </div>
            <button onclick="addSitelink()" class="text-[11px] font-semibold text-blue-600 hover:text-blue-800 flex items-center gap-1">
              <i data-lucide="plus" class="w-3 h-3"></i> Add Sitelink
            </button>
          </div>

          <div id="sitelinksContainer" class="space-y-3">
            <!-- Injected dynamically -->
          </div>
        </div>

      </div>
    </div>

    <!-- RIGHT COLUMN: DEDICATED AD PREVIEW SESSION -->
    <div id="previewSessionPanel" class="flex-1 bg-[#f0f3f6] flex flex-col h-full overflow-hidden transition-all duration-300">
      
      <!-- Preview Session Bar & Channel Selectors -->
      <div class="bg-white border-b border-gray-200 px-4 md:px-6 py-2.5 flex items-center justify-between flex-shrink-0 shadow-2xs">
        
        <!-- Channels (Search, GDN, YouTube, Discover, Gmail, All) -->
        <div class="flex items-center space-x-1 sm:space-x-1.5 overflow-x-auto pb-1 sm:pb-0" id="channelTabNav">
          <button onclick="switchChannel('search')" id="tab-search" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-semibold bg-blue-50 text-blue-700 border border-blue-200">
            <svg class="w-3.5 h-3.5" viewBox="0 0 24 24"><path fill="#4285F4" d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2zm-1 14.5v-9l6 4.5z"/></svg>
            <span>Search</span>
          </button>
          <button onclick="switchChannel('display')" id="tab-display" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100">
            <i data-lucide="layout-grid" class="w-3.5 h-3.5 text-green-600"></i>
            <span>Display</span>
          </button>
          <button onclick="switchChannel('youtube')" id="tab-youtube" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100">
            <i data-lucide="youtube" class="w-3.5 h-3.5 text-red-600"></i>
            <span>YouTube</span>
          </button>
          <button onclick="switchChannel('discover')" id="tab-discover" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100">
            <i data-lucide="compass" class="w-3.5 h-3.5 text-yellow-600"></i>
            <span>Discover</span>
          </button>
          <button onclick="switchChannel('gmail')" id="tab-gmail" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100">
            <i data-lucide="mail" class="w-3.5 h-3.5 text-red-500"></i>
            <span>Gmail</span>
          </button>
          <button onclick="switchChannel('all')" id="tab-all" class="channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100">
            <i data-lucide="layers" class="w-3.5 h-3.5 text-indigo-600"></i>
            <span>All Channels View</span>
          </button>
        </div>

        <!-- Session Controls: Shuffle + Device Toggle + Fullscreen Preview -->
        <div class="flex items-center gap-2 flex-shrink-0">
          <!-- ML Shuffle Button -->
          <button onclick="shuffleMachineLearningCopy()" title="Simulate how Google dynamically matches different headlines and descriptions"
            class="flex items-center gap-1 px-2.5 py-1.5 text-xs font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 transition shadow-2xs">
            <i data-lucide="shuffle" class="w-3.5 h-3.5 text-blue-600"></i>
            <span class="hidden md:inline">Shuffle Copy</span>
          </button>

          <!-- Device Toggle -->
          <div class="bg-gray-100 p-0.5 rounded-lg flex items-center border border-gray-200">
            <button onclick="setDeviceView('mobile')" id="btn-device-mobile" class="px-2 py-1 rounded-md text-xs font-medium bg-white text-gray-800 shadow-2xs flex items-center gap-1">
              <i data-lucide="smartphone" class="w-3.5 h-3.5"></i>
              <span class="hidden sm:inline">Mobile</span>
            </button>
            <button onclick="setDeviceView('desktop')" id="btn-device-desktop" class="px-2 py-1 rounded-md text-xs font-medium text-gray-500 hover:text-gray-800 flex items-center gap-1">
              <i data-lucide="monitor" class="w-3.5 h-3.5"></i>
              <span class="hidden sm:inline">Desktop</span>
            </button>
          </div>

          <!-- Presentation Mode Expand / Collapse button -->
          <button onclick="togglePresentationMode()" id="presentationModeToggleBtn"
            title="Expand to Full Client Presentation Screen"
            class="p-1.5 rounded-md border border-gray-300 bg-white hover:bg-gray-50 text-gray-600 transition">
            <i data-lucide="maximize-2" id="presentationIcon" class="w-4 h-4"></i>
          </button>
        </div>
      </div>

      <!-- Presentation Mode Banner (Shown only when in full client session) -->
      <div id="presentationNotice" class="hidden bg-gradient-to-r from-blue-600 to-indigo-700 text-white px-4 py-2 text-xs flex items-center justify-between shadow-xs">
        <div class="flex items-center gap-2 font-medium">
          <i data-lucide="presentation" class="w-4 h-4 text-blue-200"></i>
          <span><strong>Client Review Session:</strong> Fullscreen Ad Preview active. Editor panel collapsed for clean client presentation.</span>
        </div>
        <div class="flex items-center gap-2">
          <button onclick="shuffleMachineLearningCopy()" class="px-2.5 py-1 bg-white/20 hover:bg-white/30 rounded text-xs font-medium transition flex items-center gap-1">
            <i data-lucide="refresh-cw" class="w-3 h-3"></i>
            <span>Rotate ML Combination</span>
          </button>
          <button onclick="togglePresentationMode(false)" class="px-2.5 py-1 bg-white text-blue-700 hover:bg-blue-50 rounded text-xs font-bold transition">
            Exit Presentation
          </button>
        </div>
      </div>

      <!-- Viewport Canvas for Ads -->
      <div class="flex-1 overflow-y-auto p-4 md:p-8 flex justify-center items-start custom-scrollbar" id="previewViewport">
        <div id="previewCanvasWrapper" class="w-full max-w-md transition-all duration-300">
          
          <!-- 1. SEARCH PREVIEW -->
          <div id="channel-view-search" class="space-y-4">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span class="flex items-center gap-1.5"><i data-lucide="search" class="w-3.5 h-3.5 text-blue-500"></i> Google Search SERP Placement</span>
              <span class="text-[11px] text-gray-400">Sponsored Ad #1</span>
            </div>

            <!-- Realistic Google SERP Card -->
            <div class="bg-white rounded-2xl p-5 border border-gray-200 shadow-sm font-sans">
              <!-- Search query simulation -->
              <div class="flex items-center gap-2 pb-3 mb-3 border-b border-gray-100 text-xs text-gray-600">
                <span class="font-google font-bold text-base text-gray-800 tracking-tight">Google</span>
                <div class="flex-1 bg-gray-100 rounded-full px-3 py-1.5 text-xs text-gray-600 truncate flex items-center justify-between">
                  <span id="searchMockQuery">your brand products online</span>
                  <i data-lucide="search" class="w-3 h-3 text-gray-400"></i>
                </div>
              </div>

              <!-- Top Favicon & URL Domain -->
              <div class="flex items-center gap-2 mb-1.5">
                <div class="w-6 h-6 rounded-full bg-gray-100 flex items-center justify-center overflow-hidden border border-gray-200">
                  <img id="serpFavicon" src="" class="w-4 h-4 object-contain" alt="Favicon">
                </div>
                <div class="leading-tight min-w-0">
                  <div class="flex items-center gap-1.5">
                    <span id="serpBusinessName" class="text-xs font-normal text-[#202124]">Your Brand</span>
                    <span class="text-[10px] text-gray-400">•</span>
                    <span class="text-[10px] font-bold text-[#202124] uppercase tracking-wide">Sponsored</span>
                  </div>
                  <div class="text-[11px] text-[#202124] truncate" id="serpDisplayUrl">
                    https://www.yourbrand.com › Special-Offer
                  </div>
                </div>
              </div>

              <!-- Blue Google Search Headline combination -->
              <h3 class="text-lg leading-snug font-roboto text-[#1a0dab] hover:underline cursor-pointer mb-1.5 font-normal serp-link" id="serpHeadline">
                Top Rated Solutions | Official Brand Site | Save Today
              </h3>

              <!-- SERP Description -->
              <p class="text-xs text-[#4d5156] leading-relaxed mb-3" id="serpDescription">
                Discover exceptional quality and performance built for your lifestyle. Explore full range and unlock free shipping today.
              </p>

              <!-- SERP Sitelinks Grid -->
              <div id="serpSitelinksContainer" class="grid grid-cols-1 sm:grid-cols-2 gap-2 pt-2 border-t border-gray-100">
                <!-- Dynamic Sitelinks -->
              </div>
            </div>

            <!-- Notice card -->
            <div class="bg-blue-50/70 rounded-lg p-3 text-xs text-blue-800 border border-blue-100 flex items-start gap-2">
              <i data-lucide="sparkles" class="w-4 h-4 text-blue-600 flex-shrink-0 mt-0.5"></i>
              <span>Google automatically pairs high-performing headlines and descriptions dynamically based on real-time user query intent.</span>
            </div>
          </div>

          <!-- 2. DISPLAY NETWORK PREVIEW -->
          <div id="channel-view-display" class="hidden space-y-6">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span class="flex items-center gap-1.5"><i data-lucide="layout-grid" class="w-3.5 h-3.5 text-green-500"></i> Google Display Network (GDN) Responsive Formats</span>
              <span class="text-[11px] text-gray-400">3M+ Publisher Sites & Apps</span>
            </div>

            <!-- In-Feed Responsive Display Banner -->
            <div class="bg-white rounded-xl border border-gray-200 overflow-hidden shadow-sm">
              <div class="px-3 py-1.5 bg-gray-50 border-b border-gray-200 flex justify-between items-center text-[11px] text-gray-500">
                <span>Native Responsive Feed Card</span>
                <span class="bg-gray-200 text-gray-700 px-1 rounded text-[10px]">Ad</span>
              </div>
              <div class="p-3">
                <div class="relative rounded-lg overflow-hidden bg-gray-900 aspect-[16/9] mb-3">
                  <img id="displayHeroImg1" src="" class="w-full h-full object-cover" alt="Hero">
                  <div class="absolute top-2 left-2 bg-black/60 text-white text-[10px] px-2 py-0.5 rounded backdrop-blur-xs">
                    Sponsored by <span id="displayBadgeBrand">Your Brand</span>
                  </div>
                </div>
                <div class="flex items-start justify-between gap-3">
                  <div class="flex-1 min-w-0">
                    <h4 id="displayNativeTitle" class="text-sm font-semibold text-gray-900 line-clamp-1 mb-1">Empowering Your Daily Workflow</h4>
                    <p id="displayNativeDesc" class="text-xs text-gray-600 line-clamp-2">Experience seamless quality and unmatched speed built for modern workflows.</p>
                  </div>
                  <button id="displayNativeCta" class="px-3.5 py-1.5 bg-blue-600 hover:bg-blue-700 text-white font-medium text-xs rounded shadow-xs whitespace-nowrap">
                    Learn more
                  </button>
                </div>
              </div>
            </div>

            <!-- 300x250 Medium Rectangle (MPU) Banner -->
            <div class="flex flex-col items-center">
              <div class="text-[11px] text-gray-400 mb-1">Standard Rectangle (300 x 250)</div>
              <div class="w-[300px] h-[250px] bg-white border border-gray-300 rounded shadow-sm relative flex flex-col justify-between p-3 overflow-hidden">
                <div class="absolute top-1 right-1 flex items-center gap-0.5 bg-white/90 px-1 rounded text-[9px] text-gray-400">
                  <span>Ad</span>
                  <i data-lucide="info" class="w-2.5 h-2.5"></i>
                </div>
                <div class="h-[120px] rounded overflow-hidden mb-2">
                  <img id="displayMpuImg" src="" class="w-full h-full object-cover" alt="Display visual">
                </div>
                <div class="flex-1 flex flex-col justify-between">
                  <div>
                    <h5 id="displayMpuTitle" class="text-xs font-bold text-gray-900 line-clamp-1">Transform Your Daily Results</h5>
                    <p id="displayMpuDesc" class="text-[11px] text-gray-600 line-clamp-2 leading-tight mt-0.5">Explore premium solutions tailored for your business needs today.</p>
                  </div>
                  <div class="flex items-center justify-between pt-1">
                    <span id="displayMpuBrand" class="text-[10px] text-gray-400 font-medium">Your Brand</span>
                    <span id="displayMpuCta" class="px-2.5 py-1 bg-blue-600 text-white text-[11px] font-medium rounded">Shop now</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- 3. YOUTUBE AD PREVIEW -->
          <div id="channel-view-youtube" class="hidden space-y-4">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span class="flex items-center gap-1.5"><i data-lucide="youtube" class="w-3.5 h-3.5 text-red-600"></i> YouTube Mobile In-Stream & Feed Video Ad</span>
              <span class="text-[11px] text-gray-400">TrueView In-Stream Simulation</span>
            </div>

            <!-- Video Player Ad Simulation Card -->
            <div class="bg-white rounded-xl overflow-hidden border border-gray-200 shadow-sm">
              <div class="relative bg-black aspect-video overflow-hidden">
                <img id="ytVideoThumb" src="" class="w-full h-full object-cover opacity-90" alt="Video cover">
                <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-black/30 pointer-events-none"></div>

                <!-- Video Top Bar -->
                <div class="absolute top-2 left-3 flex items-center gap-2">
                  <span class="bg-yellow-400 text-black text-[10px] font-bold px-1.5 py-0.5 rounded">Ad</span>
                  <span class="text-white text-xs font-mono">0:15 / 0:30</span>
                </div>

                <!-- Skip Button -->
                <div class="absolute bottom-3 right-3 bg-black/70 border border-white/20 text-white text-xs px-3 py-1.5 rounded flex items-center gap-1">
                  <span>Skip Ad in 5s</span>
                  <i data-lucide="skip-forward" class="w-3 h-3"></i>
                </div>

                <!-- In-Stream CTA Overlay Banner -->
                <div class="absolute bottom-3 left-3 right-32 flex items-center gap-2 bg-black/60 backdrop-blur-md p-1.5 rounded-lg border border-white/10">
                  <img id="ytLogoOverlay" src="" class="w-7 h-7 rounded-full object-cover" alt="Logo">
                  <div class="min-w-0 flex-1">
                    <div id="ytOverlayTitle" class="text-white text-xs font-medium truncate">Transform Your Experience</div>
                    <div id="ytOverlayUrl" class="text-gray-300 text-[10px] truncate">yourbrand.com</div>
                  </div>
                  <span id="ytOverlayCta" class="px-2.5 py-1 bg-blue-500 text-white text-[11px] font-semibold rounded whitespace-nowrap">Learn more</span>
                </div>
              </div>

              <!-- Channel Info Below Video -->
              <div class="p-3.5">
                <div class="flex items-start gap-3">
                  <img id="ytAvatar" src="" class="w-9 h-9 rounded-full object-cover mt-0.5 border" alt="Channel avatar">
                  <div class="flex-1 min-w-0">
                    <div class="flex items-center gap-1.5">
                      <span class="text-[10px] font-bold uppercase bg-yellow-100 text-yellow-800 px-1 rounded">Sponsored</span>
                      <span id="ytChannelName" class="text-xs font-semibold text-gray-800">Your Brand Official</span>
                    </div>
                    <h3 id="ytMainTitle" class="text-sm font-semibold text-gray-900 mt-1 line-clamp-2 leading-snug">
                      Discover the next-generation approach to efficiency and speed. Built for ambitious teams.
                    </h3>
                    <div class="mt-2.5">
                      <button id="ytBottomCta" class="w-full py-2 bg-blue-600 hover:bg-blue-700 text-white text-xs font-semibold rounded-full flex items-center justify-center gap-1.5 shadow-2xs">
                        <span id="ytBottomCtaText">Learn more</span>
                        <i data-lucide="external-link" class="w-3 h-3"></i>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- 4. GOOGLE DISCOVER PREVIEW -->
          <div id="channel-view-discover" class="hidden space-y-4">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span class="flex items-center gap-1.5"><i data-lucide="compass" class="w-3.5 h-3.5 text-yellow-600"></i> Google App & Android Discover Feed</span>
              <span class="text-[11px] text-gray-400">Mobile Homepage Feed</span>
            </div>

            <!-- Google Discover Feed Card -->
            <div class="bg-white rounded-2xl overflow-hidden border border-gray-200 shadow-sm font-sans">
              <!-- Large Landscape Image (1.91:1) -->
              <div class="relative aspect-[1.91/1] bg-gray-100">
                <img id="discoverHeroImg" src="" class="w-full h-full object-cover" alt="Discover image">
                <span class="absolute bottom-2 left-2 bg-black/60 text-white text-[10px] px-2 py-0.5 rounded backdrop-blur-xs font-medium">
                  Sponsored
                </span>
              </div>

              <div class="p-4">
                <h3 id="discoverTitle" class="text-base font-semibold text-gray-900 leading-snug mb-1.5 font-google">
                  Upgrade your daily toolkit with industry-leading features tailored for maximum performance.
                </h3>
                <p id="discoverDesc" class="text-xs text-gray-600 line-clamp-2 mb-3">
                  Discover reliable engineering and modern convenience in one smart, integrated package.
                </p>

                <!-- Footer row -->
                <div class="flex items-center justify-between pt-2 border-t border-gray-100 text-xs text-gray-500">
                  <div class="flex items-center gap-2">
                    <img id="discoverLogo" src="" class="w-4 h-4 rounded-full object-contain border" alt="Site icon">
                    <span id="discoverBrand" class="font-medium text-gray-800">Your Brand</span>
                    <span class="text-[11px] text-gray-400">•</span>
                    <span class="text-[10px] font-bold text-gray-500 uppercase">Ad</span>
                  </div>

                  <div class="flex items-center gap-3 text-gray-400">
                    <button class="hover:text-gray-600"><i data-lucide="share-2" class="w-4 h-4"></i></button>
                    <button class="hover:text-gray-600"><i data-lucide="more-vertical" class="w-4 h-4"></i></button>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- 5. GMAIL PREVIEWS (Teaser & Opened) -->
          <div id="channel-view-gmail" class="hidden space-y-5">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span class="flex items-center gap-1.5"><i data-lucide="mail" class="w-3.5 h-3.5 text-red-500"></i> Gmail Promotions Tab (Closed Teaser & Open Ad)</span>
              <span class="text-[11px] text-gray-400">1.8 Billion Active Inboxes</span>
            </div>

            <!-- Closed Teaser Row in Promotions -->
            <div class="bg-white rounded-xl border border-gray-200 overflow-hidden shadow-sm">
              <div class="px-3 py-1.5 bg-gray-50 text-[11px] text-gray-500 border-b border-gray-200">
                1. Closed Teaser (Promotions Inbox Row)
              </div>
              <div class="p-3 flex items-center gap-3 hover:bg-gray-50 transition cursor-pointer">
                <img id="gmailTeaserLogo" src="" class="w-8 h-8 rounded-full object-cover border flex-shrink-0" alt="Logo">
                <div class="min-w-0 flex-1">
                  <div class="flex items-center justify-between">
                    <div class="flex items-center gap-1.5">
                      <span class="text-[10px] font-bold bg-[#1e8e3e] text-white px-1.5 py-0.2 rounded font-sans">Ad</span>
                      <span id="gmailTeaserBrand" class="text-xs font-bold text-gray-900 truncate">Your Brand</span>
                    </div>
                    <span class="text-[10px] text-gray-400">Sponsored</span>
                  </div>
                  <div class="text-xs text-gray-800 font-semibold truncate" id="gmailTeaserSubject">
                    Experience modern solutions designed for maximum productivity.
                  </div>
                  <div class="text-[11px] text-gray-500 truncate" id="gmailTeaserSnippet">
                    Get started today and discover exclusive offers built for your needs.
                  </div>
                </div>
              </div>
            </div>

            <!-- Expanded Opened Email Ad -->
            <div class="bg-white rounded-xl border border-gray-200 overflow-hidden shadow-sm font-sans">
              <div class="px-3 py-1.5 bg-gray-50 text-[11px] text-gray-500 border-b border-gray-200 flex justify-between items-center">
                <span>2. Expanded View (Opened Rich Email Ad)</span>
                <span class="text-[10px] text-gray-400">Interactive Creative</span>
              </div>
              <div class="p-4 space-y-3">
                <div class="flex items-center justify-between pb-3 border-b border-gray-100">
                  <div class="flex items-center gap-2.5">
                    <img id="gmailOpenLogo" src="" class="w-8 h-8 rounded-full object-cover border" alt="Brand">
                    <div>
                      <div class="flex items-center gap-1.5">
                        <span id="gmailOpenBrand" class="text-xs font-bold text-gray-900">Your Brand</span>
                        <span class="text-[10px] bg-green-100 text-green-800 font-bold px-1 rounded">Ad</span>
                      </div>
                      <div class="text-[11px] text-gray-500" id="gmailOpenFromEmail">offers@yourbrand.com</div>
                    </div>
                  </div>
                  <span class="text-xs text-gray-400">To: you</span>
                </div>

                <h3 id="gmailOpenHeadline" class="text-base font-bold text-gray-900">
                  Elevate Your Business Results with Proven Smart Tools
                </h3>
                <div class="rounded-lg overflow-hidden border border-gray-200">
                  <img id="gmailOpenHeroImg" src="" class="w-full aspect-[16/9] object-cover" alt="Email visual">
                </div>
                <p id="gmailOpenBody" class="text-xs text-gray-600 leading-relaxed">
                  Join thousands of satisfied clients who unlocked faster growth and reliable operations. Learn how our tailored approach helps you succeed today.
                </p>
                <div class="pt-2 flex justify-center">
                  <button id="gmailOpenCta" class="px-6 py-2 bg-blue-600 hover:bg-blue-700 text-white font-medium text-xs rounded-full shadow-sm">
                    Learn more
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- 6. ALL CHANNELS OMNICHANNEL OVERVIEW -->
          <div id="channel-view-all" class="hidden space-y-4">
            <div class="text-xs font-medium text-gray-500 flex items-center justify-between px-1">
              <span>Full Performance Max Omnichannel Overview</span>
              <span class="text-[11px] text-gray-400">Simultaneous Delivery</span>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <!-- Search Tile -->
              <div class="bg-white p-3.5 rounded-xl border border-gray-200 shadow-2xs">
                <div class="text-[11px] font-bold text-blue-600 mb-1.5 flex items-center gap-1">
                  <i data-lucide="search" class="w-3.5 h-3.5"></i> Google Search SERP
                </div>
                <div class="text-xs text-blue-800 font-medium truncate" id="allSearchHead">High Quality Solutions</div>
                <div class="text-[11px] text-gray-500 line-clamp-2 mt-1" id="allSearchDesc">Engineered for reliability and measurable real-world performance.</div>
              </div>

              <!-- Display Tile -->
              <div class="bg-white p-3.5 rounded-xl border border-gray-200 shadow-2xs">
                <div class="text-[11px] font-bold text-green-600 mb-1.5 flex items-center gap-1">
                  <i data-lucide="layout-grid" class="w-3.5 h-3.5"></i> Display Network
                </div>
                <img id="allDisplayImg" src="" class="w-full h-20 object-cover rounded mb-1.5" alt="Display">
                <div class="text-xs font-semibold text-gray-800 truncate" id="allDisplayHead">Modern Growth Tools</div>
              </div>

              <!-- YouTube Tile -->
              <div class="bg-white p-3.5 rounded-xl border border-gray-200 shadow-2xs">
                <div class="text-[11px] font-bold text-red-600 mb-1.5 flex items-center gap-1">
                  <i data-lucide="youtube" class="w-3.5 h-3.5"></i> YouTube Ads
                </div>
                <div class="relative h-20 rounded overflow-hidden bg-black mb-1.5">
                  <img id="allYtImg" src="" class="w-full h-full object-cover opacity-80" alt="YT">
                  <span class="absolute bottom-1 right-1 text-[9px] bg-black/80 text-white px-1 rounded">0:30</span>
                </div>
                <div class="text-xs text-gray-800 font-medium truncate" id="allYtHead">Official Video Spotlight</div>
              </div>

              <!-- Discover & Gmail Tile -->
              <div class="bg-white p-3.5 rounded-xl border border-gray-200 shadow-2xs">
                <div class="text-[11px] font-bold text-yellow-600 mb-1.5 flex items-center gap-1">
                  <i data-lucide="compass" class="w-3.5 h-3.5"></i> Discover & Gmail
                </div>
                <div class="text-xs font-medium text-gray-900 truncate" id="allDiscoverHead">Top Rated Smart Tools</div>
                <div class="text-[11px] text-gray-500 mt-1">Reaches mobile high-intent feeds and personal inboxes directly.</div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>

  <!-- EXPORT & CLIENT PRESENTATION MODAL -->
  <div id="exportModal" class="fixed inset-0 bg-black/60 z-50 flex items-center justify-center p-4 hidden backdrop-blur-xs">
    <div class="bg-white rounded-2xl max-w-lg w-full p-6 shadow-2xl space-y-4">
      <div class="flex items-center justify-between border-b border-gray-100 pb-3">
        <div class="flex items-center gap-2">
          <i data-lucide="file-check-2" class="w-5 h-5 text-blue-600"></i>
          <h3 class="text-base font-semibold text-gray-900">Client Sign-Off & Deliverables</h3>
        </div>
        <button onclick="closeExportModal()" class="text-gray-400 hover:text-gray-600">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <p class="text-xs text-gray-600">
        Generate approved asset matrices or print this session for client presentation decks and media plans.
      </p>

      <div class="space-y-2.5">
        <button onclick="window.print()" class="w-full py-2.5 px-4 bg-gray-100 hover:bg-gray-200 rounded-lg text-xs font-semibold text-gray-800 flex items-center justify-center gap-2 transition">
          <i data-lucide="printer" class="w-4 h-4 text-gray-600"></i>
          <span>Print or Save Client Presentation (PDF)</span>
        </button>

        <button onclick="copyFormattedMatrix()" class="w-full py-2.5 px-4 bg-blue-600 hover:bg-blue-700 rounded-lg text-xs font-semibold text-white flex items-center justify-center gap-2 transition shadow-xs">
          <i data-lucide="clipboard-copy" class="w-4 h-4"></i>
          <span>Copy Complete Asset Matrix to Clipboard</span>
        </button>

        <button onclick="copyShareableUrl()" class="w-full py-2.5 px-4 border border-gray-300 hover:bg-gray-50 rounded-lg text-xs font-semibold text-gray-700 flex items-center justify-center gap-2 transition">
          <i data-lucide="link" class="w-4 h-4 text-gray-500"></i>
          <span>Copy Direct Link for Client</span>
        </button>
      </div>

      <div id="copyToast" class="hidden p-2 text-center text-xs font-medium text-emerald-800 bg-emerald-50 rounded border border-emerald-200">
        Copied to clipboard successfully!
      </div>
    </div>
  </div>

  <!-- APPLICATION LOGIC -->
  <script>
    // Pure, Generic Clean Defaults (Oral-B completely removed)
    const initialCleanState = {
      businessName: "Your Brand",
      finalUrl: "https://www.yourbrand.com/offer",
      path1: "Special-Offer",
      path2: "Official",
      cta: "Learn more",
      headlines: [
        "Elevate Your Daily Routine",
        "Top Rated Solutions Today",
        "Built For Modern Life",
        "Official Brand Store Online",
        "Experience Exceptional Quality"
      ],
      longHeadlines: [
        "Discover personalized, high-performance solutions tailored specifically for your lifestyle",
        "Engineered for speed, durability, and convenience. Experience the trusted choice today"
      ],
      shortDesc: "Elevate your everyday experience with verified expert solutions.",
      descriptions: [
        "Experience exceptional reliability, innovative design, and proven quality backed by experts.",
        "Join over 50,000 satisfied customers who upgraded their routine with our guaranteed products."
      ],
      heroImage: "https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1200&q=80",
      logoImage: "https://images.unsplash.com/photo-1599305445671-ac291c95aaa9?auto=format&fit=crop&w=150&q=80",
      videoThumbnail: "https://images.unsplash.com/photo-1531482615713-2afd69097998?auto=format&fit=crop&w=1200&q=80",
      sitelinks: [
        { text: "Product Catalog", desc1: "Browse all trending models", desc2: "Free shipping included" },
        { text: "Special Offers", desc1: "Save up to 30% today", desc2: "Limited time pricing" },
        { text: "Customer Reviews", desc1: "Rated 4.9 by users", desc2: "Verified purchases" },
        { text: "Help & Support", desc1: "24/7 dedicated assistance", desc2: "Fast reply time" }
      ],
      activeChannel: 'search',
      device: 'mobile',
      isPresentationMode: false,
      // Dynamic ML rotation indices
      headlineRotationIndex: 0,
      longHeadlineRotationIndex: 0,
      descRotationIndex: 0
    };

    // State instance
    let state = JSON.parse(JSON.stringify(initialCleanState));

    // Templates
    const templates = {
      clean: initialCleanState,
      saas: {
        businessName: "CloudScale HQ",
        finalUrl: "https://www.cloudscalehq.io/signup",
        path1: "Free-Trial",
        path2: "Cloud",
        cta: "Sign up",
        headlines: [
          "Scale Multicloud Infrastructure",
          "Cut Cloud Hosting Costs 40%",
          "Real-Time Analytics Cloud",
          "Automate DevOps Pipelines",
          "Enterprise Kubernetes Made Easy"
        ],
        longHeadlines: [
          "Simplify cloud infrastructure monitoring and eliminate surprise bills in under 5 minutes",
          "The modern developer observability platform trusted by over 2,000 engineering teams"
        ],
        shortDesc: "Effortless multicloud observability and automated cost control.",
        descriptions: [
          "Unify logs, metrics, and traces into a single high-performance dashboard. Start free.",
          "Prevent downtime before it impacts revenue with automated AI root-cause diagnostics."
        ],
        heroImage: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1200&q=80",
        logoImage: "https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?auto=format&fit=crop&w=150&q=80",
        videoThumbnail: "https://images.unsplash.com/photo-1551836022-d5d88e9218df?auto=format&fit=crop&w=1200&q=80",
        sitelinks: [
          { text: "Interactive Sandbox", desc1: "Try live without signup", desc2: "No credit card needed" },
          { text: "ROI Calculator", desc1: "See your cloud savings", desc2: "Instant estimate" },
          { text: "Security & SOC2", desc1: "Bank-grade encryption", desc2: "HIPAA & GDPR ready" },
          { text: "Transparent Pricing", desc1: "Plans start at $29/mo", desc2: "Cancel anytime" }
        ]
      },
      retail: {
        businessName: "Nordic Haven",
        finalUrl: "https://www.nordichaven.com/escape",
        path1: "Summer",
        path2: "Getaways",
        cta: "Book now",
        headlines: [
          "Curated Luxury Cabin Rentals",
          "Handpicked Coastal Escapes",
          "Unplug in Pure Nature",
          "Best Price Guarantee",
          "Reserve Your Next Retreat"
        ],
        longHeadlines: [
          "Escape the noise with secluded Scandinavian design cabins in pristine coastal nature",
          "Book extraordinary private getaways with hot tubs, saunas, and breathtaking views"
        ],
        shortDesc: "Award-winning Scandinavian retreats and secluded nature cabins.",
        descriptions: [
          "Handcrafted hideaways surrounded by untouched forests and tranquil fjords. Book your date.",
          "Enjoy 100% flexible cancellations, private wood-fired saunas, and concierge booking service."
        ],
        heroImage: "https://images.unsplash.com/photo-1510798831971-661eb04b3739?auto=format&fit=crop&w=1200&q=80",
        logoImage: "https://images.unsplash.com/photo-1534447677768-be436bb09401?auto=format&fit=crop&w=150&q=80",
        videoThumbnail: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1200&q=80",
        sitelinks: [
          { text: "Explore All Cabins", desc1: "View photos and amenities", desc2: "Check live dates" },
          { text: "Weekend Specials", desc1: "Last-minute openings", desc2: "Up to 25% discount" },
          { text: "Guest Stories", desc1: "Over 1,200 reviews", desc2: "5-star average rating" },
          { text: "Gift Certificates", desc1: "Give unforgettable stays", desc2: "Instant delivery" }
        ]
      }
    };

    // Initialize application
    window.addEventListener('DOMContentLoaded', () => {
      lucide.createIcons();
      populateForm();
      updateAllAdPreviews();
    });

    function populateForm() {
      // 1. Text scalar fields
      document.getElementById('input-businessName').value = state.businessName;
      document.getElementById('input-finalUrl').value = state.finalUrl;
      document.getElementById('input-path1').value = state.path1;
      document.getElementById('input-path2').value = state.path2;
      document.getElementById('input-cta').value = state.cta;
      document.getElementById('input-shortDesc').value = state.shortDesc;
      document.getElementById('input-heroImage').value = state.heroImage;
      document.getElementById('input-logoImage').value = state.logoImage;
      document.getElementById('input-videoThumbnail').value = state.videoThumbnail;

      // Update counters
      updateCounter('businessName', state.businessName.length, 25);
      updateCounter('path1', state.path1.length, 15);
      updateCounter('path2', state.path2.length, 15);
      updateCounter('shortDesc', state.shortDesc.length, 60);

      // Render Dynamic Lists
      renderHeadlinesList();
      renderLongHeadlinesList();
      renderDescriptionsList();
      renderSitelinksList();

      calculateAdStrength();
      lucide.createIcons();
    }

    // Scalar inputs handler
    function handleScalarInput(field, maxLen) {
      const val = document.getElementById(`input-${field}`).value;
      state[field] = val;
      if (maxLen) {
        updateCounter(field, val.length, maxLen);
      }
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function updateCounter(field, len, max) {
      const el = document.getElementById(`counter-${field}`);
      if (!el) return;
      el.textContent = `${len} / ${max}`;
      if (len > max) {
        el.className = "font-mono text-red-600 font-bold";
      } else {
        el.className = "font-mono text-gray-400";
      }
    }

    // Headlines
    function renderHeadlinesList() {
      const container = document.getElementById('headlinesContainer');
      container.innerHTML = '';
      state.headlines.forEach((hl, idx) => {
        const charLen = hl.length;
        const isOver = charLen > 30;
        const div = document.createElement('div');
        div.className = "flex items-center gap-2";
        div.innerHTML = `
          <div class="flex-1 bg-white border ${isOver ? 'border-red-500' : 'border-gray-300'} rounded-md px-3 py-1.5 flex items-center justify-between shadow-2xs">
            <input type="text" value="${escapeHtml(hl)}" maxlength="35"
              class="w-full text-xs text-gray-800 outline-none pr-2 bg-transparent"
              placeholder="Headline ${idx + 1}"
              oninput="onHeadlineChange(${idx}, this.value)">
            <span class="text-[11px] font-mono flex-shrink-0 ${isOver ? 'text-red-600 font-bold' : 'text-gray-400'}">
              ${charLen} / 30
            </span>
          </div>
          ${state.headlines.length > 3 ? `
            <button onclick="removeHeadline(${idx})" class="p-1 text-gray-400 hover:text-red-500 transition">
              <i data-lucide="trash-2" class="w-4 h-4"></i>
            </button>
          ` : '<span class="w-6"></span>'}
        `;
        container.appendChild(div);
      });
      lucide.createIcons();
    }

    function onHeadlineChange(idx, val) {
      state.headlines[idx] = val;
      renderHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function addHeadline() {
      if (state.headlines.length >= 15) return;
      state.headlines.push("New Value Proposition");
      renderHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function removeHeadline(idx) {
      if (state.headlines.length <= 3) return;
      state.headlines.splice(idx, 1);
      renderHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    // Long Headlines
    function renderLongHeadlinesList() {
      const container = document.getElementById('longHeadlinesContainer');
      container.innerHTML = '';
      state.longHeadlines.forEach((lhl, idx) => {
        const charLen = lhl.length;
        const isOver = charLen > 90;
        const div = document.createElement('div');
        div.className = "flex items-center gap-2";
        div.innerHTML = `
          <div class="flex-1 bg-white border ${isOver ? 'border-red-500' : 'border-gray-300'} rounded-md px-3 py-1.5 flex items-center justify-between shadow-2xs">
            <input type="text" value="${escapeHtml(lhl)}" maxlength="95"
              class="w-full text-xs text-gray-800 outline-none pr-2 bg-transparent"
              placeholder="Long Headline ${idx + 1}"
              oninput="onLongHeadlineChange(${idx}, this.value)">
            <span class="text-[11px] font-mono flex-shrink-0 ${isOver ? 'text-red-600 font-bold' : 'text-gray-400'}">
              ${charLen} / 90
            </span>
          </div>
          ${state.longHeadlines.length > 1 ? `
            <button onclick="removeLongHeadline(${idx})" class="p-1 text-gray-400 hover:text-red-500 transition">
              <i data-lucide="trash-2" class="w-4 h-4"></i>
            </button>
          ` : '<span class="w-6"></span>'}
        `;
        container.appendChild(div);
      });
      lucide.createIcons();
    }

    function onLongHeadlineChange(idx, val) {
      state.longHeadlines[idx] = val;
      renderLongHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function addLongHeadline() {
      if (state.longHeadlines.length >= 5) return;
      state.longHeadlines.push("Unmatched reliability and performance designed to elevate your daily outcomes");
      renderLongHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function removeLongHeadline(idx) {
      if (state.longHeadlines.length <= 1) return;
      state.longHeadlines.splice(idx, 1);
      renderLongHeadlinesList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    // Descriptions
    function renderDescriptionsList() {
      const container = document.getElementById('descriptionsContainer');
      container.innerHTML = '';
      state.descriptions.forEach((desc, idx) => {
        const charLen = desc.length;
        const isOver = charLen > 90;
        const div = document.createElement('div');
        div.className = "flex items-center gap-2";
        div.innerHTML = `
          <div class="flex-1 bg-white border ${isOver ? 'border-red-500' : 'border-gray-300'} rounded-md px-3 py-1.5 flex items-center justify-between shadow-2xs">
            <input type="text" value="${escapeHtml(desc)}" maxlength="95"
              class="w-full text-xs text-gray-800 outline-none pr-2 bg-transparent"
              placeholder="Description ${idx + 1}"
              oninput="onDescriptionChange(${idx}, this.value)">
            <span class="text-[11px] font-mono flex-shrink-0 ${isOver ? 'text-red-600 font-bold' : 'text-gray-400'}">
              ${charLen} / 90
            </span>
          </div>
          ${state.descriptions.length > 1 ? `
            <button onclick="removeDescription(${idx})" class="p-1 text-gray-400 hover:text-red-500 transition">
              <i data-lucide="trash-2" class="w-4 h-4"></i>
            </button>
          ` : '<span class="w-6"></span>'}
        `;
        container.appendChild(div);
      });
      lucide.createIcons();
    }

    function onDescriptionChange(idx, val) {
      state.descriptions[idx] = val;
      renderDescriptionsList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function addDescription() {
      if (state.descriptions.length >= 4) return;
      state.descriptions.push("Discover why industry experts and thousands of active users trust our verified solutions.");
      renderDescriptionsList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    function removeDescription(idx) {
      if (state.descriptions.length <= 1) return;
      state.descriptions.splice(idx, 1);
      renderDescriptionsList();
      updateAllAdPreviews();
      calculateAdStrength();
    }

    // Sitelinks
    function renderSitelinksList() {
      const container = document.getElementById('sitelinksContainer');
      container.innerHTML = '';
      state.sitelinks.forEach((sl, idx) => {
        const div = document.createElement('div');
        div.className = "p-3 bg-white rounded-lg border border-gray-200 space-y-2";
        div.innerHTML = `
          <div class="flex items-center justify-between">
            <span class="font-semibold text-gray-700">Sitelink #${idx + 1}</span>
            ${state.sitelinks.length > 1 ? `
              <button onclick="removeSitelink(${idx})" class="text-gray-400 hover:text-red-500 text-xs">
                <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
              </button>
            ` : ''}
          </div>
          <div>
            <div class="flex justify-between items-center mb-0.5">
              <span class="text-[10px] text-gray-500">Link Text (Max 25)</span>
              <span class="text-[10px] font-mono text-gray-400">${sl.text.length}/25</span>
            </div>
            <input type="text" value="${escapeHtml(sl.text)}" maxlength="25"
              class="w-full px-2 py-1 text-xs border border-gray-300 rounded outline-none"
              oninput="onSitelinkChange(${idx}, 'text', this.value)">
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <div class="flex justify-between items-center mb-0.5">
                <span class="text-[10px] text-gray-500">Desc Line 1 (Max 35)</span>
                <span class="text-[10px] font-mono text-gray-400">${sl.desc1.length}/35</span>
              </div>
              <input type="text" value="${escapeHtml(sl.desc1)}" maxlength="35"
                class="w-full px-2 py-1 text-[11px] border border-gray-300 rounded outline-none"
                oninput="onSitelinkChange(${idx}, 'desc1', this.value)">
            </div>
            <div>
              <div class="flex justify-between items-center mb-0.5">
                <span class="text-[10px] text-gray-500">Desc Line 2 (Max 35)</span>
                <span class="text-[10px] font-mono text-gray-400">${sl.desc2.length}/35</span>
              </div>
              <input type="text" value="${escapeHtml(sl.desc2)}" maxlength="35"
                class="w-full px-2 py-1 text-[11px] border border-gray-300 rounded outline-none"
                oninput="onSitelinkChange(${idx}, 'desc2', this.value)">
            </div>
          </div>
        `;
        container.appendChild(div);
      });
      lucide.createIcons();
    }

    function onSitelinkChange(idx, key, val) {
      state.sitelinks[idx][key] = val;
      renderSitelinksList();
      updateAllAdPreviews();
    }

    function addSitelink() {
      if (state.sitelinks.length >= 4) return;
      state.sitelinks.push({ text: "Special Offer", desc1: "Explore exclusive savings", desc2: "Limited time availability" });
      renderSitelinksList();
      updateAllAdPreviews();
    }

    function removeSitelink(idx) {
      if (state.sitelinks.length <= 1) return;
      state.sitelinks.splice(idx, 1);
      renderSitelinksList();
      updateAllAdPreviews();
    }

    function handleFileUpload(event, key) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        state[key] = e.target.result;
        document.getElementById(`input-${key}`).value = "Local Asset Uploaded";
        updateAllAdPreviews();
      };
      reader.readAsDataURL(file);
    }

    // Google Ad Strength Calculator
    function calculateAdStrength() {
      let score = 0;
      if (state.headlines.length >= 5) score += 25;
      else score += (state.headlines.length * 4);

      if (state.longHeadlines.length >= 2) score += 25;
      else score += (state.longHeadlines.length * 10);

      if (state.descriptions.length >= 2 && state.shortDesc) score += 25;
      else score += (state.descriptions.length * 8);

      if (state.heroImage && state.logoImage) score += 15;
      if (state.sitelinks.length >= 4) score += 10;

      const circle = document.getElementById('strengthCircle');
      const text = document.getElementById('strengthText');
      const icon = document.getElementById('strengthIcon');

      // 69.1 is perimeter of r=11 circle
      const offset = 69.1 - (Math.min(score, 100) / 100) * 69.1;
      circle.style.strokeDashoffset = offset;

      if (score >= 80) {
        text.textContent = "Excellent";
        text.className = "text-xs font-bold text-green-700";
        circle.style.stroke = "#1e8e3e";
        icon.className = "w-3.5 h-3.5 text-green-600 absolute";
      } else if (score >= 60) {
        text.textContent = "Good";
        text.className = "text-xs font-bold text-blue-600";
        circle.style.stroke = "#1a73e8";
        icon.className = "w-3.5 h-3.5 text-blue-600 absolute";
      } else if (score >= 40) {
        text.textContent = "Average";
        text.className = "text-xs font-bold text-yellow-600";
        circle.style.stroke = "#f9ab00";
        icon.className = "w-3.5 h-3.5 text-yellow-600 absolute";
      } else {
        text.textContent = "Poor";
        text.className = "text-xs font-bold text-red-600";
        circle.style.stroke = "#d93025";
        icon.className = "w-3.5 h-3.5 text-red-600 absolute";
      }
    }

    // Dynamic Preview Updating
    function updateAllAdPreviews() {
      const bName = state.businessName || "Your Brand";
      document.getElementById('headerBrandSpan').textContent = bName;
      document.getElementById('formLogoThumb').src = state.logoImage;

      // Extract domain
      let domain = "yourbrand.com";
      try {
        const u = new URL(state.finalUrl.startsWith('http') ? state.finalUrl : 'https://' + state.finalUrl);
        domain = u.hostname;
      } catch(e) {
        domain = state.finalUrl || "yourbrand.com";
      }

      // Safe headlines & descriptions from rotation
      const h1 = state.headlines[state.headlineRotationIndex % state.headlines.length] || "Top Rated Brand Solution";
      const h2 = state.headlines[(state.headlineRotationIndex + 1) % state.headlines.length] || "Official Site";
      const h3 = state.headlines[(state.headlineRotationIndex + 2) % state.headlines.length] || "Shop Online Today";

      const longHead = state.longHeadlines[state.longHeadlineRotationIndex % state.longHeadlines.length] || state.longHeadlines[0] || h1;
      const desc1 = state.descriptions[state.descRotationIndex % state.descriptions.length] || state.descriptions[0] || state.shortDesc;
      const desc2 = state.descriptions[(state.descRotationIndex + 1) % state.descriptions.length] || "";

      // 1. Google Search SERP
      document.getElementById('searchMockQuery').textContent = `${bName.toLowerCase()} solutions online`;
      document.getElementById('serpBusinessName').textContent = bName;
      document.getElementById('serpFavicon').src = state.logoImage;
      let displayPath = `https://${domain}`;
      if (state.path1) displayPath += ` › ${state.path1}`;
      if (state.path2) displayPath += ` › ${state.path2}`;
      document.getElementById('serpDisplayUrl').textContent = displayPath;
      document.getElementById('serpHeadline').textContent = `${h1} | ${h2} | ${h3}`;
      document.getElementById('serpDescription').textContent = `${desc1} ${desc2}`;

      // SERP Sitelinks
      const slContainer = document.getElementById('serpSitelinksContainer');
      slContainer.innerHTML = '';
      state.sitelinks.slice(0, 4).forEach(sl => {
        const item = document.createElement('div');
        item.className = "p-2 bg-gray-50 hover:bg-gray-100 rounded border border-gray-100 cursor-pointer transition";
        item.innerHTML = `
          <div class="text-xs font-medium text-[#1a0dab] hover:underline">${escapeHtml(sl.text)}</div>
          <div class="text-[11px] text-gray-500 line-clamp-1">${escapeHtml(sl.desc1 || '')}</div>
        `;
        slContainer.appendChild(item);
      });

      // 2. Display Network
      document.getElementById('displayHeroImg1').src = state.heroImage;
      document.getElementById('displayBadgeBrand').textContent = bName;
      document.getElementById('displayNativeTitle').textContent = longHead;
      document.getElementById('displayNativeDesc').textContent = desc1;
      document.getElementById('displayNativeCta').textContent = state.cta;

      document.getElementById('displayMpuImg').src = state.heroImage;
      document.getElementById('displayMpuTitle').textContent = h1;
      document.getElementById('displayMpuDesc').textContent = desc1;
      document.getElementById('displayMpuBrand').textContent = bName;
      document.getElementById('displayMpuCta').textContent = state.cta;

      // 3. YouTube Ad
      document.getElementById('ytVideoThumb').src = state.videoThumbnail || state.heroImage;
      document.getElementById('ytLogoOverlay').src = state.logoImage;
      document.getElementById('ytOverlayTitle').textContent = h1;
      document.getElementById('ytOverlayUrl').textContent = domain;
      document.getElementById('ytOverlayCta').textContent = state.cta;
      document.getElementById('ytAvatar').src = state.logoImage;
      document.getElementById('ytChannelName').textContent = `${bName} Official`;
      document.getElementById('ytMainTitle').textContent = longHead;
      document.getElementById('ytBottomCtaText').textContent = state.cta;

      // 4. Discover
      document.getElementById('discoverHeroImg').src = state.heroImage;
      document.getElementById('discoverTitle').textContent = longHead;
      document.getElementById('discoverDesc').textContent = desc1;
      document.getElementById('discoverLogo').src = state.logoImage;
      document.getElementById('discoverBrand').textContent = bName;

      // 5. Gmail
      document.getElementById('gmailTeaserLogo').src = state.logoImage;
      document.getElementById('gmailTeaserBrand').textContent = bName;
      document.getElementById('gmailTeaserSubject').textContent = h1;
      document.getElementById('gmailTeaserSnippet').textContent = desc1;

      document.getElementById('gmailOpenLogo').src = state.logoImage;
      document.getElementById('gmailOpenBrand').textContent = bName;
      document.getElementById('gmailOpenFromEmail').textContent = `offers@${domain}`;
      document.getElementById('gmailOpenHeadline').textContent = longHead;
      document.getElementById('gmailOpenHeroImg').src = state.heroImage;
      document.getElementById('gmailOpenBody').textContent = `${desc1} ${desc2}`;
      document.getElementById('gmailOpenCta').textContent = state.cta;

      // 6. All Placements View
      document.getElementById('allSearchHead').textContent = `${h1} - ${bName}`;
      document.getElementById('allSearchDesc').textContent = desc1;
      document.getElementById('allDisplayImg').src = state.heroImage;
      document.getElementById('allDisplayHead').textContent = h1;
      document.getElementById('allYtImg').src = state.videoThumbnail || state.heroImage;
      document.getElementById('allYtHead').textContent = longHead;
      document.getElementById('allDiscoverHead').textContent = h1;
    }

    // Switch Preview Channels
    function switchChannel(channel) {
      state.activeChannel = channel;
      const channels = ['search', 'display', 'youtube', 'discover', 'gmail', 'all'];
      channels.forEach(ch => {
        const view = document.getElementById(`channel-view-${ch}`);
        const tab = document.getElementById(`tab-${ch}`);
        if (ch === channel) {
          view.classList.remove('hidden');
          tab.className = "channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-semibold bg-blue-50 text-blue-700 border border-blue-200 shadow-2xs";
        } else {
          view.classList.add('hidden');
          tab.className = "channel-tab-btn flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium text-gray-600 hover:bg-gray-100";
        }
      });
      lucide.createIcons();
    }

    // Responsive Device Toggle
    function setDeviceView(device) {
      state.device = device;
      const wrapper = document.getElementById('previewCanvasWrapper');
      const btnMobile = document.getElementById('btn-device-mobile');
      const btnDesktop = document.getElementById('btn-device-desktop');

      if (device === 'mobile') {
        wrapper.className = "w-full max-w-md transition-all duration-300";
        btnMobile.className = "px-2 py-1 rounded-md text-xs font-medium bg-white text-gray-800 shadow-2xs flex items-center gap-1";
        btnDesktop.className = "px-2 py-1 rounded-md text-xs font-medium text-gray-500 hover:text-gray-800 flex items-center gap-1";
      } else {
        wrapper.className = "w-full max-w-3xl transition-all duration-300";
        btnDesktop.className = "px-2 py-1 rounded-md text-xs font-medium bg-white text-gray-800 shadow-2xs flex items-center gap-1";
        btnMobile.className = "px-2 py-1 rounded-md text-xs font-medium text-gray-500 hover:text-gray-800 flex items-center gap-1";
      }
    }

    // Toggle Presentation Session Mode
    function togglePresentationMode(force) {
      if (typeof force === 'boolean') {
        state.isPresentationMode = force;
      } else {
        state.isPresentationMode = !state.isPresentationMode;
      }

      const editorPanel = document.getElementById('editorPanel');
      const notice = document.getElementById('presentationNotice');
      const icon = document.getElementById('presentationIcon');

      if (state.isPresentationMode) {
        editorPanel.classList.add('hidden');
        notice.classList.remove('hidden');
        icon.setAttribute('data-lucide', 'minimize-2');
        if (state.device === 'mobile') {
          // Keep comfortable preview width
          document.getElementById('previewCanvasWrapper').className = "w-full max-w-lg transition-all duration-300";
        }
      } else {
        editorPanel.classList.remove('hidden');
        notice.classList.add('hidden');
        icon.setAttribute('data-lucide', 'maximize-2');
        setDeviceView(state.device);
      }
      lucide.createIcons();
    }

    // Shuffle Machine Learning Copy Combination
    function shuffleMachineLearningCopy() {
      state.headlineRotationIndex = Math.floor(Math.random() * state.headlines.length);
      state.longHeadlineRotationIndex = Math.floor(Math.random() * state.longHeadlines.length);
      state.descRotationIndex = Math.floor(Math.random() * state.descriptions.length);
      updateAllAdPreviews();
    }

    // Template Loaders
    function loadTemplate(key) {
      if (!templates[key]) return;
      state = JSON.parse(JSON.stringify(templates[key]));
      state.activeChannel = 'search';
      state.device = 'mobile';
      state.isPresentationMode = false;
      state.headlineRotationIndex = 0;
      state.longHeadlineRotationIndex = 0;
      state.descRotationIndex = 0;

      populateForm();
      updateAllAdPreviews();
      switchChannel('search');
      setDeviceView('mobile');
    }

    function resetToEmpty() {
      state.businessName = "";
      state.finalUrl = "https://";
      state.path1 = "";
      state.path2 = "";
      state.cta = "Learn more";
      state.headlines = ["", "", ""];
      state.longHeadlines = [""];
      state.shortDesc = "";
      state.descriptions = [""];
      state.sitelinks = [{ text: "", desc1: "", desc2: "" }];
      populateForm();
      updateAllAdPreviews();
    }

    // Export & Sign-Off Modals
    function openExportModal() {
      document.getElementById('exportModal').classList.remove('hidden');
      lucide.createIcons();
    }

    function closeExportModal() {
      document.getElementById('exportModal').classList.add('hidden');
    }

    function copyFormattedMatrix() {
      let doc = `====================================================\n`;
      doc += `GOOGLE ADS PERFORMANCE MAX (PMAX) - ASSET MATRIX\n`;
      doc += `====================================================\n\n`;
      doc += `Client / Brand: ${state.businessName || 'Brand'}\n`;
      doc += `Final URL: ${state.finalUrl}\n`;
      doc += `Display Paths: /${state.path1} /${state.path2}\n`;
      doc += `Call To Action: ${state.cta}\n\n`;

      doc += `--- HEADLINES (${state.headlines.length}/15) [Max 30 Chars] ---\n`;
      state.headlines.forEach((h, i) => {
        doc += `${i + 1}. ${h} [${h.length}/30]\n`;
      });

      doc += `\n--- LONG HEADLINES (${state.longHeadlines.length}/5) [Max 90 Chars] ---\n`;
      state.longHeadlines.forEach((lh, i) => {
        doc += `${i + 1}. ${lh} [${lh.length}/90]\n`;
      });

      doc += `\n--- DESCRIPTIONS [1x 60c, Up to 4x 90c] ---\n`;
      doc += `Short Desc: ${state.shortDesc} [${state.shortDesc.length}/60]\n`;
      state.descriptions.forEach((d, i) => {
        doc += `${i + 1}. ${d} [${d.length}/90]\n`;
      });

      doc += `\n--- SITELINKS (${state.sitelinks.length}/4) ---\n`;
      state.sitelinks.forEach((s, i) => {
        doc += `${i + 1}. [${s.text}] - ${s.desc1} | ${s.desc2}\n`;
      });

      fallbackCopy(doc);
      showToast("Asset Matrix copied to clipboard!");
    }

    function copyShareableUrl() {
      fallbackCopy(window.location.href);
      showToast("Direct preview link copied!");
    }

    function showToast(msg) {
      const toast = document.getElementById('copyToast');
      toast.textContent = msg;
      toast.classList.remove('hidden');
      setTimeout(() => {
        toast.classList.add('hidden');
      }, 3000);
    }

    function fallbackCopy(text) {
      const textarea = document.createElement('textarea');
      textarea.value = text;
      textarea.style.position = 'fixed';
      textarea.style.opacity = '0';
      document.body.appendChild(textarea);
      textarea.select();
      try {
        document.execCommand('copy');
      } catch (err) {
        console.error('Clipboard error', err);
      }
      document.body.removeChild(textarea);
    }

    function escapeHtml(str) {
      return (str || '').replace(/[&<>"']/g, function(m) {
        return {
          '&': '&amp;',
          '<': '&lt;',
          '>': '&gt;',
          '"': '&quot;',
          "'": '&#39;'
        }[m];
      });
    }
  </script>
</body>
</html>
