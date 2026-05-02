<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Pack Opening</title>
<style>

body {
  margin: 0; padding: 20px;
  font-family: 'Segoe UI', sans-serif;
  background: #1a0033;
  color: #eee;
  text-align: center;
}

h1 { 
  color: #ff99ff; 
  text-shadow: 0 0 20px #ff66cc;
  font-size: 48px;
  margin: 20px 0 10px;
}

.sidebar button {
  padding: 16px 28px; 
  font-size: 19px; 
  background: linear-gradient(#8800cc, #aa00ff);
  color: white;
  border: none; 
  border-radius: 12px; 
  cursor: pointer;
  box-shadow: 0 8px 20px rgba(170, 0, 255, 0.4);
  transition: all 0.3s;
}

.sidebar button:hover {
  background: linear-gradient(#aa00ff, #cc33ff);
  transform: translateY(-3px);
  box-shadow: 0 12px 25px rgba(170, 0, 255, 0.6);
}

/* Stats */
.stats {
  font-size: 20px;
  margin: 15px 0 30px;
  text-shadow: 0 0 10px rgba(255,153,255,0.5);
}

/* Pack Area */
.pack-area {
  margin: 40px auto;
  width: 220px;
  position: relative;
  height: 340px;
}

.pack {
  width: 220px; 
  height: 300px;
  background: linear-gradient(135deg, #6600cc, #ff00aa);
  border: 12px solid gold;
  border-radius: 24px;
  box-shadow: 0 20px 50px rgba(255,0,200,0.7);
  display: flex; 
  align-items: center; 
  justify-content: center;
  font-size: 34px; 
  font-weight: bold; 
  color: white;
  position: relative;
  z-index: 10;
  cursor: pointer;
  user-select: none;
}

.pack:hover {
  box-shadow: 0 25px 60px rgba(255,100,220,0.8);
}

.flying-card, .card {
  width: 170px;
  height: 240px;
  border-radius: 14px;
  overflow: hidden;
  position: relative;
  background: #111;
  cursor: pointer;
  transition: all 0.4s ease;
  box-shadow: 0 10px 30px rgba(0,0,0,0.7);
}

/* Rarity Glows */
.flying-card.basic, .card.basic {
  border: 3px solid #aaaaaa;
  box-shadow: 0 10px 30px rgba(0,0,0,0.7),
              0 0 15px rgba(170, 170, 170, 0.6);
}

.flying-card.rare, .card.rare {
  border: 4px solid #ff00f2;
  box-shadow: 0 10px 30px rgba(0,0,0,0.7),
              0 0 25px #ff00d4,
              0 0 45px rgba(255, 0, 234, 0.7);
}

.flying-card.legendary, .card.legendary {
  border: 5px solid #fffb00;
  box-shadow: 0 10px 30px rgba(0,0,0,0.7),
              0 0 30px #fbff00,
              0 0 60px rgba(251, 255, 0, 0.8);
}

.flying-card:hover, .card:hover {
  transform: translateY(-15px) scale(1.08);
  box-shadow: 0 20px 50px rgba(0,0,0,0.8);
}

.flying-card.rare:hover, .card.rare:hover {
  box-shadow: 0 20px 50px rgba(0,0,0,0.8),
              0 0 35px #ffd700,
              0 0 70px rgba(255, 215, 0, 0.9);
}

.flying-card.legendary:hover, .card.legendary:hover {
  box-shadow: 0 20px 50px rgba(0,0,0,0.8),
              0 0 40px #ff00ff,
              0 0 80px rgba(255, 0, 255, 0.95);
}

.flying-card .image-container {
  width: 100%;
  height: 190px;
  background: #111;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

.flying-card img {
  width: 100%;
  height: 100%;
  object-fit: contain;           /* ← This is the key change */
  background: #111;
  padding: 4px;
  box-sizing: border-box;
}

.flying-card .card-name {
  padding: 12px 8px;
  font-size: 14.5px;
  font-weight: bold;
  background: rgba(0,0,0,0.85);
  text-align: center;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  line-height: 1.25;
}

.flying-card.show {
  opacity: 1;
  pointer-events: auto;
  transition: all 0.9s cubic-bezier(0.23, 1, 0.32, 1);
}

.flying-card .card-name, .card .card-name {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0,0,0,0.92));
  padding: 20px 12px 14px;
  font-size: 15px;
  font-weight: bold;
  color: white;
  text-align: center;
  text-shadow: 0 2px 6px rgba(0,0,0,0.95);
  line-height: 1.25;
  z-index: 10;
}

.cards-container {
  display: flex; flex-wrap: wrap; gap: 18px; justify-content: center; margin: 30px 0;
}

.card-name small {
  display: block;
  font-size: 13px;
  opacity: 0.95;
  margin-top: 3px;
}

.card {
  width: 170px; 
  height: 240px; 
  background: #111; 
  border: gold 14px solid;
  overflow: hidden; 
  box-shadow: 0 12px 30px gold;
  cursor: pointer; 
  transition: all 0.3s;
  display: flex;
  flex-direction: column;
}

.card .image-container {
  width: 100%;
  height: 190px;
  background: #111;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

.card img {
  width: 100%;
  height: 100%;
  object-fit: contain;           /* ← Key fix */
  background: #111;
  padding: 4px;
  box-sizing: border-box;
}

.card .card-name {
  padding: 12px 8px;
  font-size: 15px;
  font-weight: bold;
  background: rgba(0,0,0,0.75);
  text-align: center;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Library cards */
.library-card {
  width: 160px;
  height: 225px;
  border-radius: 12px;
  overflow: hidden;
  position: relative;
  background: #111;
  transition: all 0.2s;
}

.library-card.basic {
  border: 2px solid #aaaaaa;
}

.library-card.rare {
  border: 3px solid #ffd700;
  box-shadow: 0 0 20px #ffd700;
}

.library-card.legendary {
  border: 4px solid #ff00ff;
  box-shadow: 0 0 25px #ff00ff;
}

.library-card:hover {
  transform: scale(1.08);
}

.library-card img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  background: #0a0a0a;
}

.library-card .label {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0,0,0,0.9));
  padding: 12px 6px 10px;
  font-size: 13px;
  text-align: center;
  text-shadow: 0 1px 3px black;
}

  .modal, .library-modal {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.95); z-index: 300;
    align-items: center; justify-content: center;
  }
  .modal-content {
    display: flex; max-width: 1100px; width: 92%;
    background: #220033; border-radius: 20px; overflow: hidden;
  }
  .modal-card { width: 380px; flex-shrink: 0; }
  .modal-card img { width: 100%; height: auto; }
  .story-panel { flex: 1; padding: 35px; text-align: left; background: #110022; }
  .typewriter { margin-top: 20px; font-size: 17.5px; line-height: 1.65; white-space: pre-wrap; }

  .library-content {
    background: #1a0033; padding: 25px; border-radius: 20px;
    max-width: 1200px; width: 95%; max-height: 90vh; overflow-y: auto;
  }
  .library-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 16px; margin-top: 20px;
  }
  .library-card {
    width: 160px; height: 225px; border-radius: 12px; overflow: hidden;
    position: relative; cursor: pointer; transition: 0.2s;
  }
  .library-card:hover { transform: scale(1.05); }
  .library-card img { width: 100%; height: 100%; object-fit: cover; }
  .library-card.locked { filter: brightness(0.25) grayscale(1); border: 3px solid #555; }
  .library-card .label {
    position: absolute; bottom: 0; left: 0; right: 0;
    background: rgba(0,0,0,0.85); padding: 6px; font-size: 13px; text-align: center;
  }
  .library-card.rare .label      { color: #ffd700; }
  .library-card.legendary .label { color: #ff00ff; }
  .library-card .count {
    position: absolute; top: 6px; right: 6px;
    background: rgba(255,215,0,0.9); color: #000;
    font-size: 12px; font-weight: bold; padding: 2px 8px; border-radius: 10px;
  }
</style>
</head>
<body>

<div class="sidebar">
  <button onclick="openLibrary()">📚 Library</button>
  <button onclick="resetProgress()" style="background: #cc0000; margin-top: 10px;">Reset Progress</button>
</div>

<h1>Pack Opening</h1>

<div class="pack-area" id="packArea">
  <div class="pack" id="pack">OPEN PACK</div>
</div>

<p>Packs opened: <strong><span id="packsOpened">0</span></strong> | 
Cards Collected: <strong><span id="collectionCount">0</span></strong> / <span id="totalCards">90</span></p>

<div class="cards-container" id="cardsContainer"></div>

<!-- Card View Modal -->
<div class="modal" id="modal">
  <div class="modal-content">
    <div class="modal-card" id="modalCard"></div>
    <div class="story-panel">
      <h2 id="modalName"></h2>
      <button onclick="closeModal()">← Back</button>
      <button onclick="inspectCard()">Inspect Closely</button>
      <div id="story" class="typewriter"></div>
    </div>
  </div>
</div>

<!-- Library Modal -->
<div class="library-modal" id="libraryModal">
  <div class="library-content">
    <h2>📚 Collection Library <span id="libraryProgress">(0 / 90)</span></h2>
    <button onclick="closeLibrary()" style="float:right; margin-top:-10px;">Close</button>
    <div class="library-grid" id="libraryGrid"></div>
  </div>
</div>

<script>
// ==================== SAVE & LOAD SYSTEM ====================
const SAVE_KEY = 'hololivePacksSave_v1';   // Change version if you update the structure later

function saveGame() {
    const saveData = {
        packsOpened: packsOpened,
        collection: collection
    };
    localStorage.setItem(SAVE_KEY, JSON.stringify(saveData));
}

function loadGame() {
    const saved = localStorage.getItem(SAVE_KEY);
    if (!saved) return false;

    try {
        const data = JSON.parse(saved);
        
        if (data.packsOpened !== undefined) {
            packsOpened = data.packsOpened;
            document.getElementById('packsOpened').textContent = packsOpened;
        }
        
        if (data.collection) {
            collection = data.collection;
            updateCollectionCount();
        }
        return true;
    } catch (e) {
        console.error("Failed to load save:", e);
        return false;
    }
}

function resetProgress() {
    if (confirm("Delete ALL progress and start over?")) {
        localStorage.removeItem(SAVE_KEY);
        collection = {};
        packsOpened = 0;
        document.getElementById('packsOpened').textContent = '0';
        document.getElementById('collectionCount').textContent = '0';
        updateCollectionCount();
        saveGame(); // optional
    }
}

// ==================== CHARACTERS (22) ====================
const characters = [
  { id: 1, name: "Hakos Baelz",
    normal: "baelz_normal.jpg", rare: "baelz_rare.jpg", legendary: "baelz_legendary.jpg",
    normalStory: "The Embodiment of Chaos. A chaotic rat who brings fun and disorder everywhere she goes. Expect the unexpected when Bae is around!",
    rareStory: "In her rare form, Baelz has fully embraced pure chaos. Her laughter echoes through dimensions as she rewrites reality for entertainment."
  },
  { id: 2, name: "Mori Calliope",
    normal: "calliope_normal.jpg", rare: "calliope_rare.jpg", legendary: "calliope_legendary.jpg",
    normalStory: "The Grim Reaper's first apprentice and underground rap sensation. Death has never looked this cool.",
    rareStory: "As the fully awakened reaper, Calliope commands death itself with her scythe and bars."
  },
  { id: 3, name: "Takanashi Kiara",
    normal: "kiara_normal.jpg", rare: "kiara_rare.jpg", legendary: "kiara_legendary.jpg",
    normalStory: "A phoenix idol running a fast food empire in her dreams. She always comes back stronger.",
    rareStory: "Fully ignited phoenix mode. Her flames of passion burn so brightly that even death can't hold her."
  },
  { id: 4, name: "Ouro Kronii",
    normal: "kronii_normal.jpg", rare: "kronii_rare.jpg", legendary: "kronii_legendary.jpg",
    normalStory: "Warden of Time. She controls time itself, yet still struggles with deadlines.",
    rareStory: "The true Warden of Time. She can pause, rewind, or fast-forward reality at will."
  },
  { id: 5, name: "IRyS",
    normal: "irys_normal.jpg", rare: "irys_rare.jpg", legendary: "irys_legendary.jpg",
    normalStory: "A hopeful songbird from another dimension. Her voice carries the power to heal broken hearts.",
    rareStory: "In her radiant form, IRyS becomes pure hope incarnate."
  },
  { id: 6, name: "Shiori Novella",
    normal: "shiori_normal.jpg", rare: "shiori_rare.jpg", legendary: "shiori_legendary.jpg",
    normalStory: "The Archivist of Forbidden Knowledge. She knows secrets never meant to be discovered.",
    rareStory: "Having read every forbidden tome, Shiori now holds dangerous knowledge that could unravel reality."
  },
  { id: 7, name: "Raora Panthera",
    normal: "raora_normal.jpg", rare: "raora_rare.jpg", legendary: "raora_legendary.jpg", 
    normalStory: "Stylish Italian panther artist. Always elegant and ready to paint the town.",
    rareStory: "Master artist in her prime. Every stroke brings emotions to life."
  },
  { id: 8, name: "Hoshimachi Suisei",
    normal: "suisei_normal.jpg", rare: "suisei_rare.jpg", legendary: "suisei_legendary.jpg",
    normalStory: "The Comet Idol. Her singing can pierce the heavens and her aim is even deadlier.",
    rareStory: "The Stellar Comet. Her voice and comet strikes have reached legendary status."
  },
  { id: 9, name: "Houshou Marine",
    normal: "marine_normal.jpg", rare: "marine_rare.jpg", legendary: "marine_legendary.jpg",
    normalStory: "The energetic pirate captain who seeks treasure, adventure, and simp tax.",
    rareStory: "Captain of the seas in her ultimate form. Her charisma and greed know no bounds."
  },
  { id: 10, name: "Nekomata Okayu",
    normal: "okayu_normal.jpg", rare: "okayu_rare.jpg", legendary: "okayu_legendary.jpg",
    normalStory: "The lazy but powerful cat who loves onigiri and long naps.",
    rareStory: "Fully awakened cat spirit. Her power is as immense as her love for food and sleep."
  },
  { id: 11, name: "Shiranui Flare",
    normal: "flare_normal.jpg", rare: "flare_rare.jpg", legendary: "flare_legendary.jpg",
    normalStory: "Kind-hearted half-elf dark elf archer who loves saying 'Ara ara~'.",
    rareStory: "The legendary dark elf archer. Her arrows never miss and her kindness never wavers."
  },
  { id: 12, name: "Kaela Kovalskia",
    normal: "kaela_normal.jpg", rare: "kaela_rare.jpg", legendary: "kaela_legendary.jpg",
    normalStory: "The enigmatic singer with a voice that can move mountains.",
    rareStory: "The celestial singer. Her voice has the power to heal and destroy."
  },
  { id: 13, name: "Oozora Subaru",
    normal: "subaru_normal.jpg", rare: "subaru_rare.jpg", legendary: "subaru_legendary.jpg",
    normalStory: "The energetic pirate captain who seeks treasure, adventure, and simp tax.",
    rareStory: "Captain of the seas in her ultimate form. Her charisma and greed know no bounds."
  },
  { id: 14, name: "Nakiri Ayame",
    normal: "ayame_normal.jpg", rare: "ayame_rare.jpg", legendary: "ayame_legendary.jpg",
    normalStory: "The gentle guardian of the forest, wielding the power of nature.",
    rareStory: "The mighty forest spirit. Her connection to nature is unmatched."
  },
  { id: 15, name: "Inugami Korone",
    normal: "korone_normal.jpg", rare: "korone_rare.jpg", legendary: "korone_legendary.jpg",
    normalStory: "The energetic and mischievous fox spirit who loves causing chaos.",
    rareStory: "The powerful fox spirit. Her antics are legendary."
  },
  { id: 16, name: "Tokoyami Towa",
    normal: "towa_normal.jpg", rare: "towa_rare.jpg", legendary: "towa_legendary.jpg",
    normalStory: "The gentle and kind-hearted mermaid who loves the ocean and its creatures.",
    rareStory: "The powerful mermaid queen. Her voice can calm the storms and her compassion knows no bounds."
  },
  { id: 17, name: "Shishiro Botan",
    normal: "botan_normal.jpg", rare: "botan_rare.jpg", legendary: "botan_legendary.jpg",
    normalStory: "The gentle and kind-hearted rabbit spirit who loves gardening and peaceful moments.",
    rareStory: "The mighty rabbit spirit. Her wisdom and grace are unmatched."
  },
  { id: 18, name: "Omaru Polka",
    normal: "omaru_normal.jpg", rare: "omaru_rare.jpg", legendary: "omaru_legendary.jpg",
    normalStory: "The energetic and cheerful dragon girl who loves music and dancing.",
    rareStory: "The powerful dragon girl. Her presence fills the air with magic and joy."
  },
  { id: 19, name: "Takane Lui",
    normal: "lui_normal.jpg", rare: "lui_rare.jpg", legendary: "lui_legendary.jpg",
    normalStory: "The gentle and kind-hearted bird spirit who loves singing and flying.",
    rareStory: "The mighty bird spirit. Her songs can move the heavens and her compassion knows no bounds."
  },
  { id: 20, name: "Hakui Koyori",
    normal: "koyori_normal.jpg", rare: "koyori_rare.jpg", legendary: "koyori_legendary.jpg",
    normalStory: "The gentle and kind-hearted cat spirit who loves tea and quiet moments.",
    rareStory: "The powerful cat spirit. Her grace and wisdom are unmatched."
  },
  { id: 21, name: "Kazuma Iroha",
    normal: "iroha_normal.jpg", rare: "iroha_rare.jpg", legendary: "iroha_legendary.jpg",
    normalStory: "The gentle and kind-hearted rabbit spirit who loves gardening and peaceful moments.",
    rareStory: "The mighty rabbit spirit. Her wisdom and grace are unmatched."
  },
  { id: 22, name: "Juufuutei Raden",
    normal: "raden_normal.jpg", rare: "raden_rare.jpg", legendary: "raden_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 23, name: "Ishmael",
    normal: "ishmael_normal.jpg", rare: "ishmael_rare.jpg", legendary: "ishmael_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 24, name: "Ryoshuu",
    normal: "ryoshu_normal.jpg", rare: "ryoshu_rare.jpg", legendary: "ryoshu_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 25, name: "Faust",
    normal: "faust_normal.jpg", rare: "faust_rare.jpg", legendary: "faust_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 26, name: "Don Quixote",
    normal: "don_quixote_normal.jpg", rare: "don_quixote_rare.jpg", legendary: "don_quixote_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 27, name: "Outis",
    normal: "outis_normal.jpg", rare: "outis_rare.jpg", legendary: "outis_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 28, name: "Tifa Lockhart",
    normal: "tifa_normal.jpg", rare: "tifa_rare.jpg", legendary: "tifa_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 29, name: "Y'shtola Rhul",
    normal: "yshtola_normal.jpg", rare: "yshtola_rare.jpg", legendary: "yshtola_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
  { id: 30, name: "Alisaie Leveilleur",
    normal: "alisae_normal.jpg", rare: "alisae_rare.jpg", legendary: "alisae_legendary.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
];

const TOTAL_UNIQUE_CARDS = 90; // 30 characters × 3 main variants (Basic + Rare + Legendary). Adjust if needed.

let collection = {};        // { fullId: count }
let packsOpened = 0;
let flyingCards = [];       // Track current flying cards to remove them

const packEl = document.getElementById('pack');
const cardsContainer = document.getElementById('cardsContainer');
const modal = document.getElementById('modal');
const modalCard = document.getElementById('modalCard');
const modalName = document.getElementById('modalName');
const storyEl = document.getElementById('story');
const libraryModal = document.getElementById('libraryModal');
const libraryGrid = document.getElementById('libraryGrid');

let currentCard = null;

// Load saved progress on page load
loadGame();

// ==================== GET RANDOM CARD ====================
function getRandomCard() {
  const char = characters[Math.floor(Math.random() * characters.length)];
  const roll = Math.random();

  let type = 'basic';
  let image = char.normal;
  let story = char.normalStory;

  if (roll < 0.04) {           // 4% Legendary
    type = 'legendary';
    image = char.legendary;
    story = char.legendaryStory;
  } else if (roll < 0.18) {    // 14% Rare
    type = 'rare';
    image = char.rare;
    story = char.rareStory;
  }

  const offset = type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
  const fullId = char.id + offset;

  return { ...char, type, image, story, fullId };
}

// ==================== CLEAR PREVIOUS CARDS ====================
function clearPreviousCards() {
  flyingCards.forEach(card => {
    if (card.parentNode) card.parentNode.removeChild(card);
  });
  flyingCards = [];
}

// ==================== PACK OPENING ====================
document.getElementById('packArea').addEventListener('click', () => {
  if (packEl.classList.contains('shaking') || packEl.classList.contains('opening')) return;

  packsOpened++;
  document.getElementById('packsOpened').textContent = packsOpened;

  clearPreviousCards();                    // ← NEW: Remove old cards

  const packRect = packEl.getBoundingClientRect();
  const containerRect = cardsContainer.getBoundingClientRect();

  packEl.classList.add('shaking');

  setTimeout(() => {
    packEl.classList.remove('shaking');
    packEl.classList.add('opening');

    const newCards = [];
    for (let i = 0; i < 5; i++) {
      const cardData = getRandomCard();
      
      if (!collection[cardData.fullId]) collection[cardData.fullId] = 0;
      collection[cardData.fullId]++;

      newCards.push(cardData);
    }

    // Create flying cards (flying down)
    newCards.forEach((cardData, index) => {
      const flying = document.createElement('div');
      flying.className = `flying-card ${cardData.type || 'basic'}`;
      
      flying.innerHTML = `
        <img src="images/${cardData.image}" alt="${cardData.name}">
        <div class="card-name">
          ${cardData.name}<br>
          <small>
              ${cardData.type === 'legendary' ? '◆ Legendary' : 
              cardData.type === 'rare' ? '★ Rare' : ''}
          </small>
        </div>
      `;

      flying.style.left = `${-2000}px`;
      flying.style.top = `${0}px`;

      cardsContainer.appendChild(flying);
      flyingCards.push(flying);

      setTimeout(() => {
        const offsetX = (index - 2) * 10;
        const finalLeft = 0 + offsetX;
        const finalTop = 0;

        flying.style.left = `${finalLeft}px`;
        flying.style.top = `${finalTop}px`;
        flying.style.transform = `scale(1) rotate(${Math.random()*10 - 5}deg)`;
        flying.classList.add('show');

        setTimeout(() => {
          flying.style.pointerEvents = 'auto';
          flying.onclick = () => showCard(cardData);
        }, 1100);
      }, 180 + index * 90);
    });

    updateCollectionCount();
    saveGame();

    setTimeout(() => {
      packEl.classList.remove('opening');
    }, 1500);

  }, 600);
});

function updateCollectionCount() {
  const uniqueCollected = Object.keys(collection).length;
  document.getElementById('collectionCount').textContent = uniqueCollected;
  saveGame();
}

// ==================== CARD MODAL ====================
function showCard(card) {
  currentCard = card;
  modalCard.innerHTML = `<img src="images/${card.image}" alt="${card.name}">`;
  modalName.textContent = `${card.name} — ${card.type === 'legendary' ? 'Legendary' : card.type === 'rare' ? 'Rare' : 'Basic'}`;
  storyEl.textContent = '';
  modal.style.display = 'flex';
}

function inspectCard() {
  if (!currentCard) return;
  storyEl.textContent = '';
  let i = 0;
  const text = currentCard.story;
  const int = setInterval(() => {
    if (i < text.length) storyEl.textContent += text[i++];
    else clearInterval(int);
  }, 35);
}

function closeModal() {
  modal.style.display = 'none';
}

// ==================== LIBRARY ====================
function openLibrary() {
  libraryGrid.innerHTML = '';

  characters.forEach(char => {
    appendLibraryCard(char, 'basic', collection[char.id] || 0);
    appendLibraryCard(char, 'rare', collection[char.id + 100] || 0);
    appendLibraryCard(char, 'legendary', collection[char.id + 200] || 0);
  });

  const uniqueCollected = Object.keys(collection).length;
  document.getElementById('libraryProgress').textContent = `(${uniqueCollected} / ${TOTAL_UNIQUE_CARDS})`;
  libraryModal.style.display = 'flex';
}

function appendLibraryCard(char, type, count) {
  const offset = type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
  const fullId = char.id + offset;
  const imageFile = type === 'legendary' ? char.legendary : type === 'rare' ? char.rare : char.normal;

  const isOwned = count > 0;

  const div = document.createElement('div');
  div.className = `library-card ${type} ${isOwned ? '' : 'locked'}`;
  div.innerHTML = `
    <img src="${isOwned ? 'images/' + imageFile : 'images/locked.png'}" alt="${char.name}">
    <div class="label">${char.name} ${type === 'legendary' ? '◆ Legendary' : type === 'rare' ? '★ Rare' : 'Basic'}</div>
    ${count > 0 ? `<div class="count">×${count}</div>` : ''}
  `;

  if (isOwned) {
    div.onclick = () => {
      const cardData = {
        ...char,
        type: type,
        image: imageFile,
        story: type === 'legendary' ? char.legendaryStory : type === 'rare' ? char.rareStory : char.normalStory
      };
      showCard(cardData);
      closeLibrary();
    };
  }
  libraryGrid.appendChild(div);
}

function closeLibrary() {
  libraryModal.style.display = 'none';
}

// Escape key
document.addEventListener('keydown', e => {
  if (e.key === "Escape") {
    if (libraryModal.style.display === 'flex') closeLibrary();
    else if (modal.style.display === 'flex') closeModal();
  }
});
</script>
