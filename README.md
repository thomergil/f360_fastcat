# `f360_fastcat`

`f360_fastcat` is a Ruby script that concatenates multiple Fusion 360-generated G-code files while cleaning and optimizing them. It removes all Fusion 360–specific comments and fixes rapid move feedrate issues imposed by the Fusion 360 Personal Use post processor, ensuring that rapid moves run at full speed and transitions between files are safe.

## WARNING / DISCLAIMER

This software is provided "as-is" without any warranties or guarantees. Use it at your own risk. The author(s) assume no responsibility or liability for any **damage to your CNC machine or other equipment** resulting from the use of this script. Always thoroughly verify, simulate, and review the generated G-code before running it on your machine. **Use of this script may lead to unexpected machine behavior, damage, or personal injury.**

## Features

- **Fusion 360 Comment Removal:** 
  
  Remove all comments related to Fusion 360/F360 (e.g., those discussing reduced rapid feed rates, machining time, etc.).
  
- **Rapid Move Feedrate Fix:** 
  
  Automatically removes any F0 feedrate parameters from G0/G1 moves so that your machine uses its full rapid speed.
  
- **Safe File Concatenation:** 
  
  Retains the proper initialization (header) from the first file and inserts a tool-change sequence between subsequent files to ensure safe transitions.
  
- **Clean Output:** 
  
  Produces a single G-code file without unwanted initialization or comments.

## Requirements

- Ruby 2.0 or higher

## Usage

1. **Make the script executable** (if necessary):
   
   - Use `chmod +x f360_fastcat` in your terminal.
   
2. **Run the script** by specifying one or more input G-code files and an output file.  
   Optionally, use the `-v` or `--verbose` flag for verbose output.

   **Example:**

       ./f360_fastcat input1.nc input2.nc output.nc

   This command will concatenate `input1.nc` and `input2.nc` into a single file `output.nc`, with Fusion 360 comments removed and rapid move feedrate corrections applied.

## Contributing

Contributions, issues, and feature requests are welcome! Please use the GitHub issue tracker to submit bugs or suggestions.

## License

This project is released under the MIT License.
