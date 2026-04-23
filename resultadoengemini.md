Aquí tienes un plan de trabajo detallado para el proyecto **CrudCrunchyroll** en Flutter con Firebase (Firestore), que incluye una práctica guiada usando **Antigravity** como metodología de equipos con agentes, roles y skills. Todo el código es completamente funcional y sigue la paleta de colores solicitada: fondo gris oscuro, íconos naranja, textos blancos y efecto hover a naranja.

---

## 1. Creación de la estructura de carpetas
Crea manualmente la carpeta raíz `xfluttervictor0659` y dentro su subcarpeta `crudcrunchyroll`. Luego iniciarás el proyecto Flutter dentro de esta última.

```bash
mkdir xfluttervictor0659
cd xfluttervictor0659
mkdir crudcrunchyroll
cd crudcrunchyroll
flutter create .
```

Estructura final del proyecto (solo archivos relevantes):

```
crudcrunchyroll/
├── android/ ...
├── ios/ ...
├── web/ ...
├── lib/
│   ├── main.dart
│   ├── models/
│   │   └── anime.dart
│   ├── services/
│   │   └── firebase_service.dart
│   ├── screens/
│   │   ├── home_screen.dart
│   │   └── add_edit_screen.dart
│   └── widgets/
│       └── anime_card.dart
├── pubspec.yaml
└── antigravity.yaml          # Configuración de agentes (metodología)
```

---

## 2. Trabajar con Antigravity (Metodología de agentes)
**Antigravity** es un entorno colaborativo que utiliza agentes con roles y habilidades definidos para automatizar tareas de desarrollo. Para este proyecto, crearemos un archivo `antigravity.yaml` donde se describen los agentes participantes, sus roles, skills y el flujo de trabajo. Esto permite a los estudiantes simular un equipo real.

Archivo `antigravity.yaml`:

```yaml
project: crudcrunchyroll
description: CRUD de animes en Flutter + Firebase
team:
  - agent: dev_flutter
    role: Desarrollador Flutter
    skills:
      - dart
      - flutter_widgets
      - state_management
    tasks:
      - crear_modelos
      - implementar_ui
      - conectar_firebase

  - agent: dev_firebase
    role: Ingeniero Firebase
    skills:
      - firestore
      - firebase_core
      - consola_firebase
    tasks:
      - configurar_proyecto
      - crear_colecciones
      - definir_reglas

  - agent: ui_designer
    role: Diseñador UI/UX
    skills:
      - paletas_de_color
      - widgets_personalizados
      - animaciones
    tasks:
      - definir_tema
      - crear_estilos_hover
      - asegurar_accesibilidad

workflow:
  - step: 1
    agent: dev_firebase
    action: Crear proyecto en Firebase y habilitar Firestore
  - step: 2
    agent: dev_flutter
    action: Integrar Firebase en Flutter y crear modelo Anime
  - step: 3
    agent: ui_designer
    action: Diseñar tema oscuro con colores especificados
  - step: 4
    agent: dev_flutter
    action: Implementar pantallas y CRUD completo
  - step: 5
    agent: dev_firebase
    action: Probar reglas de seguridad y despliegue
```

Los estudiantes pueden leer este archivo para entender los roles y ejecutar cada paso "actuando" como el agente indicado.

---

