# LAB 11 — LABORATORIO EN CLASE (GUÍA DETALLADA PASO A PASO)
## Curso: Realidad Virtual y Aumentada | PSISP08075
### Semana 11 — Scripts e Inputs: Sistema de Interacción AR

---

> **Esta guía está escrita para principiantes.**
> Cada paso incluye exactamente qué ver en pantalla, qué hacer y qué esperar.
> Si algo no coincide con lo que ves, detente y compara con la descripción antes de continuar.

| Campo | Detalle |
|-------|---------|
| **Tiempo estimado** | 35–40 minutos |
| **Modalidad** | Individual, en clase |
| **Resultado final** | App AR que detecta TAP, SWIPE y PINCH sobre objetos 3D |
| **Entrega** | Commit en GitHub antes del final de clase |

---

## QUE VAS A CONSTRUIR

Al terminar este laboratorio tendrás una aplicación AR que:

```
Usuario toca la pantalla una vez (TAP)
  → Aparece un cubo 3D en el plano detectado
  → Texto en pantalla dice "TAP en (x, y)"

Usuario arrastra el dedo horizontalmente (SWIPE)
  → El cubo rota sobre su eje vertical
  → Texto dice "SWIPE →" o "SWIPE ←"

Usuario pone dos dedos y los aleja/acerca (PINCH)
  → El cubo crece o se reduce
  → Texto dice "PINCH — escalar"
```

---

## PARTE A — ABRIR UNITY Y CREAR EL PROYECTO

### PASO A-1 — Abrir Unity Hub (2 min)

**¿Qué es Unity Hub?**
Unity Hub es el programa que te permite crear y gestionar proyectos de Unity. Es diferente a Unity mismo — primero abres Hub, luego desde Hub abres Unity.

**Cómo abrirlo:**

En Windows:
1. Busca en el menú de inicio: escribe `Unity Hub`
2. Haz clic en el ícono naranja con la letra "U"

En Mac:
1. Abre Spotlight (Cmd + Espacio)
2. Escribe `Unity Hub`
3. Presiona Enter

**Lo que debes ver:**
```
┌─────────────────────────────────────────────────────┐
│  Unity Hub 3.x                                      │
│  ┌──────────┐  ┌───────────┐  ┌───────────────────┐│
│  │ Projects │  │  Installs │  │  Community        ││
│  └──────────┘  └───────────┘  └───────────────────┘│
│                                                     │
│  [+ New project]                    [Open project]  │
│                                                     │
│  (lista de proyectos recientes)                     │
└─────────────────────────────────────────────────────┘
```

**Si Unity Hub no está instalado:** avísale al docente antes de continuar.

---

### PASO A-2 — Crear un nuevo proyecto (3 min)

1. En Unity Hub, haz clic en el botón azul **"New project"** (esquina superior derecha)

2. Se abre una ventana con plantillas (templates). Debes ver:
   ```
   Editor Version: 2022.3.x LTS  ← verificar que dice 2022.3
   
   Templates:
   ○ 2D
   ○ 3D                          ← seleccionar este
   ● 3D (URP)                    ← o este (cualquiera sirve)
   ○ AR Mobile
   ○ VR Core
   ```
   Selecciona **"3D (URP)"** haciendo clic sobre él (debe quedar resaltado en azul).

3. En la sección inferior, configura:
   ```
   Project name: lab_11_inputs    ← escribe exactamente esto
   Location: (deja la ruta por defecto o elige tu carpeta preferida)
   ```

   **IMPORTANTE:** El nombre `lab_11_inputs` debe estar en minúsculas y con guiones bajos, sin espacios ni mayúsculas.

4. Haz clic en el botón azul **"Create project"**

5. Unity tardará entre 1 y 3 minutos en crear el proyecto. Verás una barra de progreso. **NO cierres Unity Hub durante este tiempo.**

**Lo que debes ver cuando termine:**
- Se abre Unity Editor (la ventana principal de Unity)
- En el centro hay una escena 3D vacía con una cuadrícula gris
- Hay varias ventanas: Scene, Game, Hierarchy, Inspector, Project

