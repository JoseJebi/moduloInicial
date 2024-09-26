# moduloInicial

Documentación de instalación de Odoo con Docker Compose.

-Lo primero que hice fue crear un directorio al que llamé Odoo.

-En ese directorio creé 3 directorios:

  -Al primer directorio lo llamé config_odoo. En ese directorio creé un archivo de configuración que usaremos más tarde.

  -En odoo.conf añadimos una serie de opciones relacionadas con la máquina virtual Linux en la que estará Odoo. Ponemos las rutas donde queremos que se guarden los módulos o addons que hagamos, otra ruta para los datos, y otra ruta para el log. Además, añadimos una contraseña de administrador.

  -Al segundo directorio lo llamé dev-addons. En ese de momento no hacemos nada.

  -Al tercer directorio lo llamé log. Ahí tampoco hacemos nada.

-Por último, después de crear los 3 directorios, creé un archivo, docker-compose.yml

  -En este archivo es donde vamos a tener el código que Docker Compose va a interpretar para realizar la instalación. Entonces en este archivo le vamos a dar una serie de parámetros de instalación: La versión de Odoo y de Postgre que usaremos, el enlace entre ambos, el puerto donde tendremos Odoo, los volúmenes donde estarán los containers, los usos que le damos a los 3 directorios que creamos antes, etc.

-Después de eso tendremos que abrir powershell con permisos de administrador e irnos al directorio Odoo (el directorio de docker-compose.yml).

-Ejecutamos el comando "Docker Compose up" y Docker Compose realiza la instalación con los parametros que le dimos en el archivo yml.

-Abrimos Docker y vemos que ya nos sale el container. Lo desplegamos para ver los 2 containers que lleva debajo: El de Odoo y el de Postgre.

-Abrimos la consola del container de Odoo. En la máquina virtual Linux nos movemos hasta mnt/extra-addons.

-Hacemos un comando:

    odoo scaffold nombremodulo

-(siendo nombremodulo el nombre del módulo que deseamos crear)

-Ahora tenemos que volver a Windows, al directorio dev-addons, y nos aparece un directorio con el nombre de nuestro módulo. Hay que modificar una serie de cosas, entonces nos viene bien abrir el módulo como proyecto en un IDE que soporte Python

-Lo primero que tenemos que hacer es entrar al manifest y descomentar, en el apartado data, una línea (la 25) que controla la la seguridad de las tablas.

    'security/ir.model.access.csv',

-Después tenemos que entrar en views/views.xml. Aquí debemos descomentar varias líneas:

  -El primer párrafo, que es el que nos permitirá ver el árbol de datos cuando abramos el módulo. Podemos descomentar todo menos la línea de value2. Cuidado con las tabulaciones que Python es sensible.

    <record model="ir.ui.view" id="dam2.list">
      <field name="name">dam2 list</field>
      <field name="model">dam2.dam2</field>
      <field name="arch" type="xml">
        <tree>
          <field name="name"/>
          <field name="value"/>
          <!-- <field name="value2"/> -->
        </tree>
      </field>
    </record>

  -El segundo párrafo (actions opening views on models).

    <record model="ir.actions.act_window" id="dam2.action_window">
      <field name="name">dam2 window</field>
      <field name="res_model">dam2.dam2</field>
      <field name="view_mode">tree,form</field>
    </record>

  -Top menu item y menu categories (las 2 líneas debajo de esos 2 comentarios) para que nos salga el módulo en menús de Docker.

    <!-- Top menu item -->

    <menuitem name="dam2" id="dam2.menu_root"/>

    <!-- menu categories -->

    <menuitem name="Menu 1" id="dam2.menu_1" parent="dam2.menu_root"/>

  -Una vez que hemos hecho esto ya podemos abrir Odoo desde el puerto (podemos hacerlo desde la vista del container de Docker) con la contraseña que pusimos en odoo.conf, activar las opciones de desarrollador, y actualizar nuestro módulo para ver su contenido.
