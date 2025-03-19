# Architecture Document 

## Architecture
This architecture employs Clean Architecture, an industry-standard design pattern that prioritizes separation of concerns, testability, scalability, and maintainability. Implemented in Flutter with Riverpod for state management, this architecture ensures efficient data flow and UI responsiveness. It integrates seamlessly with a Node.js backend utilizing SQL Server and MongoDB databases, providing a modular and adaptable foundation for long-term development. The structure adheres to dependency inversion principles, enabling flexibility and future enhancements.

---
```
##Architecture Structure
my_app/
├── android/                    # Android-specific files
├── ios/                        # iOS-specific files
├── assets/                     # Static assets (images, icons, fonts)
│   ├── bottom_nav_bar_icons/
│   ├── icons/
│   └── images/
├── lib/                        # Main application code
│   ├── core/                   # Shared infrastructure and utilities
│   │   ├── config/             # Configuration files
│   │   ├── network/            # API communication
│   │   ├── di/                 # Dependency injection
│   │   ├── utils/              # Utility functions
│   │   ├── local_storage/      # Local database and caching
│   │   ├── error/              # Error handling
│   ├── domain/                 # Business logic and core definitions
│   │   ├── entities/           # Business entities
│   │   ├── usecases/           # Application-specific business rules
│   │   ├── repositories/       # Abstract repositories
│   ├── data/                   # Data layer for external interactions
│   │   ├── models/             # Data models for API and storage
│   │   ├── datasources/        # API and database data sources
│   │   ├── repositories/       # Repository implementations
│   ├── presentation/           # User interface and state management
│   │   ├── features/           # Feature-specific UI components
│   │   ├── navigation/         # Routing and navigation
│   │   ├── widgets/            # Shared UI components
│   ├── theme/                  # Global theme and styles
│   ├── main.dart               # Application entry point
│   ├── app.dart                # Main app widget
│   ├── routes.dart             # Application navigation routes
├── test/                       # Unit and widget tests
│   ├── features/               # Feature-specific tests
│   ├── integration/            # Integration tests
│   ├── unit/                   # Unit tests
├── build/                      # Output of the build process
├── web/                        # Web-specific files
├── macos/                      # macOS-specific files
├── windows/                    # Windows-specific files
├── linux/                      # Linux-specific files
├── pubspec.yaml                # Project dependencies
├── pubspec.lock                # Locked dependencies
├── README.md                   # Project documentation
├── .gitignore                  # Git ignore rules
├── .metadata                   # Flutter metadata
├── .packages                   # Package configurations
├── analysis_options.yaml       # Linter rules
├── flutter_launcher_icons.yaml # Launcher icons configuration
└── l10n/                       # Localization files
```

## Example Architecture
Below is the project structure implementing Simplified Clean Architecture with Flutter and Riverpod:

```
my_app/
my_healthcare_app/
├── android/
├── ios/
├── assets/
│   ├── icons/
│   ├── images/
│   └── fonts/
├── lib/
│   ├── core/
│   │   ├── config/
│   │   │   └── app_config.dart
│   │   ├── network/
│   │   │   ├── api_client.dart
│   │   │   ├── api_exception.dart
│   │   │   └── network_info.dart
│   │   ├── di/
│   │   │   └── injection.dart
│   │   ├── utils/
│   │   │   └── logger.dart
│   │   ├── local_storage/
│   │   │   └── local_storage.dart
│   │   ├── error/
│   │       └── error_handler.dart
│   ├── domain/
│   │   ├── entities/
│   │   │   ├── user.dart
│   │   │   ├── patient.dart
│   │   │   ├── doctor.dart
│   │   ├── usecases/
│   │   │   ├── auth_usecases.dart
│   │   │   ├── patient_usecases.dart
│   │   │   ├── doctor_usecases.dart
│   │   ├── repositories/
│   │       ├── auth_repository.dart
│   │       ├── patient_repository.dart
│   │       ├── doctor_repository.dart
│   ├── data/
│   │   ├── models/
│   │   │   ├── user_model.dart
│   │   │   ├── patient_model.dart
│   │   │   ├── doctor_model.dart
│   │   ├── datasources/
│   │   │   ├── remote/
│   │   │   │   ├── remote_auth_datasource.dart
│   │   │   │   ├── remote_patient_datasource.dart
│   │   │   │   ├── remote_doctor_datasource.dart
│   │   │   ├── local/
│   │   │       ├── local_auth_datasource.dart
│   │   │       ├── local_patient_datasource.dart
│   │   │       ├── local_doctor_datasource.dart
│   │   ├── repositories/
│   │       ├── auth_repository_impl.dart
│   │       ├── patient_repository_impl.dart
│   │       ├── doctor_repository_impl.dart
│   ├── presentation/
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   ├── patient/
│   │   │   ├── doctor/
│   │   ├── navigation/
│   │   ├── widgets/
│   ├── theme/
│   ├── main.dart
│   ├── app.dart
│   ├── routes.dart
├── test/
│   ├── features/
│   ├── integration/
│   ├── unit/
├── pubspec.yaml
├── README.md
├── .gitignore
└── analysis_options.yaml
```