```
┌────────────┬──────────────────────────────┬──────────────┐
│ Hierarchy  │          Scene               │  Inspector   │
│            │    (vista 3D de la escena)   │              │
│ SampleScene│                              │ (vacío)      │
│  Main Cam  │                              │              │
│  Dir Light │                              │              │
├────────────┴──────────────────────────────┴──────────────┤
│                     Project / Console                     │
└───────────────────────────────────────────────────────────┘
```

---

## PARTE B — INSTALAR LOS PAQUETES DE AR

### PASO B-1 — Abrir el Package Manager (1 min)

1. En la barra de menú superior (la barra con File, Edit, Assets, etc.), haz clic en **Window**
2. En el menú desplegable, busca y haz clic en **Package Manager**

Se abre una ventana llamada "Package Manager". Esta ventana te permite instalar extensiones de Unity.

**Lo que ves:**
```
┌────────────────────────────────────────────────────────┐
│ Package Manager                                         │
│                                                         │
│  Packages:  [Unity Registry ▼]                          │
│  ──────────────────────────────                         │
│  2D Animation                           5.x    Install  │
│  AR Foundation                          5.x    Install  │  ← busca este
│  Addressables                           1.x    ...      │
│  ...                                                    │
└────────────────────────────────────────────────────────┘
```

**Si ves "In Project" en lugar de "Unity Registry":**
Haz clic en el menú desplegable que dice "In Project" y cámbialo a **"Unity Registry"**. Esto muestra todos los paquetes disponibles, no solo los instalados.

---

### PASO B-2 — Instalar AR Foundation (2 min)

1. En el buscador del Package Manager (arriba a la derecha), escribe: `AR Foundation`
2. Aparecerá en la lista. Haz clic sobre **"AR Foundation"** para seleccionarlo
3. En el panel derecho verás la descripción. Verifica que la versión sea **5.x** (ejemplo: 5.1.5)
4. Haz clic en el botón azul **"Install"** (esquina inferior derecha)
5. Espera a que termine de instalar (la rueda de carga desaparece cuando termina)

**Señal de éxito:** aparece un pequeño ícono de check verde junto al nombre del paquete.

---

### PASO B-3 — Instalar Google ARCore XR Plugin (2 min)

1. En el buscador del Package Manager, borra lo anterior y escribe: `ARCore`
2. Selecciona **"Google ARCore XR Plugin"**
3. Verifica versión **5.x**
4. Haz clic en **"Install"**
5. Espera

---

### PASO B-4 — Instalar XR Interaction Toolkit (2 min)

1. En el buscador, escribe: `XR Interaction Toolkit`
2. Selecciona **"XR Interaction Toolkit"**
3. Verifica versión **2.5.x**
4. Haz clic en **"Install"**

**IMPORTANTE — ventana emergente:**
Unity puede mostrar una ventana preguntando si quieres activar el "new Input System backend". Haz clic en **"Yes"** o **"Enable"**. Unity se reiniciará automáticamente.

**Si Unity se reinicia:** es normal. Vuelve a abrir tu proyecto cuando termine.

5. Después de instalar, en el panel derecho del Package Manager verás una pestaña **"Samples"**. Haz clic en ella.
6. Busca **"XR Device Simulator"** y haz clic en **"Import"**
7. Espera a que importe (aparecerá en tu carpeta Assets)

---

### PASO B-5 — Configurar XR Plug-in Management (2 min)

1. En la barra de menú, haz clic en **Edit**
2. Haz clic en **Project Settings...**
3. Se abre la ventana "Project Settings" con muchas secciones en la izquierda
4. Busca y haz clic en **"XR Plug-in Management"** (en el lado izquierdo)
5. Verás pestañas en la parte superior: Windows, Android, iOS, etc.

**Configurar para Android:**
6. Haz clic en la pestaña con el ícono de Android (robot verde)
7. Activa la casilla **"ARCore"** (haz clic en ella hasta que aparezca el check ☑)

**Configurar para el Editor (para probar en PC):**
8. Haz clic en la pestaña de escritorio (ícono de monitor)
9. Si ves **"XR Simulation"**, actívalo. Si no aparece, está bien — usaremos el Device Simulator.

---

### PASO B-6 — Configurar Input Handling (1 min)

**¿Por qué?** Unity tiene dos sistemas de detección de entrada (Input): uno antiguo y uno nuevo. Para este lab usaremos el antiguo (más simple), pero debemos asegurarnos de que esté activo.

