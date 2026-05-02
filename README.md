<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hololive Arcane Packs</title>
<style>
    :root {
        --accent: #ff66cc;
    }

    body {
        margin: 0; 
        padding: 20px;
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

    button {
        padding: 12px 24px; 
        font-size: 18px; 
        background: linear-gradient(#8800cc, #aa00ff);
        color: white;
        border: none; 
        border-radius: 12px; 
        cursor: pointer;
        box-shadow: 0 8px 20px rgba(170, 0, 255, 0.4);
        transition: all 0.3s;
    }

    button:hover {
        background: linear-gradient(#aa00ff, #cc33ff);
        transform: translateY(-3px);
        box-shadow: 0 12px 25px rgba(170, 0, 255, 0.6);
    }

    .stats {
        font-size: 20px;
        margin: 15px 0 30px;
        text-shadow: 0 0 10px rgba(255,153,255,0.5);
    }

    /* Pack */
    .pack-area {
        margin: 40px auto;
        width: 220px;
        height: 340px;
        position: relative;
    }

    .pack {
        width: 220px; 
        height: 300px;
        background: linear-gradient(135deg, #6600cc, #ff00aa);
        border: 12px solid gold;
        border-radius: 24px;
        display: flex; 
        align-items: center; 
        justify-content: center;
        font-size: 34px; 
        font-weight: bold; 
        color: white;
        box-shadow: 0 20px 50px rgba(255,0,200,0.7);
        cursor: pointer;
        user-select: none;
        transition: all 0.3s;
    }

    .pack:hover {
        box-shadow: 0 25px 60px rgba(255,100,220,0.8);
    }

    /* Cards */
    .flying-card, .card {
        width: 170px;
        height: 240px;
        border-radius: 14px;
        overflow: hidden;
        background: #111;
        cursor: pointer;
        transition: all 0.4s ease;
        box-shadow: 0 10px 30px rgba(0,0,0,0.7);
        position: relative;
    }

    .flying-card.basic, .card.basic { border: 3px solid #aaaaaa; }
    .flying-card.rare, .card.rare { 
        border: 4px solid #ff00f2;
        box-shadow: 0 10px 30px rgba(0,0,0,0.7), 0 0 25px #ff00d4;
    }
    .flying-card.legendary, .card.legendary { 
        border: 5px solid #fffb00;
        box-shadow: 0 10px 30px rgba(0,0,0,0.7), 0 0 30px #fbff00;
    }

    .flying-card:hover, .card:hover {
        transform: translateY(-15px) scale(1.08);
    }

    .flying-card .image-container,
    .card .image-container {
        width: 100%;
        height: 190px;
        background: #111;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
    }

    .flying-card img,
    .card img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        padding: 4px;
        box-sizing: border-box;
    }

    .card-name {
        position: absolute;
        bottom: 0;
        left: 0; right: 0;
        background: linear-gradient(transparent, rgba(0,0,0,0.92));
        padding: 20px 12px 14px;
        font-size: 15px;
        font-weight: bold;
        text-align: center;
        text-shadow: 0 2px 6px rgba(0,0,0,0.95);
    }

    .cards-container {
        display: flex; 
        flex-wrap: wrap; 
        gap: 18px; 
        justify-content: center; 
        margin: 30px 0;
    }

    /* Library */
    .library-card {
        width: 160px;
        aspect-ratio: 160 / 225;
        border-radius: 12px;
        overflow: hidden;
        position: relative;
        background: #111;
        transition: 0.3s;
        cursor: pointer;
    }

    .library-card img {
        width: 100%;
        height: 100%;
        max-width: 300px;
        max-height: 300px;
        object-fit: contain;
        padding: 4px;
        box-sizing: border-box;
    }

    .library-card .label {
        position: absolute;
        bottom: 0;
        left: 0; right: 0;
        background: linear-gradient(transparent, rgba(0,0,0,0.9));
        padding: 14px 8px 10px;
        font-size: 13px;
        text-align: center;
    }

    .library-card .count {
        position: absolute;
        top: 8px;
        right: 8px;
        background: rgba(0,0,0,0.8);
        color: #fff;
        padding: 2px 8px;
        border-radius: 12px;
        font-size: 13px;
        font-weight: bold;
        z-index: 10;
    }

    .library-card.basic { border: 2px solid #aaaaaa; }
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

    /* Modals */
    .modal, .library-modal {
        width: 100%;
        height: 190px;
        background: #111;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
    }

    .modal-content {
        display: flex;
        max-width: 1100px;
        width: 100%;
        max-height: 85vh;
        background: #220033;
        border-radius: 20px;
        overflow: hidden;
        box-shadow: 0 20px 60px rgba(255, 0, 200, 0.5);
        border: 3px solid #ff99ff;
    }

    .modal-card img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        padding: 4px;
        box-sizing: border-box;
    }

    .story-panel {
        flex: 1;
        padding: 30px;
        text-align: left;
        background: #110022;
        overflow-y: auto;
    }

    .library-content {
        background: #1a0033;
        padding: 20px;
        border-radius: 20px;
        width: 100%;
        max-width: 1000px;
        max-height: 92vh;
        overflow-y: auto;
    }

    .library-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
        gap: 16px;
        margin-top: 15px;
    }

    .craft-btn {
        position: absolute;
        bottom: 8px;
        left: 50%;
        transform: translateX(-50%);
        padding: 6px 14px;
        font-size: 12px;
        background: linear-gradient(#00cc66, #00aa55);
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        z-index: 20;
    }

    .craft-btn:hover { background: linear-gradient(#00ff88, #00cc66); }

    @media (max-width: 480px) {
        h1 { font-size: 2rem; }
        .pack { font-size: 28px; height: 280px; }
        .flying-card, .card { width: 148px; height: 208px; }
    }
</style>
</head>
<body>

<div>
    <button onclick="openLibrary()">📚 Library</button>
    <button onclick="resetProgress()" style="background: #cc0000; margin-left: 10px;">Reset Progress</button>
</div>

<h1>Hololive Packs</h1>

<div class="pack-area" id="packArea">
    <div class="pack" id="pack">OPEN PACK</div>
</div>

<p class="stats">
    Packs opened: <strong><span id="packsOpened">0</span></strong> | 
    Cards Collected: <strong><span id="collectionCount">0</span></strong> / <span id="totalCards">90</span>
</p>

<div class="cards-container" id="cardsContainer"></div>

<!-- Card Modal -->
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
        <button onclick="closeLibrary()" style="float:right;">Close</button>
        <button onclick="showCraftingHelp()" style="margin: 10px 0;">ℹ️ How Crafting Works</button>
        
        <div class="library-grid" id="libraryGrid"></div>
    </div>
</div>

<script>
// ==================== SAVE & LOAD ====================
const SAVE_KEY = 'hololivePacksSave_v2';

let collection = {};        // { fullId: count }
let packsOpened = 0;

function saveGame() {
    localStorage.setItem(SAVE_KEY, JSON.stringify({ packsOpened, collection }));
}

function loadGame() {
    const saved = localStorage.getItem(SAVE_KEY);
    if (!saved) return;
    
    try {
        const data = JSON.parse(saved);
        packsOpened = data.packsOpened || 0;
        collection = data.collection || {};
        document.getElementById('packsOpened').textContent = packsOpened;
        updateCollectionCount();
    } catch (e) {
        console.error("Save load failed", e);
    }
}

function resetProgress() {
    if (confirm("Delete ALL progress and start over?")) {
        localStorage.removeItem(SAVE_KEY);
        collection = {};
        packsOpened = 0;
        document.getElementById('packsOpened').textContent = '0';
        updateCollectionCount();
    }
}

// ==================== CHARACTERS ====================
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
// ==================== CARD LOGIC ====================
const TOTAL_UNIQUE_CARDS = 90;

function getRandomCard() {
    const char = characters[Math.floor(Math.random() * characters.length)];
    const roll = Math.random();
    
    let type = 'basic', image = char.normal, story = char.normalStory;
    
    if (roll < 0.04) {
        type = 'legendary';
        image = char.legendary;
        story = char.legendaryStory || char.rareStory;
    } else if (roll < 0.18) {
        type = 'rare';
        image = char.rare;
        story = char.rareStory;
    }
    
    const offset = type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
    const fullId = char.id + offset;
    
    return { ...char, type, image, story, fullId };
}

// ==================== DOM ELEMENTS ====================
const packEl = document.getElementById('pack');
const cardsContainer = document.getElementById('cardsContainer');
const modal = document.getElementById('modal');
const modalCard = document.getElementById('modalCard');
const modalName = document.getElementById('modalName');
const storyEl = document.getElementById('story');
const libraryModal = document.getElementById('libraryModal');
const libraryGrid = document.getElementById('libraryGrid');

let currentCard = null;
let flyingCards = [];

// Load game
loadGame();

// ==================== PACK OPENING ====================
document.getElementById('packArea').addEventListener('click', () => {
    if (packEl.classList.contains('shaking')) return;

    packsOpened++;
    document.getElementById('packsOpened').textContent = packsOpened;

    // Clear old flying cards
    flyingCards.forEach(c => c.remove());
    flyingCards = [];

    packEl.classList.add('shaking');

    setTimeout(() => {
        packEl.classList.remove('shaking');
        packEl.classList.add('opening');

        const newCards = [];
        for (let i = 0; i < 5; i++) {
            const cardData = getRandomCard();
            collection[cardData.fullId] = (collection[cardData.fullId] || 0) + 1;
            newCards.push(cardData);
        }

        // Create flying cards
        newCards.forEach((cardData, index) => {
            const flying = document.createElement('div');
            flying.className = `flying-card ${cardData.type}`;
            flying.innerHTML = `
                <img src="images/${cardData.image}" alt="${cardData.name}">
                <div class="card-name">
                    ${cardData.name}<br>
                    <small>${cardData.type === 'legendary' ? '◆ Legendary' : cardData.type === 'rare' ? '★ Rare' : ''}</small>
                </div>
            `;
            
            flying.style.position = '0px';
            flying.style.left = '-2000px';
            cardsContainer.appendChild(flying);
            flyingCards.push(flying);

            setTimeout(() => {
                flying.style.transition = 'all 0.9s cubic-bezier(0.23, 1, 0.32, 1)';
                flying.style.left = `${(index - 2) * 100}px`;
                flying.style.top = '0px';
                flying.classList.add('show');
                
                setTimeout(() => flying.onclick = () => showCard(cardData), 1100);
            }, 180 + index * 90);
        });

        updateCollectionCount();
        saveGame();

        setTimeout(() => packEl.classList.remove('opening'), 1500);
    }, 600);
});

function updateCollectionCount() {
    const count = Object.keys(collection).length;
    document.getElementById('collectionCount').textContent = count;
    saveGame();
}

// ==================== MODALS ====================
function showCard(card) {
    currentCard = card;
    modalCard.innerHTML = `<img src="images/${card.image}" alt="${card.name}">`;
    modalName.textContent = `${card.name} — ${card.type.charAt(0).toUpperCase() + card.type.slice(1)}`;
    storyEl.textContent = '';
    modal.style.display = 'flex';
}

function inspectCard() {
    if (!currentCard) return;
    storyEl.textContent = '';
    let i = 0;
    const text = currentCard.story;
    const interval = setInterval(() => {
        if (i < text.length) storyEl.textContent += text[i++];
        else clearInterval(interval);
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

    document.getElementById('libraryProgress').textContent = 
        `(${Object.keys(collection).length} / ${TOTAL_UNIQUE_CARDS})`;
    
    libraryModal.style.display = 'flex';
}

function appendLibraryCard(char, type, count) {
    const offset = type === 'legendary' ? 200 : type === 'rare' ? 100 : 0;
    const fullId = char.id + offset;
    const imageFile = type === 'legendary' ? char.legendary : type === 'rare' ? char.rare || char.normal : char.normal;

    const div = document.createElement('div');
    div.className = `library-card ${type}`;

    let html = `
        <img src="${count > 0 ? 'images/' + imageFile : 'https://via.placeholder.com/160x225/111111/555555?text=?'}">
        <div class="label">${char.name}<br><small>${type === 'legendary' ? '◆ Legendary' : type === 'rare' ? '★ Rare' : 'Basic'}</small></div>
    `;

    if (count > 0) {
        html += `<div class="count">×${count}</div>`;
    }

    // Crafting button
    if ((type === 'basic' || type === 'rare') && count >= 5) {
        html += `
            <button class="craft-btn" onclick="event.stopImmediatePropagation(); craftCard(${char.id}, '${type}')">
                Craft ↑
            </button>
        `;
    }

    div.innerHTML = html;

    if (count > 0) {
        div.onclick = () => {
            const cardData = {
                ...char,
                type,
                image: imageFile,
                story: type === 'legendary' ? (char.legendaryStory || char.rareStory) : 
                       type === 'rare' ? char.rareStory : char.normalStory
            };
            showCard(cardData);
            closeLibrary();
        };
    }

    libraryGrid.appendChild(div);
}

function craftCard(charId, currentType) {
    const currentOffset = currentType === 'basic' ? 0 : 100;
    const nextOffset = currentType === 'basic' ? 100 : 200;
    const currentFullId = charId + currentOffset;
    const nextFullId = charId + nextOffset;

    if ((collection[currentFullId] || 0) < 5) return alert("Need 5 copies to craft!");

    collection[currentFullId] -= 5;
    if (collection[currentFullId] <= 0) delete collection[currentFullId];

    collection[nextFullId] = (collection[nextFullId] || 0) + 1;

    alert(`✅ Crafted 1 ${currentType === 'basic' ? 'Rare' : 'Legendary'} card!`);
    openLibrary();
    updateCollectionCount();
}

function showCraftingHelp() {
    alert("Crafting Rules:\n\n• 5 Basic → 1 Rare (same character)\n• 5 Rare → 1 Legendary (same character)");
}

function closeLibrary() {
    libraryModal.style.display = 'none';
}

// Keyboard support
document.addEventListener('keydown', e => {
    if (e.key === "Escape") {
        if (libraryModal.style.display === 'flex') closeLibrary();
        else if (modal.style.display === 'flex') closeModal();
    }
});
</script>
</body>
</html>
