# Non Negotiables · guía paso a paso

App de hábitos, rachas, peso y reto de libros para el iPhone. Se instala desde la web, no necesita App Store y tus datos se guardan solo en tu móvil.

Te llevará unos 20 minutos la primera vez. Usa un **ordenador** para los pasos 1 a 7 y el **iPhone** para el 8 en adelante.

---

## 1. Crea una cuenta en GitHub

Ve a **https://github.com/signup** y créate una cuenta gratis. Tu nombre de usuario formará parte de la dirección de la app, por ejemplo `https://TU-USUARIO.github.io/non-negotiables/`.

## 2. Crea el repositorio

1. Arriba a la derecha, pulsa **+** → **New repository**.
2. En **Repository name** escribe `non-negotiables`.
3. Marca **Public**. Hace falta para que GitHub Pages sea gratis. El código será visible, pero tus datos no, porque viven en tu móvil.
4. No marques nada más. Pulsa **Create repository**.

## 3. Sube los archivos

1. Descomprime el `.zip` que te han pasado.
2. En la página de tu repositorio, pulsa el enlace **uploading an existing file**.
3. Abre la carpeta `non-negotiables` en tu ordenador, selecciona **todo lo que hay dentro** (archivos y carpetas `icons` y `notify`) y arrástralo a la página.
4. Abajo, pulsa **Commit changes**.

> Si al terminar no ves las carpetas `icons` y `notify` en el repositorio, súbelas otra vez arrastrando cada carpeta.

## 4. Crea el archivo de notificaciones

La carpeta `.github` empieza por un punto y casi nunca se sube al arrastrar. Créala a mano:

1. En tu repositorio, pulsa **Add file** → **Create new file**.
2. En el nombre escribe exactamente: `.github/workflows/notify.yml`. Al escribir cada `/` verás que se crea una carpeta.
3. Abre en tu ordenador el archivo `workflow-notificaciones.yml`, copia **todo** su contenido y pégalo en el cuadro grande.
4. Pulsa **Commit changes** dos veces.

## 5. Publica la app

1. En tu repositorio ve a **Settings** → **Pages** (menú de la izquierda).
2. En **Source** elige **Deploy from a branch**.
3. En **Branch** elige `main` y `/ (root)`. Pulsa **Save**.
4. Espera uno o dos minutos y recarga la página. Arriba saldrá **Your site is live at…** con tu dirección. Esa es tu app.

## 6. Crea tus claves de notificaciones

Las notificaciones necesitan dos claves que son solo tuyas.

1. Abre en el navegador `https://TU-USUARIO.github.io/non-negotiables/setup.html`.
2. Pulsa **Generar mis claves**. Te saldrán dos: la **pública** y la **privada**. Deja la página abierta.
3. En tu repositorio ve a **Settings** → **Secrets and variables** → **Actions** → **New repository secret** y crea estos dos secretos:

| Name | Secret |
|---|---|
| `VAPID_PUBLIC` | la clave **pública** |
| `VAPID_PRIVATE` | la clave **privada** |

4. Ahora pon la clave **pública** en la app. En tu repositorio abre el archivo `config.js`, pulsa el lápiz ✏️ para editarlo y pega la clave entre las comillas de `clavePublica`:

```js
clavePublica: 'BLa_clave_publica_que_te_ha_salido...',
```

5. Pulsa **Commit changes**. La clave privada **nunca** va en `config.js`.

## 7. Ajusta tu reto de libros (opcional)

En el mismo `config.js` puedes cambiar el reto: fecha de inicio, fecha de fin y número de libros. Las fechas van en formato `AAAA-MM-DD`:

```js
retoLibros: {
  inicio: '2026-05-31',
  fin:    '2027-05-31',
  libros: 40
}
```

## 8. Instala la app en el iPhone

1. Abre tu dirección `https://TU-USUARIO.github.io/non-negotiables/` en **Safari**. Tiene que ser Safari.
2. Pulsa el botón **Compartir** (el cuadrado con la flecha hacia arriba).
3. Pulsa **Añadir a pantalla de inicio**. Ponle el nombre que quieras y pulsa **Añadir**.
4. A partir de ahora abre la app **siempre desde ese icono**, no desde Safari.

Hace falta iOS 16.4 o superior para las notificaciones.

## 9. Activa las notificaciones

1. Abre la app desde el icono.
2. Pulsa el botón de ajustes de arriba a la derecha → **Activar notificaciones** → **Permitir**.
3. Te saldrá un código largo que empieza por `{"endpoint":`. Pulsa **Enviar código** y mándatelo a ti mismo (WhatsApp, correo, Notas…) para poder copiarlo en el ordenador.
4. En el ordenador, en tu repositorio: **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:

| Name | Secret |
|---|---|
| `PUSH_SUBSCRIPTION` | el código entero, tal cual |

## 10. Prueba que llegan

1. En tu repositorio, ve a la pestaña **Actions**. Si te pide activarlas, pulsa el botón verde para permitirlas.
2. A la izquierda pulsa **Notificaciones** → **Run workflow**.
3. Elige `weigh` y pulsa **Run workflow**. En unos segundos te llegará al iPhone **⚖️ PÉSATEEE!!!! ⚖️**.
4. Repite con `daily` para ver el recordatorio de hábitos.

Si sale una cruz roja, pulsa encima y lee el mensaje: casi siempre es un secreto con un nombre mal escrito o una clave pública distinta en `config.js` y en `VAPID_PUBLIC`.

## 11. Frases de mentalidad (opcional)

Si quieres recibir tus propias frases cada hora, crea otro secreto llamado `MENTALIDAD` con tus frases en este formato exacto (entre corchetes, cada frase entre comillas y separadas por comas):

```json
["Primera frase.", "Segunda frase.", "Tercera frase."]
```

La frase 1 llega hacia las 6:45, la 2 hacia las 7:45 y así cada hora, hasta un máximo de 17 frases (la última, a las 22:45). Si no creas este secreto, no se envían frases.

---

## Qué notificaciones recibirás

| Cuándo | Aviso |
|---|---|
| Lunes, 6:30 | ⚖️ PÉSATEEE!!!! ⚖️ |
| Cada día, 20:00 | Los hábitos que te faltan ese día |
| Cada hora, de 6:45 a 22:45 | Tus frases, si has creado `MENTALIDAD` |

Funciona en cualquier zona horaria: usa la hora de tu iPhone. GitHub a veces retrasa los envíos unos minutos.

## Cosas importantes

- **Tus datos viven solo en tu iPhone.** Si borras el icono de la pantalla de inicio, se borran. Haz copias de vez en cuando en Ajustes → **Guardar copia**.
- **Si cambias de móvil o reinstalas la app**, restaura la copia y repite el paso 9 con el código nuevo (edita el secreto `PUSH_SUBSCRIPTION`).
- **Para actualizar la app** después de cambiar algo en GitHub, cierra la app del todo y ábrela con internet.
- **No compartas tu clave privada** ni el código `PUSH_SUBSCRIPTION` con nadie.
