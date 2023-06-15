# Introducción
En este punto de tu trayecto, es posible que desees compartir lo que has construido. Una captura de pantalla o un video son un buen comienzo, pero tus amigos y familiares disfrutarán mucho más de una versión interactiva. Es hora de hacer que esas experiencias de WebGL estén en vivo.

# Soluciones
Hace años, no teníamos tantas soluciones para poner un sitio web en vivo. Hoy en día, es un poco más complicado, pero también tenemos acceso a muchas soluciones útiles.

# Compilación tradicional
En la siguiente sección, vamos a utilizar una solución que no requiere que te suscribas a una solución de alojamiento "tradicional" como OVH, 1and1 o Gandhi, donde tienes que cargar los archivos manualmente mediante un cliente FTP. Algunos de ustedes, sin embargo, pueden tener un host como uno de estos y solo quieren obtener esos archivos que se supone que debes cargar.

No puedes simplemente poner todo el proyecto con la carpeta node_modules/ y la configuración de Vite en el host. Primero, necesitas "compilar" tu proyecto dentro de esa configuración de webpack para crear archivos HTML, CSS, JS y activos que puedan ser interpretados por los navegadores.

Para compilar tu proyecto, ejecuta npm run build en la terminal.

Este comando ejecutará el script ubicado en el archivo /package.json en la propiedad scripts > build.

Espera unos segundos y los archivos deberían estar disponibles en la carpeta /dist/ que se creará al ejecutar build. Luego puedes subir esos archivos en línea usando tu cliente FTP favorito.

Cada vez que desees cargar una nueva versión, ejecuta npm run build nuevamente, incluso si la carpeta /dist/ ya existe.

No vamos a cubrir la configuración de una de esas soluciones de alojamiento "tradicionales" porque vamos a usar una solución más apropiada en la siguiente sección.

# Vercel
Vercel es una de esas soluciones de alojamiento "modernas" y cuenta con integración continua (automatización de pruebas, implementación y otros pasos de desarrollo como este). Es muy amigable para los desarrolladores y fácil de configurar.

Puedes usarlo para proyectos complejos, pero también para sitios web muy simples de "una sola página" como los que creamos en este curso.

Antes de continuar, ten en cuenta que no hay ninguna asociación entre mí (Bruno Simon) y Vercel. Simplemente me gusta usarlo para mis pequeñas experiencias creativas.

También existen otras buenas alternativas que debemos mencionar, como Netlify y GitHub Pages.

Ten en cuenta también que es posible que veas ligeras diferencias entre el resto de esta lección y tu propia experiencia con Vercel. Es una solución bastante nueva y los desarrolladores siguen mejorando el servicio.

# Crear una cuenta
Primero, ve a vercel.com y crea una cuenta.

Puedes elegir entre diferentes métodos de inicio de sesión, como la conexión con GitHub, la conexión con GitLab, la conexión con Bitbucket o el acceso clásico por correo electrónico.

Las opciones de "conexión" pueden ser buenas opciones porque una de las grandes características de Vercel es que permite la integración continua como solución de versionamiento. Si no sabes qué son GitHub, GitLab y Bitbucket, son soluciones de alojamiento para

 tus repositorios Git. En otras palabras, es donde la mayoría de los desarrolladores guardan su código.

Si estás familiarizado con ellos, puedes elegirlos sin problemas. Esto simplificará el proceso y Vercel recuperará automáticamente tu repositorio, te ayudará a configurar la versión en vivo y la actualizará automáticamente cuando envíes nuevas versiones al repositorio. Incluso puedes elegir una rama específica.

Para aquellos de ustedes que no estén familiarizados con las soluciones de alojamiento de Git, no se preocupen, vamos a mantener esta lección accesible para la mayoría de los estudiantes y elegir la solución de correo electrónico. Incluso si estás utilizando Git actualmente, esta solución funcionará correctamente. Haz clic en el enlace de Correo electrónico:

Luego, ingresa tu dirección de correo electrónico y sigue los pasos para crear tu cuenta:

Vercel te enviará una confirmación por correo electrónico con un enlace para que puedas iniciar sesión. Una vez que hayas hecho clic en ese enlace, deberías estar conectado.

# Agregar Vercel a tu proyecto
Vercel está disponible como un módulo NPM que puedes instalar globalmente en tu computadora o como una dependencia en tu proyecto. Vamos a agregarlo al proyecto para que, si queremos configurar el proyecto en otra computadora o compartirlo con otro desarrollador, no tengamos que instalar nada en esa computadora.

