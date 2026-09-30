# LED Screen Designer v20.27 — Windows build

Repository package for building the Windows version with GitHub Actions.

## Build
1. Upload all files and folders from this archive to the repository root.
2. Open **Actions → Build Windows EXE → Run workflow**.
3. When the job finishes, download artifact **LED_Screen_Designer_v20_27_Windows**.
4. Extract the artifact completely and run `LED_Screen_Designer_v20_27.exe` from inside the extracted folder.

Do not move only the EXE out of the folder: this is an `onedir` build and the neighboring runtime files are required.

## Diagnostics
If startup fails inside the Python application, an error window is shown and a log is written to:

`%LOCALAPPDATA%\LED_Screen_Designer\startup_error.log`

The artifact also contains `RUN_WITH_DIAGNOSTICS.bat`.

## Application icon
`assets/app.ico` is generated from the supplied LED JPEG and is used both for the Windows executable and the application window.

## Windows Tcl/Tk fix
This repository build explicitly restores Python's Tcl/Tk runtime data into
`_internal/_tcl_data` and `_internal/_tk_data` after PyInstaller finishes.
The workflow verifies `init.tcl` and `tk.tcl` before publishing the artifact,
preventing the `pyi_rth__tkinter` / `Tcl data directory ... not found` startup failure.
