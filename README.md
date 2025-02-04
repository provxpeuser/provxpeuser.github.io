<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="icon" type="icon/x-icon" href="https://myapps.classlink.com/assets/images/classlink-logo.svg" />
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>  My Apps </title>
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #FF6961;
            color: white;
            margin: 0;
            padding: 0;
            overflow-y: scroll;
        }

        #particleCanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            z-index: 0; /* Canvas is at the back */
        }

        #urlInput:focus, #titleInput:focus, #faviconInput:focus {
            outline: none;
            box-shadow: inset 0 4px 10px rgba(255, 255, 255, 0.3);
        }

        #openNewTabButton:hover, #resetButton:hover, #settingsButton:hover {
            box-shadow: 0 0 10px #3498db, 0 0 20px #3498db;
        }

        #openNewTabButton:active, #resetButton:active {
            box-shadow: 0 0 15px #5dade2;
        }

        #settingsMenu {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #1e1e1e;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            width: 300px;
            text-align: left;
            z-index: 2; /* Ensures settings menu is above everything */
        }

        .toggle-button {
            background-color: #3498db;
            color: white;
            padding: 8px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
            margin-right: 8px;
        }

        .toggle-button.active {
            background-color: #e74c3c;
        }

        div[style*="text-align: center;"] {
            z-index: 1; /* Ensures inputs and buttons are above the canvas */
            position: relative; /* Create stacking context for z-index */
        }

        .particle {
            position: absolute;
            background-color: white;
            border-radius: 50%;
            opacity: 0.7;
            animation: fall infinite linear;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100%);
                opacity: 0.7;
            }
            100% {
                transform: translateY(100vh);
                opacity: 0;
            }
        }

        .url-button {
            background-color: #db9e9e;
            color: white;
            padding: 10px 25px;
            border: White;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 5px;
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.4), 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .url-button:hover {
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.5), 0 10px 15px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
        }

        .url-button:active {
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.4), 0 2px 4px rgba(0, 0, 0, 0.2);
            transform: translateY(2px);
        }

        .blocked {
            background-color: rgba(0,0,0,0.5);
            color: rgb(0, 0, 0);
            padding: 10px 25px;
            border: rgb(0, 0, 0);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 100000px;
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.4), 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .separator {
            border-top: 2px solid #e09090;
            margin: 20px 0;
            width: 80%;
            margin-left: auto;
            margin-right: auto;
        }

        .section-header {
            font-size: 1.5em;
            color: white;
            margin-top: 40px;
            margin-bottom: 10px;
        }
        .page-title {
            font-size: 3em;
            color: white;
            margin-top: 20px;
            margin-bottom: 20px;
        }
        .paragraph {
            font-size: 0.75em;
            color: white;
            margin-top: 2.5px;
            margin-bottom: 5px;
        }

    </style>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400&display=swap" rel="stylesheet">
</head>
<body>

<canvas id="particleCanvas"></canvas>

<div style="text-align: center; margin-top: 60px; position: relative; z-index: 1;">
      <h1 class="page-title">👑Harlem My King 👑</h1>
      <h1 class="paragraph">Made by Jebunn | Still In Development!</p>
      <p class="paragraph"> </p>
    <input type="text" id="urlInput" style="padding: 8px 15px; border-radius: 8px; border: none; background-color: #ffffff; color: rgb(0, 0, 0); width: 90%; box-shadow: inset 0 3px 6px rgba(255, 255, 255, 0.3);" placeholder="Enter a URL or search term">
    <button id="openNewTabButton" style="background-color: #d18282; color: white; padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer; transition: all 0.3s ease; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3), inset 0 -2px 0 rgba(0, 0, 0, 0.2);">Open</button>
    <button id="settingsButton" style="font-size: 1.5em; background-color: transparent; border: none; border-radius: 50%; cursor: pointer; color: white; padding: 8px; margin-left: 8px; transition: all 0.3s ease; transform: translateY(4px); box-shadow: 0 3px 6px rgba(0, 0, 0, 0.3);">⚙️</button>

    <h5 class="paragraph">*Info and Debugging at the bottom*</h5>
    <h5 class="paragraph">This website is private and if this site has been leaked it will be blocked and currently this website is only given to only 4 people including me.</h5>
    <h5 class="paragraph">Link has been given to Harlem, Aj, Jayden and Michael</h5>
