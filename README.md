<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Song Store</title>
<style>
body { font-family: Arial, sans-serif; margin:0; padding:0; background:#f4f4f4; }
header { background:#111; color:#fff; padding:40px; text-align:center; }
h1 { margin:0; font-size:2.5rem; }
section { padding:40px; }
.songs { display:grid; grid-template-columns:repeat(auto-fit, minmax(250px,1fr)); gap:20px; margin-bottom:40px; }
.song { padding:20px; border:1px solid #ccc; border-radius:10px; text-align:center; background:#fff; position: relative; }
button, .buyBtn { padding:10px 20px; border:0; background:#111; color:#fff; border-radius:5px; cursor:pointer; margin-top:10px; }
footer { background:#111; color:#fff; text-align:center; padding:20px; margin-top:40px; }
.translate-select { margin-bottom:10px; padding:6px; border-radius:5px; }
.category-section { margin-bottom:50px; }
.category-title { font-size:1.8rem; margin-bottom:20px; }
.price { font-weight:bold; margin-top:10px; }
</style>
</head>
<body>

<header>
  <div style="text-align:right; margin-bottom:10px;">
    <select id="globalLang" class="translate-select">
      <option value="en">English</option>
      <option value="es">Spanish</option>
      <option value="de">German</option>
    </select>
  </div>
  <h1>Song Store</h1>
  <p>Buy Exclusive Beats & Tracks Instantly</p>
</header>

<section>
  <h2>Available Songs</h2>
  <div id="songsContainer"></div>
</section>

<footer>
  <p>© 2025 Song Store – All Rights Reserved</p>
</footer>

<script>
const categories = ['Hip-Hop','Pop','EDM','Chill'];
const songs = [];
// Besplatni online demo mp3 fajlovi
const demoUrls = [
  'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3',
  'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3',
  'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3',
  'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3',
  'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3'
];

// Kreiraj po 10 pjesama po kategoriji
categories.forEach(cat=>{
  for(let i=1;i<=10;i++){
    songs.push({
      title:`${cat} Song ${i}`,
      file: demoUrls[i % demoUrls.length],
      category: cat,
      price: 10
    });
  }
});

function renderSongs(){
  const container = document.getElementById('songsContainer');
  container.innerHTML='';
  categories.forEach(cat=>{
    const catSection = document.createElement('div');
    catSection.className='category-section';
    const catTitle = document.createElement('div');
    catTitle.className='category-title';
    catTitle.textContent=cat;
    catSection.appendChild(catTitle);

    const catSongsDiv = document.createElement('div');
    catSongsDiv.className='songs';

    songs.filter(s=>s.category===cat).forEach(s=>{
      const div = document.createElement('div');
      div.className='song';
      div.innerHTML = `
        <select class="translate-select">
          <option value="en">English</option>
          <option value="es">Spanish</option>
          <option value="de">German</option>
        </select>
        <h3>${s.title}</h3>
        <audio controls><source src="${s.file}" type="audio/mpeg"></audio>
        <div class="price">Price: €${s.price}</div>
        <form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_blank">
          <input type="hidden" name="cmd" value="_xclick">
          <input type="hidden" name="business" value="tvojemail@paypal.com">
          <input type="hidden" name="item_name" value="${s.title}">
          <input type="hidden" name="amount" value="${s.price}">
          <input type="hidden" name="currency_code" value="EUR">
          <input type="submit" value="Buy Now" class="buyBtn">
        </form>
      `;
      catSongsDiv.appendChild(div);
    });

    catSection.appendChild(catSongsDiv);
    container.appendChild(catSection);
  });
}

renderSongs();
</script>

</body>
</html>
