# english-ver-level-02-to-japanese-ver-level-03.md

## English ver LEVEL 02 = Japanese ver Level 03 MAP

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
* I : 不可視スイッチ（Invisible plate - 床を踏むことで動作する見えないほど小さなスイッチ）
* U : 上り階段（Stairs up - 一つ上の階へ移動できる）
* S : 下り階段（Stairs down - 一つ下の階へ移動できる）
* T : テレポーター（Teleporter - 違う場所へワープする）
* W : 点滅テレポーター（Blinking teleporter - 出現、消滅を交互に繰り返すテレポート）
* `>` : 右回転スピナー (Spinner - 進入した向きから90度時計回りに回転する)
* `<` : 左回転スピナー (Spinner - 進入した向きから90度反時計回りに回転する)
* `^` : 180度回転スピナー (Spinner - 進入した向きから180度反転する)

```
  0000001111111111222222222233333333
  4567890123456789012345678901234567
09@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@09
10@.....<..@@@@@......@@@@@@@@@@@@@@10
11@@.@.@.@.@@@..@@.@.@.@@@@@@.M@@@@@11
12@........@@@...@@@@...@@@.@@.@@@@@12
13@@.@.@.@.@@@....P.@@@.@@@.....@@@@13
14@...>.^....@@@@@@TX@...@@.@@.@@@@@14
15@@.@.@.@.@.@....@P.@....@@@@...@@@15
16@...>.>..@.@..@X..@@@@@@@@@@@@.@@@16
17@@.@.@.@.@.@M@@@@@@@@@@@@@.@...@@@17
18@...>....@.@.....@@@T@.....@.@@@@@18
19@M.@.@.@F@.@@@@@.@@@.@.@@@.@...@@@19
20@.@@@@@@.@.....@.@@@@@...@.@@@.@@@20
21@@@T@@@@@@@@@@B@B@@@@@@@.@.@...@@@21
22@@@.@@@....@@@.@.@@@@..D.@.@@@.@@@22
23@.M@..@..@L@@.....@@@P@@@@.....@@@23
24@.@@..@..@.B.......B.X...@.@@@@@@@24
25@..M.@@@.@@@@.....@@@@@@.@.....@@@25
26@@..@XBP.@.B.......B..@@.@@@@@.@@@26
27@...@.@@@@.@@.....@@@.@..@...@.@@@27
28@@.@@.D.@@..@@@.@@@@..@.@@...@.@@@28
29@...@@@.@.@...@.@@...@@......@..@@29
30@...@@@L@T@...@..@.@..@@@@@@@@@@@@30
31@@......@@..@.@@.@......@@S@@@@@@@31
32@@..@@@@.@....@@.@@@@@@..@...@@@@@32
33@@@@@@@@M@@@@.@@.@@@.B.@..@..@@@@@33
34@..............@.@...@.@..@......@34
35@D@D@D@D@D@D@D@@.@@.@@....@@L@M@L@35
36@T@T@T@T@T@T@T@@.@....@@@.@@.@.@.@36
37@@@@@@@@@@@@@@@@.@@@@.@...@@@@@@.@37
38@@@@.W......@@@@.@....@...@@.....@38
39@@@@@@@@@@@M@@@@.@@@@@@@@@@@.@..@@39
40@@U....................L.L.L.@..@@40
41@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@41
  0000001111111111222222222233333333
  4567890123456789012345678901234567
```


Items
01 (14,38) Bezerker Helm, Suede Boots, Leather Pants, Leather Jerkin
02 (13,38) Arrow, Waterskin, Cheese
03 (08,38) Compass
04 (21,23) Chest [Apple, Cheese, Scroll (“Ya will create a stamina potion”), Scroll (“Some doors can be opened with a Zo spell”), Gold Coin (2)]
05 (17,29) Drumstick
06 (05,34) Chest [Mirror Of Dawn]
07 (12,32) Drumstick, Gold Key, Apple, Leather Jerkin
08 (09,27) Silver Coin
09 (09,28) Bread
10 (06,31) Arrow
11 (05,27) Wand (Charges=15)
12 (05,23) Chest [Silver Coin, Copper Coin (3), Magical Box (Blue)]
13 (08,25) Gold Key
14 (08,23) Corn, Apple, Cheese (2)
15 (09,24) Leather Pants
16 (14,20) Bread
17 (06,12) Cheese
18 (12,16) Arrow
19 (12,20) Cheese, Wooden Shield
20 (05,20) Gold Key, Sabre, Fine Robe (Body), Fine Robe (Legs)
21 (18,11) Arrow
22 (27,15) Gold Key
23 (24,15) Helmet
24 (24,14) Elven Huke
25 (28,22) Apple
26 (34,22) Sling
27 (32,21) Cheese
28 (32,19) Apple
29 (29,14) Rabbit’s Foot
30 (31,11) Blue Gem, Drumstick
31 (32,29) Cheese
32 (30,27) Gold Key
33 (31,27) Bezerker Helm
34 (32,27) Bread
35 (28,33) Arrow
36 (22,38) Gold Key
37 (32,40) Ra Key
38 (32,38) Empty Flask, Scroll (“The spell Des Ew weakens nonmaterial beings”)
39 (34,39) Torch (Charges=15)
40 (35,39) Torch (Charges=15)
41 (35,40) Cheese, Bread, Drumstick, Apple
42 (32,36) Empty Flask, Mail Aketon
43 (34,36) Drumstick (2), Sword

Inscriptions
I01 (19,28) “Choose your door choose your fate”
I02 (16,26) “Chambers of the guardian”
I03 (16,24) “The vault”
I04 (14,24) “You must pay for your entrance.”
I05 (12,26) “Cast your influence, cast your might”
I06 (18,22) “The Matrix”
I07 (20,22) “Time is of the essence”
I08 (20,18) “Hit and run”
I09 (22,24) “Room of the gem”
I10 (25,24) “Step right up going down…”
I11 (22,26) “Creature cavern”
I12 (32,39) “Vi altar of rebirth”

Locks
L01 (11,34) Mirror Of Dawn
L02 (14,24) Gold Coin (2)
L03 (11,29) Silver Coin
L04 (05,23) Copper Coin
L05 (26,24) Blue Gem
L06 (26,40) Gold Key
L07 (28,40) Gold Key
L08 (30,40) Gold Key
L09 (36,36) Gold Key
L10 (33,34) Gold Key

Notes
A. (12,26) Cast a Zo spell to open the door, then throw an item to close the pit.
B. (21,16) Press the button and throw an item in the teleporter.

Creatures
01 (15,30) Trolin (3)
02 (13,34) Rockpile
03 (12,32) Mummy (2)
04 (11,22) Trolin (2)
05 (11,23) Mummy (4)
06 (06,29) Rockpile (2)
07 (06,26) Trolin (1)
08 (05,25) Trolin (4) [Cheese]
09 (23,12) Trolin (2)
10 (26,19) Rockpile (2)
11 (35,29) Trolin (2)
12 (32,21) Mummy (4)
13 (32,17) Rockpile (2)
14 (24,30) Trolin (2)
15 (22,31) Mummy (3)
16 (28,37) Trolin (3)
17 (29,38) Trolin Generator (1-4)
18 (25,37) Trolin (4) [Screamer Slice, Cheese]
19 (32,36) Rockpile (2)
20 (34,36) Trolin (2)
