<Clientes s>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mercado Potencial - Arte Personalizado</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      transition: background-color 0.3s, color 0.3s;
    }
    .light-mode {
      background-color: #f5f5f5;
      color: #222;
    }
    .dark-mode {
      background-color: #121212;
      color: #eee;
    }
    h1 {
      text-align: center;
    }
    .toggle-btn {
      display: block;
      margin: 0 auto;
      padding: 10px 20px;
      background-color: #0077b6;
      color: #fff;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
    .dark-mode .toggle-btn {
      background-color: #005f73;
    }
    canvas {
      margin: 30px auto;
      display: block;
      max-width: 700px;
    }
  </style>
</head>
<body class="light-mode">
  <h1>Mercado Potencial de Arte Personalizado - 2026</h1>
  <button class="toggle-btn" onclick="toggleMode()">Cambiar modo</button>

  <canvas id="ingresosChart"></canvas>
  <canvas id="edadChart"></canvas>
  <canvas id="mercadoChart"></canvas>
  <canvas id="ocupacionChart"></canvas>

  <script>
    let isDark = false;

    function getColors(isDark) {
      return isDark ? {
        background: ['#ffb703','#fb8500','#219ebc','#8ecae6'],
        border: '#fff'
      } : {
        background: ['#023047','#219ebc','#8ecae6','#ffb703'],
        border: '#000'
      };
    }

    // Gráfico de asalariados vs ingresos altos
    const ingresosCtx = document.getElementById('ingresosChart').getContext('2d');
    const ingresosChart = new Chart(ingresosCtx, {
      type: 'bar',
      data: {
        labels: ['Asalariados totales', 'Ingresos altos ($1,8M-$12M)'],
        datasets: [{
          label: 'Cantidad de personas',
          data: [9800000, 962474],
          backgroundColor: getColors(isDark).background[0]
        }]
      },
      options: { responsive: true, scales: { y: { beginAtZero: true } } }
    });

    // Gráfico de edad 30-60 años
    const edadCtx = document.getElementById('edadChart').getContext('2d');
    const edadChart = new Chart(edadCtx, {
      type: 'doughnut',
      data: {
        labels: ['Mujeres 30-60 años', 'Hombres 30-60 años'],
        datasets: [{
          data: [2011500, 2484000],
          backgroundColor: getColors(isDark).background,
          borderColor: getColors(isDark).border,
          borderWidth: 1
        }]
      },
      options: { responsive: true, plugins: { legend: { position: 'bottom' } } }
    });

    // Gráfico de mercado potencial
    const mercadoCtx = document.getElementById('mercadoChart').getContext('2d');
    const mercadoChart = new Chart(mercadoCtx, {
      type: 'pie',
      data: {
        labels: ['Potenciales compradores (~192.000)', 'Resto asalariados'],
        datasets: [{
          data: [192000, 9438000],
          backgroundColor: getColors(isDark).background,
          borderColor: getColors(isDark).border,
          borderWidth: 1
        }]
      },
      options: { responsive: true, plugins: { legend: { position: 'bottom' } } }
    });

    // Gráfico de ocupación principal
    const ocupacionCtx = document.getElementById('ocupacionChart').getContext('2d');
    const ocupacionChart = new Chart(ocupacionCtx, {
      type: 'bar',
      data: {
        labels: ['Comercio', 'Servicios financieros y empresariales'],
        datasets: [{
          label: 'Cantidad de personas',
          data: [1134000, 55000],
          backgroundColor: getColors(isDark).background[1]
        }]
      },
      options: { responsive: true, scales: { y: { beginAtZero: true } } }
    });

    // Alternar modo
    function toggleMode() {
      const body = document.body;
      isDark = !isDark;
      if (isDark) {
        body.classList.remove("light-mode");
        body.classList.add("dark-mode");
      } else {
        body.classList.remove("dark-mode");
        body.classList.add("light-mode");
      }
      const colors = getColors(isDark);
      ingresosChart.data.datasets[0].backgroundColor = colors.background[0];
      edadChart.data.datasets[0].backgroundColor = colors.background;
      edadChart.data.datasets[0].borderColor = colors.border;
      mercadoChart.data.datasets[0].backgroundColor = colors.background;
      mercadoChart.data.datasets[0].borderColor = colors.border;
      ocupacionChart.data.datasets[0].backgroundColor = colors.background[1];
      ingresosChart.update();
      edadChart.update();
      mercadoChart.update();
      ocupacionChart.update();
    }
  </script>
</body>
</html>