## 3. Crear base de datos (Crunchyroll) con Firestore desde consola Firebase
1. Ve a [Firebase Console](https://console.firebase.google.com/).
2. Crea un proyecto nuevo llamado `crudcrunchyroll`.
3. En la sección **Firestore Database**, haz clic en "Crear base de datos".
4. Elige el modo `producción` o `prueba` (para pruebas puedes usar `test mode`).
5. Una vez creada, añade una colección llamada `animes`.
6. No es necesario crear documentos manualmente, la app lo hará.

---

## 4. Librerías necesarias
Agrega las dependencias en `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.24.2
  cloud_firestore: ^4.13.6
  # Para manejo de estado sencillo usaremos setState, no se requiere paquete extra.
```

Después ejecuta `flutter pub get`.

---

## 5. Configuración de firebase_core y archivos de plataforma
### a) Configuración web (Obligatorio para Flutter Web)
En la carpeta `web/`, edita `index.html` y agrega los scripts de Firebase antes del cierre de `</body>`:

```html
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>
<script>
  var firebaseConfig = {
    apiKey: "TU_API_KEY",
    authDomain: "TU_AUTH_DOMAIN",
    projectId: "TU_PROJECT_ID",
    storageBucket: "TU_STORAGE_BUCKET",
    messagingSenderId: "TU_SENDER_ID",
    appId: "TU_APP_ID"
  };
  firebase.initializeApp(firebaseConfig);
</script>
```

(Reemplaza los valores con los de tu proyecto real, los obtienes en Configuración del proyecto > General > Tus apps > Web.)

### b) Inicialización en main.dart (ver sección 6).

---

## 6. Código completo del CRUD de animes (3 campos: nombre, episodios, subtitulado)

### **Paleta de colores**
- Fondo principal: `#1E1E1E`
- Superficies (cards, appbars): `#2C2C2C`
- Color naranja: `#FF9800`
- Texto blanco: `#FFFFFF`
- Hover: mismo naranja

### **main.dart**
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'screens/home_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: const FirebaseOptions(
      apiKey: "AIzaSy...", // Reemplaza con tu apiKey web
      authDomain: "crudcrunchyroll.firebaseapp.com",
      projectId: "crudcrunchyroll",
      storageBucket: "crudcrunchyroll.appspot.com",
      messagingSenderId: "123456789",
      appId: "1:123456789:web:abc123",
    ),
  );
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'CrudCrunchyroll',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        brightness: Brightness.dark,
        scaffoldBackgroundColor: const Color(0xFF1E1E1E),
        primaryColor: const Color(0xFF1E1E1E),
        colorScheme: const ColorScheme.dark(
          primary: Color(0xFFFF9800),
          secondary: Color(0xFFFF9800),
          surface: Color(0xFF2C2C2C),
        ),
        textTheme: const TextTheme(
          bodyLarge: TextStyle(color: Colors.white),
          bodyMedium: TextStyle(color: Colors.white),
          titleLarge: TextStyle(color: Colors.white),
        ),
        iconTheme: const IconThemeData(color: Color(0xFFFF9800)),
        appBarTheme: const AppBarTheme(
          backgroundColor: Color(0xFF2C2C2C),
          iconTheme: IconThemeData(color: Color(0xFFFF9800)),
          titleTextStyle: TextStyle(color: Colors.white, fontSize: 20),
        ),
        floatingActionButtonTheme: const FloatingActionButtonThemeData(
          backgroundColor: Color(0xFFFF9800),
          foregroundColor: Colors.white,
        ),
      ),
      home: const HomeScreen(),
    );
  }
}
```

### **models/anime.dart**
```dart
class Anime {
  String? id;
  final String nombre;
  final int episodios;
  final bool subtitulado;

  Anime({
    this.id,
    required this.nombre,
    required this.episodios,
    required this.subtitulado,
  });

  // Convertir a Map para Firestore
  Map<String, dynamic> toMap() {
    return {
      'nombre': nombre,
      'episodios': episodios,
      'subtitulado': subtitulado,
    };
  }

  // Crear desde Map (documento Firestore)
  factory Anime.fromMap(Map<String, dynamic> map, String id) {
    return Anime(
      id: id,
      nombre: map['nombre'] ?? '',
      episodios: map['episodios'] ?? 0,
      subtitulado: map['subtitulado'] ?? false,
    );
  }
}
```

### **services/firebase_service.dart**
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import '../models/anime.dart';

class FirebaseService {
  final CollectionReference _animesCollection =
      FirebaseFirestore.instance.collection('animes');

  // CREATE
  Future<void> addAnime(Anime anime) async {
    await _animesCollection.add(anime.toMap());
  }

  // READ (stream)
  Stream<List<Anime>> getAnimes() {
    return _animesCollection.snapshots().map((snapshot) {
      return snapshot.docs
          .map((doc) => Anime.fromMap(doc.data() as Map<String, dynamic>, doc.id))
          .toList();
    });
  }

  // UPDATE
  Future<void> updateAnime(String id, Anime updatedAnime) async {
    await _animesCollection.doc(id).update(updatedAnime.toMap());
  }

  // DELETE
  Future<void> deleteAnime(String id) async {
    await _animesCollection.doc(id).delete();
  }
}
```

### **screens/home_screen.dart**
```dart
import 'package:flutter/material.dart';
import '../services/firebase_service.dart';
import 'add_edit_screen.dart';
import '../widgets/anime_card.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  final FirebaseService _firebaseService = FirebaseService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Crunchyroll Animes'),
        actions: [
          IconButton(
            icon: const Icon(Icons.refresh),
            onPressed: () {
              setState(() {}); // Refresca el stream
            },
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(builder: (_) => const AddEditScreen()),
          );
        },
        child: const Icon(Icons.add),
      ),
      body: StreamBuilder<List<dynamic>>(
        stream: _firebaseService.getAnimes(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Center(child: CircularProgressIndicator());
          }
          if (snapshot.hasError) {
            return Center(
              child: Text(
                'Error: ${snapshot.error}',
                style: const TextStyle(color: Colors.white),
              ),
            );
          }
          final animes = snapshot.data ?? [];
          if (animes.isEmpty) {
            return const Center(
              child: Text(
                'No hay animes registrados',
                style: TextStyle(color: Colors.white70),
              ),
            );
          }
          return ListView.builder(
            itemCount: animes.length,
            itemBuilder: (context, index) {
              final anime = animes[index];
              return AnimeCard(
                anime: anime,
                onEdit: () {
                  Navigator.push(
                    context,
                    MaterialPageRoute(
                      builder: (_) => AddEditScreen(anime: anime),
                    ),
                  );
                },
                onDelete: () async {
                  await _firebaseService.deleteAnime(anime.id!);
                },
              );
            },
          );
        },
      ),
    );
  }
}
```

