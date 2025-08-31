# Becker\&Barrientos – Sitio + Backend IA

A continuación tienes **todos los archivos** listos para que publiques el frontend en **GitHub Pages** y el backend (proxy de Gemini) en **Vercel** (o Render/Fly). Incluye manejo de errores, seguridad básica, y UI mejorada.

---

## 1) `/frontend/index.html`

> **Frontend estático** listo para GitHub Pages. Llama a tu backend con `POST /api/ideas`.

```html
<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Becker&Barrientos - Soluciones en Construcción</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest"></script>
  <style>
    body { font-family: 'Inter', sans-serif; }
    .loader { border: 4px solid #f3f3f3; border-top: 4px solid #F58220; border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; }
    @keyframes spin { 0% { transform: rotate(0deg);} 100% { transform: rotate(360deg);} }
  </style>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            'brand-blue': '#005A9C',
            'brand-orange': '#F58220',
          }
        }
      }
    }
  </script>
</head>
<body class="bg-gray-50">
  <!-- Modal -->
  <div id="notification-modal" class="fixed inset-0 bg-black/50 z-50 hidden items-center justify-center">
    <div class="bg-white rounded-2xl p-8 shadow-xl w-full max-w-md text-center">
      <div id="modal-content"></div>
      <button id="close-modal-btn" class="mt-6 bg-brand-blue text-white font-bold py-2 px-6 rounded-lg hover:bg-blue-800">Cerrar</button>
    </div>
  </div>

  <!-- Header -->
  <header class="bg-white/80 backdrop-blur-sm sticky top-0 z-40 shadow-md">
    <div class="container mx-auto px-6 py-3">
      <div class="flex justify-between items-center">
        <a href="#inicio" class="flex items-center space-x-2">
          <svg class="h-10 w-10 text-brand-blue" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M2 20h20v2H2v-2zM4 18h2V8.66l6-3.6 6 3.6V18h2V7l-8-4.8L4 7v11z"/></svg>
          <span class="text-2xl font-extrabold text-gray-800">Becker<span class="text-brand-orange">&</span>Barrientos</span>
        </a>
        <nav class="hidden md:flex space-x-8">
          <a href="#servicios" class="text-gray-600 hover:text-brand-orange font-medium">Servicios</a>
          <a href="#proyectos" class="text-gray-600 hover:text-brand-orange font-medium">Proyectos</a>
          <a href="#nosotros" class="text-gray-600 hover:text-brand-orange font-medium">Nosotros</a>
          <a href="#asistente-ia" class="text-gray-600 hover:text-brand-orange font-medium">✨ Asistente IA</a>
          <a href="#contacto" class="text-gray-600 hover:text-brand-orange font-medium">Contacto</a>
        </nav>
        <button id="mobile-menu-button" class="md:hidden p-2 rounded-md text-gray-600 hover:bg-gray-100">
          <i data-lucide="menu" class="h-6 w-6"></i>
        </button>
      </div>
    </div>
    <div id="mobile-menu" class="hidden md:hidden bg-white shadow-lg">
      <a href="#servicios" class="block py-3 px-6 text-gray-700 hover:bg-gray-100 font-medium">Servicios</a>
      <a href="#proyectos" class="block py-3 px-6 text-gray-700 hover:bg-gray-100 font-medium">Proyectos</a>
      <a href="#nosotros" class="block py-3 px-6 text-gray-700 hover:bg-gray-100 font-medium">Nosotros</a>
      <a href="#asistente-ia" class="block py-3 px-6 text-gray-700 hover:bg-gray-100 font-medium">✨ Asistente IA</a>
      <a href="#contacto" class="block py-3 px-6 text-gray-700 hover:bg-gray-100 font-medium">Contacto</a>
    </div>
  </header>

  <main>
    <!-- Hero -->
    <section id="inicio" class="bg-white">
      <div class="container mx-auto px-6 py-24 md:py-32 text-center">
        <h1 class="text-4xl md:text-6xl font-extrabold text-gray-900 leading-tight mb-4">
          Construimos tus ideas, <span class="text-brand-blue">creamos tu futuro.</span>
        </h1>
        <p class="max-w-3xl mx-auto text-lg md:text-xl text-gray-600 mb-8">
          Soluciones confiables en estructuras metálicas, obras de cemento y carpintería. Calidad y cercanía en cada paso.
        </p>
        <a href="#contacto" class="bg-brand-orange hover:bg-orange-600 text-white font-bold py-3 px-8 rounded-lg text-lg transition-transform hover:scale-105 inline-block">
          Cotiza tu Proyecto
        </a>
      </div>
    </section>

    <!-- Servicios -->
    <section id="servicios" class="py-20">
      <div class="container mx-auto px-6 text-center">
        <h2 class="text-3xl font-bold text-gray-800 mb-2">Nuestros Servicios</h2>
        <p class="text-lg text-gray-500 mb-8">Soluciones integrales para tu hogar o empresa.</p>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-2xl transition hover:-translate-y-2">
            <i data-lucide="factory" class="h-10 w-10 text-brand-blue mx-auto mb-4"></i>
            <h3 class="text-xl font-bold text-gray-800 mb-3">Estructuras Metálicas</h3>
            <p class="text-gray-600">Soldadura certificada para galpones, techumbres y ampliaciones.</p>
          </div>
          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-2xl transition hover:-translate-y-2">
            <i data-lucide="square" class="h-10 w-10 text-brand-blue mx-auto mb-4"></i>
            <h3 class="text-xl font-bold text-gray-800 mb-3">Obras de Cemento</h3>
            <p class="text-gray-600">Radiers, muros y fundaciones con terminaciones profesionales.</p>
          </div>
          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-2xl transition hover:-translate-y-2">
            <i data-lucide="ruler" class="h-10 w-10 text-brand-blue mx-auto mb-4"></i>
            <h3 class="text-xl font-bold text-gray-800 mb-3">Carpintería a Medida</h3>
            <p class="text-gray-600">Muebles, revestimientos y soluciones de madera a medida.</p>
          </div>
          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-2xl transition hover:-translate-y-2">
            <i data-lucide="shield" class="h-10 w-10 text-brand-blue mx-auto mb-4"></i>
            <h3 class="text-xl font-bold text-gray-800 mb-3">Cercos y Rejas</h3>
            <p class="text-gray-600">Seguridad con estilo para tu propiedad.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Proyectos (galería simple) -->
    <section id="proyectos" class="py-20 bg-white">
      <div class="container mx-auto px-6 text-center">
        <h2 class="text-3xl font-bold text-gray-800 mb-2">Proyectos Destacados</h2>
        <p class="text-lg text-gray-500 mb-8">Nuestro trabajo habla por nosotros.</p>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div class="rounded-lg overflow-hidden shadow-lg group"><img src="https://images.unsplash.com/photo-1596328330544-7df7f7dc4e0b?q=80&w=800&auto=format&fit=crop" alt="Estructura metálica" class="w-full h-56 object-cover group-hover:scale-110 transition"/></div>
          <div class="rounded-lg overflow-hidden shadow-lg group"><img src="https://images.unsplash.com/photo-1566616213899-2a4a7b74127c?q=80&w=800&auto=format&fit=crop" alt="Cerco metálico" class="w-full h-56 object-cover group-hover:scale-110 transition"/></div>
          <div class="rounded-lg overflow-hidden shadow-lg group"><img src="https://images.unsplash.com/photo-1541888946425-d81bb19240f5?q=80&w=800&auto=format&fit=crop" alt="Radier" class="w-full h-56 object-cover group-hover:scale-110 transition"/></div>
        </div>
      </div>
    </section>

    <!-- Nosotros -->
    <section id="nosotros" class="py-20">
      <div class="container mx-auto px-6">
        <div class="flex flex-col md:flex-row items-center gap-12">
          <div class="md:w-1/2"><img src="https://images.unsplash.com/photo-1581092580497-c2d22c6c9c34?q=80&w=800&auto=format&fit=crop" alt="Equipo" class="rounded-xl shadow-2xl w-full"/></div>
          <div class="md:w-1/2">
            <h2 class="text-3xl font-bold text-gray-800 mb-4">Sobre Becker&Barrientos</h2>
            <p class="text-gray-600 leading-relaxed mb-8">Pasión por construir con calidad y cumplir lo prometido. Soluciones duraderas para familias y pymes.</p>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-6 text-center">
              <div class="p-4 rounded-lg hover:bg-gray-100"><i data-lucide="badge-check" class="h-8 w-8 text-brand-blue mx-auto mb-2"></i><h4 class="font-bold text-brand-blue">Profesionalismo</h4><p class="text-gray-600 text-sm">Plazos, presupuesto y calidad.</p></div>
              <div class="p-4 rounded-lg hover:bg-gray-100"><i data-lucide="handshake" class="h-8 w-8 text-brand-blue mx-auto mb-2"></i><h4 class="font-bold text-brand-blue">Cercanía</h4><p class="text-gray-600 text-sm">Comunicación directa y transparente.</p></div>
              <div class="p-4 rounded-lg hover:bg-gray-100"><i data-lucide="lightbulb" class="h-8 w-8 text-brand-blue mx-auto mb-2"></i><h4 class="font-bold text-brand-blue">Creatividad</h4><p class="text-gray-600 text-sm">Soluciones ingeniosas.</p></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Asistente IA -->
    <section id="asistente-ia" class="py-20 bg-gray-100">
      <div class="container mx-auto px-6 text-center">
        <h2 class="text-3xl font-bold text-gray-800 mb-2">✨ Asistente de Proyectos IA</h2>
        <p class="text-lg text-gray-500 mb-8 max-w-2xl mx-auto">Describe tu necesidad y te sugerimos ideas constructivas que podemos ejecutar.</p>
        <div class="max-w-2xl mx-auto bg-white p-8 rounded-xl shadow-lg">
          <textarea id="ai-prompt-input" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-brand-blue outline-none" placeholder="Ej: 'Patio de tierra se inunda. Quiero un espacio para mesa y quincho.'"></textarea>
          <button id="generate-ideas-btn" class="mt-4 bg-brand-orange hover:bg-orange-600 text-white font-bold py-3 px-8 rounded-lg">Generar Ideas</button>
          <div id="ai-results-container" class="mt-8 text-left grid grid-cols-1 md:grid-cols-2 gap-6"></div>
        </div>
      </div>
    </section>

    <!-- Contacto -->
    <section id="contacto" class="py-20 bg-white">
      <div class="container mx-auto px-6">
        <div class="max-w-3xl mx-auto text-center">
          <h2 class="text-3xl font-bold text-gray-800 mb-2">¿Tienes un proyecto?</h2>
          <p class="text-lg text-gray-500 mb-8">Completa el formulario y te contactamos.</p>
        </div>
        <div class="max-w-2xl mx-auto mt-8 bg-gray-50 p-8 rounded-xl shadow-lg">
          <form onsubmit="event.preventDefault(); showModal('Gracias, te contactaremos a la brevedad.'); this.reset();">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
              <div>
                <label class="block text-gray-700 font-medium mb-2">Nombre</label>
                <input type="text" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-brand-blue outline-none" required />
              </div>
              <div>
                <label class="block text-gray-700 font-medium mb-2">Email</label>
                <input type="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-brand-blue outline-none" required />
              </div>
            </div>
            <div class="mb-6">
              <label class="block text-gray-700 font-medium mb-2">Tipo de Servicio</label>
              <select class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-brand-blue outline-none bg-white">
                <option>Estructuras Metálicas</option>
                <option>Obras de Cemento</option>
                <option>Carpintería</option>
                <option>Cercos y Rejas</option>
                <option>Otro</option>
              </select>
            </div>
            <div class="mb-6">
              <label class="block text-gray-700 font-medium mb-2">Mensaje</label>
              <textarea rows="5" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-brand-blue outline-none" required></textarea>
            </div>
            <div class="text-center">
              <button type="submit" class="bg-brand-orange hover:bg-orange-600 text-white font-bold py-3 px-12 rounded-lg">Enviar</button>
            </div>
          </form>
        </div>
      </div>
    </section>
  </main>

  <footer class="bg-gray-800 text-white">
    <div class="container mx-auto px-6 py-8 flex flex-col md:flex-row justify-between items-center text-center md:text-left">
      <div class="mb-4 md:mb-0">
        <h3 class="text-xl font-bold">Becker&Barrientos</h3>
        <p class="text-gray-400">Construyendo calidad y confianza.</p>
      </div>
      <div class="text-gray-400">
        <p>&copy; 2025 Becker&Barrientos. Todos los derechos reservados.</p>
      </div>
    </div>
  </footer>

  <script>
    lucide.createIcons();

    const mobileMenuButton = document.getElementById('mobile-menu-button');
    const mobileMenu = document.getElementById('mobile-menu');
    const modal = document.getElementById('notification-modal');
    const modalContent = document.getElementById('modal-content');
    const closeModalBtn = document.getElementById('close-modal-btn');

    mobileMenuButton.addEventListener('click', () => mobileMenu.classList.toggle('hidden'));
    mobileMenu.querySelectorAll('a').forEach(a => a.addEventListener('click', () => mobileMenu.classList.add('hidden')));
    closeModalBtn.addEventListener('click', () => modal.classList.add('hidden'));

    function showModal(title, message, isError = false) {
      modalContent.innerHTML = `
        <h3 class="text-2xl font-bold ${isError ? 'text-red-600' : 'text-brand-blue'} mb-4">${title}</h3>
        <div class="text-gray-600">${message}</div>`;
      modal.classList.remove('hidden');
    }

    // Asistente IA via backend /api/ideas
    const generateBtn = document.getElementById('generate-ideas-btn');
    const promptInput = document.getElementById('ai-prompt-input');
    const resultsContainer = document.getElementById('ai-results-container');

    generateBtn.addEventListener('click', async () => {
      const userPrompt = (promptInput.value || '').trim();
      if (!userPrompt) return showModal('Error', 'Por favor, describe tu idea o necesidad.', true);

      resultsContainer.innerHTML = '<div class="loader col-span-full mx-auto"></div>';
      generateBtn.disabled = true; generateBtn.textContent = 'Generando...';

      try {
        const response = await fetch('/api/ideas', {
          method: 'POST', headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ input: userPrompt })
        });

        if (!response.ok) throw new Error('No se pudo generar ideas');
        const { text } = await response.json();
        displayResults(text);
      } catch (e) {
        console.error(e);
        showModal('Sin conexión con IA', 'Intenta más tarde o contáctanos directo 📞.', true);
        resultsContainer.innerHTML = '<p class="text-red-500 col-span-full">No se pudieron generar ideas.</p>';
      } finally {
        generateBtn.disabled = false; generateBtn.textContent = 'Generar Ideas';
      }
    });

    function displayResults(text) {
      resultsContainer.innerHTML = '';
      const ideas = (text || '').split('---').map(t => t.trim()).filter(Boolean);

      ideas.forEach(ideaText => {
        const lines = ideaText.split('\n').map(l => l.trim()).filter(Boolean);
        const titleLine = lines.find(l => l.startsWith('###')) || '### Idea de Proyecto';
        const title = titleLine.replace('###', '').trim();
        const serviceLine = lines.find(l => l.startsWith('**')) || '';
        const service = serviceLine.replace('**', '').replace('Servicio B&B Relacionado:', '').trim() || 'Servicio General';
        const description = lines.filter(l => !l.startsWith('###') && !l.startsWith('**')).join(' ');

        const card = document.createElement('div');
        card.className = 'bg-white p-6 rounded-xl shadow-lg border-l-4 border-brand-orange';
        card.innerHTML = `
          <h3 class="text-2xl font-bold text-brand-blue mb-3">${title}</h3>
          <p class="text-gray-600 mb-4">${description}</p>
          <div class="bg-blue-100 text-brand-blue text-sm font-semibold px-3 py-1 rounded-full inline-flex items-center gap-2">
            <i data-lucide="briefcase" class="h-4 w-4"></i>${service}
          </div>`;
        resultsContainer.appendChild(card);
      });
      lucide.createIcons();
    }
  </script>
</body>
</html>
```