1. Sigue en la ventana "Project Settings"
2. En el lado izquierdo, busca y haz clic en **"Player"**
3. Busca la sección **"Other Settings"** (puede que tengas que hacer scroll hacia abajo)
4. Dentro de "Other Settings", busca **"Active Input Handling"**
5. Haz clic en el menú desplegable y selecciona **"Both"**

```
Active Input Handling: [Both ▼]
                        Input Manager (Old)
                     ● Both
                        Input System Package (New)
```

6. Unity puede pedir reiniciar → haz clic en **"Apply"** o **"Restart"**

---

## PARTE C — CONFIGURAR LA ESCENA AR

### PASO C-1 — Limpiar la escena (1 min)

La escena nueva tiene dos objetos que no necesitamos para AR:

1. Mira la ventana **Hierarchy** (lista de objetos a la izquierda)
2. Verás:
   ```
   Hierarchy
   └── SampleScene
       ├── Main Camera       ← eliminar
       └── Directional Light ← eliminar
   ```
3. Haz clic en **"Main Camera"** para seleccionarlo (se resalta en azul)
4. Presiona la tecla **Delete** (o Backspace en Mac) → el objeto desaparece de la lista
5. Haz clic en **"Directional Light"**
6. Presiona **Delete**

**Resultado esperado:**
```
Hierarchy
└── SampleScene
    (vacío — no hay objetos)
```

---

### PASO C-2 — Agregar AR Session (1 min)

AR Session es el componente que activa el sistema de Realidad Aumentada (ARCore).

1. En la ventana **Hierarchy**, haz **clic derecho** en un área vacía
2. En el menú que aparece, pasa el cursor sobre **"XR"**
3. En el submenú, haz clic en **"AR Session"**

**Lo que ves en Hierarchy:**
```
Hierarchy
└── SampleScene
    └── AR Session       ← nuevo objeto creado
```

4. Haz clic en **"AR Session"** en la Hierarchy
5. Mira el **Inspector** (panel derecho) — debes ver dos componentes: "AR Session" y "AR Input Manager"

---

### PASO C-3 — Agregar XR Origin (1 min)

XR Origin es la "cámara AR" — el origen del mundo de realidad aumentada.

1. En la ventana **Hierarchy**, haz **clic derecho** en un área vacía
2. Pasa el cursor sobre **"XR"**
3. Haz clic en **"XR Origin (Mobile AR)"**

   > **Nota:** si no ves esta opción, busca "AR Session Origin" — es el nombre en versiones más antiguas de AR Foundation.

**Lo que ves en Hierarchy:**
```
Hierarchy
└── SampleScene
    ├── AR Session
    └── XR Origin (Mobile AR)
        └── Camera Offset
            └── Main Camera     ← esta es la cámara AR
```

---

### PASO C-4 — Agregar componentes al XR Origin (2 min)

1. Haz clic en **"XR Origin (Mobile AR)"** en la Hierarchy para seleccionarlo
2. Mira el **Inspector** — verás los componentes actuales del objeto

3. **Agregar AR Plane Manager:**
   - Haz clic en el botón **"Add Component"** (al final del Inspector)
   - En el buscador que aparece, escribe: `AR Plane Manager`
   - Haz clic en **"AR Plane Manager"** cuando aparezca en la lista
   - Aparece el componente en el Inspector

4. **Configurar AR Plane Manager:**
   En el componente "AR Plane Manager" que aparece:
   - Campo **"Plane Prefab"**: haz clic en el círculo pequeño a la derecha del campo → se abre una ventana de selección → busca `AR Default Plane` y haz doble clic
   - Campo **"Detection Mode"**: haz clic en el desplegable y selecciona **"Horizontal"**

5. **Agregar AR Raycast Manager:**
   - Haz clic en **"Add Component"** de nuevo
   - Escribe: `AR Raycast Manager`
   - Haz clic en **"AR Raycast Manager"**

**Resultado en Inspector de XR Origin:**
```
Inspector — XR Origin (Mobile AR)
├── Transform
├── XR Origin (Script)
├── AR Plane Manager (Script)
│   ├── Plane Prefab: AR Default Plane
│   └── Detection Mode: Horizontal
└── AR Raycast Manager (Script)
```

