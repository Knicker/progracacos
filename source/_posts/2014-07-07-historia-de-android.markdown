---
layout: post
title: "Transición entre Activities"
date: 2014-10-07 20:03:41 +0200
comments: true
categories: android
published: false
---

La transición entre Activities la realizaremos con `overridePendingTransition()` que sobreescribirá las animaciones por defecto por las animaciones que pasemos por parámetro.<!-- more --> Tendremos que llamar al método siempre que vaya a suceder una transición, como por ejemplo, al abrir o cerrar una `Activity` e indicar las animaciones de entrada y salida. 


#Animación XML
Para ello tendremos que crear archivos XML donde indicaremos el comportamiento de las animaciones con ayuda diferentes atributos para definir el comportamiento de nuestra animación, a continuación: 

- `translate`: desplazamiento.
	- `fromXDelta`, `toXDelta`: Valor inicial y final sobre el eje X.
	- `fromYDelta`, `toYDelta`: Valor inicial y final sobre el eje Y.
- `rotate`: rotación. 
	- `fromDegress`, `toDegrees`: Valor inicial y final en grados de la rotación (un giro completo sería de 0 a 360). 
	- `pivotX`, `pivotY`: Punto sobre el que se realizará el giro. 
- `scale`: tamaño.
	- `fromXScale`, `toXScale`: Valor inicial y final para el tamaño del eje X. 
	- `fromYScale`, `toYScale`: Valor inicial y final para el tamaño del eje Y. 
	- `pivotX`, `pivotY`: Punto sobre el que se realizará el zoom. 
- `alpha`: opacidad. 
	- `fromAlpha`, `toAlpha`: Valor inicial y final de la opacidad. 

En este caso crearemos cuatro para recrear el efecto de la animación de transición por defecto de `Android 2.0` que es un desplazamiento horizontal donde simula la actividad entrante empujando a la actividad saliente. 

El evento `onClick()` de la actividad principal, sobreescribimos las transiciones pendientes al llamar a la segunda actividad: 
``` java 
startActivity(intent);				
overridePendingTransition(R.anim.entrar_derecha, 
		R.anim.salir_izquierda);
```

``` xml entrar_derecha.xml
<translate 
	android:toXDelta="0%" 
	android:fromXDelta="100%" 
	android:duration="600" />
```

``` xml salir_izquierda.xml
<translate 
	android:toXDelta="-100%" 
	android:fromXDelta="0%" 
	android:duration="600" />
```

Y hacemos lo mismo en el evento `onFinish()` de la segunda actividad: 
``` java
super.finish();
overridePendingTransition(R.anim.entrar_izquierda, 
		R.anim.salir_derecha);
```

``` xml entrar_izquierda.xml
<translate 
	android:toXDelta="0%" 
	android:fromXDelta="-100%" 
	android:duration="600" />
```

``` xml salir_derecha.xml
<translate 
	android:toXDelta="100%" 
	android:fromXDelta="0%" 
	android:duration="600" />
```