---

## Detailed Description of Each Folder

### 1. `assets/`
#### Technical Description
The `assets/` directory stores static files such as images, icons, and fonts used in the app. These are typically referenced in the Flutter `pubspec.yaml` file for inclusion in the build process. Subdirectories organize assets by type or purpose for clarity.

#### Layman’s Terms
This is like the app’s photo album and sticker collection. It holds pictures, icons, and fonts that make the app look nice and user-friendly.

#### File Types and Usage
- **File Types**: `.png`, `.jpg`, `.svg` (images/icons), `.ttf` (fonts).
- **How**: Declared in `pubspec.yaml` (e.g., `flutter: assets: - assets/images/`), then loaded in code with `Image.asset()` or `Icon()`.
- **Subdirectories**:
  - `bottom_nav_bar_icons/`: Icons for navigation bar (e.g., home, profile).
  - `icons/`: General-purpose icons.
  - `images/`: Backgrounds, logos, or illustrations.

#### Example
- **File**: `assets/images/logo.png`
  - **Code**: `Image.asset('assets/images/logo.png', width: 100)`
  - **Use**: Displays the app’s logo on the splash screen.

---

### 2. `lib/src/core/`
#### Technical Description
The `core/` directory contains shared utilities and infrastructure that support the app’s operation. It’s a foundational layer providing reusable tools like configuration, networking, dependency injection, utilities, and local storage.

#### Layman’s Terms
This is the app’s toolbox, holding essentials like settings, a phone to call the server, a way to share tools, shortcuts, and a notepad for quick notes.

#### Subdirectories, File Types, and Usage
- **`config/`**: Configuration files.
  - **File**: `app_config.dart`
  - **Content**: Constants or classes for environment settings (e.g., API URLs).
  - **Example**: `const String apiBaseUrl = 'https://api.healthcare-mvp.com';`
  - **Use**: Defines the backend address for API calls.
- **`network/`**: Networking utilities.
  - **Files**: `api_client.dart`, `api_exception.dart`, `network_info.dart`
  - **Content**: HTTP client (e.g., Dio), custom exceptions, connectivity checks.
  - **Example**: `Future<Map<String, dynamic>> post(String endpoint, dynamic data) async { ... }`
  - **Use**: Sends login data to the Node.js backend.
- **`di/`**: Dependency injection setup.
  - **File**: `injection.dart`
  - **Content**: Riverpod providers or a DI framework (e.g., GetIt).
  - **Example**: `final apiClientProvider = Provider((ref) => ApiClient());`
  - **Use**: Shares the API client across the app.
- **`utils/`**: Helper functions.
  - **File**: `logger.dart`
  - **Content**: Logging utility for debugging.
  - **Example**: `void log(String message) => print('[DEBUG] $message');`
  - **Use**: Logs errors or events during development.
- **`local/`**: Local storage management.
  - **File**: `local_storage.dart`
  - **Content**: Functions using packages like `shared_preferences`.
  - **Example**: `Future<void> saveToken(String token) async { ... }`
  - **Use**: Saves a user’s login token locally.

---

### 3. `lib/src/domain/`
#### Technical Description
The `domain/` directory encapsulates the app’s business logic and core data structures. It’s independent of UI and external systems, focusing on the app’s purpose with entities, services, and models.

#### Layman’s Terms
This is the app’s brain, figuring out what things are (entities), how to do stuff (services), and how to understand server info (models).

