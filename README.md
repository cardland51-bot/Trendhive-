<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>TrendHive</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@600&display=swap');

:root {
  --gold: #f5c842;
  --black-glass: rgba(10, 10, 10, 0.8);
  --shine: rgba(245, 200, 66, 0.2);
}

html, body {
  margin: 0; padding: 0;
  font-family: 'Orbitron', sans-serif;
  background: linear-gradient(135deg, #000 0%, #1a1a1a 100%);
  display: flex; flex-direction: column; align-items: center;
  overflow-x: hidden; scroll-behavior: smooth;
}

/* Honeycomb Overlay */
.honeycomb-overlay {
  position: fixed; top:0; left:0; width:100vw; height:100vh;
  pointer-events:none;
  background-image: radial-gradient(circle at 1px 1px, rgba(245,200,66,0.08) 1px, transparent 0);
  background-size: 60px 60px;
  animation: honeycomb-shimmer 10s linear infinite;
  z-index: 0;
}
@keyframes honeycomb-shimmer { from {background-position:0 0;} to {background-position:60px 60px;} }

/* Content Box */
.content-box {
  position: relative; z-index:1;
  background: var(--black-glass); backdrop-filter: blur(10px);
  border: 1px solid var(--shine); padding: 60px 20px; border-radius: 20px;
  box-shadow: 0 0 40px rgba(245,200,66,0.1); text-align: center;
  max-width: 90%; margin: 20px 0;
}

h1 { color: var(--gold); font-size:3rem; margin:0; letter-spacing:2px; text-shadow:0 0 10px rgba(245,200,66,0.3); }
p { color:#ddd; margin-top:15px; font-size:1.2rem; letter-spacing:1px; }
.button {
  margin-top:25px; background: var(--gold); color:#000; border:none;
  padding:12px 30px; border-radius:30px; font-weight:bold; cursor:pointer;
  box-shadow:0 0 15px rgba(245,200,66,0.3); transition: all 0.3s ease;
}
.button:hover { background:#ffd85f; box-shadow:0 0 25px rgba(245,200,66,0.5); }

.chart-container {
  width:100%; max-width:800px; margin:30px auto; background: var(--black-glass);
  padding:20px; border-radius:20px; border:1px solid var(--shine);
  box-shadow:0 0 30px rgba(245,200,66,0.1); position: relative;
}

.ghost-label {
  position:absolute; color:#ffd85f; font-weight:bold; pointer-events:none;
  opacity:0; animation: floatUp 2s ease-out forwards;
}
@keyframes floatUp { 0% {opacity:1; transform:translateY(0);} 100% {opacity:0; transform:translateY(-50px);} }
</style>
</head>
<body>

<div class="honeycomb-overlay"></div>

<div class="content-box">
  <h1>TrendHive</h1>
  <p>See Trends Before They Happen.</p>
  <button class="button" id="enterButton">Enter The Hive</button>
</div>

<div class="chart-container" id="chartSection">
  <canvas id="liveTrendChart"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
// Categories and Chart
const categories = ['Tech', 'Music', 'Politics', 'Health', 'Entertainment'];
const ctx = document.getElementById('liveTrendChart').getContext('2d');
const trendChart = new Chart(ctx, {
  type: 'bar',
  data: {
    labels: categories,
    datasets: [{
      label: 'Number of Trends',
      data: [0,0,0,0,0],
      backgroundColor: ['#2a2a72','#3f3fbd','#5a5ae0','#7a7aed','#9a9af0']
    }]
  },
  options: {
    responsive:true,
    plugins:{
      legend:{display:false},
      tooltip:{
        callbacks: {
          label: function(context) {
            const tips = [
              "High engagement", "Viral spike", "Buzzing", "Trending worldwide", "Watch this category"
            ];
            return `Count: ${context.raw} | ${tips[Math.floor(Math.random()*tips.length)]}`;
          }
        }
      }
    },
    scales:{y:{beginAtZero:true}}
  }
});

// Simulate trends and ghost labels
function generateTrends() {
  const counts = {Tech:0, Music:0, Politics:0, Health:0, Entertainment:0};
  for(let i=0;i<2;i++){ // 2 per second
    const cat = categories[Math.floor(Math.random()*categories.length)];
    counts[cat]++;
    createGhost(cat);
  }
  return counts;
}

// Ghost floating label
function createGhost(category) {
  const chart = document.getElementById('liveTrendChart');
  const rect = chart.getBoundingClientRect();
  const x = Math.random() * rect.width;
  const y = Math.random() * rect.height * 0.6;
  const ghost = document.createElement('div');
  ghost.className = 'ghost-label';
  ghost.style.left = `${x}px`;
  ghost.style.top = `${y}px`;
  ghost.textContent = `#${category} Trend`;
  chart.parentElement.appendChild(ghost);
  setTimeout(()=>ghost.remove(), 2000);
}

// Update Chart
function updateChart() {
  const newCounts = generateTrends();
  trendChart.data.datasets[0].data = trendChart.data.datasets[0].data.map((v,i)=>v+newCounts[categories[i]]);
  trendChart.update();
}

// Start mock pipeline
setInterval(updateChart, 1000);

// Enter The Hive scroll
document.getElementById('enterButton').addEventListener('click', () => {
  document.getElementById('chartSection').scrollIntoView({behavior:'smooth'});
});
</script>

</body>
</html>
