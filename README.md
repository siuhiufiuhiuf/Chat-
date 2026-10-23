# Conecta — Chat comunitario

Página web para GitHub Pages con:
- Entrada con nombre/apodo.
- Lista de personas conectadas.
- Chat compartido entre dispositivos usando Firebase Realtime Database.
- Límite de 1 mensaje cada 30 segundos por pestaña/sesión.
- Filtro básico de vocabulario ofensivo y obsceno.
- Diseño adaptable a celulares y computadores.

## Importante
GitHub Pages solo publica archivos estáticos; **no guarda ni sincroniza por sí solo los mensajes**. Este proyecto usa Firebase para compartir el chat. El filtro de palabras y el temporizador del navegador son una primera barrera, no una protección infalible: para un chat público real debes reforzar límites y moderación en el servidor y no publicar reglas abiertas.

## Configuración sencilla de Firebase

1. Entra a https://console.firebase.google.com/ e inicia sesión.
2. Crea un proyecto.
3. En **Build / Authentication**, abre **Sign-in method** y activa **Anonymous**.
4. En **Build / Realtime Database**, crea una base de datos.
5. Copia la URL de la base de datos que te da Firebase.
6. En la configuración del proyecto, agrega una aplicación web (`</>`) y copia su configuración.
7. Abre `index.html` y reemplaza los valores `PEGA_AQUI...` del objeto `firebaseConfig` por los valores reales.
   - `databaseURL` debe ser la URL exacta que Firebase te dio.
8. En Realtime Database > **Rules**, usa reglas de prueba solo para comprobarlo y no dejes una base de datos pública abierta. Reglas sugeridas para un prototipo con autenticación anónima:

```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

Estas reglas permiten que cualquier persona que se autentique anónimamente pueda leer/escribir en toda la base de datos. **No son adecuadas para un chat público definitivo**: pueden permitir spam o borrar datos. Para publicarlo para muchas personas, lo correcto es validar mensajes y el límite de 30 segundos con reglas/servidor más estrictos. No compartas datos privados en el chat.

## Publicar en GitHub Pages

1. Crea un repositorio en https://github.com/ .
2. Sube `index.html` y `README.md` a la raíz del repositorio.
3. Abre **Settings > Pages**.
4. En **Build and deployment**, elige **Deploy from a branch**.
5. Selecciona la rama `main` y la carpeta `/ (root)`, guarda.
6. Espera a que GitHub Pages publique el sitio y abre la URL que aparece en esa misma sección.

## Personalizar
- El nombre del sitio, colores y textos están en `index.html`.
- La lista `blockedWords` contiene el vocabulario bloqueado; puedes ampliarla. Los filtros por palabras pueden tener falsos positivos y no detectan todas las variantes.
- El límite de 30 segundos del navegador se puede evadir si alguien manipula el código. Refuérzalo en el servidor antes de usarlo con un público amplio.
