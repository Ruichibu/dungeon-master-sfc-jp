# english-ver-level-09-to-japanese-ver-level-10.md

## English ver LEVEL 09 = Japanese ver Level 10 MAP

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
  01111111111222222222233333333334
  90123456789012345678901234567890
09@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@09
10@@@@@S....@@@U@..........@@.@@@@10
11@@@@@@@@...@..@.@@.@@.@@..@M@@@@11
12@...@@@@@@.@..@.@...@.@@@....@@@12
13@@@.@@@..@.@..@.@T..@.@...@@.@@@13
14@@.....@.@..@@@.@@@@@...@.@@.@@@14
15@@@@.@.@.@@............@@....@@@15
16@..@.@...@@@@@@@@.@@.@.@.@@B@@@@16
17@....@.@........@.......M@@.@@@@17
18@.@@@@@@@@@@@@@..@@@@@B@@@....@@18
19@.@@...@.T.@.T.@....@@......@.@@19
20@..L.@.@.@...@.@@@.X@@@@.@@.@.@@20
21@@@@...@.T.@.T.@@@@D@@@@.......@21
22@@@@.@...@.T.@...U@..L..@@.@@@.@22
23@@@@...@.T.@.T.@@@@D@@@.@@.....@23
24@..L.@.@.@.T.@.@...X@T@XXX@...@@24
25@.@@...@...@...@.@@@@.@X@X@....@25
26@.@@@@@@@@@@@@@@.@...@@X@XT@..@@26
27@.....@@.......@.@.@..@X@X.@...@27
28@..@.....@..@....@@...@XXX@..@.@28
29@@@..@...@.@.@.@@.......@@...@.@29
30@@@.@@@@@@.@.@@@..@@@@@@@@.@.@.@30
31@.@..@.....@.....@@@@..........@31
32@M@@@@@@@@@..@@..@@U@.@@@B@@B@@@32
33@......IB...@@@@@@@.M.@@@....@@@33
34@...@..@@@@@...T@@@S@@U.S@.....@34
35@@......@@......@@@@@.@@@....@.@35
36@@@@....@@..@M@@.F.M....@.@.@@.@36
37@......@@@B@@.@.@@@@@..........@37
38@.....@@@@.@@@@.@......@.@.@@.@@38
39@.....@...I.......@.@@@@M@..@.@@39
40@.@@@@@.@@@.@@@.@@@.@@@..@@...@@40
41@.I.....@@@.@@@.....@@..@@@@@@@@41
42@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@42
  01111111111222222222233333333334
  90123456789012345678901234567890
```

Items
01 (30,25) Yew Staff (Charges=12)
02 (13,22) Key Of B
03 (10,12) Apple, Bread
04 (15,31) Corn, Cheese
05 (35,27) Cheese, Water Flask, Ful Bomb
06 (27,26) Corn
07 (27,27) Torch (Charges=15)
08 (16,36) Armet
09 (10,31) Speedbow
10 (24,35) Foot Plate, Leg Plate
11 (22,37) Drumstick, Moonstone
12 (24,37) Corn
13 (32,40) Scroll “Shield potion Ya Bro. Magic shield Ya Ir.”
14 (27,36) Torso Plate, Ful Bomb
15 (25,36) Boots Of Speed
16 (38,40) Bread
17 (38,21) Bread
18 (33,16) Shield Of Lyte, Scroll “Mana potion Zo Bro Ra creates a pure mana potion.”
19 (36,10) Hardcleave
20 (28,13) Magnifier

Inscriptions
I01 (24,22) “Beware my twisted humor the deceiver the snake”
I02 (13,22) “Choose a door”
I03 (32,23) “Zooooom”

Locks
L01 (13,21) Key Of B
L02 (13,23) Key Of B
L03 (29,22) Key Of B
L04 (30,32) Skeleton Key

Notes
A. (15,33) Creatures in this room are kept in place by invisible teleporters. Some of them are disabled by pressing the button at (16,33) or by walking at (11,41).
B. When you reach a corner of the Zooooom, you are teleported one step forward and turned 90 degrees. So if you enter the Zooooom forward, you have to step out of it with a step to the right.

Creatures
01 (15,22) Wizard Eye Generator (1-4)
02 (13,21) Skeleton
03 (17,16) Giggler
04 (20,17) Wizard Eye (3) [Key Of B]
05 (13,27) Skeleton (4) [Key Of B]
06 (18,27) Giant Scorpion
07 (25,31) Wizard Eye (2)
08 (10,33) Skeleton (4)
09 (10,34) Giggler (2)
10 (15,35) Wizard Eye
11 (15,36) Skeleton
12 (15,37) Wizard Eye
13 (14,38) Wizard Eye
14 (13,39) Skeleton
15 (14,39) Wizard Eye
16 (12,41) Giggler Generator (1)
17 (23,34) Giggler
18 (26,39) Giggler Generator (1)
19 (28,41) Giant Scorpion
20 (33,40) Skeleton
21 (39,28) Giant Scorpion
22 (37,25) Wizard Eye Generator (1-4)
23 (35,19) Giggler
24 (31,17) Giant Scorpion Generator (1)
25 (33,16) Wizard Eye [Skeleton Key]
26 (27,13) Giant Scorpion
27 (21,15) Giggler
