# McPrinty OrcaSlicer Configs

> **Acknowledgment**: Special thanks to [RetroD on Printables](https://www.printables.com/@RetroD) and [YouTube](https://www.youtube.com/@Retro_D) for their excellent work on the base OrcaSlicer profiles for K1/K1C/K1 Max - 0.4 nozzle. Their profiles served as the launching point for this effort.

> **Note**: These configs are specifically designed for the **Creality K1C with CFS (Creality Filament System) upgrade**. They may not work correctly on stock K1C or other printer models.

Optimized OrcaSlicer profiles for the **Creality K1C** with a 0.4mm nozzle.

## Features

- **Process Profiles**: Layer heights from 0.10mm (UltraFine) to 0.30mm (Draft), with Standard and Speed variants
- **Filament Profiles**: PLA (41 colors), ABS, ASA, PETG, TPU, and CF-PLA
- **Machine Profile**: Custom K1C configuration with optimized start/end G-code
- **First Layer Tuning**: Slower first layer speeds (25mm/s) for better bed adhesion
- **Klipper Macros**: Custom G-code macros required for the slicer profiles to work

## IMPORTANT: Klipper Macros Required

The machine profile references custom Klipper macros that must be installed on your printer for these configs to work properly. The slicer's start/end G-code calls macros like:

- `START_PRINT` - Print initialization sequence
- `END_PRINT` - Print completion and cooldown
- `SAFE_WIPE_V2` - Nozzle wipe routine
- `CUSTOM_PURGE_LINE` - Adaptive purge line positioning
- `PAUSE` / `RESUME` - Enhanced pause/resume handling

### Installing Klipper Macros

1. SSH into your K1C or access via Fluidd/Mainsail
2. Copy the files from the `klipper-macros/` folder to your printer's config directory
3. Add this line to your `printer.cfg` if not already present:
   ```
   [include gcode_macro.cfg]
   ```
4. Restart Klipper

### Klipper Config Files Included

| File | Description |
|------|-------------|
| `printer.cfg` | Main printer configuration |
| `gcode_macro.cfg` | All custom G-code macros |
| `printer_params.cfg` | Printer parameters |
| `box.cfg` | CFS/AMS box integration |
| `sensorless.cfg` | Sensorless homing configuration |

**Warning**: These configs are customized for the K1C. Review them before applying to ensure compatibility with your setup. Back up your existing configs first!

## Installation

### Option 1: Download ZIP

1. Click the green **Code** button above and select **Download ZIP**
2. Extract the ZIP file
3. Copy the folders to your OrcaSlicer user config directory:

| OS | Config Location |
|----|-----------------|
| Windows | `%APPDATA%\OrcaSlicer\user\default\` |
| macOS | `~/Library/Application Support/OrcaSlicer/user/default/` |
| Linux | `~/.config/OrcaSlicer/user/default/` |

### Option 2: Git Clone

```bash
# Navigate to your OrcaSlicer config directory
cd ~/.config/OrcaSlicer/user/default/  # Linux example

# Clone directly into the directory (backup existing configs first!)
git clone https://github.com/Jsimpson90/McPrinty-Orca-Configs.git .
```

## Important: Machine Name Dependency

The filament and process profiles are linked to a specific machine name: **`My-K1C-0.4-Noz`**

### To use these profiles:

1. **Install the machine profile first** - Copy the `machine/` folder contents
2. Restart OrcaSlicer
3. Select **My-K1C-0.4-Noz** as your printer
4. The filament and process profiles will now appear in the dropdowns

### To use with your own machine name:

If you want to use a different machine name, you'll need to update the `compatible_printers` field in each profile:

```bash
# Example: Replace machine name in all JSON files
find . -name "*.json" -exec sed -i 's/My-K1C-0.4-Noz/Your-Machine-Name/g' {} \;
```

Or manually edit the JSON files and change:
```json
"compatible_printers": ["My-K1C-0.4-Noz"]
```
to:
```json
"compatible_printers": ["Your-Machine-Name"]
```

## Profile Overview

### Process Profiles (Print Settings)

| Layer Height | Quality | Variants |
|--------------|---------|----------|
| 0.10mm | UltraFine | Standard, Speed |
| 0.12mm | SuperFine | Standard, Speed |
| 0.16mm | Fine | Standard, Speed |
| 0.20mm | Quality | Standard, Speed |
| 0.24mm | Fast | Standard, Speed |
| 0.28mm | Rapid | Standard, Speed |
| 0.30mm | Draft | Standard, Speed, Super-Speed |

Each profile has a `-NO-SUPPORTS` variant with supports disabled.

### Filament Profiles

- **PLA**: 41 color variants (White, Black, Red, Blue, Green, etc.)
- **PLA-Speed**: Higher flow rates for faster printing
- **PLA-Super-Speed**: Maximum speed PLA settings
- **CF-PLA**: Carbon fiber reinforced PLA
- **ABS / ABS-Speed**: Standard and speed ABS profiles
- **ASA**: UV-resistant outdoor filament
- **PETG**: Food-safe, flexible filament
- **TPU**: Flexible filament

## Customization

These profiles are tuned for my K1C but should work well as a starting point. You may need to adjust:

- **Temperatures**: Based on your specific filament brand
- **Retraction**: If you experience stringing
- **Pressure Advance**: Run a PA calibration for your setup
- **First Layer**: Z-offset calibration is still required

## License

These configs are provided as-is. Feel free to use, modify, and share.

## Issues

If you find problems or have suggestions, please open an issue on GitHub.
