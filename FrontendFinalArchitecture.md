# Architecture Document

## Architecture
This architecture adopts Clean Architecture, a widely recognized design pattern that emphasizes separation of concerns, testability, scalability, and maintainability. Built in Flutter with Riverpod for state management, it ensures efficient data flow, reactive UI updates, and modular organization. The structure separates features by user types (patient, doctor, pharmacist, ISP) while isolating common functionality, adhering to dependency inversion principles. This provides a simple yet robust foundation for reorganizing existing code, supporting long-term growth and ease of learning for beginners.

---

## Architecture Structure
```
DaxP/
├── android/                    # Android-specific files
├── ios/                        # iOS-specific files
├── assets/                     # Static assets (images, icons, fonts)
│   ├── bottom_nav_bar_icons/
│   ├── icons/
│   ├── images/
│   └── fonts/
├── lib/                        # Main application code
│   ├── main.dart               # Application entry point with Riverpod
│   ├── app.dart                # Main app widget
│   ├── routes.dart             # Application navigation routes
│   ├── theme/                  # Global theme and styles
│   ├── core/                   # Shared infrastructure and utilities
│   │   ├── constants/          # App-wide constants
│   │   ├── errors/             # Error handling
│   │   ├── utils/              # Utility functions
│   │   ├── network/            # API communication
│   │   └── local_storage/      # Local database and caching
│   ├── common/                 # Common features across all users
│   │   ├── auth/               # Authentication feature
│   │   │   ├── data/           # Data layer
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/         # Business logic layer
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/   # UI and state management layer
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   ├── splash/             # Splash screen feature
│   │   │   └── presentation/   # UI layer (no data/domain needed)
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   └── choose_role/        # Role selection feature
│   │       └── presentation/   # UI layer (no data/domain needed)
│   │           ├── screens/
│   │           └── widgets/
│   ├── features/               # User-specific and shared features
│   │   ├── patient/            # Patient-specific features
│   │   │   ├── data/           # Data layer
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/         # Business logic layer
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/   # UI and state management layer
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   ├── doctor/             # Doctor-specific features
│   │   │   ├── data/           # Data layer
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/         # Business logic layer
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/   # UI and state management layer
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   ├── pharmacist/         # Pharmacist-specific features
│   │   │   ├── data/           # Data layer
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/         # Business logic layer
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/   # UI and state management layer
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   ├── isp/                # ISP-specific features
│   │   │   ├── data/           # Data layer
│   │   │   │   ├── datasources/
│   │   │   │   ├── models/
│   │   │   │   └── repositories/
│   │   │   ├── domain/         # Business logic layer
│   │   │   │   ├── entities/
│   │   │   │   ├── repositories/
│   │   │   │   └── usecases/
│   │   │   └── presentation/   # UI and state management layer
│   │   │       ├── providers/
│   │   │       ├── screens/
│   │   │       └── widgets/
│   │   └── shared/             # Features shared across some users
│   │       ├── cart/           # Cart feature
│   │       │   ├── data/
│   │       │   ├── domain/
│   │       │   └── presentation/
│   │       └── medication_guide/  # Medication guide feature
│   │           ├── data/
│   │           ├── domain/
│   │           └── presentation/
│   ├── di/                     # Dependency injection with Riverpod
│   └── widgets/                # Shared UI components
├── test/                       # Unit and widget tests
│   ├── unit/
│   ├── widget/
│   └── integration/
├── pubspec.yaml                # Project dependencies (includes flutter_riverpod)
├── README.md                   # Project documentation
├── .gitignore                  # Git ignore rules
└── analysis_options.yaml       # Linter rules
```

## Example Architecture
Below is the project structure implementing Simplified Clean Architecture with Flutter and Riverpod, including `domain/`, `data/`, and `presentation/` layers:

