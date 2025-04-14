<p align="center"><b>Mobile Programming (2025)</b><br>Sepuluh Nopember Institute of Technology</p>

<p align="center"><img src="https://raw.githubusercontent.com/Rubinskiy/IF184202-Data-Structures/main/its.png" style="transform: scale(0.5);"></p>
  
<p align="center">Source code to a Flutter App that was created for <a href="#">EF234601</a>.</p>
<p align="center">All solutions were created by <a href="https://github.com/Rubinskiy">Robin</a></p>

<hr>

UPDATE: This app now uses Hive, a lightweight and fast NoSQL database, for local data storage. Instead of using in-memory lists, all tasks are persisted to the device's storage.

#### Task Model

A Task model is created to represent a task with properties like `id`, `title`, `description`, and `isCompleted`. The model also includes methods to convert the task to a Map for storage and to create a Task from a Map.

```dart
class Task {
  final String id;
  String title;
  String description;
  bool isCompleted;

  Task({
    required this.id,
    required this.title,
    required this.description,
    this.isCompleted = false,
  });

  // converrt the task to a map foor storage
  Map<String, dynamic> toMap() {
    return {
      'id': id,
      'title': title,
      'description': description,
      'isCompleted': isCompleted,
    };
  }

  // create task from a map
  factory Task.fromMap(Map<String, dynamic> map) {
    return Task(
      id: map['id'],
      title: map['title'],
      description: map['description'],
      isCompleted: map['isCompleted'],
    );
  }
}
```

#### Hive Implementation

1. **Initialization**: Hive is initialized in the main function:
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Hive.initFlutter(); // <-- initialize Hive
  await Hive.openBox('tasks'); // <-- open a box named 'tasks'
  runApp(const MyApp());
}
```

2. **Storage Operations**:
   - **Create**: Tasks are stored as maps using `_taskBox.add(task.toMap())`
   - **Read**: Tasks are retrieved and converted back to task objects using `Task.fromMap()`
   - **Update**: Tasks are updated using `_taskBox.putAt(index, updatedTask.toMap())`
   - **Delete**: Tasks are removed using `_taskBox.deleteAt(index)`

### Dependencies

I'm using Hive 2.2.3 and Hive Flutter 1.1.0.