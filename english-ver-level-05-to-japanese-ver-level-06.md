# english-ver-level-05-to-japanese-ver-level-06.md

## English ver LEVEL 05 = Japanese ver Level 06 MAP

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
  000000111111111122222222223333333
  456789012345678901234567890123456
04@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@04
05@..@..@@@@@@@@.....@@@@@...@@@@@@05
06@@....@@@U@@.F.....@@@@@@@M@@@@@@06
07@@.@.T@@...@@@.....@@..@.......@@07
08@@.@@@@@.....M.....@@..@@@@@@@.@@08
09@@..@@@@@M@@@@.....@@@W@.......@@09
10@@@..........@@@T@@@@@B@.@@.@@@@@10
11@..@@@@.@@@@..@@@@.@@@W@@.....@@@11
12@..@@@..@@@@@.@@.@B@@@.@@@@@@.@@@12
13@B@....@@..........XL..X.D.@..@@@13
14@.@.@@@@@.@D@@@@@@@.@@@@@@.@@.@@@14
15@.@.@@@.L.@XTTTTTTT.@@@@.L.M..@@@15
16@.@.@..@@.@.@@@@@@@@@@@@@@.@@.@@@16
17@.@.@..B..@....@@@@@@......@..@@@17
18@.@.@..@@@@@...@.L.L..@@@@@@..@@@18
19@...@@@..@@@@@@@.@.@@......@@@.@@19
20@...@.DI.@@@@@@@.@@@@@@@@...@@.@@20
21@@@.@.@..@@......@...M.@.@....M@@21
22@.@.@.@@@@@M@@@@MB...@@...@..@.@@22
23@.@.@.M.@.....@@.@...@@.@.......@23
24@...@.@@@.....@@.@@@@@@...@.@...@24
25@.@.@.@U......D..@@@.@@..X....@.@25
26@.@.@.@@@.....@@.@...M.@..@.....@26
27@.@.@.M.@.....@@.D...@@@.@.@..@.@27
28@.@@@.@@@@@@@@@@.@....@.M....@..@28
29@...@.@T.@@@@@@@B@@..@@@..@.....@29
30@.@.@.@.XDX..@@@.@@@@@@..@S@.@.@@30
31@.@@@.@..@...@.XX@..@@@..@.@...@@31
32@.....@@I@...@.TP@P..@@@@@.@@@M@@32
33@..@@.@@.@..I@D@X@..@@@@@@..@@.@@33
34@@..@....@@@@@.@@@...@@@@@@.@@@@@34
35@@@...@@@@@@..@@@@@B@....@@.@@@@@35
36@@@@@.................@@....@@@@@36
37@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@37
  000000111111111122222222223333333
  456789012345678901234567890123456
```

Items
01 (22,05) Drumstick
02 (16,06) Cheese, Bro Potion
03 (12,07) Ven Potion
04 (14,07) Torch (Charges=13)
05 (17,24) Iron Key
06 (18,34) Iron Key
07 (26,26) Iron Key, Mail Aketon
08 (26,21) Iron Key
09 (15,21) Large Shield
10 (27,28) Ros Potion, Vi Potion, Drumstick, Torch (Charges=15)
11 (34,33) Magical Box (Blue)
12 (34,19) Iron Key, Torso Plate
13 (28,15) Magical Box (Green)
14 (29,11) Drumstick (2)
15 (28,10) Yew Staff (Charges=10)
16 (32,09) Casque’n Coif
17 (29,05) Vorpal Blade (Charges=14)
18 (25,08) Solid Key
19 (22,11) Corn, Throwing Star (2)
20 (18,17) Drumstick
21 (18,18) Mithral Aketon, Slayer (2)
22 (11,15) Magical Box (Green) (2)
23 (09,17) Torch (Charges=15)
24 (06,11) Magical Box (Blue)
25 (12,21) Vorpal Blade (Charges=0)
26 (16,30) Crossbow
27 (14,33) Chest [Slayer, Water Flask, Drumstick]
28 (24,32) Mithral Mail

Inscriptions
I01 (12,25) “The riddle room”
I02 (13,23) “I am all I am none”
I03 (16,23) “A golden head and tail but no body”
I04 (13,27) “Hard as rocks blue as sky twinkle in womans eye”
I05 (16,27) “I arch yet have no back”
I06 (22,26) “The grave of king Filius explorer of combinations”
I07 (24,22) “The grave of king Milias the golden who even”
I08 (24,23) “In death thirsts for bullion.”
I09 (25,18) “If you want to stay alive you better turn and run”
I10 (25,17) “I hate cowards”
I11 (25,19) “I don’t like to be ignored”
I12 (23,14) “Test your strength”
I13 (19,09) “Ha ha ha”
I14 (30,33) “Altar of Vi”

Locks
L01 (22,23) Gold Coin
L02 (21,18) Iron Key
L03 (23,18) Iron Key
L04 (27,17) Iron Key
L05 (30,16) Iron Key
L06 (25,13) Stone Key
L07 (13,16) Iron Key

Notes
A. (13,25) Each of the four alcoves requires one of these four items: a Mirror Of Dawn, a Gold Coin, a Blue Gem and a Bow. Once three items are in place, the door will open. The fourth item will reveal the hidden alcove.
B. (18,31) Pull the lever, then put any item on ground in the teleporter (do not throw it) so that it gets at (20,33). The door will then open.
C. You need to press the two buttons at (24,25) and (25,28) to open the wall. The two other buttons are already in the correct state.
D. A skeleton must walk on the pressure pad to open the wall. Leaving an item on floor will not work.

Creatures
01 (13,07) Skeleton
02 (18,34) Wizard Eye
03 (23,27) Wizard Eye
04 (23,22) Skeleton (2)
05 (30,23) Skeleton Generator (4)
06 (34,22) Wizard Eye Generator (2)
07 (34,20) Skeleton (2)
08 (29,07) Skeleton (4)
09 (11,15) Giant Wasp (3)
10 (11,10) Skeleton (2)
11 (05,11)-(06,12) Wizard Eye (4)
12 (05,24) Wizard Eye Generator (1-4)
13 (09,25) Skeleton (2)
14 (11,21) Skeleton (4)
15 (12,19) Skeleton (1)
16 (11,27) Skeleton (4)
17 (11,23) Skeleton (2)
18 (12,33) Skeleton Generator (1-4)
19 (15,33) Giant Wasp Generator (1)
20 (16,32) Skeleton Generator (1)
21 (23,33) Wizard Eye
