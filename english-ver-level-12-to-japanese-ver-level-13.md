# english-ver-level-12-to-japanese-ver-level-13.md

## English ver LEVEL 12 = Japanese ver Level 13 MAP

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
  22222233333333334444444
  45678901234567890123456
29@@@@@@@@@@@@@@@@@@@@@@@29
30@........@@@@@@@..B..@@30
31@.@@@@@@.I...@@...@..@@31
32@.@@@@U@@@T..@@....@B@@32
33@......@.@@@@@....@..@@33
34@.@@@@.M...@@........@@34
35@.@@@@.@@@.@@.........@35
36@........@.U@...@.....@36
37@.@@@@@@.@@@@.........@37
38@.@@U@@@...@@.........@38
39@.M.M@@@@@.@@.......P.@39
40@@@@S@@@@@.@@....P....@40
41@@T@@@.S@@..MI..P@....@41
42@...@@.@@@@@@.....@...@42
43@.@..@..............@.@43
44@@..@@@@@@@@@P........@44
45@@.@.@@@@@@@@....@...@@45
46@@.@......@@@...@....@@46
47@@.@......@@@........@@47
48@@..I.....@@.........@@48
49@..@......@@@.@@@@@@@@@49
50@@@@@@@@@@@@@@@@@@@@@@@50
```

Items
01 (43,31) Flamitt (Charges=7), The Hellion

Locks
L01 (25,38) Skeleton Key

Notes
A. (35,41) Lord Chaos cannot be killed by using normal weapons and spells. You must use The Firestaff (completed with the power gem from Level 13) as follow:

Use War Cry to “push” Lord Chaos into a corner,
Block him by using the Fluxcage spell of The Firestaff all around him except on the square he is standing in.
Use the Fuse spell of The Firestaff on Lord Chaos.
The easiest way to Fuse Lord Chaos is to enter the small room at (43,31), close the doors and sleep. Lord Chaos will teleport himself into the room and wake you. You just have to make two fluxcages before you can fuse him.

Creatures
01 (27,48) Black Flame Generator (1)
02 (32,31) Black Flame Generator (1)
03 (37,40) Black Flame Generator (1)
04 (38,40) Black Flame Generator (1)
05 (39,40) Black Flame Generator (1)
06 (37,42) Black Flame Generator (1)
07 (38,42) Black Flame Generator (1)
08 (38,47) Demon
09 (43,46) Black Flame
10 (43,41) Black Flame Generator (1)
11 (44,40) Black Flame Generator (1)
12 (45,39) Black Flame Generator (1)
13 (42,39) Demon (2)
14 (44,35) Demon (2)
15 (44,34) Black Flame Generator (1)
16 (39,33) Black Flame
17 (40,30) Lord Chaos
18 (44,30) Demon