---

## 2) `/backend/server.js`

> **Servidor Express** que actúa como **proxy seguro** a Gemini. Lee `GEMINI_API_KEY` desde variables de entorno. Incluye rate limit, CORS y sanitización básica.

```js
// server.js
import express from 'express';
import cors from 'cors';
import rateLimit from 'express-rate-limit';

const app = express();
app.use(express.json({ limit: '1mb' }));
app.use(cors());

const limiter = rateLimit({ windowMs: 60 * 1000, max: 30 });
app.use('/api/', limiter);

const MODEL = 'gemini-2.0-flash';
const API_KEY = process.env.GEMINI_API_KEY;

function sanitize(text = '') {
  return String(text).slice(0, 1200); // corta prompts muy largos
}

const SYSTEM_PROMPT = `
Eres un asistente experto y amigable de la constructora 'Becker&Barrientos'.
Especialidades: Estructuras Metálicas, Obras de Cemento, Carpintería a Medida, Cercos y Rejas.
Un cliente describirá una necesidad. Propondrás 1 o 2 ideas que podamos construir.
Formato por idea:
1) Título con '###'.
2) 2–3 frases de descripción (beneficios y solución).
3) Línea '**Servicio B&B Relacionado: <uno de las especialidades>**'.
Responde solo con ese formato. Separa ideas con '---'.
`;

app.post('/api/ideas', async (req, res) => {
  try {
    if (!API_KEY) return res.status(500).json({ error: 'Falta GEMINI_API_KEY' });
    const userInput = sanitize(req.body?.input || '');
    if (!userInput) return res.status(400).json({ error: 'input requerido' });

    const payload = {
      contents: [
        { role: 'user', parts: [{ text: userInput }] }
      ],
      systemInstruction: { role: 'system', parts: [{ text: SYSTEM_PROMPT }] }
    };

    const url = `https://generativelanguage.googleapis.com/v1beta/models/${MODEL}:generateContent?key=${API_KEY}`;
    const r = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload)
    });

    if (!r.ok) {
      const t = await r.text();
      return res.status(502).json({ error: 'IA no disponible', details: t.slice(0, 200) });
    }

    const data = await r.json();
    const text = data?.candidates?.[0]?.content?.parts?.[0]?.text || '';
    return res.json({ text });
  } catch (e) {
    console.error(e);
    return res.status(500).json({ error: 'Error interno' });
  }
});