</div>

<div id="settingsMenu">
    <span id="closeMenu" style="float: right; cursor: pointer; color: #aaa;">❌</span>
    <h3 style="color: #fff; border-bottom: 1px solid #555; padding-bottom: 10px; margin-bottom: 15px;">Settings</h3>
    <label style="color: #bbb; margin-bottom: 5px; display: block;">Default Browsers:</label>
    <div style="margin-bottom: 15px;">
        <button id="googleButton" class="toggle-button active">Google</button>
        <button id="bingButton" class="toggle-button">Bing</button>
    </div>

    <label style="color: #bbb; margin-bottom: 5px; display: block;">Tab Title:</label>
    <input type="text" id="titleInput" style="width: 100%; padding: 8px; border-radius: 8px; border: none; background-color: #333; color: white; box-shadow: inset 0 3px 6px rgba(0, 0, 0, 0.3); margin-bottom: 10px;">

    <label style="color: #bbb; margin-bottom: 5px; display: block;">Favicon URL:</label>
    <input type="text" id="faviconInput" style="width: 100%; padding: 8px; border-radius: 8px; border: none; background-color: #333; color: white; box-shadow: inset 0 3px 6px rgba(0, 0, 0, 0.3); margin-bottom: 15px;">

    <div style="margin-bottom: 15px;">
        <label style="color: #bbb;">Particles:</label>
        <button id="particlesToggle" class="toggle-button active">On</button>
    </div>
    
    <button id="resetButton" style="background-color: #e74c3c; color: white; padding: 8px 20px; border: none; border-radius: 8px; cursor: pointer; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); transition: all 0.3s ease;">Reset</button>
</div>

<!-- Example Buttons Section -->
<div style="text-align: center; margin-top: 40px;">
    <h2 class="section-header">Goto Links</h2>
    <h5 class="paragraph">Links That most people use or need</p>
    <div class="separator"></div>
    <button class="url-button" data-url="https://google.com" onclick="openURLFromButton(this)">Google</button>
    <button class="url-button" data-url="https://onecompiler.com/embed/html" onclick="openURLFromButton(this)">HTML Compiler</button>
    <button class="url-button" data-url="https://www.desmos.com/testing/virginia/scientific" onclick="openURLFromButton(this)">Desmos Scientific Calculator</button>
    <button class="url-button" data-url="https://getliner.com" onclick="openURLFromButton(this)">Getliner AI</button>
    

</div>

