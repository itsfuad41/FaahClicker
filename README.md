# FaahClicker

FaahClicker is a Windows macro recorder and player. It can record keyboard and mouse actions, save them as macro files, and replay them with configurable speed and repeat settings.

**Current version:** 1.0.6

**Developer:** Md. Fuad Hasan  
**Contact:** itsfuad.41@outlook.com

## Features

- Record keyboard presses, mouse clicks, scrolling, optional delays, and optional mouse movement.
- Save and open macros in `.fc` or `.json` format.
- Adjust playback speed and repeat count, or repeat until stopped.
- Configure global play/stop and record/stop hotkeys.
- Optionally stop playback when the mouse is moved.
- Enable **Enter to Down** to replace one selected Enter key with **Tab → Left Arrow → Down Arrow**. Choose either the main keyboard Enter or numeric-keypad Enter.

## Run the app

Download and run `FaahClicker-v1.0.6.exe` on Windows. The app opens with play and record buttons:

1. Select **File → New** or press the record button to start recording.
2. Press record again to stop, then select **File → Save** to save the macro.
3. Open a saved macro with **File → Open**, then press play to run it.
4. Configure playback, recording, and hotkeys from the **Options** menu.

Default global hotkeys:

- `3` — toggle playback
- `Ctrl+5` — toggle recording

Use **Options → Settings → Hotkeys Setting** to change them.

## Enter to Down

Open **Options → Settings → Enter to Down**, enable the option, and select the Enter key to use:

- **Main keyboard Enter**
- **Numeric keypad Enter**

When the selected Enter key is pressed, the app suppresses that Enter input and sends Tab, Left Arrow, and Down Arrow in sequence. The setting is saved between runs.

## GitHub kill switch

The app reads `kill-switch.json` from the `main` branch of the configured GitHub repository:

```json
{
  "enabled": true
}
```

Set `enabled` to `false` and publish the file to disable v1.0.6 instances that can reach the updated file. Running instances check again every 30 seconds. When the file is missing, invalid, or unreachable, the app continues running (fail-open).

This is a best-effort remote switch, not an offline enforcement mechanism: it cannot disable older builds that do not include the check, and it cannot take effect on a machine that cannot retrieve the updated file. To re-enable the app, set `enabled` back to `true`.

## Build from source

Requires Python for Windows, `pynput`, and PyInstaller. From the project directory:

```powershell
py -m pip install pynput pyinstaller
py -m PyInstaller --noconsole --onefile --clean --name "FaahClicker-v1.0.6" --icon="FaahClicker.ico" --add-data "FaahClicker.ico;." FaahClicker.py
```

The executable is written to `dist\FaahClicker-v1.0.6.exe`.
