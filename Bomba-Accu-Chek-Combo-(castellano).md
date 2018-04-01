# TRABAJO EN PROCESO

**Este software es parte de una solución "hágalo usted mismo" y no es un producto, pero es indispensable que usted lea, aprenda y entienda el sistema incluyendo el modo de uso.**

**Esta solución no gestionará su diabetes por usted, pero si pone el tiempo necesario en montarlo y aprender, va a permitirle una mejora considerable tanto en su diabetes como en su calidad de vida. No tenga prisa, permítase tiempo para aprender. Sólo usted es responsable de lo que haga con él.**

## Requisitos de Hardware

- Una bomba de insulina Roche Accu-Chek Combo (con cualquier firmware, todas funcionan)
- Un Smartpix o dispositivo Realtyme junto con un Software Configuración 360 que configure la bomba.
  Roche envía dispositivos Smartpix a los clientes que lo sociliten de forma gratuita.
-  Un teléfono compatible: Teléfono Android con  LineageOS 14.1 (antes conocido como CyanogenMod) o Android 8.1 (Oreo). La lista de teléfonos compatibles puede encontrarse en el siguiente documento [AAPS Phones](https://docs.google.com/spreadsheets/d/1gZAsN6f0gv6tkgy9EBsYl0BQNhna0RDqA9QGycAqCQc/edit#gid=698881435).
* Por favor, tenga en cuenta que esta no es una lista completa y es un reflejo de las experiencias personales de los ususarios. Le animamos a que comparta aquí también sus experiencias para ayudar a otros (todos estos proyectos se basan en la idea de "pagar o devolver la ayuda a la comunidad"). 
- Tenga presente que aunque Android 8.1 permite la comunicación con la Combo, todavía hay algunos problemas con AAPS en 8.1. 
  Para aquellos usuarios avanzados, es posible conectar con un teléfono desbloqueado, y transferirlo a otro 
 teléfono desbloqueado para usarlo con ruffy/AAPS, que también está debloqueado. Esto permitiría usar teléfonos con  Android < 8.1. Esto no se ha probado lo suficiente: https://github.com/gregorybel/combo-pairing/blob/master/README.md

## Limitaciones

- No pueden utilizarse los bolos duales y cuadrados ("extended bolus" y "multiwave bolus").
- Solo puede utilizarse un perfil de basal.
- Si se programa un perfil basal diferente de 1, o se utilizan bolos duales o cuadrados, se estará interfiriendo con las basales temporales y se forzará al lazo cerrado a suspenderse durante 6 horas, puesto que no puede funcionar de forma segura bajo estas condiciones. 
 
- A día de hoy no se puede establecer la hora y la fecha desde la bomba. Los cambios de horarios deben hacerse de forma manual (conviene deshabilitar el ajuste automático del reloj en la tarde y cambiarlo por la mañana junto al reloj de la bomba para evitar la alarma nocturna).
- En este momento solo pueden usarse basales en rango de 0.05 a 10 unidades/hora. Esto también ocurre cuando se modifica un perfil, por ejemplo, cuando se aumenta un 200% la basal más alta no puede sobrepasar las 5 U/h ya que esto la duplicaría. De igual modo, si se reduce un 50%, la basal más baja debe ser de al menos un 0.10 U/h.
- Si el lazo cerrado requiere que una basal temporal en proceso sea cancelada, la Combo, en lugar de eso, pondrá en marcha una basal temporal del 90% o del 110% durante 15 minutos. Esto ocurre porque cuando se cancela una basal temporal se pone en marcha una alerta en la bomba que da lugar a muchas vibraciones. 
- En ocasiones (más o menos cada par de días) AAPS puede fallar hasta cancelar automáticamente una alerta de CANCELACIÓN de BASAL TEMPORAL. El usuario tendrá que hacerle frente a este problema (apretando el botón de reinicio o "refresh" en AAPS para transferir el aviso a AAPS o confirmando la alerta en la bomba).

- La estabilidad de la conexión de bluetooth variará con diferentes teléfonos, causando alarmas de "bomba fuera de cobertura" cuando no pueda establecerse conexión con la bomba. Si le ocurre este error, asegúrese de que el bluetooth está habilitado, presione el botón de reinicio ("refresh") en la Combo para ver si esto lo causó un problema ocasional y si todavía no se establece conexión, reinicie el teléfono. Generalmente esto último solucionará el problema.
  Hay otra situación en la que un reinicio no resuelve el problema, pero donde ha de presionarse un botón de la bomba (el que resetea el bluetooth de la bomba), antes de que la bomba acepte las conexiones de otro teléfono. No hay mucho que hacer en este moemento para remediar estos problemas. Si ve estos errores con frecuencia, su única opción a día de hoy es probar otro teléfono que funcione bien con AndroidAPS y con la Combo (lea más arriba).
 
- Mandar un bolo desde la bomba es una acción que no siempre va a detectarse a tiempo y quizás tarde hasta 20 minutos en el peor de los casos. Los bolos puestos desde la bomba se revisan siempre antes de poner una basal temporal mayor u otro bolo desde AAPS, pero debido a sus limitaciones, AAPS  rehusará poner dichas basales temporales o bolos calculados en base a cálculos entendidos como erróneos (por tanto, no mande bolos desde la bomba, lea la sección sobre "Uso").

- Debe evitarse programar una basal temporal desde la bomba porque el lazo cerrado es quien pone en marcha todas las basales temporales. El sistema puede tardar hasta 20 minutos en detectar una basal temporal establecida en la bomba y su efecto se tendrá en cuenta sólo en el momento en el que se detecte la temporal, de forma que en el peor de los casos habrá 20 minutos de basal temporal que no se reflejen en la información de la "insulina a bordo".

## Configuración 

- Configure la bomba usando el software de configuración 360.
  - Imprescindible (marcado en verde en las fotos):
    - Ajuste/deje la configuración de menú como "Standard", de esta manera sólo se mostrarán los menús y acciones que    admite el sistema y ocultará aquellos que no son compatibles (bolo extendido/ bolo múltiple,
      múltiples perfiles de basal ), los cuales estan restringidos porque no se pueden usar de manera segura con el lazo cerrado.
    - Verifique que la opción Quick Info Text está a  "QUICK INFO" (sin las comillas, lo encontrará debajo de  _Insulin Pump Options_).
    - Ajuste  TBR _Maximum Adjustment_ to 500% (es la basal máxima temporal)
    - Deshabilitar (poner a of)_Signal End of Temporary Basal Rate_ (es señal de final de basal temporal)
    - Ajustar  TBR _Duration increment_  a 15 minutos (es la duración de la basal temporal)  
    - Activar Bluetooth
  - Recomendado (marcado en azul en las fotos)
    - ajuste la alarma de unidades mínimas en el reservorio según su gusto.
    - Configure el bolo máximo de manera que sea conservador y seguro de acuerdo con su terapia protegiéndose de un posible fallo de software.
    - de la misma forma, configure  máxima duración de la basal temporal"maximum TBR duration"  como seguridad. Permita al , de manera que la bomba pueda ser puesta a 0% de basal durante 3 horas.
    - Habilite el bloqueo de las teclas para prevenir introducir bolos desde la bomba, especialmente si ya era usuario de la bomba y tiene la costumbre de hacerlo así.
    - Ajuste "display timeout" (tiempo de espera de pantalla) y "menu timeout" ( tiempo de espera menú) a un  mínimo de 5.5 y 5 respectivamente. Esto permite a AAPS a recuperarse mas rápidamente de las situaciones de error y evitar las vibraciones que pudieran ocurrir por este error
      

![](https://github.com/MilosKozak/AndroidAPS/blob/combo/documentation/images/combo-menu-settings.png)
![](https://github.com/MilosKozak/AndroidAPS/blob/combo/documentation/images/combo-pump-options-settings.png)
![](https://github.com/MilosKozak/AndroidAPS/blob/combo/documentation/images/combo-tbr-settings.png)
![](https://github.com/MilosKozak/AndroidAPS/blob/combo/documentation/images/combo-bolus-settings.png)
![](https://github.com/MilosKozak/AndroidAPS/blob/combo/documentation/images/combo-insulin-settings.png)

- Instale AndroidAPS conforme está descrito en [AndroidAPS wiki](http://wiki.AndroidAPS.org) utilizando la rama `combo` .
- Asegúrese de leer la wiki para entender como ajustar AndroidAPS.
- Seleccione en primer lugar el plugin MDI en AndroidAPS, not el plugin Combo inicialmente para evitar que el plugin Combo
  pueda interferir con ruffy durante el proceso de emparejamiento.
- Siga el enlace http://ruffy.AndroidAPS.org y clone ruffy via git. Use la misma rama que uso para 
  AndroidAPS, a día de hoy es la `combo`, pero en breve será la `master` y `dev`.
- Instale ruffy y utilícelo para emparejar la bomba. Si no funciona tras muchos intentos, cambie a la rama `pairing`, empareje con la bomba y vuelva de nuevo a la rama original.
  Si la bomba ya esta emparejada y puede ya ser controlada con ruffy, es suficiente con instalar la rama `combo`.
  Notese que el proceso de emparejamiento es algo delicado (aunque solamente deberá hacerse una vez) y puede requerir varios intentos; confirme rápidamente las indicaciones y, cuando comience de nuevo, salga previamente del menú bluetooth de la bomba. Otra opción para probar es ir al menú de Bluetooth del teléfono después de iniciar el proceso de emparejamiento (ya que esto provoca que el Bluetooth del teléfono sea visible mientras se muestra dicho menú) y volver a cambiar a ruffy después de confirmar el emparejamiento en la bomba, cuando la bomba muestre el código de autorización. If you're unsuccessful in pairing the pump (say after 10 attempts), try waiting up to 10s before confirming the pairing on the pump (when the name of the phone is displayed on the pump). If you have configured the menu timeout to be 5s above, you need to increase it again. Some users reported they needed to do this.
- Una vez que AAPS está utilizando ruffy, esta aplicación no deberá ser utilizada. La forma más sencilla de conseguir esto es reiniciar el telefono una vez finalizado el proceso de emparejamiento y dejar que AAPS inicie ruffy en segundo plano.
- Si la bomba es totalmente nueva, sera necesario suministrar un bolo para que la bomba cree la primera entrada del histórico.
- Antes de habilitar el plugin Combo en AAPS asegurese de que el perfil está correcto y activo (!) y que su perfil basal esta actualizado puesto que AAPS sincronizará su perfil basal con la bomba. Sólo entonces active el plugin Combo. Pulse el boton de actualización en la pestaña Combo para inicializar la bomba.
- Con el fin de verificar el funcionamiento correcto, con la bomba **desconectada**, utilice AAPS para fijar una Basal Temporal del 500% durante 15 minutos y para lanzar un bolo. La bomba mostrará la basal incrementada y tendrá un bolo en el histórico. AAPS mostrará igualmente la Basal ejecutándose y el bolo entregado.

## Uso

- Tenga en cuenta que esto no es un producto, especialmente al principio, el usuario necesita monitorear y comprender el sistema, sus limitaciones y cómo puede fallar. Se recomienda NO utilizar este sistema cuando la persona que lo utiliza no pueda comprender completamente el sistema.
- Lea la documentación de OpenAPS https://openaps.org para entender el algoritmo de loop en el que se basa AndroidAPS.
- Lea la wiki para aprender y entender el funcionamiento de AndroidAPS http://wiki.AndroidAPS.org
- Esta integración utiliza la misma funcionalidad que proporciona el medidor que viene con el Combo. El medidor permite reflejar la pantalla de la bomba y envía las pulsaciones de los botones hacia la bomba. La conexión a la bomba y este reenvío es lo que hace la aplicación Ruffy. El componente `scripter` lee la pantalla y automatiza el ingreso de bolos, TBRs, etc. y asegura que las entradas se procesen correctamente. AAPS interactúa luego con el componente `scripter` para aplicar comandos de loop y administrar bolos. Este modo tiene algunas restricciones: es comparativamente lento (pero lo suficientemente rápido para lo que se usa), y establecer un TBR o administrar un bolo hace que la bomba vibre.
- La integración del Combo con AndroidAPS esta diseñada con la suposición de que todas las entradas son realizadas utilizando AndroidAPS. Los bolos introducidos directamente en la bomba serán detectados por AAPS, pero puede tardarse hasta 20 minutos en que AAPS reconozca dicho bolo. La lectura de los bolos entregados directamente por la bomba es una característica de seguridad y no debe usarse con regularidad (el loop requiere el conocimiento de los carbohidratos consumidos, que no pueden ser introducidos en la bomba, lo que es otra razón para que todas las entradas deban realizarse mediante AndroidAPS). 
- No fije o cancele dosis basales temporales directamente en la bomba. El loop supone tener el control de los TBR y no puede trabajar con seguridad en otro caso, ya que no es posible conocer el inicio del TBR si este se ha realizado directamente a través de la bomba.
- El primer perfil basal de la bomba es leído al iniciarse la aplicación y es actualizado por AAPS.
  La dosis basal no debe ser modificada manualmente en la bomba, pero será detectada y corregida como una medida de seguridad (no debe confiar en las medidas de seguridad por defecto, esto esta previsto para detectar cambios no intencionados en la bomba).
- Es recomendable habilitar el bloqueo de teclas en la bomba para evitar aplicar bolos desde la bomba, especialmente si la bomba se ha usado previamente para administras "bolos rápidos" y se ha adquirido este hábito.
  Adicionalmente, con el bloqueo de teclas activado, no se interrumpirá la comunicación que pudiera haber activa entre AAPS y la bomba si se presiona accidentalmente una tecla.
- Cuando una alerta de BOLO/TBR CANCELADA se inicia en la bomba mientras se suministra un bolo o se fija una TBR, se produce una desconexión entre bomba y telefono, lo que sucede de vez en cuando. AAPS reintentará la reconexión y confirmará la alerta y luego reintentará la última acción (los bolos NO se reintentan por motivos de seguridad). Sin embargo, esta alarma puede ignorarse puesto que AAPS la confirmará automáticamente, normalmente en unos 30s (cancelarla no es un problema, pero obligará a la acción actual a esperar hasta que se apague la pantalla de la bomba antes de que pueda reconectar con la bomba). Si la alarma de la bomba continua, la confirmación automática fallará, en cuyo caso deberá confirmarse por el usuario manualmente.
- Cuando se produzca una alarma de cartucho bajo o batería baja durante la suministración de un bolo, se mostrará el defecto como una notificación en AAPS. Si ocurre mientras no haya conexión con la bomba, yendo a la pestaña Combo y pulsando el botón de refrescar, podrán reconocerse estas alertas desde la notificación que aparecerá en AAPS.
- Cuando AAPS falla en la confirmación de una alerta de TBR cancelada, o alguna es iniciada por alguna otra razón, pulsando el botón de actualizar en la pestaña Combo se establece la conexión con la bomba, se confirman las alertas y se muestra una notificación parar ella en AAPS. Esto puede realizarse de forma segura, ya que estas alertas son benignas - un TBR apropiado será fijado nuevamente durante la próxima iteración del loop. 
- Para el resto de alertas de la bomba: Conectando con la bomba se mostrará el mensaje de alerta en la pestaña Combo, por ejemplo "Estado: E4: Oclusión" y se mostrará una notificicación en la pantalla principal. 
  Un error mostrará una notificación urgente. AAPS nunca confirmará errores graves en la bomba de manera que esta vibrará y sonará para estar seguros que el usuario sea informado de una acción critica que requiera una acción.
- Una vez emparejado, ruffy no debe ser usado directamente (AAPS lo ejecutará en segundo plano en caso de ser necesario), ya que utilizar ruffy y AAPS al mismo tiempo no esta soportado.
- Si AAPS se detiene (o si es parada por el depurador) mientras AAPS y la bomba estuvieran comunicando (usando ruffy), pudiera ser necesario forzar el cierre de ruffy. Reiniciando AAPS se reiniciaría ruffy de nuevo.
  Reiniciar el teléfono es también un modo sencillo de resolver este problema si usted no sabe como forzar el cierre de una aplicación.
- No pulse ningún botón de la bomba mientras AAPS comunica con la bomba (se muestra el logo bluetooth en la bomba).