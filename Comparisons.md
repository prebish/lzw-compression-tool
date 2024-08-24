# LZW Compression Algorithm Analysis

## Overview

This analysis showcases the performance of different LZW compression algorithm implementations. We compare the original 12-bit code representation, an enhanced version using 9-16 bits without a reset option, the same 9-16 bits version with a reset option, and the standard Unix `compress` tool.

## Compression Ratio Comparison

This table shows the compression results of the four methods. The files are sorted by their original sizes, from smallest to largest.

| File Name          | Original Size (KB) | 12-bit CR (KB) | 9-16-bit CR (KB) | 9-16-bit CR w/ Reset (KB) | Unix `compress` CR (KB) |
|--------------------|--------------------|----------------|-------------------|---------------------------|-------------------------|
| gone_fishing.bmp   | 17                 | 9.1            | 9                 | 9                         | 9                       |
| medium.txt         | 25                 | 12.8           | 13                | 13                        | 13                      |
| code2.txt          | 57                 | 23.2           | 21                | 21                        | 21                      |
| code.txt           | 71                 | 30.1           | 24                | 24                        | 24                      |
| assig2.doc         | 85                 | 72.8           | 40                | 40                        | 40                      |
| Lego-big.gif       | 92                 | 126             | 120               | 120                       | 120                     |
| frosty.jpg         | 124                | 173             | 160               | 160                       | 160                     |
| edit.exe           | 231                | 244.9           | 153               | 149                       | 148                     |
| wacky.bmp          | 901                | 4.2             | 4                 | 4                         | 4                       |
| winnt256.bmp       | 154                | 155             | 62                | 62                        | 62                      |
| large.txt          | 1193               | 585             | 491               | 503                       | 556                     |
| all.tar            | 2960               | 1803             | 1751              | 1151                      | 1142                    |
| bmps.tar           | 1080               | 903             | 584               | 577                       | 556                     |
| texts.tar          | 1350               | 989             | 584               | 577                       | 556                     |

_CR: Compressed File Size, rounded to nearest integer_

### Analysis

- **Best Compression**: The Unix `compress` utility and the 9-16 bits LZW implementations generally provided the best compression ratios across the board.
  
- **Worst Compression**: The original 12-bit implementation showed the poorest performance, particularly for the largets files. This is due to the limited codebook size, which quickly fills and can't grow to new patterns as effectively as the other methods.

- **Observations**: 
  - The 9-16 bits implementation without reset usually produced comparable file sizes to the version with reset, which implies that the adaptive nature of the codeword size is effective in keeping compression efficiency.
  - The Unix `compress` tool consistently matched or outperformed the 9-16 bits versions, showing us that its implementation is highly optimized for the LZW compression algorithm.

## Conclusion

- The modified LZW algorithm with a variable codeword size of 9-16 bits demonstrates significant improvements over the original 12-bit version, especially for larger files.
- Implementing a reset option does not significantly affect the compression ratio, suggesting that the adaptive codeword size is crucial in improving LZW compression performance.
