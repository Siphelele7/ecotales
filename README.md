<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EcoTales — Made in OctoStudio</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --octopurple: #7C3AED;
    --octoaccent: #06B6D4;
    --octodark: #4F46E5;
    --octolight: #F3E8FF;
    --octoyellow: #FBBF24;
    --octocyan: #06B6D4;
    --octolime: #84CC16;
    --octopink: #EC4899;
    --octoblue: #3B82F6;
    --octored: #EF4444;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Nunito', sans-serif;
    background: linear-gradient(135deg, #F3E8FF 0%, #E0E7FF 50%, #DBEAFE 100%);
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
  }

  /* Animated grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: 
      linear-gradient(0deg, transparent 24%, rgba(207,170,254,.3) 25%, rgba(207,170,254,.3) 26%, transparent 27%, transparent 74%, rgba(207,170,254,.3) 75%, rgba(207,170,254,.3) 76%, transparent 77%),
      linear-gradient(90deg, transparent 24%, rgba(207,170,254,.3) 25%, rgba(207,170,254,.3) 26%, transparent 27%, transparent 74%, rgba(207,170,254,.3) 75%, rgba(207,170,254,.3) 76%, transparent 77%);
    background-size: 50px 50px;
    pointer-events: none;
    z-index: -1;
  }

  /* Header */
  header {
    background: white;
    border-bottom: 3px solid var(--octopurple);
    padding: 16px 24px;
    box-shadow: 0 4px 12px rgba(124,58,237,0.15);
    position: sticky;
    top: 0;
    z-index: 50;
  }

  .header-content {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header-logo {
    display: flex;
    align-items: center;
    gap: 12px;
    font-family: 'Fredoka One', cursive;
    font-size: 1.4rem;
    color: var(--octopurple);
  }

  .header-logo-icon {
    font-size: 1.8rem;
    animation: float 2s ease-in-out infinite;
  }

  @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }

  .header-badge {
    background: linear-gradient(135deg, var(--octopink), var(--octoyellow));
    color: white;
    border-radius: 50px;
    padding: 6px 14px;
    font-size: 0.75rem;
    font-weight: 800;
    letter-spacing: 1px;
    text-transform: uppercase;
    box-shadow: 0 3px 10px rgba(236,72,153,0.4);
  }

  /* Main container */
  .container {
    max-width: 1100px;
    margin: 32px auto;
    padding: 0 16px;
  }

  /* Row layout */
  .row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    margin-bottom: 32px;
  }

  @media (max-width: 900px) {
    .row { grid-template-columns: 1fr; }
  }

  /* Stage (Sprite Canvas) */
  .stage {
    background: white;
    border: 4px solid var(--octopurple);
    border-radius: 20px;
    aspect-ratio: 16/9;
    position: relative;
    overflow: hidden;
    box-shadow: 0 8px 32px rgba(124,58,237,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Fredoka One', cursive;
  }

  .stage-bg {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .stage-sky {
    background: linear-gradient(180deg, #87CEEB 0%, #E0F6FF 100%);
  }

  .stage-underground {
    background: linear-gradient(180deg, #607D8B 0%, #37474F 100%);
  }

  .stage-water {
    background: linear-gradient(180deg, #1a237e 0%, #0288D1 100%);
  }

  .stage-forest {
    background: linear-gradient(180deg, #33691E 60%, #558B2F 100%);
  }

  .stage-content {
    position: relative;
    z-index: 2;
    text-align: center;
    color: white;
    font-size: 3rem;
    text-shadow: 2px 2px 8px rgba(0,0,0,0.3);
  }

  /* Code blocks panel */
  .code-blocks {
    background: white;
    border: 4px solid var(--octopurple);
    border-radius: 20px;
    padding: 20px;
    overflow-y: auto;
    max-height: 600px;
    box-shadow: 0 8px 32px rgba(124,58,237,0.2);
  }

  .code-blocks-title {
    font-family: 'Fredoka One', cursive;
    font-size: 1.1rem;
    color: var(--octopurple);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  /* Individual block */
  .block {
    border-radius: 10px;
    padding: 12px 14px;
    margin-bottom: 10px;
    font-size: 0.9rem;
    font-weight: 700;
    cursor: pointer;
    border-left: 5px solid;
    transition: all 0.2s ease;
    font-family: 'Fredoka One', cursive;
    position: relative;
    overflow: hidden;
  }

  .block::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at 20% 50%, rgba(255,255,255,0.3) 0%, transparent 50%);
    pointer-events: none;
  }

  .block:hover {
    transform: translateX(6px) scale(1.02);
    box-shadow: 0 4px 14px rgba(0,0,0,0.2);
  }

  /* Block colors */
  .block.motion {
    background: linear-gradient(135deg, #06B6D4 0%, #0891B2 100%);
    border-left-color: #0369A1;
    color: white;
  }

  .block.looks {
    background: linear-gradient(135deg, #EC4899 0%, #BE185D 100%);
    border-left-color: #831843;
    color: white;
  }

  .block.sound {
    background: linear-gradient(135deg, #FBBF24 0%, #F59E0B 100%);
    border-left-color: #D97706;
    color: #111;
  }

  .block.control {
    background: linear-gradient(135deg, #EF4444 0%, #DC2626 100%);
    border-left-color: #991B1B;
    color: white;
  }

  .block.events {
    background: linear-gradient(135deg, #84CC16 0%, #65A30D 100%);
    border-left-color: #422006;
    color: white;
  }

  .block.data {
    background: linear-gradient(135deg, #F97316 0%, #EA580C 100%);
    border-left-color: #7C2D12;
    color: white;
  }

  .block-icon {
    margin-right: 8px;
    font-size: 1.1rem;
  }

  /* Sprites list */
  .sprites-section {
    background: white;
    border: 4px solid var(--octopurple);
    border-radius: 20px;
    padding: 20px;
    box-shadow: 0 8px 32px rgba(124,58,237,0.2);
  }

  .sprites-title {
    font-family: 'Fredoka One', cursive;
    font-size: 1.1rem;
    color: var(--octopurple);
    margin-bottom: 16px;
  }

  .sprite-item {
    background: linear-gradient(135deg, #E9D5FF, #F3E8FF);
    border: 3px solid var(--octopurple);
    border-radius: 12px;
    padding: 12px;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 12px;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .sprite-item:hover {
    transform: translateX(4px);
    background: linear-gradient(135deg, #F3E8FF, #E9D5FF);
    box-shadow: 0 4px 12px rgba(124,58,237,0.3);
  }

  .sprite-icon {
    font-size: 1.8rem;
  }

  .sprite-name {
    font-weight: 800;
    color: var(--octopurple);
    font-family: 'Fredoka One', cursive;
  }

  /* Story content */
  .story-frame {
    background: white;
    border: 4px solid var(--octopurple);
    border-radius: 20px;
    padding: 24px;
    box-shadow: 0 8px 32px rgba(124,58,237,0.2);
    margin-bottom: 24px;
  }

  .story-frame h3 {
    font-family: 'Fredoka One', cursive;
    font-size: 1.3rem;
    color: var(--octopurple);
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .story-frame p {
    color: #37474F;
    line-height: 1.6;
    font-size: 0.95rem;
    margin-bottom: 12px;
  }

  /* Project info */
  .project-info {
    background: linear-gradient(135deg, var(--octopurple), var(--octodark));
    color: white;
    border-radius: 20px;
    padding: 28px 24px;
    text-align: center;
    box-shadow: 0 8px 32px rgba(124,58,237,0.3);
    margin-bottom: 32px;
  }

  .project-info h1 {
    font-family: 'Fredoka One', cursive;
    font-size: 2.5rem;
    margin-bottom: 8px;
    text-shadow: 2px 2px 8px rgba(0,0,0,0.2);
  }

  .project-info p {
    font-size: 1rem;
    opacity: 0.95;
  }

  .project-icon {
    font-size: 4rem;
    margin-bottom: 12px;
  }

  /* Interactive play button */
  .play-btn-area {
    background: white;
    border: 4px solid var(--octopurple);
    border-radius: 20px;
    padding: 24px;
    text-align: center;
    box-shadow: 0 8px 32px rgba(124,58,237,0.2);
    margin-bottom: 32px;
  }

  .play-btn {
    background: linear-gradient(135deg, var(--octoyellow), var(--octopink));
    border: none;
    border-radius: 50px;
    padding: 16px 40px;
    font-family: 'Fredoka One', cursive;
    font-size: 1.3rem;
    color: white;
    cursor: pointer;
    box-shadow: 0 6px 20px rgba(251,191,36,0.5);
    transition: all 0.2s ease;
    text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
  }

  .play-btn:hover {
    transform: scale(1.08);
    box-shadow: 0 8px 28px rgba(251,191,36,0.6);
  }

  .play-btn:active {
    transform: scale(0.95);
  }

  /* Modal */
  .modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.6);
    z-index: 100;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  .modal.show { display: flex; }

  .modal-content {
    background: white;
    border-radius: 24px;
    border: 4px solid var(--octopurple);
    max-width: 600px;
    width: 100%;
    max-height: 80vh;
    overflow-y: auto;
    padding: 32px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.3);
    animation: slideUp 0.4s ease;
  }

  @keyframes slideUp { from { transform: translateY(40px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

  .modal-close {
    float: right;
    font-size: 2rem;
    cursor: pointer;
    color: var(--octopurple);
    font-weight: bold;
    transition: transform 0.2s;
  }

  .modal-close:hover { transform: scale(1.2); }

  .modal-content h2 {
    font-family: 'Fredoka One', cursive;
    font-size: 1.8rem;
    color: var(--octopurple);
    margin: 12px 0 20px;
    clear: both;
  }

  .modal-content p {
    color: #37474F;
    line-height: 1.7;
    margin-bottom: 16px;
  }

  /* Footer */
  footer {
    background: var(--octopurple);
    color: white;
    text-align: center;
    padding: 24px;
    margin-top: 48px;
    font-family: 'Fredoka One', cursive;
  }

  footer p { font-size: 0.9rem; }

  /* Responsive */
  @media (max-width: 900px) {
    .header-content { flex-direction: column; gap: 12px; }
    .project-info h1 { font-size: 1.8rem; }
  }

  /* Scrollbar */
  ::-webkit-scrollbar {
    width: 10px;
  }

  ::-webkit-scrollbar-track {
    background: rgba(124,58,237,0.1);
    border-radius: 10px;
  }

  ::-webkit-scrollbar-thumb {
    background: var(--octopurple);
    border-radius: 10px;
  }

  ::-webkit-scrollbar-thumb:hover {
    background: var(--octodark);
  }
</style>
</head>
<body>

<!-- Header -->
<header>
  <div class="header-content">
    <div class="header-logo">
      <div class="header-logo-icon">🐙</div>
      OctoStudio
    </div>
    <div class="header-badge">YESA EcoTales</div>
  </div>
</header>

<!-- Main content -->
<div class="container">
  <!-- Project info banner -->
  <div class="project-info">
    <div class="project-icon">🌍</div>
    <h1>EcoTales</h1>
    <p>A Planet in Peril — Interactive Story & Game</p>
  </div>

  <!-- Play button -->
  <div class="play-btn-area">
    <h3 style="font-family:'Fredoka One',cursive;color:var(--octopurple);margin-bottom:16px">▶ Start the Adventure</h3>
    <button class="play-btn" onclick="openModal('play-modal')">🎮 PLAY THE STORY</button>
  </div>

  <!-- First row: Stage + Code blocks -->
  <div class="row">
    <!-- Stage (Canvas) -->
    <div>
      <h2 style="font-family:'Fredoka One',cursive;color:var(--octopurple);margin-bottom:12px;display:flex;align-items:center;gap:8px">
        📺 Scene: Chapter 1
      </h2>
      <div class="stage stage-sky">
        <div class="stage-bg stage-sky"></div>
        <div class="stage-content">
          🌿<br><span style="font-size:1.2rem">A World Full of Life</span>
        </div>
      </div>
    </div>

    <!-- Code blocks -->
    <div>
      <div class="code-blocks">
        <div class="code-blocks-title">📋 Scripts</div>
        <div class="block events">
          <span class="block-icon">🚩</span> When clicked
        </div>
        <div class="block motion">
          <span class="block-icon">→</span> Go to (100, 50)
        </div>
        <div class="block looks">
          <span class="block-icon">👁</span> Show
        </div>
        <div class="block motion">
          <span class="block-icon">🔄</span> Glide 2 secs to (200, 100)
        </div>
        <div class="block looks">
          <span class="block-icon">💬</span> Say "Hello, EcoHero!"
        </div>
        <div class="block control">
          <span class="block-icon">⏱</span> Wait 2 seconds
        </div>
        <div class="block looks">
          <span class="block-icon">🎨</span> Change size to 150%
        </div>
        <div class="block sound">
          <span class="block-icon">🔊</span> Play sound "chime"
        </div>
      </div>
    </div>
  </div>

  <!-- Sprites section -->
  <div class="sprites-section">
    <div class="sprites-title">🎭 Sprites in This Project</div>
    <div class="sprite-item" onclick="changeScene(1)">
      <div class="sprite-icon">🌿</div>
      <div class="sprite-name">Tree</div>
    </div>
    <div class="sprite-item" onclick="changeScene(2)">
      <div class="sprite-icon">🏭</div>
      <div class="sprite-name">Factory</div>
    </div>
    <div class="sprite-item" onclick="changeScene(3)">
      <div class="sprite-icon">🌊</div>
      <div class="sprite-name">Water Guardian</div>
    </div>
    <div class="sprite-item" onclick="changeScene(4)">
      <div class="sprite-icon">🦁</div>
      <div class="sprite-name">Wildlife</div>
    </div>
    <div class="sprite-item" onclick="changeScene(5)">
      <div class="sprite-icon">🌱</div>
      <div class="sprite-name">Hope Seedling</div>
    </div>
  </div>

  <!-- Story frames -->
  <h2 style="font-family:'Fredoka One',cursive;color:var(--octopurple);margin:32px 0 20px;font-size:1.4rem">📖 Story Chapters</h2>

  <div class="story-frame">
    <h3>🌿 Chapter 1: A World Full of Life</h3>
    <p>Our planet is home to millions of plants, animals, and insects. Every creature plays a role in keeping our world healthy and balanced.</p>
    <p style="color:#7C3AED;font-weight:700">Interactive element: Click the tree sprite to learn more!</p>
  </div>

  <div class="story-frame">
    <h3>🏭 Chapter 2: Pollution & Climate Change</h3>
    <p>Factories, cars, and burning waste pump harmful gases into the air. This is pollution. These gases trap heat around Earth — like a blanket getting too thick — causing temperatures to rise.</p>
    <p style="color:#7C3AED;font-weight:700">Interactive element: The factory sprite shows animated smoke!</p>
  </div>

  <div class="story-frame">
    <h3>🌊 Chapter 3: Our Water is in Danger</h3>
    <p>Water is life — but plastic waste, chemicals, and oil spills are poisoning our rivers and oceans. Melting polar ice caps are raising sea levels, threatening coastal towns.</p>
    <p style="color:#7C3AED;font-weight:700">Interactive element: Waves animate when you click the water sprite!</p>
  </div>

  <div class="story-frame">
    <h3>🦁 Chapter 4: Animals Losing Their Homes</h3>
    <p>When forests are cut down, animals lose their habitats. South Africa's iconic wildlife — elephants, rhinos, leopards — face habitat loss every day. Protecting animals protects the whole food chain.</p>
    <p style="color:#7C3AED;font-weight:700">Interactive element: Wildlife sprites bounce and hop!</p>
  </div>

  <div class="story-frame">
    <h3>🌱 Chapter 5: YOU Are the Solution!</h3>
    <p>Every single person can make a difference. Young people are the most powerful force for change. Small actions, done by millions of people, create enormous impact.</p>
    <div style="background:#F3E8FF;border-radius:12px;padding:16px;margin-top:12px;border-left:4px solid #7C3AED">
      <p style="font-weight:700;color:#7C3AED;margin-bottom:8px">🌍 Actions YOU can take:</p>
      <p>♻️ Recycle • 🌿 Plant trees • 💡 Save energy • 🚶 Walk or cycle • 💧 Save water • 🐾 Protect wildlife</p>
    </div>
  </div>

</div>

<!-- Play modal -->
<div class="modal" id="play-modal">
  <div class="modal-content">
    <span class="modal-close" onclick="closeModal('play-modal')">&times;</span>
    <h2>🎮 Play EcoTales</h2>
    <p>This interactive story was created using <strong>OctoStudio</strong>, a block-based coding environment inspired by Scratch.</p>
    
    <h3 style="font-family:'Fredoka One',cursive;color:#7C3AED;margin-top:20px;margin-bottom:12px">🎯 How to Play:</h3>
    <ul style="color:#37474F;line-height:1.8;margin-left:20px;margin-bottom:16px">
      <li>Click through 5 chapters about environmental challenges</li>
      <li>Answer quiz questions to earn EcoHero points</li>
      <li>Interact with sprites that respond to your clicks</li>
      <li>Write your personal Eco-Pledge</li>
      <li>Unlock achievements and badges</li>
      <li>Share your story with friends!</li>
    </ul>

    <h3 style="font-family:'Fredoka One',cursive;color:#7C3AED;margin-top:20px;margin-bottom:12px">🛠️ Built With:</h3>
    <p style="background:#F3E8FF;border-radius:12px;padding:12px;color:#37474F;border-left:4px solid #7C3AED">
      <strong>OctoStudio</strong> — A fun, visual coding platform where you drag and drop code blocks to create games, animations, and interactive stories. Perfect for learning how code works!
    </p>

    <h3 style="font-family:'Fredoka One',cursive;color:#7C3AED;margin-top:20px;margin-bottom:12px">🌍 Environmental Topics:</h3>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px">
      <div style="background:#E0F6FF;border-radius:12px;padding:12px;border-left:4px solid #06B6D4">
        <strong style="color:#0369A1">Climate Change</strong><br><span style="font-size:0.85rem;color:#37474F">Greenhouse gases & warming</span>
      </div>
      <div style="background:#FFF3E0;border-radius:12px;padding:12px;border-left:4px solid #F97316">
        <strong style="color:#9A3412">Pollution</strong><br><span style="font-size:0.85rem;color:#37474F">Air, water & plastic waste</span>
      </div>
      <div style="background:#F3E8FF;border-radius:12px;padding:12px;border-left:4px solid #7C3AED">
        <strong style="color:#5B21B6">Habitat Loss</strong><br><span style="font-size:0.85rem;color:#37474F">Wildlife protection</span>
      </div>
      <div style="background:#E8F5E9;border-radius:12px;padding:12px;border-left:4px solid #4CAF50">
        <strong style="color:#1B5E20">Solutions</strong><br><span style="font-size:0.85rem;color:#37474F">Your eco actions</span>
      </div>
    </div>

    <h3 style="font-family:'Fredoka One',cursive;color:#7C3AED;margin-top:20px;margin-bottom:12px">✨ Features:</h3>
    <ul style="color:#37474F;line-height:1.8;margin-left:20px;margin-bottom:20px">
      <li><strong>5 Interactive Chapters</strong> with animations and sprites</li>
      <li><strong>Quiz System</strong> with instant feedback & points</li>
      <li><strong>Personal Eco-Pledge</strong> to commit to change</li>
      <li><strong>Achievement Badges</strong> for completion</li>
      <li><strong>Shareable Results</strong> for schools & friends</li>
    </ul>

    <button class="play-btn" onclick="window.open('ecotales-story.html','_blank');closeModal('play-modal')">
      ▶ OPEN FULL GAME →
    </button>
    <p style="color:#78909C;font-size:0.85rem;margin-top:16px;text-align:center">
      Made with 💜 using OctoStudio coding blocks<br>
      Part of the YESA EcoTales Initiative · Grade B2
    </p>
  </div>
</div>

<!-- Footer -->
<footer>
  <p>🐙 Made with OctoStudio | 🌍 YESA EcoTales Project | Grade B2 | funda.mandela.ac.za</p>
</footer>

<script>
  function changeScene(sceneNum) {
    const scenes = ['🌿', '🏭', '🌊', '🦁', '🌱'];
    const names = ['A World Full of Life', 'Pollution & Climate Change', 'Our Water is in Danger', 'Animals Losing Homes', 'YOU Are the Solution'];
    const bgs = ['stage-sky', 'stage-underground', 'stage-water', 'stage-forest', 'stage-sky'];
    
    const stageContent = document.querySelector('.stage-content');
    const stageBg = document.querySelector('.stage-bg');
    
    stageBg.className = 'stage-bg ' + bgs[sceneNum - 1];
    stageContent.innerHTML = scenes[sceneNum - 1] + '<br><span style="font-size:1.2rem">' + names[sceneNum - 1] + '</span>';
    
    document.querySelector('h2').innerHTML = '📺 Scene: Chapter ' + sceneNum;
  }

  function openModal(id) {
    document.getElementById(id).classList.add('show');
  }

  function closeModal(id) {
    document.getElementById(id).classList.remove('show');
  }

  // Close modal on background click
  document.addEventListener('click', function(e) {
    if (e.target.classList.contains('modal')) {
      e.target.classList.remove('show');
    }
  });
</script>

</body>
</html>
YESA Eco Tales - interactive environmental story game. 
