# dungeon-master-sfc-jp

SFC版『ダンジョン・マスター』の正確な攻略データを蓄積するためのリポジトリです。

主な目的は、生成AIによるハルシネーション（存在しない攻略情報の創作）を防ぎ、原作に忠実なデータを提供することです。

また、将来的には、プレイヤーの謎解きの楽しさを損なわない「段階的なヒント」を提供できるAIアシスタントへの応用も視野に入れています。

## Scope of This Repository

This repository focuses on the following versions:

- Original Dungeon Master (PC version and faithful recreations such as RTC)
- Japanese Super Famicom version

Fan-made dungeons, custom campaigns, and unofficial expansions are outside the scope of this repository.

Only data originating from the official game versions listed above is considered canonical.

## Level Numbering

To bridge the gap between global technical data and the Japanese community's conventions, this repository establishes a clear mapping between the English canonical database notation and the Japanese representation.

- **English version (Encyclopaedia/Technical Standard):** Numbers floors from **LEVEL 00 to LEVEL 13**.
- **Japanese version (Official Manual/Community Standard):** Numbers floors from **LEVEL 01 to LEVEL 14** as the official Japanese instruction manual explicitly designates the 1st floor as LEVEL 01.

All map files and cross-references within this repository use the following unified mapping:

| English Notation | Japanese Notation | Floor (English) | 階層 (Japanese) |
| :--- | :--- | :--- | :--- |
| **LEVEL 00** | LEVEL 01 | 1st floor | 1階 |
| **LEVEL 01** | LEVEL 02 | basement 1st floor | 地下1階 |
| **LEVEL 02** | LEVEL 03 | basement 2nd floor | 地下2階 |
| **LEVEL 03** | LEVEL 04 | basement 3rd floor | 地下3階 |
| **LEVEL 04** | LEVEL 05 | basement 4th floor | 地下4階 |
| **LEVEL 05** | LEVEL 06 | basement 5th floor | 地下5階 |
| **LEVEL 06** | LEVEL 07 | basement 6th floor | 地下6階 |
| **LEVEL 07** | LEVEL 08 | basement 7th floor | 地下7階 |
| **LEVEL 08** | LEVEL 09 | basement 8th floor | 地下8階 |
| **LEVEL 09** | LEVEL 10 | basement 9th floor | 地下9階 |
| **LEVEL 10** | LEVEL 11 | basement 10th floor | 地下10階 |
| **LEVEL 11** | LEVEL 12 | basement 11th floor | 地下11階 |
| **LEVEL 12** | LEVEL 13 | basement 12th floor | 地下12階 |
| **LEVEL 13** | LEVEL 14 | basement 13th floor | 地下13階 |

## Coordinate System

This repository uses the original Dungeon Master global coordinates.

X increases to the right.
Y increases downward.
Coordinates are preserved exactly as shown in the source maps.
X coordinates do not necessarily start at 0.
Y coordinates do not necessarily start at 0.
Do not convert, normalize, or offset coordinates unless explicitly instructed to do so.

The original coordinates are considered canonical. Any alternative coordinate systems are derived representations.
