# Salesforce: Conversión ID15 a ID18 en Excel

Salesforce trabaja con un identificador único de 15 caracteres de longitud. Este identificador único es "case sensitive", es decir, que es único siempre que se consideren diferentes las mayúsculas y las minúsculas, o lo que es lo mismo, la letra "a" es un valor diferente a la letra "A".

Sin embargo, cuando se hacen comparaciones en otras herramientas que no distinguen mayúsculas de minúsculas (como puede ser la función BUSCARV de Excel tan ampliamente utilizada) se generan algunas dificultades. Por ello, Salesforce trabaja también con un identificador de 18 caracteres (los 15 iniciales + 3 caracteres adicionales) que si permiten comparación en herramientas que no distinguen mayúsculas y minúsculas. Este ID18 es único independiente de que la comparación se haga de este modo. 

A continuación os muestro una formula de Excel que calcula el ID de longitud 18 de Salesforce a partir del ID de longitud 15.

Suponiendo que insertáis el ID15 en la casilla A2, podéis usar la siguiente fórmula para que calcule el ID18:
```cpp
=CONCATENAR(A2;
EXTRAE("ABCDEFGHIJKLMNOPQRSTUVWXYZ012345";(
SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;1;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;1;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;2;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;2;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;3;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;4;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;4;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;8;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;5;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;16;0);0)
+1);1);
EXTRAE("ABCDEFGHIJKLMNOPQRSTUVWXYZ012345";(
SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;6;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;1;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;7;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;2;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;8;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;4;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;9;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;8;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;10;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;16;0);0)
+1);1);
EXTRAE("ABCDEFGHIJKLMNOPQRSTUVWXYZ012345";(
SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;11;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;1;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;12;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;2;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;13;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;4;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;14;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;8;0);0)
+SI.ERROR(SI(ENCONTRAR(EXTRAE(A2;15;1);"ABCDEFGHIJKLMNOPQRSTUVWXYZ")>0;16;0);0)
+1);1))
```

Este sería el resultado con un ejemplo:

![Resultado Excel](/img/salesforce-id.png)