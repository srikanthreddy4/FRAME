# FRAME --- File Reader and Assistance for Memory Enhancement.

FRAME is a Flutter application designed to bring document reading and
active learning into one place. Its main navigation provides access to
folders, PDF reading, AI-powered search, and flashcard decks.

> **Project status:** This README is based on the app entry point
> (`main.dart`). Some screens are imported from other files, so their
> detailed behavior should be confirmed against their implementations.

## Features

-   **Folder-based navigation** --- browse documents through the app's
    folder screen.
-   **PDF reading and viewing** --- open PDF files from the folder list
    and access a dedicated PDF viewer.
-   **PDF lock state** --- save a PDF's locked state and file path using
    local preferences.
-   **AI search screen** --- access the app's AI search interface.
-   **Flashcard learning** --- access the deck screen for
    flashcard-based learning.
-   **Persistent local preferences** --- retain selected PDF lock
    information between app launches.
-   **Simple navigation** --- move between Home, PDF, AI, and FlashLearn
    from the bottom navigation bar.

## Tech Stack

-   **Flutter** --- cross-platform application UI
-   **Dart** --- application programming language
-   **Provider** --- state management for the lock provider
-   **SharedPreferences** --- local storage for PDF lock state and path
-   **flutter_dotenv** --- environment-variable configuration

Other packages may be used by the individual screens. Check
`pubspec.yaml` for the complete dependency list.

## Project Structure

The following is the structure indicated by imports in `main.dart`; add
or adjust entries to match the complete repository.

``` text
lib/
├── main.dart
├── screens/
│   ├── ai_search_screen.dart
│   ├── deck_screen.dart
│   ├── flashcard_screen.dart
│   ├── folder_list_screen.dart
│   ├── pdf_reader_screen.dart
│   └── pdf_viewer_screen.dart
└── utils/
    └── lock_provider.dart
```

## Getting Started

### Prerequisites

Install the Flutter SDK and set up an Android emulator or a physical
device. For other platforms, follow the relevant Flutter platform setup
guide.

Verify your installation:

``` bash
flutter doctor
```

### 1. Clone the repository

Replace `<https://github.com/srikanthreddy4/FRAME>` with the URL of your GitHub repository.

``` bash
git clone <https://github.com/srikanthreddy4/FRAME>
cd <https://github.com/srikanthreddy4/FRAME>
```

### 2. Install dependencies

``` bash
flutter pub get
```

### 3. Configure environment variables

If the app or its AI-search implementation requires API credentials,
create a local `.env` file in the project root and add the variables
expected by your code.

Example only---replace the name and value with the variable your
implementation actually reads:

``` dotenv
API_KEY=your_api_key_here
```

**Important:** Do not commit `.env` files or API secrets. Add them to
`.gitignore`, and commit a safe `.env.example` containing variable names
without real credentials.

The supplied `main.dart` currently attempts to load `.env` from a
machine-specific absolute Windows path. Before sharing or running the
project on another machine, change this to a project-relative
configuration, for example:

``` dart
await dotenv.load(fileName: '.env');
```

Ensure the file exists and handle missing configuration appropriately.
If you use `flutter_dotenv`, also follow its package instructions for
declaring the environment file in `pubspec.yaml` where required.

### 4. Run the app

``` bash
flutter run
```

## How the App Is Organized

-   `main.dart` initializes Flutter, loads environment configuration,
    registers `LockProvider`, and launches the application.
-   `FolderListScreen` is the home screen and passes selected PDF paths
    to the PDF viewer.
-   `PDFReaderScreen` provides the PDF tab when no PDF is locked.
-   `PDFViewerScreen` receives a PDF path and a callback for toggling
    its lock state.
-   `AISearchScreen` is the AI search destination.
-   `DeckScreen` is the FlashLearn destination.
-   `SharedPreferences` stores the `pdf_locked` boolean and `pdf_path`
    string.

## Configuration & Security Notes

-   Keep API keys and other secrets out of source control.
-   Avoid hard-coded local file paths; they will not work on other
    developers' computers.
-   Validate that a stored PDF path still exists before attempting to
    open it.
-   Treat locally stored lock state as an application feature, **not as
    strong file encryption or a security boundary**.
-   Review error handling for missing `.env` files and unavailable PDF
    files before releasing the app.

## Roadmap

Possible next steps (update this list as features are implemented):

-   [ ] Document the supported environment variables.
-   [ ] Add screenshots or a short demo GIF.
-   [ ] Add tests for PDF navigation and lock-state persistence.
-   [ ] Document AI search setup and supported models/services.
-   [ ] Add setup instructions for each supported platform.
-   [ ] Add release and build instructions.

## Contributing

Contributions and suggestions are welcome.

1.  Fork the repository.
2.  Create a feature branch.
3.  Make your changes and test them.
4.  Open a pull request describing the change.

