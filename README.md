# Ajustador de alineación palabra por palabra

Herramienta web para corregir a mano los tiempos de inicio y fin de cada palabra
de una oración grabada, a partir de una alineación automática (por ejemplo, los
TextGrid de Montreal Forced Aligner convertidos a CSV).

A diferencia de Praat, donde los intervalos son contiguos y mover un límite
desplaza a la palabra vecina, aquí **cada palabra es independiente**.

## Uso

1. Abre `index.html` en el navegador (o la página publicada).
2. Carga el audio de la oración (WAV, MP3 o MP4).
3. Carga el CSV de palabras alineadas.
4. Arrastra cada palabra o sus bordes hasta que coincida con lo que escuchas.
5. Si una fila contiene dos palabras juntas, selecciónala, coloca el cabezal
   entre ellas y pulsa **Dividir en el cabezal**; o escribe una palabra nueva con
   su inicio y fin en el formulario **Añadir palabra**.
6. Escribe la palabra objetivo y pulsa **Enmarcar**.
7. Pulsa **Descargar esta oración** (funciona aunque no hayas corregido nada),
   o **Descargar todas las oraciones** para guardar todo lo corregido en la sesión.

No se sube nada a ningún servidor: todo se procesa en tu navegador.

## Formato del CSV

Columnas obligatorias: `xmin`, `xmax`, `texto`.
Opcionales: `archivo`, `duracion`, `objetivo`.

```
archivo,xmin,xmax,duracion,texto
mi_audio,0.10,0.50,0.40,le
mi_audio,0.50,1.20,0.70,je'elo'
```

El CSV puede contener muchas oraciones, con una fila por palabra (varias filas
comparten el mismo `archivo`). La herramienta muestra solo las palabras de la
oración cuyo nombre coincide con el audio cargado (sin extensión). Las oraciones
ya corregidas se marcan con ✎ en el selector, y las correcciones se conservan al
cambiar de audio durante la sesión. Acepta coma o punto decimal.

El CSV exportado agrega `objetivo` (palabra enmarcada) y `modificado`
(palabras que se ajustaron a mano), útil para reportar cuántos tiempos se corrigieron.

## Atajos

| Tecla | Acción |
|---|---|
| Espacio | Reproducir o pausar |
| Enter | Escuchar la palabra seleccionada |
| ← → | Mover la palabra 10 ms |
| Shift + ← → | Ajustar el inicio |
| Alt + ← → | Ajustar el final |

## Publicar en GitHub Pages

Sube `index.html` a un repositorio, entra a *Settings → Pages* y elige la rama
principal como origen. La herramienta queda disponible en
`https://<usuario>.github.io/<repositorio>/`.