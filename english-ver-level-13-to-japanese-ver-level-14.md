# english-ver-level-13-to-japanese-ver-level-14.md

## English ver LEVEL 13 = Japanese ver Level 14 MAP

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
  333333333344444444445
  012345678901234567890
33@@@@@@@@@@@@@@@@@@@@@33
34@@@@@@@@.........@@@@34
35@@@@@@@@.@@@.@@@.@@@@35
36@@@@@@@@.........@@.@36
37@@@@@@@@@@@@@@@@ID..@37
38@@@@@...@@@@@@@@@@..@38
39@@@..............@@X@39
40@@.X..............@D@40
41UD.@..@.............@41
42@@.X..............@@@42
43@@@..............@@@@43
44@@@@@...@@@@@@@@@@@@@44
45@@@@@@@@@@@@@@@@@@@@@45
  333333333344444444445
  012345678901234567890
```

Items
01 (34,42) Copper Coin
02 (35,39) Silver Coin
03 (35,43) Silver Coin
04 (37,38) Copper Coin
05 (37,42) Boulder
06 (37,44) Copper Coin
07 (38,41) Silver Coin, Boulder
08 (39,40) Ashes
09 (40,39) Boulder
10 (40,42) Copper Coin
11 (41,41) Ashes
12 (42,42) Ashes
13 (43,40) Square Key, Ashes
14 (43,43) Boulder
15 (44,39) Boulder
16 (44,42) Ashes
17 (44,43) Ashes
18 (45,40) Ashes
19 (47,40) Copper Coin (3), Gold Coin, Calista
20 (47,42) Blue Gem, Green Gem (2), Eye Of Time (Charges=5)
21 (48,38) Silver Coin
22 (49,36) Scroll “Only the touch of the proper spell will free the gem and only the Firestaff can possess it.”
23 (48,33) Copper Coin

Locks
L01 (48,41) Square Key
L02 (48,38) Gold Coin (2), Silver Coin
L03 (28,41) Winged Key

Notes
A. (49,36) Cast the spell Zo Kath Ra. Use the spell to free the power gem, then use the Firestaff on it to combine them.
Getting out of this room with the complete Firestaff will activate the pressure pad at (49,39), which toggles two walls on level 12 preventing you from going to the upper levels. You can avoid that by throwing the complete Firestaff through the door to the south before stepping on the pressure plate.

Creatures
01 (49,41) Red Dragon