---

### PASO C-5 — Crear la UI de texto (3 min)

El texto en pantalla que mostrará qué gesto detectamos.

1. En la **Hierarchy**, haz **clic derecho** en área vacía
2. Pasa el cursor sobre **"UI"**
3. Haz clic en **"Canvas"**

   Se crea un Canvas. Unity puede preguntarte si quieres importar los recursos de TextMeshPro — haz clic en **"Import TMP Essentials"**.

4. Ahora haz **clic derecho** sobre el **"Canvas"** (no en área vacía — sobre el objeto Canvas)
5. Ve a **"UI"** → **"Text - TextMeshPro"**

6. Se crea un objeto de texto dentro del Canvas. En la Hierarchy:
   ```
   Canvas
   └── Text (TMP)    ← renombrar esto
   ```

7. Haz **doble clic** sobre "Text (TMP)" en la Hierarchy para renombrarlo
8. Escribe: `TextGesto` y presiona Enter

9. Con `TextGesto` seleccionado, configura en el **Inspector**:

   **Sección Rect Transform (posición y tamaño):**
   - Haz clic en el cuadrado de "Anchors" (el cuadrado con flechas pequeñas)
   - Se abre una grilla de anclaje. Haz clic en la opción **"top center"** (centro arriba)
   - Establece estos valores:
     ```
     Pos X: 0
     Pos Y: -80
     Width: 600
     Height: 80
     ```

   **Sección TextMeshPro - Text (UI):**
   - **Text**: borra el texto por defecto y escribe: `Gesto detectado`
   - **Font Size**: `36`
   - **Font Style**: Normal
   - **Alignment**: Center (el ícono de texto centrado)
   - **Color**: haz clic en el rectángulo de color → aparece el selector → arrastra la ruedita de brillo a lo más alto (blanco puro) → haz clic en OK

   **Resultado:** el Canvas debe verse en la ventana Game como un texto blanco en la parte superior de la pantalla.

---

### PASO C-6 — Crear el prefab del Cubo (2 min)

El cubo es el objeto 3D que aparecerá en AR.

1. En la **Hierarchy**, haz **clic derecho** en área vacía
2. Ve a **"3D Object"** → **"Cube"**
3. Se crea un cubo. En la Hierarchy verás: `Cube`

4. Con el Cubo seleccionado, en el **Inspector** → sección **Transform**:
   - Cambia la **Scale** a: X = `0.1`, Y = `0.1`, Z = `0.1`
   
   *(Esto lo hace pequeño — 10 cm de lado, un tamaño realista para AR)*

5. Renombra el cubo: haz doble clic en "Cube" en la Hierarchy → escribe `CuboPrefab` → Enter

6. **Crear la carpeta Prefabs:**
   - En la ventana **Project** (panel inferior), haz clic en la carpeta **"Assets"**
   - Haz **clic derecho** en el área de contenidos → **"Create"** → **"Folder"**
   - Escribe: `Prefabs` → Enter

7. **Convertir el cubo en prefab:**
   - En la **Hierarchy**, haz clic y MANTÉN presionado sobre `CuboPrefab`
   - Arrastra hacia la carpeta `Prefabs` en la ventana **Project**
   - Suelta cuando estés sobre la carpeta
   - Unity pregunta "Create Original Prefab?" → haz clic en **"Original Prefab"**

8. El objeto en Hierarchy ahora tiene texto azul = es un prefab ✓

9. **Eliminar el cubo de la escena** (el prefab ya está guardado):
   - Haz clic en `CuboPrefab` en la Hierarchy
   - Presiona **Delete**

**Verificación:**
```
Hierarchy:
├── AR Session
├── XR Origin (Mobile AR)
└── Canvas
    └── TextGesto

Project/Assets/Prefabs:
└── CuboPrefab.prefab  ← debe estar aquí
```

---

## PARTE D — ESCRIBIR EL SCRIPT

### PASO D-1 — Crear la carpeta Scripts (1 min)

1. En la ventana **Project**, haz clic en la carpeta **"Assets"**
2. Haz **clic derecho** → **"Create"** → **"Folder"**
3. Escribe: `Scripts` → Enter

