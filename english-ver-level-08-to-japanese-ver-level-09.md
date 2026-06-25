# english-ver-level-08-to-japanese-ver-level-09.md

## English ver LEVEL 08 = Japanese ver Level 09 MAP

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
  11111111122222222223333333333444
  12345678901234567890123456789012
04@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@04
05@.@@@@@.....@@@......@@@...@@T@@05
06@..M......@.@...@......@...@@@@@06
07@..@.@@@..@....@@@@@@@.@......@@07
08@...@@@@@@@@@@..@..XXX.@@@@@..@@08
09@...@.......@@@@@..XXX.@@..@..@@09
10@..@..@..@@S@.....@@@@.@@@.@..@@10
11@..@.@..@.P@@.@@@@@..@...@.@..@@11
12@@.@...@.@P...@@@@@.@@@..@.@@B@@12
13@@@@..@@.@D@@@@@..@..@.....@@.@@13
14@@@...@..@.......@@@...@.@@...@@14
15@@@.@.@@....@@@.@@.@.@@@.@@..@@@15
16@@.@@..@@@I@U@@....@.@.....@..@@16
17@@M@@@..B..@.@@@@.@@@@.@@@.@@.@@17
18@....@@@@B@@......@@@@.@@@.@..@@18
19@@....@@..@@@@.@@@@.@@@@@.....@@19
20@.@....@..@.....@@@.@..D..@@..@@20
21@......@.@@@@@@@@.....@@@@@@.@@@21
22@@..@....@.@..@S....@@@@@@@@..@@22
23@@@.@.@@@@.@..@@@...@...@@@@@.@@23
24@@.........@..B...@@@.@....@@.@@24
25@@.@@...@@@@@@@.@@@P@.@@.@.@@.@@25
26@.....@..@@.@@@.@......@T@..@@@@26
27@@@@B@@@@@...@@.@.@@.@.@@@@..@@@27
28@@.....@.B..@@@.@.@@@@.@.@@@...@28
29@.@..@.@.@@@@@@.@@@@@@.@...@.@@@29
30@......@...@@@@.@U@..@.@.@.@.@@@30
31@@@.@@@.@@.@@U@.M.@..@.@.@.@.@@@31
32@.....@....@@.@@@S@@..@@...@.@@@32
33@.@.@.@@@......@@@@@@M.....@.@@@33
34@.@@@@@...@@@@@@@U.S@@...@@@.@@@34
35@..^...@@F@......@@@@..@.@...@@@35
36@@@@@@......@..@...B....@@@@@@@@36
37@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@37
  11111111122222222223333333333444
  12345678901234567890123456789012
```

## アイテム (Items)
* **T01** (L08, 35, 25) Vi Potion (2)
* **T02** (L08, 22, 28) Scroll “Lightning bolt Oh Kath Ra”
* **T03** (L08, 35, 28) Torch (Charges=15), Apple
* **T04** (L08, 31, 30) Magical Box (Blue)
* **T05** (L08, 30, 30) Pendant Feral
* **T06** (L08, 13, 16) Storm Ring (Charges=4), Torch (Charges=15), Drumstick
* **T07** (L08, 40, 05) Vi Potion, Chest [Green Gem, Scroll (“Put the gem back…”)]
* **T08** (L08, 28, 06) Rope
* **T09** (L08, 15, 06) Corbamite
* **T10** (L08, 15, 07) Torch (Charges=15)
* **T11** (L08, 13, 12) Dragon Steak, Corn, Apple, Cheese
* **T12** (L08, 30, 19) Empty flask, Scroll “The spell Oh Ew Ra bestows magic vision.”
* **T13** (L08, 23, 22) Ra Key

## 壁の文字（Inscriptions）
* **I01** (L08, 19, 34) “When is rock not rock”
* **I02** (L08, 28, 10) “What is under foot is soon overhead”
* **I03** (L08, 35, 20) “Lighter than a feather”

## 鍵穴（Locks）
* **L01** (L08, 35, 20) Corbamite
* **L02** (L08, 26, 30) Skeleton Key

## 特殊ギミック注記（Notes）
* **N01** “Put The Gem Back” puzzle: Use the lever twice to make the chest fall down the pit and close the pit again. Go downstairs from `(L08, 22, 10)` and grab the chest. Get back upstairs then again upstairs from `(L08, 23, 16)`. Drop the Green Gem at `(L07, 21, 12)`. This will open the door at `(L08, 21, 13)`. Get back downstairs. Another solution is to jump in the pit (or Climb Down with a rope) instead of dropping the Green Gem. Then use the green button to open the door.
* **N02** Place items on the pressure plates to trigger the fireballs, and quickly move out of their way. Once each pressure plate is triggered, you can walk across safely. If you play with only two champions, place them in front and turn sideways when the fireballs are shot so that they pass behind your champions.

## モンスター（Monsters）
* **M01** (L08, 21, 32) Pain Rat Generator (1)
* **M02** (L08, 27, 35) Ruster
* **M03** (L08, 35, 30) Vexirk [Cheese, Corn]
* **M04** (L08, 14, 30) Pain Rat
* **M05** (L08, 14, 19) Pain Rat
* **M06** (L08, 17, 12) Vexirk (2) [Screamer Slice, Bread, Apple, Corn, Cheese]
* **M07** (L08, 26, 14) Ruster
* **M08** (L08, 24, 07) Ruster
* **M09** (L08, 12, 06) Vexirk [Skeleton Key]
* **M10** (L08, 35, 15) Ruster
* **M11** (L08, 35, 05) Pain Rat Generator (1)
* **M12** (L08, 29, 22) Pain Rat
