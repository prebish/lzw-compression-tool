
# LZW Compression Tool

A Java-based implementation of the LZW (Lempel-Ziv-Welch) compression algorithm, featuring adaptive codeword size and optional codebook reset functionality. This project compares various implementations and analyzes their performance.

### Table of Contents

- [Overview](#overview)
- [Installation & Setup](#installation--setup)
    1. [Clone the Repository](#1-clone-the-repository)
    2. [Compile the Program](#2-compile-the-program)
- [Usage](#usage)
    - [Running the Compression and Decompression](#running-the-compression-and-decompression)
    - [Testing and Debugging](#testing-and-debugging)
- [Performance Analysis](#performance-analysis)
- [License](#license)

## Overview

This project implements the LZW compression algorithm in Java. The goal is to enhance the original algorithm by using adaptive codeword sizes and allowing for codebook resets when the maximum codebook size is reached. The project includes comparisons between the original 12-bit implementation, a 9-16 bit adaptive implementation, and the Unix `compress` tool.

## Installation & Setup

Ensure that you have the latest version of the Java Development Kit installed.  
You can download it [<u>**here**</u>](https://www.oracle.com/java/technologies/downloads/).

### 1. Clone the Repository
```bash
git clone https://github.com/username/lzw-compression-tool.git
```

### 2. Compile the Program
```bash
cd ./lzw-compression-tool
javac -d build ./src/*.java
```

## Usage

Run the program using the following commands, replacing `<input_file>` with your file and `<output_file>` with the desired output filename.

### Running the Compression and Decompression

**Compression** (with adaptive codeword size and optional reset):
```bash
java -cp build LZW - r < <input_file> > <output_file>.lzw
```

**Decompression**:
```bash
java -cp build LZW + < <input_file>.lzw > <output_file>.rec
```

### Testing and Debugging

To test and debug the program, use the provided `test.sh` and `test.bat` scripts, or run the Java commands manually. Debugging output can be redirected to a file using:

```bash
java LZW - < input.txt > input.lzw 2> debug-compress.txt
java LZW + < input.lzw > input.rec 2> debug-expand.txt
```

This allows side-by-side comparison of the compression and expansion processes.

## Performance Analysis

This project includes a detailed analysis comparing the compression ratios of different LZW implementations. Below is a summary of the performance on various test files:

| File Name          | Original Size (KB) | 12-bit CR (KB) | 9-16-bit CR (KB) | 9-16-bit CR w/ Reset (KB) | Unix `compress` CR (KB) |
|--------------------|--------------------|----------------|-------------------|---------------------------|-------------------------|
| gone_fishing.bmp   | 17                 | 9.1            | 9                 | 9                         | 9                       |
| medium.txt         | 25                 | 12.8           | 13                | 13                        | 13                      |
| code2.txt          | 57                 | 23.2           | 21                | 21                        | 21                      |
| code.txt           | 71                 | 30.1           | 24                | 24                        | 24                      |
| assig2.doc         | 85                 | 72.8           | 40                | 40                        | 40                      |
| Lego-big.gif       | 92                 | 126            | 120               | 120                       | 120                     |
| frosty.jpg         | 124                | 173            | 160               | 160                       | 160                     |
| edit.exe           | 231                | 244.9          | 153               | 149                       | 148                     |
| wacky.bmp          | 901                | 4.2            | 4                 | 4                         | 4                       |
| winnt256.bmp       | 154                | 155            | 62                | 62                        | 62                      |
| large.txt          | 1193               | 585            | 491               | 503                       | 556                     |
| all.tar            | 2960               | 1803           | 1751              | 1151                      | 1142                    |
| bmps.tar           | 1080               | 903            | 584               | 577                       | 556                     |
| texts.tar          | 1350               | 989            | 584               | 577                       | 556                     |

*CR: Compressed File Size, rounded to the nearest integer.*

### Observations

- The 9-16 bits implementation generally provided better compression ratios compared to the 12-bit version.
- The Unix `compress` tool consistently performed well, showing high optimization.
- Implementing the reset option did not significantly impact compression ratios, indicating that the adaptive codeword size is a critical factor.

## License
This project is licensed under the **GNU License** - see the `LICENSE` file for details.
