FLYCASUAL UI QOL MOD  v1.0.0
=============================
A quality-of-life mod for Fly Casual (X-Wing AMG simulator): readable UI,
calmer camera, movement forecasting, and targeting lines.

Runs on BepInEx 5 (included). No game files are replaced, so it can be
removed at any time. All changes are visual and on your screen only, so you
can still play online with players who do not have the mod.


WHAT'S IN THIS FOLDER
---------------------
  Install.bat                    One-click installer
  Uninstall.bat                  Removes the mod (optionally BepInEx too)
  Game Files\                    Everything that goes into the game folder
  FlyCasual_UI_QOL_Mod_v1.0.0.zip  Same game files, zipped for sharing
  Source\                        C# source code for the mod
  README.txt                     This file


INSTALLATION
------------

NOTE: YOU DO NOT HAVE TO USE THE INSTALLER IF .BAT FILES ARE SCARY! The zip folder is just included for sharing of the unzipped "game files" folder.

Option A: Installer
  1. Close Fly Casual.
  2. Double-click Install.bat.
  3. Confirm the detected game folder, or paste the folder that contains
     "Fly Casual.exe".
  4. Start the game. Press F8 to open the mod settings.

Option B: Manual
  1. Close Fly Casual.
  2. Copy everything INSIDE "Game Files" into the folder that contains
     "Fly Casual.exe". Allow it to merge folders.
     When done, "winhttp.dll" and the "BepInEx" folder sit next to
     "Fly Casual.exe".
  3. Start the game.

Note: the included BepInEx.cfg sets the entrypoint to "Camera". This is
required. With BepInEx's default ("Application") this Unity version hangs at
startup with no window. If you already had BepInEx installed, the installer
keeps your config and changes only that line (backup: BepInEx.cfg.bak).


FEATURES
--------
UI
  * UI scale: shrinks the game's whole interface (rosters, menus, maneuver
    dial). Default 80%, adjustable 40% to 150%.
  * Ship nameplates: ID, pilot, initiative, ship type, hull/shield bar, force,
    stress and ion status. Colored by player (green/red, or blue/orange in
    colorblind mode).
      - Hidden until you hover a ship. Fades in and out.
      - During combat the attacker and target show theirs automatically.
      - Hold Left Alt to show every ship's nameplate.
      - Drawn underneath the game's HUD, so the dial and panels stay on top.
      - Ships that already moved or attacked are dimmed.
      - Labels push apart instead of overlapping.

Targeting lines
  * Attack arrow from attacker to target in the attacker's color, with the
    range ("Range 1-3" or "Out of range").
  * While choosing a target (attacks, target locks, ship-selecting abilities),
    a faint arrow with range points to the ship you hover.
  * Thin arrows for active target locks. Brighter when you hover either ship
    or hold Left Alt.

Camera
  * Cinematic attack camera off by default. When on, it eases in over a
    configurable time instead of a 2-second linear swing.
  * Edge-scrolling off by default (stops accidental drifting).
  * Panning speed scales with zoom and is frame-rate independent.
  * Smooth, less sensitive zoom and rotation.
  * Focus on the selected ship and one-key view reset.
  * Optional auto-follow of the ship currently activating.

Movement planning
  * Hover any maneuver on the dial to see a see-through ghost of your ship at
    the end position, with its flight path and a label:
        Cyan    clear
        Yellow  bump (names the ship)
        Orange  lands on / flies over an obstacle, or hits a device
        Red     flies off the board
  * Hold G during the Planning phase to see ghosts for all of your ships'
    dialed maneuvers at once.
  * Reverse and sideslip maneuvers show "no preview" instead of a ghost.


CONTROLS
--------
  F8          Open / close the mod settings panel (changes apply live)
  F6          Toggle nameplates on / off
  Left Alt    Show all nameplates and highlight all lock lines (vanilla key)
  F           Glide camera to the selected ship
  Home        Reset camera to the default view
  G (hold)    Planning phase: show ghosts for all your dialed maneuvers

All keys can be changed in the config file.


SETTINGS FILE
-------------
Created after the first launch:
  <game folder>\BepInEx\config\tytan.flycasual.qol.cfg

Every option has a description in that file. Main options:
  [UI]        UiScale, Nameplates, NameplateVisibility (HoverOnly / Always /
              AltOnly), NameplateFontSize, ColorblindPalette,
              DimActivatedShips, TargetingLines, LockLines
  [Camera]    CinematicAttackCamera, CinematicTransitionSeconds,
              EdgeScrolling, PanSpeed, ZoomScaledPan, SmoothZoom,
              ZoomSensitivity, RotateSensitivity, FollowActiveShip, keys
  [Planning]  ManeuverPreview, ShowAllPlansKey, GhostOpacity


UNINSTALL
---------
Close the game and run Uninstall.bat. It removes the mod and its settings,
then asks whether to remove BepInEx as well (say No if you use other
BepInEx mods). Removing BepInEx returns the game to vanilla.

Manual: delete "BepInEx\plugins\FlyCasualQoL". To remove BepInEx as well,
delete the "BepInEx" folder, "winhttp.dll", "doorstop_config.ini" and
".doorstop_version" from the game folder.


TROUBLESHOOTING
---------------
  * Game shows no window / hangs at startup:
    open BepInEx\config\BepInEx.cfg and make sure the line under
    [Preloader.Entrypoint] reads:  Type = Camera
  * Mod does not seem to load:
    check BepInEx\LogOutput.log for the line "Fly Casual QoL 1.0.0 loaded".
    "Unable to start Unity log writer" in that log is harmless.
  * After a Fly Casual update, if something breaks, check LogOutput.log for
    warnings starting with "Nameplates:", "ManeuverPreview:", "TargetLines:"
    or "CameraTweaks:". Each feature fails on its own without stopping the
    game.


BUILDING FROM SOURCE
--------------------
Requires the .NET SDK (6 or newer).
  1. Open Source\FlyCasualQoL.csproj and set <GameManaged> to your
     "Fly Casual_Data\Managed" folder if the game is not at the default path.
  2. In the Source folder run:  dotnet build -c Release
  3. Copy bin\Release\netstandard2.1\FlyCasualQoL.dll to
     <game folder>\BepInEx\plugins\FlyCasualQoL\


Tested with Fly Casual on Unity 2023.2.22 (Mono) and BepInEx 5.4.23.2.