```
my_DaxP_app/
├── android/
├── ios/
├── assets/
│   ├── bottom_nav_bar_icons/
│   ├── icons/
│   ├── images/
│   └── fonts/
├── lib/
│   ├── main.dart
│   ├── app.dart
│   ├── routes.dart
│   ├── theme/
│   │   └── app_theme.dart
│   ├── core/
│   │   ├── constants/
│   │   │   └── colors.dart
│   │   ├── errors/
│   │   │   └── failures.dart
│   │   ├── utils/
│   │   │   └── logger.dart
│   │   ├── network/
│   │   │   ├── api_client.dart
│   │   │   └── network_info.dart
│   │   └── local_storage/
│   │       └── local_storage.dart
│   ├── common/
│   │   ├── auth/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── auth_remote_datasource.dart
│   │   │   │   │   └── auth_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── user_model.dart
│   │   │   │   └── repositories/
│   │   │   │       └── auth_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── user.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── auth_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       └── login_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── auth_provider.dart
│   │   │       ├── screens/
│   │   │       │   ├── sign_in_screen.dart
│   │   │       │   └── sign_up_screen.dart
│   │   │       └── widgets/
│   │   │           └── auth_button.dart
│   │   ├── splash/
│   │   │   └── presentation/
│   │   │       ├── screens/
│   │   │       │   └── splash_screen.dart
│   │   │       └── widgets/
│   │   │           └── splash_logo.dart
│   │   └── choose_role/
│   │       └── presentation/
│   │           ├── screens/
│   │           │   └── choose_role_screen.dart
│   │           └── widgets/
│   │               └── role_button.dart
│   ├── features/
│   │   ├── patient/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── patient_remote_datasource.dart
│   │   │   │   │   └── patient_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── patient_model.dart
│   │   │   │   └── repositories/
│   │   │   │       └── patient_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── patient.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── patient_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       └── get_patient_profile_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── patient_provider.dart
│   │   │       ├── screens/
│   │   │       │   ├── home_screen.dart
│   │   │       │   └── pharmacy_screen.dart
│   │   │       └── widgets/
│   │   │           └── patient_home_widget.dart
│   │   ├── doctor/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── doctor_remote_datasource.dart
│   │   │   │   │   └── doctor_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── doctor_model.dart
│   │   │   │   └── repositories/
│   │   │   │       └── doctor_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── doctor.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── doctor_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       └── get_doctor_schedule_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── doctor_provider.dart
│   │   │       ├── screens/
│   │   │       │   └── doctor_home_screen.dart
│   │   │       └── widgets/
│   │   │           └── schedule_card.dart
│   │   ├── pharmacist/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── pharmacist_remote_datasource.dart
│   │   │   │   │   └── pharmacist_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── pharmacist_model.dart
│   │   │   │   └── repositories/
│   │   │   │       └── pharmacist_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── pharmacist.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── pharmacist_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       └── get_pharmacist_approvals_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── pharmacist_provider.dart
│   │   │       ├── screens/
│   │   │       │   └── pharmacist_home_screen.dart
│   │   │       └── widgets/
│   │   │           └── approval_card.dart
│   │   ├── isp/
│   │   │   ├── data/
│   │   │   │   ├── datasources/
│   │   │   │   │   ├── isp_remote_datasource.dart
│   │   │   │   │   └── isp_local_datasource.dart
│   │   │   │   ├── models/
│   │   │   │   │   └── isp_model.dart
│   │   │   │   └── repositories/
│   │   │   │       └── isp_repository_impl.dart
│   │   │   ├── domain/
│   │   │   │   ├── entities/
│   │   │   │   │   └── isp.dart
│   │   │   │   ├── repositories/
│   │   │   │   │   └── isp_repository.dart
│   │   │   │   └── usecases/
│   │   │   │       └── get_isp_providers_usecase.dart
│   │   │   └── presentation/
│   │   │       ├── providers/
│   │   │       │   └── isp_provider.dart
│   │   │       ├── screens/
│   │   │       │   └── isp_home_screen.dart
│   │   │       └── widgets/
│   │   │           └── provider_tile.dart
│   │   └── shared/
│   │       ├── cart/
│   │       │   ├── data/
│   │       │   │   ├── datasources/
│   │       │   │   │   └── cart_local_datasource.dart
│   │       │   │   ├── models/
│   │       │   │   │   └── cart_item_model.dart
│   │       │   │   └── repositories/
│   │       │   │       └── cart_repository_impl.dart
│   │       │   ├── domain/
│   │       │   │   ├── entities/
│   │       │   │   │   └── cart_item.dart
│   │       │   │   ├── repositories/
│   │       │   │   │   └── cart_repository.dart
│   │       │   │   └── usecases/
│   │       │   │       └── add_to_cart_usecase.dart
│   │       │   └── presentation/
│   │       │       ├── providers/
│   │       │       │   └── cart_provider.dart
│   │       │       ├── screens/
│   │       │       │   └── cart_screen.dart
│   │       │       └── widgets/
│   │       │           └── cart_item_widget.dart
│   │       └── medication_guide/
│   │           ├── data/
│   │           ├── domain/
│   │           └── presentation/
│   │               ├── providers/
│   │               │   └── medication_guide_provider.dart
│   │               ├── screens/
│   │               │   └── medication_guide_screen.dart
│   │               └── widgets/
│   ├── di/
│   │   └── injection.dart
│   └── widgets/
│       ├── dialog/
│       │   └── custom_dialog.dart
│       └── drawer/
│           └── app_drawer.dart
├── test/
├── pubspec.yaml
├── README.md
├── .gitignore
└── analysis_options.yaml
```