---

### PASO D-2 — Crear el archivo C# (1 min)

1. Haz **clic** en la carpeta **Scripts** para abrirla (ahora está vacía)
2. Haz **clic derecho** en el área vacía de la carpeta
3. Ve a **"Create"** → **"C# Script"**
4. Escribe el nombre: `InputAR` → presiona Enter

   **MUY IMPORTANTE:** el nombre debe ser exactamente `InputAR` con la A y la R mayúsculas. Si lo escribes diferente, tendrás errores.

5. Doble clic en el archivo `InputAR` para abrirlo en Visual Studio (o el editor de código configurado)

---

### PASO D-3 — Escribir el código completo (12 min)

Cuando se abra el editor de código, verás algo así:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InputAR : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

**Borra TODO el contenido** y escribe (o copia) el siguiente código completo:

```csharp
using UnityEngine;
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;
using System.Collections.Generic;
using TMPro;

[RequireComponent(typeof(ARRaycastManager))]
public class InputAR : MonoBehaviour
{
    [Header("Configuración")]
    public GameObject prefabObjeto;
    public TextMeshProUGUI textoGesto;
    public float velocidadRotacion = 0.4f;
    public float sensibilidadPinch = 1.0f;

    private ARRaycastManager raycastManager;
    private List<ARRaycastHit> hits = new List<ARRaycastHit>();
    private GameObject objetoAR;

    private float distanciaInicialPinch;
    private float escalaInicialPinch;

    void Awake() => raycastManager = GetComponent<ARRaycastManager>();

    void Update()
    {
        if (Input.touchCount == 0) return;

        if (Input.touchCount == 2)
        {
            MostrarGesto("PINCH - escalar");
            ManejarPinch();
        }
        else if (Input.touchCount == 1)
        {
            Touch t = Input.GetTouch(0);

            if (t.phase == TouchPhase.Began)
            {
                MostrarGesto("TAP en " + t.position.ToString());
                ManejarTap(t.position);
            }
            else if (t.phase == TouchPhase.Moved && objetoAR != null)
            {
                if (Mathf.Abs(t.deltaPosition.x) > 5f)
                {
                    string dir = t.deltaPosition.x > 0 ? "SWIPE ->" : "SWIPE <-";
                    MostrarGesto(dir);
                    ManejarRotacion(t);
                }
            }
        }
    }

    void ManejarTap(Vector2 posicion)
    {
        hits.Clear();
        if (raycastManager.Raycast(posicion, hits, TrackableType.PlaneWithinPolygon))
        {
            Pose pose = hits[0].pose;
            if (objetoAR == null)
                objetoAR = Instantiate(prefabObjeto, pose.position, pose.rotation);
            else
                objetoAR.transform.SetPositionAndRotation(pose.position, pose.rotation);
        }
    }

    void ManejarRotacion(Touch t)
    {
        float angulo = -t.deltaPosition.x * velocidadRotacion;
        objetoAR.transform.Rotate(Vector3.up, angulo, Space.World);
    }

    void ManejarPinch()
    {
        if (objetoAR == null) return;

        Touch t0 = Input.GetTouch(0);
        Touch t1 = Input.GetTouch(1);

        if (t0.phase == TouchPhase.Began || t1.phase == TouchPhase.Began)
        {
            distanciaInicialPinch = Vector2.Distance(t0.position, t1.position);
            escalaInicialPinch = objetoAR.transform.localScale.x;
            return;
        }

        float distanciaActual = Vector2.Distance(t0.position, t1.position);
        float factor = distanciaActual / distanciaInicialPinch;
        float nuevaEscala = Mathf.Clamp(
            escalaInicialPinch * factor * sensibilidadPinch,
            0.05f, 3f);

        objetoAR.transform.localScale = Vector3.one * nuevaEscala;
    }

    void MostrarGesto(string mensaje)
    {
        if (textoGesto != null)
            textoGesto.text = mensaje;
    }
}
```

**Después de escribir el código:**
1. Guarda el archivo: **Ctrl + S** (Windows) o **Cmd + S** (Mac)
2. Vuelve a Unity (haz clic en la barra de tareas o Alt+Tab)
3. Espera a que Unity compile el script (verás un pequeño ícono girando en la esquina inferior derecha)
4. Cuando termine, mira la ventana **Console** (panel inferior) — NO deben aparecer mensajes de error en rojo

