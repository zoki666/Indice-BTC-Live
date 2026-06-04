# 📊 Índice BTC-Live

**Índice macro de Bitcoin para acumulación y distribución a largo plazo.**

Índice BTC-Live publicado en Github Pages: https://zoki666.github.io/Indice-BTC-Live/

El Índice BTC-Live combina **8 indicadores clave** (sentimiento, análisis técnico, on-chain y macro) en una puntuación única de 0 a 100.  
Cada indicador se mide de 0 a 10 con la misma lógica:

- **10 = suelo del mercado → oportunidad de compra**
- **0 = techo del mercado → señal de venta**

El índice final es un promedio ponderado que da más peso a los indicadores con mejor historial predictivo.

---

## 🧭 Interpretación rápida

| Rango | Significado | Acción recomendada |
|-------|-------------|-------------------|
| **75 – 100** | Suelo / zona de acumulación | Compras DCA, aumentar exposición |
| **26 – 74** | Neutral | Mantener posición, cautela |
| **0 – 25** | Techo / zona de distribución | Vender parcialmente, proteger capital |

---

## 🧩 Indicadores incluidos

| Letra | Indicador | Tipo | Peso | Qué mide |
|-------|-----------|------|------|----------|
| **C** | Pi Cycle Top | Técnico | 20% | Distancia al cruce de medias móviles que históricamente marcó techos |
| **F** | Fear & Greed | Sentimiento | 15% | Miedo/codicia del mercado (Alternative.me) |
| **R** | RSI 14 Diario | Técnico | 15% | Sobrecompra / sobreventa |
| **E** | EMA 200 Diaria | Técnico | 15% | Distancia del precio a la media de 200 días |
| **K** | Funding Rate | Derivados | 10% | Tasa de financiación de futuros perpetuos |
| **T** | BTC Dominance | Macro | 10% | Dominancia de Bitcoin frente al total del mercado cripto |
| **U** | USDT Dominance | Macro | 10% | Capitalización de USDT (refugio en stablecoins) |
| **V** | Volatilidad 30d | Técnico | 5% | Volatilidad histórica anualizada |

Cada indicador se calcula en tiempo real desde APIs públicas (Binance, Bybit, KuCoin, CoinGecko, CoinCap, Alternative.me) con **proveedores de respaldo** automáticos si el principal falla.

---

## 📱 Instalación como App (PWA)

La web es una **Progressive Web App** instalable en Android, iOS y escritorio.

### Requisitos
- Un servidor con HTTPS (GitHub Pages, Netlify, Vercel, etc.)
- Los tres archivos: `index.html`, `manifest.json`, `sw.js`

### Instalación rápida con GitHub Pages
1. Sube los tres archivos a un repositorio público en GitHub.
2. Ve a *Settings → Pages* y activa GitHub Pages desde la rama `main`.
3. Abre la URL `https://tuusuario.github.io/repositorio` en Chrome (móvil o escritorio).
4. Aparecerá el aviso **"Añadir a pantalla de inicio"** (o búscalo en el menú del navegador).

### Probar en local (sin instalación definitiva)
En la carpeta del proyecto, ejecuta:

    python -m http.server 8000

Luego accede desde el móvil (misma red WiFi) a `http://IP_DEL_PC:8000`.

---

## 🌗 Tema oscuro / claro

La app incluye un botón flotante (🌙/☀️) que cambia entre tema oscuro (por defecto) y claro.  
La preferencia se guarda automáticamente.

---

## 💰 Donación

Si el índice te resulta útil, puedes apoyar el proyecto:

- **On-chain:** `bc1qthc87aykdj2tjrxlqe7k9emz3txphrprm0scu6`
- **Lightning:** `ffg@cake.cash`

El botón `₿` en la esquina inferior derecha abre un modal con QR y direcciones copiables.

---

## 🔄 Actualización de datos

Los datos se refrescan automáticamente cada **15 minutos**.  
Los indicadores basados en velas diarias cambian una vez al día, pero la consulta frecuente permite detectar caídas de proveedores y usar los respaldos.

---

## 🧰 Tecnologías utilizadas

- HTML5 + CSS3 (glassmorphism, animaciones, variables CSS)
- JavaScript vanilla (fetch, async/await, cálculos de indicadores)
- Sin frameworks, sin dependencias externas
- PWA con Service Worker para caché offline

---

## ⚠️ Descargo de responsabilidad

Este índice es una **herramienta educativa** basada en datos históricos.  
**No constituye asesoramiento financiero.** El rendimiento pasado no garantiza resultados futuros. Invierte solo lo que estés dispuesto a perder.

---

## 📄 Licencia

Código abierto bajo licencia MIT.  
Creado con ❤️ para la comunidad Bitcoin.