En la terminal de tu proyecto, ejecuta npm install vercel. Después de un breve tiempo, la instalación se completará, pero probablemente notarás que hay algunas vulnerabilidades. La terminal te indicará que ejecutes una auditoría para solucionarlas. Por lo general, puedes ignorar estas advertencias, ya que probablemente sean falsos positivos.

Aunque hemos agregado Vercel como una dependencia del proyecto, en lugar de manera global, aún no está disponible en la terminal. Tus scripts de NPM tendrán acceso a él, pero primero debes realizar el siguiente cambio.

En package.json, en la propiedad "scripts", agrega un nuevo script llamado "deploy" y escribe "vercel --prod" como valor (no olvides la coma después del script "dev"):

```json
{
  "scripts": {
    // ...
    "deploy": "vercel --prod"
  }
}
```

Si usas el comando "vercel" sin "--prod", el código se publicará en una URL de vista previa para que puedas probarlo antes de pasar a producción. Aunque es una característica interesante, no necesitamos una versión de vista previa.

A partir de ahora, si quieres implementar tu proyecto en línea, simplemente ejecuta npm run deploy en la terminal.

Implementar por primera vez
La primera vez que quieras implementar tu proyecto, Vercel te pedirá información para conectar con tu cuenta y configurar el proyecto.

En la terminal, ejecuta npm run deploy.

Si anteriormente elegiste conectarte con un correo electrónico, usa las flechas hacia arriba y hacia abajo para seleccionar "Continuar con el correo electrónico" y presiona Enter.

Luego, escribe tu correo electrónico.

Vercel te enviará un correo electrónico como antes. Haz clic en el enlace disponible en ese correo electrónico y la terminal debería continuar automáticamente al siguiente paso.

En este punto, se te pedirá confirmación para configurar e implementar la carpeta actual. Elige Y y presiona Enter.

Puedes tener múltiples ámbitos y equipos

 asociados con tu cuenta. Si acabas de crear tu cuenta, probablemente solo haya uno. Selecciona ese ámbito presionando Enter.

En nuestro caso, estamos creando un nuevo proyecto y no queremos asociar nuestro código con un proyecto existente. Escribe n y presiona Enter.

Vercel intentará adivinar el nombre del proyecto, pero puedes cambiarlo a cualquier cosa que desees. Puedes usar minúsculas, números y guiones. Presiona Enter.

Si estás ejecutando ese código en la raíz de la carpeta del proyecto, puedes mantener ./ y presionar Enter.

Vercel tiene configuraciones predeterminadas para cosas como el comando de construcción o la carpeta de destino del paquete. Necesitamos anular esas configuraciones. Escribe y y presiona Enter.

El comando de construcción predeterminado de Vercel es npm run build y es el mismo para nosotros. Pero el directorio de salida predeterminado de Vercel es "public" mientras que el nuestro es "dist".

Usa las flechas hacia arriba y hacia abajo para mover el cursor en el directorio de salida y presiona Espacio para seleccionarlo. Luego, presiona Enter para pasar al siguiente paso.

Escribe "dist" y presiona Enter.

¡Eso es todo! Tu sitio web debería comenzar a implementarse en Vercel.

Espera uno o dos minutos y Vercel debería mostrarte la URL de la versión en vivo.

Vercel debería copiar automáticamente esa URL en tu portapapeles. Puedes pegarla en tu navegador favorito y probar la versión en vivo.

# Configuraciones adicionales

Ve a vercel.com y asegúrate de haber iniciado sesión.

Deberías tener acceso a tu panel y ver tu proyecto.

Haz clic en tu proyecto. Esta es la pantalla que deberías ver a continuación.

Aquí puedes ver una vista previa de tu proyecto, obtener información sobre las últimas compilaciones, cambiar las preferencias de implementación, ver posibles errores, etc.

Incluso puedes agregar un dominio personalizado, pero no lo abordaremos en esta lección.

# Precios

Pero espera, ¿todo es gratuito?

Sí y no. Si solo quieres compartir esas increíbles experiencias WebGL que estás construyendo con el mundo sin fines comerciales, el plan gratuito (llamado Hobby) debería ser más que suficiente. Puedes crear tantos proyectos como desees con todas las características que acabamos de ver.

Pero si tienes fines comerciales o deseas utilizar características específicas como equipos, protecciones de contraseña para la vista previa, firewalls, etc., es posible que necesites utilizar un plan de pago.

Además, el plan Hobby tiene limitaciones de ancho de banda y tiempo de compilación. Esto significa que si tu sitio web recibe mucha atención o implementas demasiadas veces, deberás cambiar a un plan de pago.

Los planes y precios se pueden encontrar aquí: vercel.com/pricing
