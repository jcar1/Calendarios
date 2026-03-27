# 🎾 Circuito ITF 2026 — Planificador

Planificador de torneos ITF M15/M25 para España y países cercanos, con planificación IA personalizada.

---

## 🚀 Despliegue en Vercel (paso a paso)

### 1. Sube el código a GitHub

```bash
# En tu ordenador, dentro de esta carpeta:
git init
git add .
git commit -m "Initial commit — Circuito ITF 2026"

# Crea un repo en github.com y luego:
git remote add origin https://github.com/TU_USUARIO/circuito-itf.git
git branch -M main
git push -u origin main
```

### 2. Conecta con Vercel

1. Ve a [vercel.com](https://vercel.com) e inicia sesión con tu cuenta de GitHub
2. Pulsa **"Add New Project"**
3. Selecciona el repositorio `circuito-itf`
4. Vercel detecta automáticamente la configuración — pulsa **"Deploy"**

### 3. Añade la API key de Anthropic (IMPRESCINDIBLE)

Sin este paso la planificación IA no funcionará:

1. En el dashboard de Vercel, entra en tu proyecto
2. Ve a **Settings → Environment Variables**
3. Añade la variable:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-api03-...` (tu clave de [console.anthropic.com/keys](https://console.anthropic.com/keys))
   - **Environment:** Production (y Preview si quieres)
4. Pulsa **Save**
5. Ve a **Deployments** y haz **Redeploy** para que coja la variable

### 4. ¡Listo!

Tu planificador estará disponible en `https://circuito-itf.vercel.app` (o el dominio que Vercel asigne).

---

## 📁 Estructura del proyecto

```
circuito-itf/
├── public/
│   └── index.html        # Frontend completo (HTML + CSS + JS)
├── api/
│   └── chat.js           # Proxy serverless → Anthropic API
├── vercel.json           # Configuración de rutas Vercel
├── package.json          # Metadatos Node.js
├── .gitignore            # Excluye .env y node_modules
└── README.md             # Este archivo
```

---

## 🔒 Seguridad

- La API key de Anthropic **nunca** se expone al navegador
- El frontend llama a `/api/chat` (tu propio servidor Vercel)
- El servidor inyecta la key en la llamada a Anthropic
- Los datos del circuito se guardan en `localStorage` del navegador de cada usuario

---

## 💾 Portabilidad de datos

Los datos (circuito, torneos propios, jugador) se guardan en `localStorage`.
Para llevarlos entre dispositivos usa los botones:
- **💾 Guardar copia (.json)** — exporta todos tus datos
- **📂 Cargar copia (.json)** — importa en otro dispositivo

---

## 🛠 Desarrollo local

```bash
# Instala Vercel CLI
npm i -g vercel

# Crea .env.local con tu API key
echo "ANTHROPIC_API_KEY=sk-ant-api03-..." > .env.local

# Arranca el servidor local
vercel dev
# → Abre http://localhost:3000
```
