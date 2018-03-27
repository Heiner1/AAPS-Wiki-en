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
  Notese que el proceso de emparejamiento es algo delicado (aunque solamente deberá hacerse una vez) y puede requerir varios intentos; confirme rápidamente las indicaciones y, cuando comience de nuevo, salga previamente del menú bluetooth de la bomba. Otra opción para probar es ir al menú de Bluetooth del teléfono después de iniciar el proceso de emparejamiento (ya que esto provoca que el Bluetooth del teléfono sea visible mientras se muestra dicho menú) y volver a cambiar a ruffy después de confirmar el emparejamiento en la bomba, cuando la bomba muestre el código de autorización.
- When AAPS is using ruffy, the ruffy app can't be used. The easiest way is to just
  reboot the phone after the pairing process and let AAPS start ruffy in the background.
- If the pump is completely new, you need to do one bolus on the pump, so the pump creates a first history entry.
- Before enabling the Combo plugin in AAPS make sure your profile is set up
  correctly and activated(!) and your basal profile is up to date as AAPS will sync the basal profile
  to the pump. Then activate the Combo plugin. Press the _Refresh_ button on the Combo tab to initialize the 
  pump.
- To verify your setup, with the pump **disconnected**, use AAPS to set a TBR of 500% for 15 min and issue a bolus. The pump should now have a TBR running and the bolus in the history. AAPS should also show the active TBR and delivered bolus.

## Usage

- Keep in mind that this is not a product, esp. in the beginning the user needs to monitor and understand the system,
  its limitations and how it can fail. It is strongly advised NOT to use this system when the person
  using it is not able to fully understand the system.
- Read the OpenAPS documentation https://openaps.org to understand the loop algorithm AndroidAPS
  is based upon.
- Read the wiki to learn about and understand AndroidAPS http://wiki.AndroidAPS.org
- This integration uses the same functionality which the meter provides that comes with the Combo.
  The meter allows to mirror the pump screen and forwards button presses to the pump. The connection
  to the pump and this forwarding is what the ruffy app does. A `scripter` components reads the screen
  and automates entering boluses, TBRs etc and making sure inputs are processed correctly.
  AAPS then interacts with the scripter to apply loop commands and to administer boluses.
  This mode has some restrictions: it's comparatively slow (but well fast enough for what it is used for),
  and setting a TBR or giving a bolus causes the pump to vibrate.
- The integration of the Combo with AndroidAPS is designed with the assumption that all inputs are
  made via AndroidAPS. Boluses entered on the pump directly will be detected by AAPS, but it can take
  up to 20 min before AndroidAPS becomes aware of such a bolus. Reading boluses delivered directly on
  the pump is a safety feature and not meant to be regularly used (the loop requires knowledge of carbs
  consumed, which can't be entered on the pump, which is another reason why all inputs should be done
  in AndroidAPS). 
- Don't set or cancel a TBR on the pump. The loop assumes control of TBR and cannot work reliably otherwise, since it's not possible to determine the start time of a TBR that was set by the user on the pump.
- The pump's first basal rate profile is read on application start and is updated by AAPS.
  The basal rate should not be manually changed on the pump, but will be detected and corrected as a safety
  measure (don't rely on safety measures by default, this is meant to detect an unintended change on the pump).
- It's recommended to enable key lock on the pump to prevent bolusing from the pump, esp. when the
  pump was used before and using the "quick bolus" feature was a habit.
  Also, with keylock enabled, accidentally pressing a key will NOT interrupt active communication
  between AAPS and pump.
- When a BOLUS/TBR CANCELLED alert starts on the pump during bolusing or setting a TBR, this is
  caused by a disconnect between pump and phone, which happens from time to time. AAPS will try to reconnect and confirm the alert
  and then retry the last action (boluses are NOT retried for safety reasons). Therefore,
  such an alarm can be ignored as AAPS will confirm it automatically, usually within 30s (cancelling it is not problem, but will lead to the currently
  active action to have to wait till the pump's display turns off before it can reconnect to the
  pump). If the pump's alarm continues, automatic corfirmation failed, in which case the user
  needs to confirm the alarm manually.
- When a low cartridge or low battery alarm is raised during a bolus, they are confirmed and shown
  as a notification in AAPS. If they occur while no connection is open to the pump, going to the
  Combo tab and hitting the Refresh button will take over those alerts by confirming them and
  show a notification in AAPS.
- When AAPS fails to confirm a TBR CANCELLED alert, or one is raised for a different reason,
  hitting Refresh in the Combo tab establishes a connection, confirms the alert and shows
  a notification for it in AAPS. This can safely be done, since those alerts are benign - an
  appropriate TBR will be set again during the next loop iteration.
- For all other alerts raised by the pump: connecting to the pump will show the alert message in
  the Combo tab, e.g. "State: E4: Occlusion" as well as showing a notification on the main screen.
  An error will raise an urgent notification. AAPS never confirms serious errors on the pump,
  but let's the pump vibrate and ring to make sure the user is informed of a critical situation
  that needs action.
- After pairing, ruffy should not be used directly (AAPS will start in the background as needed),
  since using ruffy at AAPS at the same time is not supported.
- If AAPS crashes (or is stopped from the debugger) while AAPS and the pump were communicating (using
  ruffy), it might be necessary to force close ruffy. Restarting AAPS will start ruffy again.
  Restarting the phone is also an easy way to resolve this if you don't know how to force kill
  an app.
- Don't press any buttons on the pump while AAPS communicates with the pump (Bluetooth logo is
  shown on the pump).