<div style="text-align: center; margin-top: 40px;">
    <h2 class="section-header">Games</h2>
    <h5 class="paragraph">An Great Asortment of games that are fun when needed to waste time.</p>
    <div class="separator"></div>
    <button class="url-button" data-url="https://slope-c.glitch.me/" onclick="openURLFromButton(this)">Slope</button>
    <button class="url-button" data-url="https://Slowroads.io" onclick="openURLFromButton(this)">Slowroads</button>
    <button class="url-button" data-url="https://deadshot.io" onclick="openURLFromButton(this)">Deadshot</button>
    <button class="url-button" data-url="https://slope-c.glitch.me/" onclick="openURLFromButton(this)">Slope</button>
    <button class="url-button" data-url="https://krunker.io" onclick="openURLFromButton(this)">Krunker</button>
    <button class="url-button" data-url="https://salcininkaikultura.lt/expo/" onclick="openURLFromButton(this)">Drift Hunters</button>
    <button class="url-button" data-url="https://softbodytetris.netlify.app" onclick="openURLFromButton(this)">Sofybody Tetris</button>
    <button class="url-button" data-url="https://www.hoodamath.com/mobile/games/drift-boss/game.html" onclick="openURLFromButton(this)">Drift Boss</button>
    <button class="url-button" data-url="https://games.cdn.famobi.com/html5games/c/cut-the-rope/v070/?fg_domain=play.famobi.com&fg_aid=A-SILVERGAMES&fg_uid=4531b37c-a8e0-4a67-9ebd-e8d3190b6277&fg_pid=8a24e5f2-94a8-4593-b4e5-81cc68f524c8&fg_beat=969&original_ref=https%3A%2F%2Fwww.silvergames.com%2F" onclick="openURLFromButton(this)">Cut The Rope</button>
    <button class="url-button" data-url="https://www.2048.org/" onclick="openURLFromButton(this)">2048</button>
    <button class="url-button" data-url="https://paper-io.com/" onclick="openURLFromButton(this)">Paper.io </button>
    <button class="url-button" data-url="https://bab.dev/flappy-bird" onclick="openURLFromButton(this)">Flappy Bird</button>
    <button class="url-button" data-url="https://1kh0.github.io/projects/retro-bowl/index.html" onclick="openURLFromButton(this)">Retro Bowl</button>
    <button class="url-button" data-url="https://bab.dev/blockblast" onclick="openURLFromButton(this)">Block Blast</button>
    <button class="url-button" data-url="https://bab.dev" onclick="openURLFromButton(this)">Bab.Dev</button>
    </Div>

<div style="text-align: center; margin-top: 40px;">
    <h2 class="section-header">Minecraft</h2>
    <h5 class="paragraph">This is part of games and it is the eaglercraft part of games</p>
        <button class="url-button" data-url="https://eaglercraft.com" onclick="openURLFromButton(this)">Eaglercraft</button>
        <button class="url-button" data-url="https://html-classic.itch.zone/html/7086310/PrecisionClient-Static-main/index.html" onclick="openURLFromButton(this)">Precision Client</button>
        <button class="url-button" data-url="https://resent4-0.vercel.app/" onclick="openURLFromButton(this)">Resent 4.0</button>
    <div class="separator"></div>
</div>

<div style="text-align: center; margin-top: 40px;">
    <h2 class="section-header">Goguardian/Securly Bypassers | Private Links</h2>
    <h5 class="paragraph">This is for bypassing in a better way | information to fix issues below.</p>
    <div class="separator"></div>
    <button class="url-button" data-url="https://salemmiddleschoolclc.com.chickenkiller.com" onclick="openURLFromButton(this)">Space Proxy</button>
    <button class="url-button" data-url="https://light.simpanan.web.id" onclick="openURLFromButton(this)">Light Proxy</button>
</div>

<div style="text-align: center; margin-top: 40px;">
    <h2 class="section-header">Information</h2>
    <div class="separator"></div>
    <p class="paragraph">Made by Jebunn "vscode" Salem Middle School </p>
    <p class="paragraph">Always include "https://" at the beginning of your URL unless you are searching the web</p>
    <p class="paragraph">When using the searchbar, some sites may not work due to CORS policy</p>
    <p class="paragraph">The "Goguardian/Securly Blockers" Links are broken, to fix this use a cloaker in the settings</p>
</div>

  

<script>
let currentSearchEngine = "google";
let particlesEnabled = true;

function isValidURL(string) {
    try {
        new URL(string.startsWith("http") ? string : "https://" + string);
        return true;
    } catch (_) {
        return false;
    }
}

function openURLFromButton(button) {
    let url = button.getAttribute("data-url");
    loadWebsiteInNewTab(url);
}

