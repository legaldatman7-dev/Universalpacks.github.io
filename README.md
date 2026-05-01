<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hololive Arcane Packs</title>
<style>
  body {
    margin: 0; padding: 20px;
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(#1a0033, #000022);
    color: #eee;
    text-align: center;
  }
  h1 { color: #ff99ff; text-shadow: 0 0 15px #ff66cc; }

  .sidebar { position: fixed; left: 20px; top: 50%; transform: translateY(-50%); z-index: 50; }
  .sidebar button {
    padding: 14px 24px; font-size: 18px; background: #6600aa; color: white;
    border: none; border-radius: 10px; cursor: pointer;
  }
  .sidebar button:hover { background: #aa00ff; }

  .pack-area { margin: 40px auto; width: 200px; cursor: pointer; position: relative; }
  .pack {
    width: 200px; height: 280px;
    background: linear-gradient(135deg, #6600cc, #ff00aa);
    border: 10px solid gold;
    border-radius: 20px;
    box-shadow: 0 15px 40px rgba(255,0,200,0.6);
    display: flex; align-items: center; justify-content: center;
    font-size: 32px; font-weight: bold; color: white;
  }
  .pack.shaking { animation: shake 0.5s linear infinite; }
  .pack.opening { animation: packRip 1.1s forwards; }
  @keyframes shake { 0%,100%{transform:rotate(-8deg);} 50%{transform:rotate(8deg);} }
  @keyframes packRip { 0%{transform:scale(1);} 60%{transform:scale(1.2) rotate(20deg);} 100%{transform:scale(0.5) rotate(-40deg); opacity:0;} }

  .cards-container {
    display: flex; flex-wrap: wrap; gap: 18px; justify-content: center; margin: 30px 0;
  }
  .card {
    width: 170px; height: 240px; background: #111; border-radius: 14px;
    overflow: hidden; box-shadow: 0 10px 25px rgba(0,0,0,0.8);
    cursor: pointer; transition: 0.3s;
  }
  .card:hover { transform: translateY(-18px) scale(1.1); }

  .card.basic     { border: 3px solid #aaa; }
  .card.rare      { border: 5px solid #ffd700; box-shadow: 0 0 30px #ffcc00; }
  .card.legendary { border: 6px solid #ff00ff; box-shadow: 0 0 40px #ff00ff; }
  .card.collab    { border: 6px solid #00ffff; box-shadow: 0 0 40px #00ffff; }

  .card img { width: 100%; height: 190px; object-fit: cover; }
  .card-name {
    padding: 10px 6px; font-size: 15px; font-weight: bold;
    background: rgba(0,0,0,0.75);
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
  .library-card.collab .label    { color: #00ffff; }
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
</div>

<h1>Hololive Packs</h1>

<div class="pack-area" id="packArea">
  <div class="pack" id="pack">OPEN PACK</div>
</div>

<p>Packs opened: <strong><span id="packsOpened">0</span></strong> | 
Cards Collected: <strong><span id="collectionCount">0</span></strong> / <span id="totalCards">44</span></p>

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
    <h2>📚 Collection Library <span id="libraryProgress">(0 / 44)</span></h2>
    <button onclick="closeLibrary()" style="float:right; margin-top:-10px;">Close</button>
    <div class="library-grid" id="libraryGrid"></div>
  </div>
</div>

<script>
// ==================== CHARACTERS (22) ====================
const characters = [
  { id: 1, name: "Hakos Baelz",
    normal: "baelz_normal.jpg", rare: "baelz_rare.jpg",
    normalStory: "The Embodiment of Chaos. A chaotic rat who brings fun and disorder everywhere she goes. Expect the unexpected when Bae is around!",
    rareStory: "In her rare form, Baelz has fully embraced pure chaos. Her laughter echoes through dimensions as she rewrites reality for entertainment."
  },
  { id: 2, name: "Mori Calliope",
    normal: "calliope_normal.jpg", rare: "calliope_rare.jpg",
    normalStory: "The Grim Reaper's first apprentice and underground rap sensation. Death has never looked this cool.",
    rareStory: "As the fully awakened reaper, Calliope commands death itself with her scythe and bars."
  },
  { id: 3, name: "Takanashi Kiara",
    normal: "kiara_normal.jpg", rare: "kiara_rare.jpg",
    normalStory: "A phoenix idol running a fast food empire in her dreams. She always comes back stronger.",
    rareStory: "Fully ignited phoenix mode. Her flames of passion burn so brightly that even death can't hold her."
  },
  { id: 4, name: "Ouro Kronii",
    normal: "kronii_normal.jpg", rare: "kronii_rare.jpg",
    normalStory: "Warden of Time. She controls time itself, yet still struggles with deadlines.",
    rareStory: "The true Warden of Time. She can pause, rewind, or fast-forward reality at will."
  },
  { id: 5, name: "IRyS",
    normal: "irys_normal.jpg", rare: "irys_rare.jpg",
    normalStory: "A hopeful songbird from another dimension. Her voice carries the power to heal broken hearts.",
    rareStory: "In her radiant form, IRyS becomes pure hope incarnate."
  },
  { id: 6, name: "Shiori Novella",
    normal: "shiori_normal.jpg", rare: "shiori_rare.jpg",
    normalStory: "The Archivist of Forbidden Knowledge. She knows secrets never meant to be discovered.",
    rareStory: "Having read every forbidden tome, Shiori now holds dangerous knowledge that could unravel reality."
  },
  { id: 7, name: "Raora Panthera",
    normal: "raora_normal.jpg", rare: "raora_rare.jpg",
    normalStory: "Stylish Italian panther artist. Always elegant and ready to paint the town.",
    rareStory: "Master artist in her prime. Every stroke brings emotions to life."
  },
  { id: 8, name: "Hoshimachi Suisei",
    normal: "suisei_normal.jpg", rare: "suisei_rare.jpg",
    normalStory: "The Comet Idol. Her singing can pierce the heavens and her aim is even deadlier.",
    rareStory: "The Stellar Comet. Her voice and comet strikes have reached legendary status."
  },
  { id: 9, name: "Houshou Marine",
    normal: "marine_normal.jpg", rare: "marine_rare.jpg",
    normalStory: "The energetic pirate captain who seeks treasure, adventure, and simp tax.",
    rareStory: "Captain of the seas in her ultimate form. Her charisma and greed know no bounds."
  },
  { id: 10, name: "Nekomata Okayu",
    normal: "okayu_normal.jpg", rare: "okayu_rare.jpg",
    normalStory: "The lazy but powerful cat who loves onigiri and long naps.",
    rareStory: "Fully awakened cat spirit. Her power is as immense as her love for food and sleep."
  },
  { id: 11, name: "Shiranui Flare",
    normal: "flare_normal.jpg", rare: "flare_rare.jpg",
    normalStory: "Kind-hearted half-elf dark elf archer who loves saying 'Ara ara~'.",
    rareStory: "The legendary dark elf archer. Her arrows never miss and her kindness never wavers."
  },
  { id: 12, name: "Kaela Kovalskia",
    normal: "kaela_normal.jpg", rare: "kaela_rare.jpg",
    normalStory: "The enigmatic singer with a voice that can move mountains.",
    rareStory: "The celestial singer. Her voice has the power to heal and destroy."
  },
  { id: 13, name: "Oozora Subaru",
    normal: "subaru_normal.jpg", rare: "subaru_rare.jpg",
    normalStory: "The energetic pirate captain who seeks treasure, adventure, and simp tax.",
    rareStory: "Captain of the seas in her ultimate form. Her charisma and greed know no bounds."
  },
  { id: 14, name: "Nakiri Ayame",
    normal: "ayame_normal.jpg", rare: "ayame_rare.jpg",
    normalStory: "The gentle guardian of the forest, wielding the power of nature.",
    rareStory: "The mighty forest spirit. Her connection to nature is unmatched."
  },
  { id: 15, name: "Inugami Korone",
    normal: "korone_normal.jpg", rare: "korone_rare.jpg",
    normalStory: "The energetic and mischievous fox spirit who loves causing chaos.",
    rareStory: "The powerful fox spirit. Her antics are legendary."
  },
  { id: 16, name: "Tokoyami Towa",
    normal: "towa_normal.jpg", rare: "towa_rare.jpg",
    normalStory: "The gentle and kind-hearted mermaid who loves the ocean and its creatures.",
    rareStory: "The powerful mermaid queen. Her voice can calm the storms and her compassion knows no bounds."
  },
  { id: 17, name: "Shishiro Botan",
    normal: "botan_normal.jpg", rare: "botan_rare.jpg",
    normalStory: "The gentle and kind-hearted rabbit spirit who loves gardening and peaceful moments.",
    rareStory: "The mighty rabbit spirit. Her wisdom and grace are unmatched."
  },
  { id: 18, name: "Omaru Polka",
    normal: "omaru_normal.jpg", rare: "omaru_rare.jpg",
    normalStory: "The energetic and cheerful dragon girl who loves music and dancing.",
    rareStory: "The powerful dragon girl. Her presence fills the air with magic and joy."
  },
  { id: 19, name: "Takane Lui",
    normal: "lui_normal.jpg", rare: "lui_rare.jpg",
    normalStory: "The gentle and kind-hearted bird spirit who loves singing and flying.",
    rareStory: "The mighty bird spirit. Her songs can move the heavens and her compassion knows no bounds."
  },
  { id: 20, name: "Hakui Koyori",
    normal: "koyori_normal.jpg", rare: "koyori_rare.jpg",
    normalStory: "The gentle and kind-hearted cat spirit who loves tea and quiet moments.",
    rareStory: "The powerful cat spirit. Her grace and wisdom are unmatched."
  },
  { id: 21, name: "Kazuma Iroha",
    normal: "iroha_normal.jpg", rare: "iroha_rare.jpg",
    normalStory: "The gentle and kind-hearted rabbit spirit who loves gardening and peaceful moments.",
    rareStory: "The mighty rabbit spirit. Her wisdom and grace are unmatched."
  },
  { id: 22, name: "Juufuutei Raden",
    normal: "raden_normal.jpg", rare: "raden_rare.jpg",
    normalStory: "The gentle and kind-hearted dragon spirit who loves music and dancing.",
    rareStory: "The powerful dragon spirit. Her presence fills the air with magic and joy."
  },
];

const TOTAL_UNIQUE_CARDS = characters.length * 4;   // Currently 44

let collection = {};   // e.g. {"1": 5, "101": 2, "201": 1, "301": 0}
let packsOpened = 0;

const packEl = document.getElementById('pack');
const cardsContainer = document.getElementById('cardsContainer');
const modal = document.getElementById('modal');
const modalCard = document.getElementById('modalCard');
const modalName = document.getElementById('modalName');
const storyEl = document.getElementById('story');
const libraryModal = document.getElementById('libraryModal');
const libraryGrid = document.getElementById('libraryGrid');

let currentCard = null;

// ==================== PACK OPENING WITH ANIMATION ====================
document.getElementById('packArea').addEventListener('click', () => {
  if (packEl.classList.contains('shaking') || packEl.classList.contains('opening')) return;

  packsOpened++;
  document.getElementById('packsOpened').textContent = packsOpened;

  packEl.classList.add('shaking');

  setTimeout(() => {
    packEl.classList.remove('shaking');
    packEl.classList.add('opening');

    setTimeout(() => {
      cardsContainer.innerHTML = '';

      for (let i = 0; i < 5; i++) {
        const card = getRandomCard();
        collection[card.fullId] = (collection[card.fullId] || 0) + 1;
        renderCard(card);
      }

      updateCollectionCount();
      packEl.classList.remove('opening');
    }, 900);
  }, 700);
});

function getRandomCard() {
  const char = characters[Math.floor(Math.random() * characters.length)];
  const roll = Math.random();

  let type = 'basic';
  if (roll < 0.02) type = 'collab';
  else if (roll < 0.07) type = 'legendary';
  else if (roll < 0.29) type = 'rare';

  const offset = type === 'collab' ? 300 : type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
  const fullId = char.id + offset;

  const image = type === 'collab' ? (char.collab) :
                type === 'legendary' ? (char.legendary) :
                type === 'rare' ? char.rare : char.normal;

  const story = type === 'collab' ? (char.collabStory) :
                type === 'legendary' ? (char.legendaryStory) :
                type === 'rare' ? char.rareStory : char.normalStory;

  return {
    ...char,
    type: type,
    fullId: fullId,
    image: image,
    story: story || "A mysterious Hololive talent."
  };
}

function renderCard(card) {
  const div = document.createElement('div');
  let cls = 'basic';
  if (card.type === 'rare') cls = 'rare';
  else if (card.type === 'legendary') cls = 'legendary';
  else if (card.type === 'collab') cls = 'collab';

  div.className = `card ${cls}`;
  div.innerHTML = `
    <img src="images/${card.image}" alt="${card.name}">
    <div class="card-name">${card.name} 
      ${card.type === 'collab' ? '✦ Collab' : card.type === 'legendary' ? '◆ Legendary' : card.type === 'rare' ? '★ Rare' : ''}
    </div>
  `;
  div.onclick = () => showCard(card);
  cardsContainer.appendChild(div);
}

function updateCollectionCount() {
  const totalCollected = Object.values(collection).reduce((a, b) => a + b, 0);
  document.getElementById('collectionCount').textContent = totalCollected;
  document.getElementById('totalCards').textContent = TOTAL_UNIQUE_CARDS;
}

// ==================== CARD VIEW ====================
function showCard(card) {
  currentCard = card;
  modalCard.innerHTML = `<img src="images/${card.image}" alt="${card.name}">`;
  modalName.textContent = `${card.name} — ${card.type === 'collab' ? 'Collab' : card.type === 'legendary' ? 'Legendary' : card.type === 'rare' ? 'Rare Alt' : 'Basic'}`;
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

// ==================== LIBRARY (Fixed) ====================
function openLibrary() {
  libraryGrid.innerHTML = '';

  characters.forEach(char => {
    // Basic
    appendLibraryCard(char, 'basic', collection[char.id] || 0);
    // Rare
    appendLibraryCard(char, 'rare', collection[char.id + 100] || 0);
    // Legendary
    appendLibraryCard(char, 'legendary', collection[char.id + 200] || 0);
    // Collab
    appendLibraryCard(char, 'collab', collection[char.id + 300] || 0);
  });

  const totalCollected = Object.values(collection).reduce((a, b) => a + b, 0);
  document.getElementById('libraryProgress').textContent = `(${totalCollected} / ${TOTAL_UNIQUE_CARDS})`;
  libraryModal.style.display = 'flex';
}

function appendLibraryCard(char, type, count) {
  const offset = type === 'collab' ? 300 : type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
  const fullId = char.id + offset;
  const imageFile = type === 'collab' ? (char.collab || char.rare) :
                    type === 'legendary' ? (char.legendary || char.rare) :
                    type === 'rare' ? char.rare : char.normal;

  const isOwned = count > 0;

  const div = document.createElement('div');
  div.className = `library-card ${type} ${isOwned ? '' : 'locked'}`;
  div.innerHTML = `
    <img src="${isOwned ? 'images/' + imageFile : 'https://via.placeholder.com/160x225/111111/555555?text=?'}">
    <div class="label">${char.name} ${type === 'collab' ? '✦ Collab' : type === 'legendary' ? '◆ Legendary' : type === 'rare' ? '★ Rare' : 'Basic'}</div>
    ${count > 0 ? `<div class="count">×${count}</div>` : ''}
  `;

  if (isOwned) {
    div.onclick = () => {
      const cardData = {
        ...char,
        type: type,
        image: imageFile,
        story: type === 'collab' ? (char.collabStory || char.rareStory) :
               type === 'legendary' ? (char.legendaryStory || char.rareStory) :
               type === 'rare' ? char.rareStory : char.normalStory
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
</body>
</html>
