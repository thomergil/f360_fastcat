# `f360_fastcat`

`f360_fastcat` is a Ruby script that concatenates multiple Fusion 360-generated G-code files while cleaning and optimizing them. It removes all Fusion 360–specific comments and fixes rapid move feedrate issues imposed by the Fusion 360 Personal Use post processor, ensuring that rapid moves run at full speed and transitions between files are safe.

## WARNING / DISCLAIMER

This software is provided "as-is" without any warranties or guarantees. Use it at your own risk. The author(s) assume no responsibility or liability for any **damage to your CNC machine or other equipment** resulting from the use of this script. Always thoroughly verify, simulate, and review the generated G-code before running it on your machine. **Use of this script may lead to unexpected machine behavior, damage, or personal injury.**

## Features

- **Fusion 360 Comment Removal:**
  
  Eliminates all comments related to Fusion 360/F360 (e.g., those discussing reduced rapid feed rates, machining time, etc.).
  
- **Rapid Move Feedrate Optimization:**
  
  Fast mode automatically converts cutting moves (G1) to rapid moves (G0) when above a safe height, ensuring that non-cutting moves run at full speed.
  
- **Safe File Concatenation:**
  
  Inserts a safe tool-change sequence between subsequent files, but only if a tool change is necessary.
  
- **Configurable Safe Height & Feedrate Threshold:**
  
  Allows you to override the automatically detected safe height and adjust the feedrate drop threshold via command-line options. The feedrate threshold tells the optimizer what to consider a cutting move and a non-cutting move. If the feedrate suddenly drops to, say, 80% of the previous speed, it's safe to assume that we transitioned from a non-cutting move to a cutting move.
  
- **Dry-run Mode:**
  
  Enables a dry run where the final G-code is printed to the terminal without writing to an output file.

## Requirements

- Ruby 2.0 or higher

## Usage

1. **Make the script executable** (if necessary):

   - Use `chmod +x f360_fastcat` in your terminal.

2. **Run the script** by specifying one or more input G-code files and an output file. The following options are available:

   - `-v` or `--verbose`: Enable verbose output.
   - `--fast`: Enable rapid move optimizations.
   - `--safe-height VALUE`: Override the detected safe height (in mm).
   - `--feedrate-threshold VALUE`: Adjust the feedrate drop threshold (default is 0.75).
   - `--dry-run`: Print the final G-code to the terminal without writing to a file.

## Examples
   Concatenate files with default settings:

       ./f360_fastcat input1.nc input2.nc output.nc

   Enable fast mode with rapid move optimizations:

   ```bash
   ./f360_fastcat --fast input1.nc input2.nc output.nc
   ```

   Use a custom safe height of 10mm:

   ```bash
   ./f360_fastcat --fast --safe-height 10 input1.nc input2.nc output.nc
   ```

   Adjust the feedrate threshold to 0.8 and perform a dry run:

   ```bash
   ./f360_fastcat --fast --feedrate-threshold 0.8 --dry-run input1.nc input2.nc output.nc
   ```

## Contributing

Contributions, issues, and feature requests are welcome! Please use the GitHub issue tracker to submit bugs or suggestions.

## License

This project is released under the MIT License.