---

## Detailed Description of Each Folder

### 1. `assets/`
#### Technical Description
The `assets/` directory stores static files such as images, icons, and fonts, declared in `pubspec.yaml` for inclusion in the app build. Subdirectories organize assets by type or function, ensuring easy access across user types.

#### Layman’s Terms
This is the app’s collection of visuals—like a scrapbook with icons, pictures, and fonts to make everything look good.

#### File Types and Usage
- **File Types**: `.png`, `.jpg`, `.svg` (images/icons), `.ttf` (fonts).
- **How**: Added to `pubspec.yaml` (e.g., `flutter: assets: - assets/icons/`), accessed via `Image.asset()` or `Icon()`.
- **Subdirectories**:
  - `bottom_nav_bar_icons/`: Icons for navigation bars.
  - `icons/`: General icons (e.g., user, settings).
  - `images/`: App images (e.g., logos).
  - `fonts/`: Custom font files.

#### Example
- **File**: `assets/images/logo.png`
  - **Code**: `Image.asset('assets/images/logo.png', height: 50)`
  - **Use**: Displays the app logo on the splash screen.

---

### 2. `lib/core/`
#### Technical Description
The `core/` directory provides shared infrastructure and utilities used across all user types and features. It includes constants, error handling, helper functions, networking, and local storage, supporting the app’s foundational needs.

#### Layman’s Terms
This is the app’s shared toolbox—holding settings, a way to talk to the server, shortcuts, and a place to jot down notes everyone can use.

#### Subdirectories, File Types, and Usage
- **`constants/`**: App-wide static values.
  - **File**: `colors.dart`
  - **Content**: Color definitions.
  - **Example**: `const Color primaryColor = Color(0xFF2196F3);`
  - **Use**: Sets consistent colors across screens.
- **`errors/`**: Error handling utilities.
  - **File**: `failures.dart`
  - **Content**: Custom exception classes.
  - **Example**: `class ServerFailure implements Exception { final String message; ServerFailure(this.message); }`
  - **Use**: Handles API errors uniformly.
- **`utils/`**: Helper functions.
  - **File**: `logger.dart`
  - **Content**: Logging utility.
  - **Example**: `void log(String msg) => print('[LOG] $msg');`
  - **Use**: Debugs issues during development.
- **`network/`**: API communication tools.
  - **Files**: `api_client.dart`, `network_info.dart`
  - **Content**: HTTP client setup (e.g., Dio), connectivity checks.
  - **Example**: `final apiClientProvider = Provider((ref) => ApiClient());`
  - **Use**: Connects to the backend for all users.
- **`local_storage/`**: Local persistence.
  - **File**: `local_storage.dart`
  - **Content**: Functions using SharedPreferences.
  - **Example**: `Future<void> saveToken(String token) async { ... }`
  - **Use**: Stores login tokens locally.

---

### 3. `lib/common/`
#### Technical Description
The `common/` directory contains features shared across all user types, such as authentication, splash screen, and role selection. Each feature follows Clean Architecture with data, domain, and presentation layers where applicable, using Riverpod for state management in `presentation/`.

