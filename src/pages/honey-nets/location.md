---
layout: ./_layout.astro
---

# Ubicación

La ubicación de los honeypots es esencial para maximizar su efectividad, ya que debido a su carácter intrínsecamente pasivo una ubicación de difícil acceso eliminará gran parte de su atractivo para potenciales atacantes. Por otro lado, si su ubicación es demasiado artificial u obvia cualquier experimentado atacante la descubrirá y evitará todo contacto con ella.

Por otro lado debemos tener en cuenta que debe integrarse con el resto del sistema que tenemos ya implantado (servidores WWW, servidores de ficheros, DNS…) y asegurarnos que no interfiere con las otras medidas de seguridad que puedan ya existir en nuestra red (Firewalls, IDS…). Teniendo en cuenta que los honeypots pueden servir tanto para la detección de atacantes internos como externos, debemos tener siempre en cuenta la posibilidad de establecer honeypots internos para la detección de atacantes o sistemas comprometidos en nuestra red (por ejemplo sistemas infectados con un gusano o virus). La bibliografía consultada establece tres puntos básicos candidatos a albergar los honeypots según nuestras necesidades:

1. Antes del firewall (Front of firewall): Esta localización permite evitar el incremento del riesgo inherente a la instalación del honeypot. Como este se encuentra fuera de la zona protegida por el firewall, puede ser atacado sin ningún tipo de peligro para el resto de nuestra red (ver figura).

   ![Diagrama de la ubicación: Antes del firewall](/honey-nets/location-1.png)

   Esta ubicación nos permite tener un acceso directo a los atacantes, puesto que el firewall ya se encarga de filtrar una parte del tráfico peligroso o no deseado, obteniendo trazas reales de su comportamiento y estadísticas muy fiables sobre la cantidad y calidad de ataques que puede recibir nuestra red.

   Además con esta configuración evitaremos las alarmas de otros sistemas de seguridad de nuestra red (IDS) al recibir ataques en el honeypot. Sin embargo, existe el peligro de generar mucho tráfico debido precisamente a la facilidad que ofrece el honeypot para ser atacado. Cualquier atacante externo será lo primero que encuentra y esto generará un gran consumo de ancho de banda y espacio en los ficheros de log. Por otro lado, esta ubicación nos evita la detección de atacantes internos.

2. Detrás del firewall (Behind the firewall): En esta posición, el honeypot queda afectado por las reglas de filtrado del firewall. Por un lado tenemos que modificar las reglas para permitir algún tipo de acceso a nuestro honeypot por posibles atacantes externos, y por el otro lado, al introducir un elemento potencialmente peligroso dentro de nuestra red podemos permitir a un atacante que gane acceso al honeypot un paseo triunfal por nuestra red. La ubicación tras el firewall nos permite la detección de atacantes internos así como firewalls mal configurados, máquinas infectadas por gusanos o virus e incluso atacantes externos (ver figura).

   ![Diagrama de la ubicación: Detrás del firewall](/honey-nets/location-2.png)

   Sin embargo las contrapartidas mas destacables son la gran cantidad de alertas de seguridad que nos generarán otros sistemas de seguridad de nuestra red (Firewalls, IDS…) al recibir ataques el honeypot y la necesidad de asegurar el resto de nuestra red contra el honeypot mediante el uso de firewalls extras o sistemas de bloqueo de acceso, ya que si un atacante logra comprometer el sistema tendrá vía libre en su ataque a toda nuestra red. Hay varias circunstancias que obligan a este tipo de arquitectura, como por ejemplo la detección de atacantes internos o la imposibilidad de utilizar una dirección IP externa para el honeypot.

3. En la zona desmilitarizada: La ubicación en la zona desmilitarizada permite por un lado juntar en el mismo segmento a nuestros servidores de producción con el honeypot y por el otro controlar el peligro que añade su uso, ya que tiene un firewall que lo aísla de resto de nuestra red local (ver figura).

   ![Diagrama de la ubicación: En la zona desmilitarizada](/honey-nets/location-3.png)

   Esta arquitectura nos permite tener la posibilidad de detectar ataques externos e internos con una simple reconfiguración de nuestro sistema de firewall puesto que se encuentra en la zona de acceso público.

   Además eliminamos las alarmas de nuestros sistemas internos de seguridad y el peligro que supone para nuestra red al no estar en contacto directo con esta. La detección de atacantes internos se va algo debilitada, puesto que al no compartir el mismo segmento de red que nuestra LAN un atacante local no accederá al honeypot. Sin embargo, desde la red local si que es posible acceder al honeypot, con lo que un atacante interno que intente atacar nuestros servidores públicos u otros sistemas externos (un gusano por ejemplo) muy probablemente acabe siendo detectado.

[Fuente](https://www.cs.upc.edu/~gabriel/files/DEA-es-4HoneypotsyHoneynets.pdf)