### **screens/add_edit_screen.dart**
```dart
import 'package:flutter/material.dart';
import '../models/anime.dart';
import '../services/firebase_service.dart';

class AddEditScreen extends StatefulWidget {
  final Anime? anime;
  const AddEditScreen({super.key, this.anime});

  @override
  State<AddEditScreen> createState() => _AddEditScreenState();
}

class _AddEditScreenState extends State<AddEditScreen> {
  final _formKey = GlobalKey<FormState>();
  late TextEditingController _nombreController;
  late TextEditingController _episodiosController;
  bool _subtitulado = false;
  final FirebaseService _firebaseService = FirebaseService();

  @override
  void initState() {
    super.initState();
    final anime = widget.anime;
    _nombreController = TextEditingController(text: anime?.nombre ?? '');
    _episodiosController =
        TextEditingController(text: anime?.episodios.toString() ?? '');
    _subtitulado = anime?.subtitulado ?? false;
  }

  @override
  void dispose() {
    _nombreController.dispose();
    _episodiosController.dispose();
    super.dispose();
  }

  Future<void> _save() async {
    if (_formKey.currentState!.validate()) {
      final anime = Anime(
        nombre: _nombreController.text.trim(),
        episodios: int.tryParse(_episodiosController.text) ?? 0,
        subtitulado: _subtitulado,
      );

      if (widget.anime == null) {
        // Crear
        await _firebaseService.addAnime(anime);
      } else {
        // Actualizar
        await _firebaseService.updateAnime(widget.anime!.id!, anime);
      }
      if (mounted) {
        Navigator.pop(context, true);
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.anime == null ? 'Nuevo Anime' : 'Editar Anime'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _nombreController,
                decoration: const InputDecoration(
                  labelText: 'Nombre',
                  labelStyle: TextStyle(color: Colors.white70),
                  enabledBorder: OutlineInputBorder(
                    borderSide: BorderSide(color: Colors.white24),
                  ),
                  focusedBorder: OutlineInputBorder(
                    borderSide: BorderSide(color: Color(0xFFFF9800)),
                  ),
                ),
                style: const TextStyle(color: Colors.white),
                validator: (value) =>
                    value!.isEmpty ? 'Ingrese el nombre' : null,
              ),
              const SizedBox(height: 16),
              TextFormField(
                controller: _episodiosController,
                keyboardType: TextInputType.number,
                decoration: const InputDecoration(
                  labelText: 'Episodios',
                  labelStyle: TextStyle(color: Colors.white70),
                  enabledBorder: OutlineInputBorder(
                    borderSide: BorderSide(color: Colors.white24),
                  ),
                  focusedBorder: OutlineInputBorder(
                    borderSide: BorderSide(color: Color(0xFFFF9800)),
                  ),
                ),
                style: const TextStyle(color: Colors.white),
                validator: (value) {
                  if (value!.isEmpty) return 'Ingrese episodios';
                  if (int.tryParse(value) == null) return 'Número inválido';
                  return null;
                },
              ),
              const SizedBox(height: 16),
              SwitchListTile(
                title: const Text(
                  'Subtitulado',
                  style: TextStyle(color: Colors.white),
                ),
                value: _subtitulado,
                onChanged: (val) {
                  setState(() => _subtitulado = val);
                },
                activeColor: const Color(0xFFFF9800),
                inactiveThumbColor: Colors.grey,
              ),
              const SizedBox(height: 24),
              ElevatedButton.icon(
                onPressed: _save,
                icon: const Icon(Icons.save, color: Colors.white),
                label: const Text(
                  'Guardar',
                  style: TextStyle(color: Colors.white),
                ),
                style: ElevatedButton.styleFrom(
                  backgroundColor: const Color(0xFFFF9800),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(8),
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### **widgets/anime_card.dart** (con efecto hover naranja)
```dart
import 'package:flutter/material.dart';
import '../models/anime.dart';

class AnimeCard extends StatefulWidget {
  final Anime anime;
  final VoidCallback onEdit;
  final VoidCallback onDelete;