#### Layman’s Terms
This is the app’s shared space—things like login, the welcome screen, and picking your role that everyone uses.

#### Subdirectories, File Types, and Usage
- **`auth/`**: Authentication feature.
  - **Structure**:
    - `data/datasources/`: 
      - **File**: `auth_remote_datasource.dart`
      - **Content**: `Future<Map<String, dynamic>> login(String email, String password) async { ... }`
      - **Use**: Fetches user data from backend.
    - `data/models/`: 
      - **File**: `user_model.dart`
      - **Content**: `class UserModel { final String id; UserModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses API response.
    - `data/repositories/`: 
      - **File**: `auth_repository_impl.dart`
      - **Content**: `class AuthRepositoryImpl implements AuthRepository { ... }`
      - **Use**: Implements login logic.
    - `domain/entities/`: 
      - **File**: `user.dart`
      - **Content**: `class User { final String id; User(this.id); }`
      - **Use**: Core user object.
    - `domain/repositories/`: 
      - **File**: `auth_repository.dart`
      - **Content**: `abstract class AuthRepository { Future<User> login(String email, String password); }`
      - **Use**: Defines login contract.
    - `domain/usecases/`: 
      - **File**: `login_usecase.dart`
      - **Content**: `class LoginUseCase { Future<User> call(String email, String password) => repo.login(email, password); }`
      - **Use**: Executes login logic.
    - `presentation/providers/`: 
      - **File**: `auth_provider.dart`
      - **Content**: `final authProvider = StateNotifierProvider((ref) => AuthNotifier(ref.read(loginUseCaseProvider)));`
      - **Use**: Manages login state.
    - `presentation/screens/`: 
      - **File**: `sign_in_screen.dart`
      - **Content**: `class SignInScreen extends ConsumerWidget { ... }`
      - **Use**: Displays login UI.
    - `presentation/widgets/`: 
      - **File**: `auth_button.dart`
      - **Content**: `class AuthButton extends StatelessWidget { ... }`
      - **Use**: Reusable login button.
  - **Example**: `ref.read(authProvider.notifier).login('email', 'pass');`
  - **Use**: Manages login/signup for all users.
- **`splash/`**: Splash screen feature.
  - **Structure**:
    - `presentation/screens/`: 
      - **File**: `splash_screen.dart`
      - **Content**: `class SplashScreen extends StatelessWidget { ... }`
      - **Use**: Shows initial UI.
    - `presentation/widgets/`: 
      - **File**: `splash_logo.dart`
      - **Content**: `class SplashLogo extends StatelessWidget { ... }`
      - **Use**: Displays logo.
  - **Example**: `Image.asset('assets/images/logo.png')`
  - **Use**: Displays initial app screen (no data/domain needed).
- **`choose_role/`**: Role selection feature.
  - **Structure**:
    - `presentation/screens/`: 
      - **File**: `choose_role_screen.dart`
      - **Content**: `class ChooseRoleScreen extends StatelessWidget { ... }`
      - **Use**: Shows role options.
    - `presentation/widgets/`: 
      - **File**: `role_button.dart`
      - **Content**: `class RoleButton extends StatelessWidget { ... }`
      - **Use**: Role selection button.
  - **Example**: `ElevatedButton(onPressed: () => navigateToRole(), child: Text('Patient'))`
  - **Use**: Lets users pick their role (no data/domain needed).

---

### 4. `lib/features/`
#### Technical Description
The `features/` directory organizes user-specific and shared features, each following Clean Architecture with data, domain, and presentation layers. Riverpod manages state within `presentation/`, separating logic by user type (patient, doctor, pharmacist, ISP).

#### Layman’s Terms
This is the app’s job board—split into tasks for patients, doctors, pharmacists, and ISPs, plus some shared jobs everyone can use.

#### Subdirectories, File Types, and Usage
- **`patient/`**: Patient-specific features.
  - **Structure**:
    - `data/datasources/`: 
      - **File**: `patient_remote_datasource.dart`
      - **Content**: `Future<Map<String, dynamic>> getProfile(String id) async { ... }`
      - **Use**: Fetches patient data.
    - `data/models/`: 
      - **File**: `patient_model.dart`
      - **Content**: `class PatientModel { final String id; PatientModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses patient data.
    - `data/repositories/`: 
      - **File**: `patient_repository_impl.dart`
      - **Content**: `class PatientRepositoryImpl implements PatientRepository { ... }`
      - **Use**: Implements patient data access.
    - `domain/entities/`: 
      - **File**: `patient.dart`
      - **Content**: `class Patient { final String id; Patient(this.id); }`
      - **Use**: Core patient object.
    - `domain/repositories/`: 
      - **File**: `patient_repository.dart`
      - **Content**: `abstract class PatientRepository { Future<Patient> getProfile(String id); }`
      - **Use**: Defines patient data contract.
    - `domain/usecases/`: 
      - **File**: `get_patient_profile_usecase.dart`
      - **Content**: `class GetPatientProfileUseCase { Future<Patient> call(String id) => repo.getProfile(id); }`
      - **Use**: Fetches patient profile.
    - `presentation/providers/`: 
      - **File**: `patient_provider.dart`
      - **Content**: `final patientProvider = StateNotifierProvider((ref) => PatientNotifier(ref.read(getPatientProfileUseCaseProvider)));`
      - **Use**: Manages patient state.
    - `presentation/screens/`: 
      - **File**: `home_screen.dart`
      - **Content**: `class HomeScreen extends ConsumerWidget { ... }`
      - **Use**: Displays patient home.
    - `presentation/widgets/`: 
      - **File**: `patient_home_widget.dart`
      - **Content**: `class PatientHomeWidget extends StatelessWidget { ... }`
      - **Use**: Reusable patient UI component.
  - **Example**: `ref.read(patientProvider.notifier).fetchProfile('123');`
  - **Use**: Manages patient-specific screens.
- **`doctor/`**: Doctor-specific features.
  - **Structure**:
    - `data/datasources/`: 
      - **File**: `doctor_remote_datasource.dart`
      - **Content**: `Future<Map<String, dynamic>> getSchedule(String id) async { ... }`
      - **Use**: Fetches doctor schedule.
    - `data/models/`: 
      - **File**: `doctor_model.dart`
      - **Content**: `class DoctorModel { final String id; DoctorModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses doctor data.
    - `data/repositories/`: 
      - **File**: `doctor_repository_impl.dart`
      - **Content**: `class DoctorRepositoryImpl implements DoctorRepository { ... }`
      - **Use**: Implements doctor data access.
    - `domain/entities/`: 
      - **File**: `doctor.dart`
      - **Content**: `class Doctor { final String id; Doctor(this.id); }`
      - **Use**: Core doctor object.
    - `domain/repositories/`: 
      - **File**: `doctor_repository.dart`
      - **Content**: `abstract class DoctorRepository { Future<Doctor> getSchedule(String id); }`
      - **Use**: Defines doctor data contract.
    - `domain/usecases/`: 
      - **File**: `get_doctor_schedule_usecase.dart`
      - **Content**: `class GetDoctorScheduleUseCase { Future<Doctor> call(String id) => repo.getSchedule(id); }`
      - **Use**: Fetches doctor schedule.
    - `presentation/providers/`: 
      - **File**: `doctor_provider.dart`
      - **Content**: `final doctorProvider = StateNotifierProvider((ref) => DoctorNotifier(ref.read(getDoctorScheduleUseCaseProvider)));`
      - **Use**: Manages doctor state.
    - `presentation/screens/`: 
      - **File**: `doctor_home_screen.dart`
      - **Content**: `class DoctorHomeScreen extends ConsumerWidget { ... }`
      - **Use**: Displays doctor home.
    - `presentation/widgets/`: 
      - **File**: `schedule_card.dart`
      - **Content**: `class ScheduleCard extends StatelessWidget { ... }`
      - **Use**: Displays schedule item.
  - **Example**: `ref.read(doctorProvider.notifier).fetchSchedule('456');`
  - **Use**: Manages doctor-specific screens.
- **`pharmacist/`**: Pharmacist-specific features.
  - **Structure**:
    - `data/datasources/`: 
      - **File**: `pharmacist_remote_datasource.dart`
      - **Content**: `Future<Map<String, dynamic>> getApprovals(String id) async { ... }`
      - **Use**: Fetches pharmacist approvals.
    - `data/models/`: 
      - **File**: `pharmacist_model.dart`
      - **Content**: `class PharmacistModel { final String id; PharmacistModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses pharmacist data.
    - `data/repositories/`: 
      - **File**: `pharmacist_repository_impl.dart`
      - **Content**: `class PharmacistRepositoryImpl implements PharmacistRepository { ... }`
      - **Use**: Implements pharmacist data access.
    - `domain/entities/`: 
      - **File**: `pharmacist.dart`
      - **Content**: `class Pharmacist { final String id; Pharmacist(this.id); }`
      - **Use**: Core pharmacist object.
    - `domain/repositories/`: 
      - **File**: `pharmacist_repository.dart`
      - **Content**: `abstract class PharmacistRepository { Future<Pharmacist> getApprovals(String id); }`
      - **Use**: Defines pharmacist data contract.
    - `domain/usecases/`: 
      - **File**: `get_pharmacist_approvals_usecase.dart`
      - **Content**: `class GetPharmacistApprovalsUseCase { Future<Pharmacist> call(String id) => repo.getApprovals(id); }`
      - **Use**: Fetches pharmacist approvals.
    - `presentation/providers/`: 
      - **File**: `pharmacist_provider.dart`
      - **Content**: `final pharmacistProvider = StateNotifierProvider((ref) => PharmacistNotifier(ref.read(getPharmacistApprovalsUseCaseProvider)));`
      - **Use**: Manages pharmacist state.
    - `presentation/screens/`: 
      - **File**: `pharmacist_home_screen.dart`
      - **Content**: `class PharmacistHomeScreen extends ConsumerWidget { ... }`
      - **Use**: Displays pharmacist home.
    - `presentation/widgets/`: 
      - **File**: `approval_card.dart`
      - **Content**: `class ApprovalCard extends StatelessWidget { ... }`
      - **Use**: Displays approval item.
  - **Example**: `ref.read(pharmacistProvider.notifier).fetchApprovals('789');`
  - **Use**: Manages pharmacist-specific screens.
- **`isp/`**: ISP-specific features.
  - **Structure**:
    - `data/datasources/`: 
      - **File**: `isp_remote_datasource.dart`
      - **Content**: `Future<Map<String, dynamic>> getProviders(String id) async { ... }`
      - **Use**: Fetches ISP providers.
    - `data/models/`: 
      - **File**: `isp_model.dart`
      - **Content**: `class IspModel { final String id; IspModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses ISP data.
    - `data/repositories/`: 
      - **File**: `isp_repository_impl.dart`
      - **Content**: `class IspRepositoryImpl implements IspRepository { ... }`
      - **Use**: Implements ISP data access.
    - `domain/entities/`: 
      - **File**: `isp.dart`
      - **Content**: `class Isp { final String id; Isp(this.id); }`
      - **Use**: Core ISP object.
    - `domain/repositories/`: 
      - **File**: `isp_repository.dart`
      - **Content**: `abstract class IspRepository { Future<Isp> getProviders(String id); }`
      - **Use**: Defines ISP data contract.
    - `domain/usecases/`: 
      - **File**: `get_isp_providers_usecase.dart`
      - **Content**: `class GetIspProvidersUseCase { Future<Isp> call(String id) => repo.getProviders(id); }`
      - **Use**: Fetches ISP providers.
    - `presentation/providers/`: 
      - **File**: `isp_provider.dart`
      - **Content**: `final ispProvider = StateNotifierProvider((ref) => IspNotifier(ref.read(getIspProvidersUseCaseProvider)));`
      - **Use**: Manages ISP state.
    - `presentation/screens/`: 
      - **File**: `isp_home_screen.dart`
      - **Content**: `class IspHomeScreen extends ConsumerWidget { ... }`
      - **Use**: Displays ISP home.
    - `presentation/widgets/`: 
      - **File**: `provider_tile.dart`
      - **Content**: `class ProviderTile extends StatelessWidget { ... }`
      - **Use**: Displays provider item.
  - **Example**: `ref.read(ispProvider.notifier).fetchProviders('101');`
  - **Use**: Manages ISP-specific screens.
- **`shared/`**: Features shared across some users.
  - **Subdirs**: `cart/`, `medication_guide/`, etc.
  - **Structure** (e.g., `cart/`):
    - `data/datasources/`: 
      - **File**: `cart_local_datasource.dart`
      - **Content**: `Future<List<Map<String, dynamic>>> getCartItems() async { ... }`
      - **Use**: Fetches cart items locally.
    - `data/models/`: 
      - **File**: `cart_item_model.dart`
      - **Content**: `class CartItemModel { final String id; CartItemModel.fromJson(Map<String, dynamic> json) : id = json['id']; }`
      - **Use**: Parses cart data.
    - `data/repositories/`: 
      - **File**: `cart_repository_impl.dart`
      - **Content**: `class CartRepositoryImpl implements CartRepository { ... }`
      - **Use**: Implements cart data access.
    - `domain/entities/`: 
      - **File**: `cart_item.dart`
      - **Content**: `class CartItem { final String id; CartItem(this.id); }`
      - **Use**: Core cart item object.
    - `domain/repositories/`: 
      - **File**: `cart_repository.dart`
      - **Content**: `abstract class CartRepository { Future<void> addItem(CartItem item); }`
      - **Use**: Defines cart data contract.
    - `domain/usecases/`: 
      - **File**: `add_to_cart_usecase.dart`
      - **Content**: `class AddToCartUseCase { Future<void> call(CartItem item) => repo.addItem(item); }`
      - **Use**: Adds item to cart.
    - `presentation/providers/`: 
      - **File**: `cart_provider.dart`
      - **Content**: `final cartProvider = StateNotifierProvider((ref) => CartNotifier(ref.read(addToCartUseCaseProvider)));`
      - **Use**: Manages cart state.
    - `presentation/screens/`: 
      - **File**: `cart_screen.dart`
      - **Content**: `class CartScreen extends ConsumerWidget { ... }`
      - **Use**: Displays cart UI.
    - `presentation/widgets/`: 
      - **File**: `cart_item_widget.dart`
      - **Content**: `class CartItemWidget extends StatelessWidget { ... }`
      - **Use**: Displays cart item UI.
  - **Example**: `ref.read(cartProvider.notifier).addItem(cartItem);`
  - **Use**: Manages shared features like cart.

---

### 5. `lib/di/`
#### Technical Description
The `di/` directory centralizes Riverpod dependency injection, defining global providers for shared dependencies like API clients and use cases.

#### Layman’s Terms
This is the app’s tool-sharing hub—making sure everyone gets the right tools (like the server phone) when they need them.

#### File Types and Usage
- **File**: `injection.dart`
- **Content**: Riverpod provider definitions.
- **Example**: 
  ```
  final apiClientProvider = Provider((ref) => ApiClient());
  final patientRepositoryProvider = Provider((ref) => PatientRepositoryImpl(ref.read(apiClientProvider)));
  final getPatientProfileUseCaseProvider = Provider((ref) => GetPatientProfileUseCase(ref.read(patientRepositoryProvider)));
  ```
- **Use**: Supplies dependencies to features.

---

### 6. `lib/widgets/`
#### Technical Description
The `widgets/` directory holds reusable UI components shared across all user types and features, enhancing consistency and reducing duplication.

#### Layman’s Terms
This is the app’s Lego box—pre-made pieces like buttons and menus anyone can use.

#### File Types and Usage
- **Subdirs**: `dialog/`, `drawer/`
- **Files**: `custom_dialog.dart`, `app_drawer.dart`
- **Content**: Stateless or stateful widgets.
- **Example**: `class CustomDialog extends StatelessWidget { ... }`
- **Use**: Shows a pop-up dialog across screens.

---

### 7. `lib/main.dart`
#### Technical Description
The `main.dart` file serves as the app’s entry point, initializing Flutter and Riverpod’s `ProviderScope`, and launching the root widget.

#### Layman’s Terms
This is the app’s on-switch—starting everything up and showing the first screen.

#### File Types and Usage
- **File**: `main.dart`
- **Content**: 
  ```
  void main() {
    runApp(ProviderScope(child: MyApp()));
  }
  ```
- **Use**: Starts the app with the splash screen.

