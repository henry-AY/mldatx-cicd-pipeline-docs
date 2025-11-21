# Configuration file (Single source of truth)

Place a JSON file named `config.json` (**STRICT**) in your CICD scripts folder (e.g., `cicd-scripts/config.json`). The automation expects that the .json filename to end with `config.json`; if it is named something else, the loader’s glob will not pick it up.

## Minimal example of `config.json`

```json
{
  "paths": {
    "BASE_PATH": "/Users/<user>/Documents/MATLAB",
    "CICD_DIR": "/Users/<user>/Documents/MATLAB/Simulink-Automation/cicd-scripts",
    "CONFIG_FILE": "/Users/<user>/Documents/MATLAB/Simulink-Automation/cicd-scripts/config.json",
    "RESULTS_FILE": "/Users/<user>/Documents/MATLAB/Simulink-Automation/test_results.csv",
    "LOG_FILE": "/Users/<user>/Documents/MATLAB/Simulink-Automation/logs"
  },

  "whitelist": {
    "project_folders": ["folder_1", "folder_2", "folder_3"],
    "project_subfolders": {
      "tests": "tests",
      "results": "results"
    }
  },

  "blacklist": {
    "project_folders": ["folder_10"]
  }
}
```
> Replace <user> with the actual device username (You can figure out who you are by typing `whoami` in the terminal).
> Make sure `CONFIG_FILE` points to the full path of this `config.json` file.

* ##### `BASE_PATH`

  * Absolute path that contains all subsystem project folders. Must be `/Users/<user>/Documents/MATLAB` (or the equivalent on a different setup). Subfolders listed in `whitelist.project_folders` are expected to live directly under this path.
  * Set `BASE_PATH` to your MATLAB Documents folder for the current user:

```swift
/Users/<user>/Documents/MATLAB/
```

* ##### `CICD_DIR`

  * Directory containing your Python + MATLAB automation scripts (e.g., `parent.py`, `helper.m`, etc.).

* ##### `CONFIG_FILE`

  * Absolute path to this `config.json`. **Filename must be** `config.json`.

* ##### `RESULTS_FILE`

  * Full path where the Python script will write the CSV summary (e.g., `test_results.csv`).

* ##### `LOG_FILE`

  * Directory where daily logs are written (e.g., `/.../logs`). The script will create it if it does not exist (provided permissions allow

* ##### `whitelist.project_folders`

  * Name of the folders of each subsystem that contain `.mldatx` test suites that you want to test.

* ##### `whitelist.project_subfolders.tests` 

  * Name of the subfolder inside each subsystem that contains `.mldatx` test suites (for example, `tests`).

* ##### `whitelist.project_subfolders.results`

  * Name of the subfolder where test MATLAB results will be exported (for example, `results`).
 
* ##### `blacklist.project_folders`

  * Optional list of folder names to skip, even if present in the whitelist.

## Important notes/gotchas

* **Filename requirement:** The config file must be named exactly `config.json`. The loader uses a glob that will only match that name.
* **Permissions:** Ensure the user running the Python script has write permission for `Documents/MATLAB`, `LOG_FILE`, and `RESULTS_FILE` directories.
* **BASE_PATH placement: `BASE_PATH` should point to your MATLAB Documents directory (i.e., `/Users/<user>/Documents/MATLAB`). Do not point `BASE_PATH` into some unrelated folder unless you know what you’re doing.
* **Paths must be absolute** (full paths work best and avoid surprises)
* **If using macOS/Windows CI runners**, adapt paths accordingly (Windows users would use `C:\Users\<user>\Documents\MATLAB`).

