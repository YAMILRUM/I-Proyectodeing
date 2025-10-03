<!DOCTYPE html>
<html lang="es" data-theme>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>La Ciberseguridad — Proyecto</title>
  <meta name="description" content="Proyecto web sobre ciberseguridad con navegación dinámica, modo oscuro y componentes interactivos." />
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'><path fill='%230ea5a4' d='M32 4l22 10v14c0 14.9-9.4 28.3-22 32C19.4 56.3 10 42.9 10 28V14z'/><path fill='%23fff' d='M32 18a10 10 0 00-10 10v6a10 10 0 0020 0v-6a10 10 0 00-10-10z'/></svg>">
  <style>
    :root{
      --bg: #ffffff; --fg:#0f172a; --muted:#6b7280; --card:#f8fafc; --border:#e5e7eb; --accent:#0ea5a4; --accent-900:#0f766e; --danger:#ef4444;
      --shadow: 0 10px 25px rgba(2,6,23,.08), 0 2px 6px rgba(2,6,23,.06);
    }
    html.dark{
      --bg:#0b1020; --fg:#e5e7eb; --muted:#9ca3af; --card:#0f172a; --border:#1f2937; --accent:#14b8a6; --accent-900:#0d9488; --shadow: 0 10px 25px rgba(0,0,0,.45), 0 2px 6px rgba(0,0,0,.35);
    }
    *{box-sizing:border-box}
    body{font-family:Inter, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji"; margin:0; color:var(--fg); background:var(--bg);}
    a{color:inherit}
    .container{max-width:1100px; margin-inline:auto; padding:0 20px}

    /* Header */
    header.hero{position:relative; overflow:hidden; color:#fff;}
    .hero-bg{position:absolute; inset:0; background:radial-gradient(1200px 500px at 10% -10%, #1e293b, transparent 60%), linear-gradient(90deg, #020617, #0b1220 60%, #0e1729);}
    .hero-inner{position:relative; padding:28px 0 14px}

    /* Topbar */
    .topbar{display:flex; align-items:center; justify-content:space-between; gap:12px}
    .brand{display:flex; align-items:center; gap:10px; font-weight:700; letter-spacing:.2px}
    .brand .logo{width:36px; height:36px; display:grid; place-items:center; border-radius:10px; background:linear-gradient(135deg,#0ea5a4,#22c55e); box-shadow:var(--shadow)}
    .brand small{opacity:.85}

    .actions{display:flex; gap:8px}
    .btn{display:inline-flex; align-items:center; gap:8px; padding:8px 12px; border-radius:10px; text-decoration:none; border:1px solid transparent; cursor:pointer; font-weight:600}
    .btn.primary{background:var(--accent); color:#fff}
    .btn.primary:hover{background:var(--accent-900)}
    .btn.ghost{background:transparent; color:#fff; border-color:rgba(255,255,255,.15)}
    .btn.ghost:hover{background:rgba(255,255,255,.08)}

    /* Nav */
    nav.navbar{margin-top:16px; background:rgba(255,255,255,.08); border:1px solid rgba(255,255,255,.15); backdrop-filter: blur(8px); border-radius:14px}
    .nav-ul{display:flex; flex-wrap:wrap; gap:6px; list-style:none; padding:8px; margin:0}
    .nav-a{color:#fff; text-decoration:none; padding:8px 10px; border-radius:10px; display:inline-flex; gap:8px; align-items:center}
    .nav-a[aria-current="page"], .nav-a:hover{background:rgba(255,255,255,.14)}

    /* Layout */
    main{padding:22px 0}
    .layout{display:grid; grid-template-columns:1fr 320px; gap:20px}
    @media (max-width: 980px){.layout{grid-template-columns:1fr}}

    .card{background:var(--card); border:1px solid var(--border); border-radius:14px; box-shadow:var(--shadow)}
    .section{padding:18px}
    .section h1, .section h2{margin:0 0 10px}
    .meta{color:var(--muted); font-size:.95rem}

    aside.aside{position:sticky; top:18px; height:fit-content}
    .aside .section ul{margin:0; padding-left:18px}

    /* Table */
    table{width:100%; border-collapse:collapse}
    th, td{padding:10px 10px; border-bottom:1px solid var(--border); text-align:left}
    thead th{position:sticky; top:0; background:var(--card); z-index:1}
    .table-wrap{overflow:auto; border:1px solid var(--border); border-radius:12px}
    .table-toolbar{display:flex; gap:10px; align-items:center; margin-bottom:10px}
    .input{padding:8px 10px; border:1px solid var(--border); border-radius:10px; background:transparent; color:inherit}

    /* Footer */
    footer{padding:22px 0; color:var(--muted); text-align:center}

    /* Chips & badges */
    .chip{display:inline-flex; align-items:center; gap:6px; padding:6px 10px; border-radius:999px; background:rgba(14,165,164,.12); color:var(--accent); border:1px solid rgba(14,165,164,.25); font-weight:600}

    /* Utilities */
    .row{display:flex; gap:12px; flex-wrap:wrap}
    .muted{color:var(--muted)}
    .sr-only{position:absolute; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0,0,0,0); white-space:nowrap; border:0}
  </style>
</head>
<body>
  <header class="hero">
    <div class="hero-bg" aria-hidden="true"></div>
    <div class="container hero-inner">
      <div class="topbar">
        <div class="brand">
          <span class="logo" aria-hidden="true">🔐</span>
          <div>
            <div>La Ciberseguridad</div>
            <small class="muted">Universidad Iberoamericana Puebla · ISC</small>
          </div>
        </div>
        <div class="actions">
          <button class="btn ghost" id="btnToggleTheme" title="Cambiar tema">🌓 <span class="hide-sm">Tema</span></button>
          <a class="btn primary" href="#/bibliografia">Ver bibliografía</a>
        </div>
      </div>

      <nav class="navbar">
        <ul class="nav-ul" role="tablist">
          <li><a class="nav-a" data-link href="#/portada">Portada</a></li>
          <li><a class="nav-a" data-link href="#/importancia">Importancia</a></li>
          <li><a class="nav-a" data-link href="#/objetivo">Objetivo</a></li>
          <li><a class="nav-a" data-link href="#/tipos">Tipos de virus</a></li>
          <li><a class="nav-a" data-link href="#/bibliografia">Bibliografía</a></li>
        </ul>
      </nav>
    </div>
  </header>

  <div class="container">
    <div class="layout">
      <main id="app" class="card section" aria-live="polite">
        <!-- El enrutador cargará aquí la página -->
      </main>

    </div>
  </div>

  <footer>
    <div class="container muted">Proyecto académico · Última edición: 30/sep/2025</div>
  </footer>

  <template id="page-portada">
    <section class="section">
      <h1>Portada</h1>
      <p class="meta">Periodo de evaluación: Primer periodo · Fecha: 19 de septiembre de 2025</p>
      <div class="card section" style="margin-top:10px">
        <div class="row">
          <span class="chip">Universidad Iberoamericana Puebla</span>
          <span class="chip">Departamento: Ingeniería en Sistemas Computacionales</span>
        </div>
        <p><strong>Equipo:</strong> Fernando José Axle Ricardez; Rodrigo Castro Bermeo; Yamil Rumilla Curiel; Erick Vázquez Juárez.</p>
      </div>
      <p class="muted">Usa el menú superior para navegar entre las secciones.</p>
    </section>
  </template>

  <template id="page-importancia">
    <section class="section">
      <h1>La importancia de la ciberseguridad</h1>
      <p class="meta">Contexto 2024–2025 · México</p>
      <article>
        <p>Hoy en día muchas personas desconocen los peligros que abundan en Internet y el mundo del <em>hacking</em>. Explorar sus áreas, causas y consecuencias es clave para entender su importancia.</p>
        <p>En México, durante 2024 y el primer trimestre de 2025, la población y las empresas han enfrentado un aumento acelerado de ciberataques de diferentes tipos. En el primer trimestre de 2025, <strong>13.5 millones de usuarios</strong> fueron afectados por <em>malware</em> e intentos de <em>phishing</em>, un alza marcada respecto a 2024. Entre las causas destacan el desconocimiento de los riesgos y vulnerabilidades presentes en redes sociales, páginas web y <em>spam</em>, así como prácticas poco seguras, especialmente en población vulnerable.</p>
        <h2>Consecuencias</h2>
        <p>El incremento de la distribución de <em>malware</em> y estafas como el <em>phishing</em> afecta a más personas cada día: infecciones, filtración de información sensible y pérdidas económicas, entre otras. Tanto individuos como empresas pueden verse afectados si no adoptan medidas de prevención.</p>
        <h2>Relevancia</h2>
        <p>El aumento de ciberataques representa una amenaza directa para ciudadanía y organizaciones: compromete información personal, económica y de seguridad. Esta investigación busca generar conciencia y promover prácticas seguras para fortalecer la cultura digital preventiva. Se apoya en estadísticas recientes y marcos normativos, beneficiando a quienes navegan por Internet y a instituciones que desean reducir riesgos.</p>
      </article>
    </section>
  </template>

  <template id="page-objetivo">
    <section class="section">
      <h1>Objetivo general</h1>
      <p>Fortalecer la cultura de ciberseguridad en usuarios y empresas en México mediante estrategias de concienciación y difusión de prácticas seguras para reducir la incidencia e impacto de ciberataques durante 2025.</p>
      <div class="card section" aria-label="Presentación Canva embebida">
        <div style="position: relative; width: 100%; padding-top: 56.25%; border-radius:12px; overflow:hidden; border:1px solid var(--border)">
          <iframe loading="lazy" title="Objetivos — Canva" style="position:absolute; inset:0; width:100%; height:100%; border:0" src="https://www.canva.com/design/DAGxd_U-OYE/QQsiGgDqwoynG8y1DaAwPQ/view?embed" allowfullscreen></iframe>
        </div>
      </div>
      <h2>Objetivos específicos (SMART)</h2>
      <ul>
        <li>Desarrollar y difundir concientización sobre <em>phishing</em> y <em>malware</em> dirigida a adolescentes, adultos jóvenes y adultos mayores antes de diciembre de 2025.</li>
        <li>Informar sobre buenas prácticas básicas (antivirus, respaldos, verificación de correos) durante el segundo semestre de 2025.</li>
        <li>Que cada persona usuaria reconozca señales básicas para identificar virus/engaños.</li>
      </ul>
      <h3>Indicadores</h3>
      <div class="card section">
        <p><strong>Indicador 1:</strong> % de usuarios capacitados en ciberseguridad.</p>
        <p><b>Fórmula:</b> (Usuarios informados ÷ Total de usuarios que vieron la página) × 100</p>
        <p><b>Línea base:</b> 0 % (2024, sin registros previos)</p>
        <p><b>Meta:</b> 40 % al cierre de 2025</p>
        <p><b>Fuente:</b> Reportes internos de talleres y campañas digitales</p>
        <hr style="border:none;border-top:1px solid var(--border)">
        <p><strong>Indicador 2:</strong> Reducción de incidentes de <em>phishing</em> en población capacitada.</p>
        <p><b>Fórmula:</b> (Incidentes reportados por informados ÷ Total de incidentes iniciales) × 100</p>
        <p><b>Línea base:</b> 13.5 millones de víctimas en T1 2025</p>
        <p><b>Meta:</b> Reducir 1 % en población capacitada al cierre de 2025</p>
      </div>
    </section>
  </template>

  <template id="page-tipos">
    <section class="section">
      <h1>Tipos de virus</h1>
      <div class="table-toolbar">
        <input id="filter" class="input" placeholder="Filtrar por nombre o año…" aria-label="Filtrar tabla" />
        <button class="btn ghost" id="btnSort">↕︎ Ordenar por año</button>
      </div>
      <div class="table-wrap">
        <table id="virusTable">
          <thead>
            <tr>
              <th>Nombre</th>
              <th data-key="anio">Año de aparición/detección en México</th>
              <th>Propagación</th>
              <th>Impacto en México</th>
              <th>Prevención / Respuesta</th>
            </tr>
          </thead>
          <tbody>
            <tr><td>ILOVEYOU</td><td>2000</td><td>Correo electrónico con adjunto (.vbs)</td><td>Afectó dependencias y empresas; caídas de sistemas.</td><td>Antivirus actualizado, no abrir adjuntos sospechosos.</td></tr>
            <tr><td>Klez</td><td>2001–2003</td><td>Correos con adjuntos maliciosos</td><td>Amplia difusión; saturaba buzones y dañaba archivos.</td><td>Filtros de correo, parches y antivirus.</td></tr>
            <tr><td>Conficker</td><td>2008–2010</td><td>Redes locales y dispositivos USB</td><td>Infecciones en instituciones públicas; riesgo de datos.</td><td>Actualizar Windows, desinfección en red.</td></tr>
            <tr><td>Stuxnet</td><td>2010</td><td>USB y redes industriales (SCADA)</td><td>Detectado en sistemas industriales; alerta sobre infraestructura crítica.</td><td>Segmentación de redes, ciberseguridad industrial.</td></tr>
            <tr><td>WannaCry</td><td>2017</td><td>Ransomware vía SMB de Windows</td><td>Afectó a varias empresas; secuestro de información.</td><td>Backups, actualización y parches.</td></tr>
            <tr><td>FluBot / SMS malware</td><td>2021</td><td>Mensajes SMS con enlaces fraudulentos</td><td>Robo de datos bancarios a usuarios.</td><td>Educación digital, filtros SMS, apps verificadas.</td></tr>
          </tbody>
        </table>
      </div>
      <p class="muted" style="margin-top:10px">Tip: Usa el filtro para encontrar rápido un caso.</p>
    </section>
  </template>

  <template id="page-bibliografia">
    <section class="section">
      <h1>Bibliografía</h1>
      <p>Incluye todas las fuentes en formato APA.</p>
      <ol>
        <li>Autor, A. A. (2025). <em>Título del artículo o informe</em>. Editorial/Entidad. URL</li>
        <li>Persona, B. B. (2024). <em>Buenas prácticas de ciberseguridad</em>. Revista/Portal. URL</li>
      </ol>
      <p class="muted">Sugerencia: añade reportes de CERT-MX, ENISA, CISA y artículos revisados por pares.</p>
    </section>
  </template>

  <script>
    // ——— Tema (claro/oscuro) con persistencia ———
    (function(){
      const root = document.documentElement;
      const saved = localStorage.getItem('theme');
      if(saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)){
        root.classList.add('dark');
      }
      document.getElementById('btnToggleTheme').addEventListener('click',()=>{
        root.classList.toggle('dark');
        localStorage.setItem('theme', root.classList.contains('dark') ? 'dark' : 'light');
      });
    })();

    // ——— Router mínimo (hash) ———
    const routes = {
      '/portada': document.getElementById('page-portada').innerHTML,
      '/importancia': document.getElementById('page-importancia').innerHTML,
      '/objetivo': document.getElementById('page-objetivo').innerHTML,
      '/tipos': document.getElementById('page-tipos').innerHTML,
      '/bibliografia': document.getElementById('page-bibliografia').innerHTML,
    };

    function render(){
      const app = document.getElementById('app');
      const path = (location.hash.replace('#','') || '/portada');
      app.innerHTML = routes[path] || routes['/portada'];
      // marcar enlace activo
      document.querySelectorAll('[data-link]').forEach(a=>{
        const target = a.getAttribute('href').replace('#','');
        a.setAttribute('aria-current', target===path ? 'page' : 'false');
      });
      // inicializar scripts por página
      if(path === '/tipos') initTiposPage();
      // scroll al inicio
      window.scrollTo({top:0, behavior:'smooth'});
    }
    window.addEventListener('hashchange', render);
    window.addEventListener('DOMContentLoaded', render);

    // ——— Tabla: filtro + orden ———
    function initTiposPage(){
      const input = document.getElementById('filter');
      const btnSort = document.getElementById('btnSort');
      const table = document.getElementById('virusTable');
      if(!table) return;
      const rows = Array.from(table.tBodies[0].rows);

      input?.addEventListener('input', () => {
        const q = input.value.toLowerCase();
        rows.forEach(tr => {
          const text = tr.innerText.toLowerCase();
          tr.style.display = text.includes(q) ? '' : 'none';
        });
      });

      let asc = true;
      btnSort?.addEventListener('click', () => {
        const parseYear = (val) => {
          const m = String(val).match(/\d{4}/);
          return m ? parseInt(m[0],10) : 0;
        };
        const sorted = rows.sort((a,b)=> asc
          ? parseYear(a.cells[1].innerText) - parseYear(b.cells[1].innerText)
          : parseYear(b.cells[1].innerText) - parseYear(a.cells[1].innerText)
        );
        const tbody = table.tBodies[0];
        tbody.innerHTML = '';
        sorted.forEach(tr=>tbody.appendChild(tr));
        asc = !asc;
      });
    }

    // ——— Imprimir contenido principal ———
    document.getElementById('btnPrint').addEventListener('click', () => {
      window.print();
    });
  </script>
</body>
</html>
