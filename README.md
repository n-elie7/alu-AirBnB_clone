# AirBnB Clone - The Console

![Python](https://img.shields.io/badge/Python-3.8.5-blue.svg)
![Style](https://img.shields.io/badge/code%20style-pycodestyle-brightgreen.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## Description

This is the first step in building a full-stack AirBnB clone web application. The project implements a command-line interpreter (console) to manage AirBnB-like objects — creating, retrieving, updating, and destroying instances such as `User`, `Place`, `State`, `City`, `Amenity`, and `Review`.

The console serves as the backbone for all future phases of the project, including HTML/CSS templating, database storage, REST API, and front-end integration.

### What it does

- Implements a **BaseModel** parent class that handles initialization, serialization, and deserialization of all instances
- Establishes a serialization/deserialization chain: `Instance ↔ Dictionary ↔ JSON string ↔ File`
- Defines all AirBnB domain classes (`User`, `State`, `City`, `Place`, `Amenity`, `Review`) inheriting from `BaseModel`
- Provides a **FileStorage** engine to persist objects across sessions
- Includes a full **unit test suite** covering all models and the storage engine

### Project Structure

```
AirBnB_clone/
├── console.py              # Entry point for the command interpreter
├── models/
│   ├── __init__.py
│   ├── base_model.py       # BaseModel class
│   ├── user.py             # User class
│   ├── state.py            # State class
│   ├── city.py             # City class
│   ├── place.py            # Place class
│   ├── amenity.py          # Amenity class
│   ├── review.py           # Review class
│   └── engine/
│       ├── __init__.py
│       └── file_storage.py # FileStorage engine
├── tests/
│   └── test_models/
│       ├── test_base_model.py
│       ├── test_user.py
│       └── ...
├── AUTHORS
└── README.md
```

---

## The Command Interpreter

The command interpreter is a custom shell built with Python's `cmd` module. It is limited to managing AirBnB objects and operates in both **interactive** and **non-interactive** modes.

### How to Start It

Make sure `console.py` is executable, then launch it:

```bash
$ ./console.py
```

Or explicitly with Python:

```bash
$ python3 console.py
```

### How to Use It

Once inside the interpreter, you'll see the `(hbnb)` prompt. You can type any of the supported commands below.

**General syntax:**

```
(hbnb) <command> <classname> [<id>] [<attribute> <value>]
```

Or using the alternative dot notation:

```
(hbnb) <classname>.<command>([<id>] [<attribute> <value>])
```

### Supported Commands

| Command | Description |
|---|---|
| `help` | Display help information |
| `quit` | Exit the console |
| `EOF` | Exit the console (Ctrl+D) |
| `create <class>` | Create a new instance and print its `id` |
| `show <class> <id>` | Print the string representation of an instance |
| `destroy <class> <id>` | Delete an instance |
| `all [class]` | Print all instances, optionally filtered by class |
| `update <class> <id> <attr> <value>` | Update an attribute of an instance |
| `count <class>` | Count the number of instances of a class |

### Available Classes

`BaseModel`, `User`, `State`, `City`, `Place`, `Amenity`, `Review`

---

## Examples

### Interactive Mode

```bash
$ ./console.py
(hbnb) help

Documented commands (type help <topic>):
========================================
EOF  all  count  create  destroy  help  quit  show  update

(hbnb) create User
9b1b3b6e-1234-5678-abcd-ef0123456789

(hbnb) show User 9b1b3b6e-1234-5678-abcd-ef0123456789
[User] (9b1b3b6e-1234-5678-abcd-ef0123456789) {'id': '9b1b3b6e-...', 'created_at': datetime.datetime(...), 'updated_at': datetime.datetime(...)}

(hbnb) update User 9b1b3b6e-1234-5678-abcd-ef0123456789 email "user@example.com"

(hbnb) all User
["[User] (9b1b3b6e-...) {'id': '...', 'email': 'user@example.com', ...}"]

(hbnb) destroy User 9b1b3b6e-1234-5678-abcd-ef0123456789

(hbnb) count User
0

(hbnb) quit
$
```

### Non-Interactive Mode

```bash
$ echo "create User" | ./console.py
(hbnb) 9b1b3b6e-1234-5678-abcd-ef0123456789
(hbnb)

$ echo "all" | ./console.py
(hbnb) [...]
(hbnb)

$ cat commands.txt
create Place
all Place
quit

$ cat commands.txt | ./console.py
(hbnb) <new-id>
(hbnb) ["[Place] (...)"]
(hbnb)
```

### Alternative Dot Notation

```bash
(hbnb) User.all()
(hbnb) User.count()
(hbnb) User.show("9b1b3b6e-1234-5678-abcd-ef0123456789")
(hbnb) User.destroy("9b1b3b6e-1234-5678-abcd-ef0123456789")
(hbnb) User.update("9b1b3b6e-...", "first_name", "John")
```

---

## Running Tests

Run the full test suite:

```bash
$ python3 -m unittest discover tests
```

Run a specific test file:

```bash
$ python3 -m unittest tests/test_models/test_base_model.py
```

Tests also pass in non-interactive mode:

```bash
$ echo "python3 -m unittest discover tests" | bash
```

---

## Requirements

- Ubuntu 20.04 LTS
- Python 3.8.5
- pycodestyle 2.7.*

---

## Authors

See [AUTHORS](./AUTHORS) file.