function loadWebsiteInNewTab(url) {
    const title = document.getElementById("titleInput").value || 'Home - Google Drive';
    const favicon = document.getElementById("faviconInput").value || 'https://ssl.gstatic.com/images/branding/product/1x/drive_2020q4_32dp.png'
    var newTab = window.open();
    newTab.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>${title}</title>
            <link rel="icon" type="image/png" href="${favicon}" sizes="16x16">
            <style>
                body {
                    margin: 0;
                    overflow: hidden;
                }
                embed {
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    border: none;
                }
            </style>
        </head>
        <body>
            <embed src="${url}">
        </body>
        </html>
    `);
    newTab.document.close();
}

document.getElementById("openNewTabButton").addEventListener("click", function() {
    let input = document.getElementById("urlInput").value.trim();
    let url;

    if (input.startsWith("https://")) {
        // If the input starts with https://, use it as is.
        url = input;
    } else {
        // Use the selected search engine (Google or Bing) for searching.
        const baseUrl = currentSearchEngine === "google" 
            ? "https://www.google.com/search?igu=1&q=" 
            : "https://www.bing.com/search?adlt=strict&q=";
        url = baseUrl + encodeURIComponent(input);
    }

    loadWebsiteInNewTab(url);
});
document.getElementById("urlInput").addEventListener("keypress", function(event) {
    if (event.key === "Enter") {
        document.getElementById("openNewTabButton").click();
    }
});

document.getElementById("settingsButton").addEventListener("click", function() {
    document.getElementById("settingsMenu").style.display = "block";
});

document.getElementById("closeMenu").addEventListener("click", function() {
    document.getElementById("settingsMenu").style.display = "none";
});

document.getElementById("resetButton").addEventListener("click", function() {
    document.getElementById("titleInput").value = 'Inbox (1)';
    document.getElementById("faviconInput").value = 'https://ssl.gstatic.com/images/branding/product/1x/drive_2020q4_32dp.png';
});

document.getElementById("googleButton").addEventListener("click", function() {
    currentSearchEngine = "google";
    this.classList.add("active");
    document.getElementById("bingButton").classList.remove("active");
});

document.getElementById("bingButton").addEventListener("click", function() {
    currentSearchEngine = "bing";
    this.classList.add("active");
    document.getElementById("googleButton").classList.remove("active");
});

document.getElementById("particlesToggle").addEventListener("click", function() {
    particlesEnabled = !particlesEnabled;
    this.classList.toggle("active");
    if (particlesEnabled) {
        startParticles();
    } else {
        stopParticles();
    }
});

const canvas = document.getElementById("particleCanvas");
const ctx = canvas.getContext("2d");

// Update canvas size to cover the full scrollable height
function updateCanvasSize() {
    canvas.width = window.innerWidth;
    canvas.height = document.documentElement.scrollHeight; // Full document height
}

updateCanvasSize(); // Initial setup

let particles = [];

function createParticles() {
    for (let i = 0; i < 100; i++) {
        particles.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            size: Math.random() * 3 + 1,
            speed: Math.random() * 2 + 0.5,
            opacity: Math.random() * 0.5 + 0.3
        });
    }
}

function drawParticles() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255, 255, 255, ${p.opacity})`;
        ctx.fill();
    });
}

function updateParticles() {
    particles.forEach(p => {
        p.y += p.speed;
        if (p.y > canvas.height) p.y = -p.size; // Reset particle to the top
    });
}

function animateParticles() {
    if (particlesEnabled) {
        drawParticles();
        updateParticles();
        requestAnimationFrame(animateParticles);
    }
}

function startParticles() {
    particles = [];
    createParticles();
    animateParticles();
}

function stopParticles() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
}

// Resize canvas and reinitialize particles when the window or document size changes
window.addEventListener("resize", () => {
    updateCanvasSize();
    if (particlesEnabled) startParticles();
});

// Add listener for scroll events to ensure particles remain visible
window.addEventListener("scroll", () => {
    canvas.height = document.documentElement.scrollHeight;
});

startParticles();
</script>

</body>
</html>


