# english-ver-level-03-to-japanese-ver-level-04.md

## English ver LEVEL 03 = Japanese ver Level 04 MAP

## 【座標および階層表記に関する絶対ルール】
* 座標は `(Lxx, X, Y)` または壁面オブジェクト用の `(Lxx, X, Y, 面)` で表記する。
  * **Lxx** = 海外PC版基準の階層表記（L00 = 1階：勇者の館 / L01 = 地下1階）
  * **X** = 横座標（右に向かって 00〜52）
  * **Y** = 縦座標（下に向かって 00〜51）
  * **面（方角）** = N（北面）, E（東面）, S（南面）, W（西面）。そのマスから見た「壁の向き」を指す。

* **【壁面の3Dグリッド反転（裏表）ルール】**
  * マップ上のすべての「壁」は厚みのないプレーンとして隣り合うマスと共有されているため、あるマスの特定の面は、隣接するマスの反対の面と【物理的に全く同じ同一の壁】を指す。
  * AIは以下の空間の対応関係を自動で計算し、同一の壁面として処理すること。
    * `(Lxx, X, Y, N)` [マスの北の壁] ＝ `(Lxx, X, Y-1, S)` [北隣のマスの南の壁]
    * `(Lxx, X, Y, S)` [マスの南の壁] ＝ `(Lxx, X, Y+1, N)` [南隣のマスの北の壁]
    * `(Lxx, X, Y, W)` [マスの西の壁] ＝ `(Lxx, X-1, Y, E)` [西隣のマスの東の壁]
    * `(Lxx, X, Y, E)` [マスの東の壁] ＝ `(Lxx, X+1, Y, W)` [東隣のマスの西の壁]

* **【マップ外周（境界線）の絶対ルール】**
  * 各マップの有効範囲外（Xが00未満、または定義された最大値を超えるエリア / Yが00未満、または最大値を超えるエリア）は、データの有無に関わらず、ゲームシステム上**「絶対に進入不可能な外壁（境界壁）」**として処理される。
  * そのため、仮に `X=00` や `Y=00` が通路（`.`）であっても、その外側（`X-01` や `Y-01`）へ進むことはできない。

## 【確定したマッピング言語】
* . : 通路（Passage - 通れる）
* @ : 通常の壁（Wall - 通れない）
* F : 偽物の壁（Fake wall - 壁に見えるが、実は通れる通路）
* M : 動く壁（Movable wall - スイッチを押すことで通路になる壁）
* P : 落とし穴（Pit - 同じ座標の一つ下の階に落とされる。ダメージを受ける）
* H : 床に見える落とし穴（Hidden pit - 見えない落とし穴）
* D : 通常の扉（Door - 遠くのスイッチを押したり、レバーを下すことで開閉するドア）
* L : 鍵で開くドア（Locked door - 遠くの鍵穴に鍵を挿しこむことで開くドア）
* B : ボタンが付いてるドア（Door button - ドアに併設されているボタンで開閉できるドア）
* K : 破壊可能なドア（Breakable door - 強力な攻撃で破壊できるドア）
* X : 床スイッチ（Pressure plate - 床を踏むことで動作するスイッチ）
* I : 不可視/極小床スイッチ（Invisible / tiny plate ── 踏むと作動する見えない床スイッチ、見えないほど小さな床スイッチ）
* U : 上り階段（Stairs up - 一つ上の階へ移動できる）
* S : 下り階段（Stairs down - 一つ下の階へ移動できる）
* T : テレポーター（Teleporter - 違う場所へワープする）
* W : 点滅テレポーター（Blinking teleporter - 出現、消滅を交互に繰り返すテレポート）
* `>` : 右回転スピナー (Spinner - 進入した向きから90度時計回りに回転する)
* `<` : 左回転スピナー (Spinner - 進入した向きから90度反時計回りに回転する)
* `^` : 180度回転スピナー (Spinner - 進入した向きから180度反転する)