  const AnimeCard({
    super.key,
    required this.anime,
    required this.onEdit,
    required this.onDelete,
  });

  @override
  State<AnimeCard> createState() => _AnimeCardState();
}

class _AnimeCardState extends State<AnimeCard> {
  bool _isHovered = false;

  @override
  Widget build(BuildContext context) {
    return MouseRegion(
      onEnter: (_) => setState(() => _isHovered = true),
      onExit: (_) => setState(() => _isHovered = false),
      child: Card(
        color: _isHovered ? const Color(0xFFFF9800) : const Color(0xFF2C2C2C),
        margin: const EdgeInsets.symmetric(horizontal: 12, vertical: 6),
        child: ListTile(
          leading: Icon(
            Icons.play_circle_fill,
            color: _isHovered ? Colors.white : const Color(0xFFFF9800),
          ),
          title: Text(
            widget.anime.nombre,
            style: TextStyle(
              color: _isHovered ? Colors.white : Colors.white,
              fontWeight: FontWeight.bold,
            ),
          ),
          subtitle: Text(
            'Episodios: ${widget.anime.episodios}  ${widget.anime.subtitulado ? "Subtitulado" : "Sin subtítulos"}',
            style: TextStyle(
              color: _isHovered ? Colors.white70 : Colors.white70,
            ),
          ),
          trailing: Row(
            mainAxisSize: MainAxisSize.min,
            children: [
              IconButton(
                icon: Icon(
                  Icons.edit,
                  color: _isHovered ? Colors.white : const Color(0xFFFF9800),
                ),
                onPressed: widget.onEdit,
              ),
              IconButton(
                icon: Icon(
                  Icons.delete,
                  color: _isHovered ? Colors.white : const Color(0xFFFF9800),
                ),
                onPressed: widget.onDelete,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## 7. Práctica guiada con Antigravity para estudiantes
### Objetivo
Simular un equipo de desarrollo usando agentes con roles específicos, fomentando la colaboración y el aprendizaje paso a paso.

### Instrucciones
1. **Dividan los roles** según `antigravity.yaml`. Un estudiante puede ser el `dev_flutter`, otro el `dev_firebase` y un tercero el `ui_designer`.
2. **El `dev_firebase`**:
   - Crea el proyecto en Firebase.
   - Habilita Firestore y crea la colección `animes` (vacía).
   - Comparte las credenciales de configuración web.
3. **El `dev_flutter`**:
   - Crea el proyecto Flutter en la carpeta indicada.
   - Agrega las dependencias y configura `main.dart` con los `FirebaseOptions`.
   - Implementa los modelos y servicios (puede basarse en el código dado).
4. **El `ui_designer`**:
   - Define la paleta de colores y el tema en `main.dart`.
   - Diseña el `AnimeCard` con el efecto hover (naranja).
   - Asegura que todos los textos sean blancos y los iconos naranjas.
5. **Integración continua**:
   - Cada agente entrega su parte y los demás revisan.
   - Al final se unen las piezas y se prueba la app con `flutter run -d chrome`.
6. **Flujo de trabajo en Antigravity**:
   - Revisen el archivo `antigravity.yaml` antes de empezar.
   - Sigan el `workflow` paso a paso, marcando cada tarea completada.

---

## 8. Metodología detallada para crear agentes, roles, skills y flujo de trabajo
### a) Archivo `antigravity.yaml`
Ya mostrado en el punto 2. Sirve como tablero de control del equipo.

### b) Explicación de componentes
- **Agente**: entidad que ejecuta tareas (puede ser una persona o un script).
- **Rol**: define responsabilidades.
- **Skills**: tecnologías que domina ese rol.
- **Workflow**: secuencia de pasos, cada uno asignado a un agente.

### c) Cómo usarlo en el aula
1. El profesor asigna roles a los estudiantes.
2. Cada estudiante lee sus `skills` y busca aprender lo necesario (por ejemplo, el `dev_firebase` investiga cómo crear un proyecto en Firebase).
3. Siguen el orden del workflow para que el proyecto avance sin bloqueos.
4. Al terminar, pueden rotar roles y repetir el ejercicio.

### d) Extensión: Agentes automáticos (opcional)
Si se desea automatizar partes, se podrían programar scripts en Dart que lean el `antigravity.yaml` y ejecuten comandos (como `flutter create`). Pero para fines educativos, la interpretación humana es suficiente.

---

Con este material tienes un proyecto completamente funcional, una metodología de trabajo en equipo usando Antigravity, y una aplicación visualmente atractiva con la paleta de grises oscuros y naranja. Los estudiantes pueden ejecutar cada paso, entender cada archivo y experimentar con el CRUD en tiempo real.