// Healthcheck
app.get('/api/health', (_, res) => res.json({ ok: true }));

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`BYB backend listo en :${PORT}`));
```

---

## 3) `/backend/package.json`

```json
{
  "name": "byb-backend",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.19.2",
    "express-rate-limit": "^7.3.0"
  },
  "engines": { "node": ">=18" }
}
```

---

## 4) `/backend/.env.example`

```bash
# Renombra este archivo a .env y coloca tu API Key real
GEMINI_API_KEY=tu_api_key_de_gemini
```

---

## 5) `/backend/vercel.json` (opcional, para desplegar fácil)

> Con esto Vercel expondrá `/api/*` en tu dominio del backend y ejecutará `server.js`.

```json
{
  "version": 2,
  "builds": [
    { "src": "server.js", "use": "@vercel/node" }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/server.js" }
  ]
}
```

---

## 6) Cómo publicarlo (paso a paso)

### Frontend en GitHub Pages

1. Crea repo `byb-site` y sube el contenido de `/frontend`.
2. En GitHub → *Settings* → *Pages* → *Build and deployment*: selecciona la rama (por ejemplo `main`) y carpeta `/ (root)` si subes `index.html` en la raíz del repo.
3. Obtendrás una URL tipo: `https://tuusuario.github.io/byb-site/`.

### Backend en Vercel

1. Crea repo `byb-backend` con los archivos de `/backend`.
2. En Vercel, **Import Project** desde GitHub.
3. En *Settings* → *Environment Variables*: agrega `GEMINI_API_KEY`.
4. Deploy.
5. Te dará una URL tipo `https://byb-backend.vercel.app`.

### Conectar Frontend y Backend

* En `index.html`, la llamada es `fetch('/api/ideas', ...)`.
* Si sirves frontend desde GitHub Pages, reemplaza por **ruta absoluta** a tu backend:

  * Busca en `index.html` esta línea dentro del `fetch`:

    ```js
    const response = await fetch('/api/ideas', {
    ```
  * **Cámbiala** a:

    ```js
    const response = await fetch('https://byb-backend.vercel.app/api/ideas', {
    ```
* Alternativa: si hosteas frontend y backend en el **mismo dominio** (por ejemplo en Vercel con monorepo), puedes dejar `/api/ideas`.

---

## 7) Test rápido

* Backend: `curl https://byb-backend.vercel.app/api/health` → debe responder `{ ok: true }`.
* Frontend: abre tu GitHub Pages, escribe un prompt y debería traer ideas en cards.

---

## 8) Hardening recomendado

* **CORS**: en producción, limita a tu dominio: `app.use(cors({ origin: 'https://tuusuario.github.io' }))`.
* **Logs**: agrega un logger como `morgan` si necesitas trazabilidad.
* **Rate limit**: ajusta `max` según tráfico.
* **Validaciones**: añade verificación de lenguaje ofensivo si te preocupa moderación.

---

## 9) Nota de marca

* Mantengo los colores `#005A9C` (azul) y `#F58220` (naranja) y el look & feel corporativo.
* El Asistente IA ahora entrega errores humanizados, loader y cards con íconos.

---

¿Necesitas que lo prepare como **monorepo** (frontend + backend juntos) para desplegar todo en Vercel con un solo click? Lo puedo versionar aquí mismo.