```
  00000000001111111111222222222233
  01234567890123456789012345678901
00..@@@@@@@@@@@@@..@@......@@@...@00
01.@..@..@....@@....@@@...@@@....@01
02.@@@@@@@..@.@@...@.@@.@.@@@.@@.@02
03.........@@.@@.@...@@@@B@...@..@03
04K@@@@@@P@@..@@.....@........@..@04
05..@@@@MX@@.@.B..@..@..@...@@@..@05
06.......@@..@.@..@..@..@@@@@@...@06
07@@@@@@D@@.@@.@.@...@.@@@@@....T@07
08.@@@@@S@...@..@@.@@@.@.....@@@@@08
09F.....@@...@..@@B@...@.@.@...@@@09
10...@@....@@@..@@.@..@@.@...@...@10
11.@@@@@@@@@@@.@...@..@@..@@@@@..@11
12.....M.S@..@.@.@.@..@@.@@@..@@.@12
13@B@@.@P@...@.@.@.@.@..@@@......@13
14...@.@@....@.@.@.@K@@.@@@..@@@@@14
15..@@.@@B@..@.@@@.@.@@.@T...@...@15
16.@...@@I@..@...@...@@T@.@@@@.@.@16
17.@B@@@@..@.@@@.@@@@..@@.@......@17
18@....@.F.@.B...T@@@.......@...@@18
19@....@@@.@@@@@@@..@@@@@@@@@...@@19
20@.I..@@..@@@@@..........@..@...@20
21@....@...@@@.F.....@@@@.B..@@@.@21
22@....@@.@@@@@@@@..@....@@@.B.@.@22
23@@....@.@......@.@@.@.@@@.@@...@23
24@@@@@B@.@......@..@...@@@T@@@@@@24
25@@@@@.@.@.@@@@.@@.@@@B@.@@@...@@25
26@@@@..@.@.@.T@..@.@...........@@26
27..I@.@..@.@@@@....@.@.@@@@....@@27
28.@...@.@@...@@@...@...@@...@@@@@28
29..@@@@.@@....@@@@@@@@@@@.@.@..@@29
30@..@@..@..@...D..T....K..@.....@30
31@......@..@...@@@@.@..@..@@@@@U@31
32@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@32
```

Items
01 (25,23) Drumstick
02 (23,31) Cheese, Water (Charges=3), Axe
03 (10,29) Gold Key
04 (12,21) Magical Box (Blue), Drumstick
05 (26,20) Scroll (“Ya Bro creates a magical shield potion”), Scroll (“The spell Oh Ven cast a cloud of poison.”)
06 (20,17) Teowand (Charges=15)
07 (23,11) Small Shield
08 (18,02) Basinet
09 (16,00) Leather Jerkin, Leather Pants
10 (14,06) Empty Flask
11 (10,12) Rapier
12 (06,18) Neta Potion, Drumstick
13 (02,23) Leg Mail
14 (01,22) Elven Boots
15 (03,18) Empty Flask
16 (00,08) Drumstick, Torch (Charges=15), Hosen
17 (10,09) Bow
18 (10,08) Gold Coin
19 (06,06) Horn Of Fear, Empty Flask

Inscriptions
I01 (30,30) “Prepare to meet your doom”
I02 (23,31) “Don’t let a closed door stop you”
I03 (29,07) “Shortcut”
I04 (14,17) “Shortcut back”
I05 (08,03) “This is my prisoner. Let him suffer.”
I06 (06,03) “You will regret that.”

Locks
L01 (25,13) Gold Coin
L02 (28,07) Gold Key

Notes
A. (19,30) A teleporter appears when the button is pressed, and teleports you in front of the door. Run through it before it closes.
B. Creatures cannot pass through this teleporter.
C. (01,14) This room is a good place to train because it contains a Screamer Generator, and Screamers are easy to kill. It is also a unlimited source of food (Screamer Slices), and you have a fountain downstairs.

Creatures
01 (26,28) Rockpile
02 (21,28) Screamer (4) [Gold Coin]
03 (21,24) Rockpile (3)[Gold Coin]
04 (11,29) Giant Wasp
05 (14,26) Magenta Worm (2) [Gold Coin]
06 (16,21) Magenta Worm (2) [Gold Coin]
07 (27,17) Ghost
08 (24,05) Magenta Worm Generator (2)
09 (15,06) Magenta Worm Generator (2)
10 (10,17) Magenta Worm Generator (2)
11 (08,14) Screamer Generator (2)
12 (07,23) Rockpile Generator (1)
13 (04,23) Magenta Worm Generator (2)
14 (04,15) Magenta Worm Generator (2)
15 (00,17) Screamer Generator (1-4)
16 (01,15) Screamer (4)
17 (07,05) Mummy
18 (02,01) Magenta Worm (2)
19 (03,01) Magenta Worm (2)
20 (05,01) Magenta Worm (2)
21 (06,01) Magenta Worm (2)