#### Subdirectories, File Types, and Usage
- **`entities/`**: Core business objects.
  - **Files**: `user.dart`, `patient.dart`, `doctor.dart`
  - **Content**: Plain Dart classes with properties.
  - **Example**: `class Patient { final String id; final String name; Patient({required this.id, required this.name}); }`
  - **Use**: Represents a patient in the app.
- **`services/`**: Business logic and data access.
  - **Files**: `auth_service.dart`, `patient_service.dart`, `doctor_service.dart`
  - **Content**: Functions that call APIs or local storage via `core/`.
  - **Example**: `Future<User> login(String email, String password) async { ... }`
  - **Use**: Logs in a user by calling the backend.
- **`models/`**: Data models for external data.
  - **Files**: `user_model.dart`, `patient_model.dart`, `doctor_model.dart`
  - **Content**: Classes with `fromJson`/`toJson` for API parsing.
  - **Example**: `class UserModel { final String id; UserModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
  - **Use**: Converts raw API data into a usable `User`.

---

### 4. `lib/src/presentation/`
#### Technical Description
The `presentation/` directory handles the UI and state management with Riverpod. It’s organized into feature-specific modules, navigation, and reusable widgets, depending on the `domain/` layer for logic.

#### Layman’s Terms
This is the app’s face—what users see and touch—split into sections (features) with pages, buttons, and a tracker (Riverpod) to keep everything updated.

#### Subdirectories, File Types, and Usage
- **`features/`**: Feature-specific modules.
  - **Subdirs**: `auth/`, `patient/`, `doctor/`, `splash/`
  - **Structure** (e.g., `auth/`):
    - `screens/`: UI pages.
      - **File**: `sign_in_screen.dart`
      - **Content**: Stateful/stateless widgets using Riverpod.
      - **Example**: `ElevatedButton(onPressed: () => ref.read(authProvider.notifier).login(), child: Text('Sign In'))`
      - **Use**: Login page UI.
    - `widgets/`: Reusable UI components.
      - **File**: `auth_button.dart`
      - **Content**: Custom button widget.
      - **Example**: `class AuthButton extends StatelessWidget { ... }`
      - **Use**: Reusable login/signup button.
    - `providers/`: Riverpod state management.
      - **File**: `auth_provider.dart`
      - **Content**: Providers for state.
      - **Example**: `final authProvider = StateNotifierProvider<AuthNotifier, User?>((ref) => AuthNotifier());`
      - **Use**: Tracks login state.
- **`navigation/`**: Routing logic.
  - **File**: `app_router.dart`
  - **Content**: Navigation setup (e.g., GoRouter).
  - **Example**: `GoRouter(routes: [GoRoute(path: '/', builder: (context, state) => SplashScreen())])`
  - **Use**: Moves between screens.
- **`widgets/`**: General reusable UI.
  - **Subdirs**: `dialog/`, `drawer/`
  - **Files**: `custom_dialog.dart`, `app_drawer.dart`
  - **Content**: Widgets for pop-ups or side menus.
  - **Example**: `class CustomDialog extends StatelessWidget { ... }`
  - **Use**: Shows a confirmation dialog.

---

### 5. `lib/src/const/`
#### Technical Description
The `const/` directory stores static values like colors, sizes, or strings to ensure consistency across the app.

#### Layman’s Terms
This is the app’s style guide, keeping colors and settings the same everywhere.

#### File Types and Usage
- **File**: `colors.dart`
- **Content**: Constant definitions.
- **Example**: `const Color primaryColor = Color(0xFF2196F3);`
- **Use**: Sets a blue color for buttons and headers.

---

### 6. `lib/src/enums/`
#### Technical Description
The `enums/` directory defines fixed sets of options to enhance type safety and readability.

#### Layman’s Terms
This is a checklist of allowed choices, like “patient” or “doctor,” to avoid mistakes.

#### File Types and Usage
- **File**: `user_role.dart`
- **Content**: Enum definitions.
- **Example**: `enum UserRole { patient, doctor, admin }`
- **Use**: Assigns roles to users.

---

### 7. `lib/main.dart`
#### Technical Description
The `main.dart` file is the app’s entry point, initializing Flutter and Riverpod, and setting up the root widget with initial routing.

#### Layman’s Terms
This is the app’s start button, turning it on and showing the first screen.

#### File Types and Usage
- **File**: `main.dart`
- **Content**: Main function and app widget.
- **Example**: `void main() { runApp(ProviderScope(child: MyApp())); }`
- **Use**: Launches the app with a splash screen.

---