**Si hay errores en rojo:** vuelve al código y compara línea por línea con el código de arriba.

---

## PARTE E — CONECTAR TODO EN UNITY

### PASO E-1 — Agregar el script al XR Origin (2 min)

1. Haz clic en **"XR Origin (Mobile AR)"** en la Hierarchy
2. En el **Inspector**, haz clic en **"Add Component"**
3. Escribe `InputAR` en el buscador
4. Haz clic en **"InputAR"** cuando aparezca

**Verificación — Inspector de XR Origin debe tener:**
```
Inspector — XR Origin (Mobile AR)
├── Transform
├── XR Origin (Script)
├── AR Plane Manager (Script)
├── AR Raycast Manager (Script)
└── Input AR (Script)            ← recién agregado
    ├── Prefab Objeto:  None (GameObject)
    ├── Texto Gesto:    None (TextMeshProUGUI)
    ├── Velocidad Rotacion: 0.4
    └── Sensibilidad Pinch: 1
```

---

### PASO E-2 — Conectar el Prefab del Cubo (1 min)

El campo "Prefab Objeto" en el script necesita saber qué objeto instanciar.

1. Con **XR Origin** seleccionado (para ver su Inspector)
2. En la ventana **Project**, navega a `Assets/Prefabs/`
3. Haz clic en `CuboPrefab` en el Project
4. **ARRASTRA** (mantén presionado y mueve) el `CuboPrefab` desde la ventana Project hasta el campo **"Prefab Objeto"** en el Inspector del script InputAR
5. Suelta cuando el campo se resalte en azul

**Verificación:**
```
Input AR (Script)
├── Prefab Objeto:  CuboPrefab  ← ya no dice "None"
```

---

### PASO E-3 — Conectar el TextGesto (1 min)

El campo "Texto Gesto" necesita saber qué objeto de texto actualizar.

1. Sigue con **XR Origin** seleccionado (Inspector visible)
2. En la **Hierarchy**, haz clic en **"TextGesto"** (que está dentro del Canvas)
3. **ARRASTRA** "TextGesto" desde la Hierarchy hasta el campo **"Texto Gesto"** en el Inspector del script InputAR
4. Suelta cuando el campo se resalte

**Verificación:**
```
Input AR (Script)
├── Prefab Objeto:  CuboPrefab
├── Texto Gesto:    TextGesto (TextMeshProUGUI)  ← conectado
```

---

## PARTE F — PROBAR EN EL EDITOR

### PASO F-1 — Agregar XR Device Simulator a la escena (2 min)

El XR Device Simulator te permite probar la app sin un celular físico.

1. En la ventana **Project**, navega a:
   ```
   Assets → Samples → XR Interaction Toolkit → 2.5.x → XR Device Simulator
   ```
   
   Si no ves la carpeta Samples, la importación aún no terminó — espera un momento.

2. Dentro de esa carpeta verás un prefab llamado **"XR Device Simulator"** (tiene un ícono especial de prefab, azul)

3. **Arrastra** ese prefab desde el Project hasta la **Hierarchy** (en un área vacía)

4. En la Hierarchy ahora tienes:
   ```
   ├── AR Session
   ├── XR Origin (Mobile AR)
   ├── Canvas
   │   └── TextGesto
   └── XR Device Simulator      ← nuevo
   ```

---

### PASO F-2 — Presionar Play y probar (3 min)

1. Busca los botones en la parte superior central de Unity:
   ```
   ▶️ ⏸ ⏭
   ```
2. Haz clic en **▶️ (Play)**

3. La pantalla de Unity cambia: la ventana **Game** pasa al frente y muestra lo que vería el usuario.

4. **Probar el TAP (clic de ratón = un toque):**
   - Haz clic izquierdo en algún lugar de la ventana Game
   - Debes ver en la parte superior el texto: `TAP en (x, y)`
   
   > Si el cubo no aparece, es porque Unity necesita un "plano AR" para colocar el objeto, y en el editor no hay cámara real. El texto del gesto sí debe aparecer.

5. Para salir del modo Play: haz clic en **▶️** de nuevo (el ícono se vuelve "stop")

