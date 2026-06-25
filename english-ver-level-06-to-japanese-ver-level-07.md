# english-ver-level-06-to-japanese-ver-level-07.md

## English ver LEVEL 06 = Japanese ver Level 07 MAP

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
  0000001111111111222222222233333
  4567890123456789012345678901234
05@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@05
06@.@.M...................B.....@06
07@M@.@..@@@.@@@.@@@.@@@.@@.....@07
08@...@..@.@.@.@.@.@.@.@.@@..@..@08
09@.@@@L@@L@@@L@@@L@@@L@@@@.....@09
10@.@@...@..@@..@@..@@..@@@@@@@M@10
11@.@.........................@.@11
12@.@L@.@@@@@@@@@.@@@@@@@@@@@.@.@12
13@.@.@.@...@...@.@...@...@@@.@@@13
14@.@.@.@.@.@...@.@...@.@.@@@.@@@14
15@.@.@.@.@.@@@@@.@@@@@.@.@@@.@@@15
16@.@.@.@.@.@...@.@...@.@.@@@.@@@16
17@.@.@.@.@.@.@.@.@.@.@.@.@@@.@@@17
18@.@.@B@.@.@.@.@.@.@.@.@.@@@.@@@18
19@.@.@.@.@.@.@.@D@.@.@.@.@@@L@@@19
20@.@.@.@.@.@.@.L.L.@.@.@.@@@..@@20
21@.@.@B@.@.@.@.@@@.@.@.@.@@@.@@@21
22@.@.@.@.@.@.@..M..@.@.@.@@@.@@@22
23@.@.@.@.@.@.@@@@@@@.@.@.@@@.@@@23
24@.@.@@@.@.@.........@.@.@@@L@@@24
25@.@.@@@.@.@@@@@.@@@@@.@.@@@..@@25
26@.@.@@@.@.............@.@@@.@@@26
27@.@.@@@.@@@@@@@@@@@@@@@.@@@L@@@27
28@.@.@@@.................@@@...@28
29@.@.@@@@@@@@@@@.@@@@@@@@@@..@.@29
30@.@.............@@..@....@U@@.@30
31@.@@@@@@@@@@@@@@T@....@@.@@@S.@31
32@.@.........@@@@...@@.@..@@@@@@32
33@...........B.@@@@@@@@@@@@@@@@@33
34@@@.........@..........S@@@@@@@34
35@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@35
  0000001111111111222222222233333
  4567890123456789012345678901234
```

Items
01 (27,32) Magical Box (Green)
02 (33,28) Scroll “Fireball Ful Ir. Fire Shield Ful Bro Neta.”
03 (33,29) Scroll “Light Oh Ir Ra. Darkness Des Ir Sar.”, Apple, Corn
04 (31,25) Scroll “The keys to passage lie hidden deep.”
05 (09,20) Magical Box (Green)
06 (09,23) Ven Potion, Ful Bomb, The Inquisitor
07 (09,07) Empty Flask (3)
08 (10,07) Scroll (3) “Neither Chaos nor Order is truly balanced”, “The Firestaff can restore balance or destroy it.”, “The power gem is sealed in the mountain by a strange magical force.”
09 (10,06) Orange Gem, Corbamite, Magnifier
10 (14,08) Torch (Charges=15)
11 (18,08) Boulder, Rock
12 (22,08) Empty Flask
13 (26,08) Water Flask
14 (29,08) Scroll “Balance is the ultimate good”
15 (31,09) Ashes, Tourquoise Key
16 (33,12) Ra Key, Scroll (5) “I fear for the people of the world should the power gem and the Firestaff get in the wrong hands”, “I have given the Firestaff much power. Power to do and undo. Power to break and mend.”, “The Firestaff can contain a being of pure alignment with its fluxcage.”, “Once fluxcaged a being can be transmuted by the power of the staff which should always be used for balance.”, “Zokathra might create a plasma that could burn through the amalgam encasing the gem.”
17 (12,08) Bolt Blade (Charges=14), Flamebain
18 (16,08) Magical Box (Green), Crown Of Nerra
19 (20,08) Boots Of Speed, Dragon Spit (Charges=10)
20 (24,08) Gem Of Ages, Illumulet, Sceptre Of Lyf (Charges=15)
21 (05,06) Winged Key
22 (19,20) The Firestaff

Inscriptions
I01 (31,28) “The tomb of The Firestaff”
I02 (10,10) “Danger Enter with caution”
I03 (09,08) “Clean flasks”
I04 (10,08) “Notes scrolls formulas spells”
I05 (09,06) “Sundry supplies”
I06 (14,07) “Fire elements”
I07 (18,07) “Earth elements”
I08 (22,07) “Air elements”
I09 (26,07) “Water elements”
I10 (33,11) “Reading room Keep out”. This inscription is actually not visible in the game because it is disabled. You can view it in a dungeon editor.

Locks
L01 (32,28) Ra Key
L02 (32,25) Ra Key
L03 (32,20) Ra Key
L04 (25,10) Tourquoise Key
L05 (21,10) Tourquoise Key
L06 (17,10) Tourquoise Key
L07 (13,10) Tourquoise Key
L08 (08,10) Ruby Key
L09 (08,11) Ra Key
L10 (17,21) Master Key
L11 (21,21) Master Key

Creatures
01 (09,19) Stone Golem
02 (09,22) Stone Golem
03 (18,22) Stone Golem
04 (20,22) Stone Golem
05 (19,34) Stone Golem