---

### PASO F-3 — Verificar en la Consola (1 min)

1. Haz clic en la pestaña **"Console"** (panel inferior)
2. Verifica que NO haya líneas rojas de error
3. Puede haber líneas amarillas (advertencias) — están bien por ahora

```
Console
──────────────────────────────────────────────────────
  (sin mensajes rojos = todo está bien)
```

---

## PARTE G — GUARDAR LA ESCENA Y HACER COMMIT

### PASO G-1 — Guardar la escena (1 min)

1. Presiona **Ctrl + S** (Windows) o **Cmd + S** (Mac)
2. Si Unity pregunta el nombre de la escena, escribe: `EscenaAR_S11` → Save

---

### PASO G-2 — Hacer commit en GitHub (3 min)

1. Abre tu terminal (CMD en Windows, Terminal en Mac)
2. Navega hasta la carpeta del repositorio del curso. Pregunta al docente la ruta si no la sabes. Generalmente es:
   ```bash
   cd ~/Desktop/rva-2026-1-uap
   ```
3. Copia los archivos del proyecto (pregunta al docente dónde deben ir, generalmente en la carpeta `entregas/`)
4. Ejecuta estos comandos uno por uno:

   ```bash
   git status
   ```
   Verás los archivos nuevos o modificados en color rojo/verde.

   ```bash
   git add .
   ```
   Prepara todos los cambios para el commit.

   ```bash
   git commit -m "feat(s11): implementar InputAR con tap swipe pinch"
   ```
   Crea el commit con el mensaje descriptivo.

   ```bash
   git push
   ```
   Sube los cambios a GitHub.

5. Si Git pide usuario/contraseña, usa las credenciales de tu cuenta GitHub.

---

## CHECKLIST FINAL — LAB EN CLASE

Marca cada casilla cuando lo hayas completado:

```
☐  Proyecto Unity creado con nombre "lab_11_inputs"
☐  AR Foundation 5.x instalado
☐  Google ARCore XR Plugin 5.x instalado
☐  XR Interaction Toolkit 2.5.x instalado (con Device Simulator)
☐  Active Input Handling configurado en "Both"
☐  AR Session en la Hierarchy
☐  XR Origin (Mobile AR) con AR Plane Manager y AR Raycast Manager
☐  Canvas con TextGesto (texto blanco, arriba centrado)
☐  CuboPrefab en Assets/Prefabs/
☐  Script InputAR.cs sin errores en Console
☐  Prefab Objeto → CuboPrefab conectado
☐  Texto Gesto → TextGesto conectado
☐  Al hacer Play y clic, el texto UI muestra "TAP en..."
☐  Sin errores rojos en Console
☐  Commit realizado con mensaje "feat(s11): implementar InputAR..."
```

---

## ERRORES COMUNES Y CÓMO RESOLVERLOS

| Síntoma | Causa | Solución paso a paso |
|---------|-------|---------------------|
| Error rojo: `The type or namespace name 'TMPro' could not be found` | TextMeshPro no importado | Window → TextMeshPro → Import TMP Essential Resources |
| Error rojo: `The type or namespace 'ARRaycastManager' does not exist` | AR Foundation no instalado | Window → Package Manager → AR Foundation → Install |
| Error: `'InputAR' class name does not match file name` | El archivo se llama diferente al script | Renombra el archivo o la clase para que coincidan |
| El texto UI no aparece en Play | TextGesto no conectado al script | Seleccionar XR Origin → arrastrar TextGesto al campo "Texto Gesto" |
| El cubo no aparece al hacer clic | CuboPrefab no conectado | Seleccionar XR Origin → arrastrar CuboPrefab al campo "Prefab Objeto" |
| No hay respuesta a los clics | Active Input Handling en "New" | Project Settings → Player → Other Settings → Active Input Handling → Both |
| Unity queda en negro al presionar Play | Falta el XR Device Simulator | Arrastrarlo desde Project a Hierarchy |
| `NullReferenceException` en Console | Una referencia está en None | Revisar todos los campos del script InputAR en Inspector |

---

*PSISP08075 | Universidad Autónoma del Perú | Ingeniería de Sistemas | Semana 11 | 2026-1*
