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
  2333333333344444444445
  9012345678901234567890
33@@@@@@@@@@@@@@@@@@@@@@33
34@@@@@@@@@.........@@@@34
35@@@@@@@@@.@@@.@@@.@@@@35
36@@@@@@@@@.........@@.@36
37@@@@@@@@@@@@@@@@@ID..@37
38@@@@@@...@@@@@@@@@@..@38
39@@@@..............@@X@39
40@@@.X..............@D@40
41@UD.@..@.............@41
42@@@.X..............@@@42
43@@@@..............@@@@43
44@@@@@@...@@@@@@@@@@@@@44
45@@@@@@@@@@@@@@@@@@@@@@45
  2333333333344444444445
  9012345678901234567890
```

## アイテム (Items)
* **T01** (L13, 34, 42) Copper Coin
* **T02** (L13, 35, 39) Silver Coin
* **T03** (L13, 35, 43) Silver Coin
* **T04** (L13, 37, 38) Copper Coin
* **T05** (L13, 37, 42) Boulder
* **T06** (L13, 37, 44) Copper Coin
* **T07** (L13, 38, 41) Silver Coin, Boulder
* **T08** (L13, 39, 40) Ashes
* **T09** (L13, 40, 39) Boulder
* **T10** (L13, 40, 42) Copper Coin
* **T11** (L13, 41, 41) Ashes
* **T12** (L13, 42, 42) Ashes
* **T13** (L13, 43, 40) Square Key, Ashes
* **T14** (L13, 43, 43) Boulder
* **T15** (L13, 44, 39) Boulder
* **T16** (L13, 44, 42) Ashes
* **T17** (L13, 44, 43) Ashes
* **T18** (L13, 45, 40) Ashes
* **T19** (L13, 47, 40) Copper Coin (3), Gold Coin, Calista
* **T20** (L13, 47, 42) Blue Gem, Green Gem (2), Eye Of Time (Charges=5)
* **T21** (L13, 48, 38) Silver Coin
* **T22** (L13, 49, 36) Scroll “Only the touch of the proper spell will free the gem and only the Firestaff can possess it.”
* **T23** (L13, 48, 33) Copper Coin

## 鍵穴（Locks）
* **L01** (L13, 48, 41) Square Key
* **L02** (L13, 48, 38) Gold Coin (2), Silver Coin
* **L03** (L13, 28, 41) Winged Key

## 特殊ギミック注記（Notes）
* **N01** (L13, 49, 36) Cast the spell Zo Kath Ra. Use the spell to free the power gem, then use the Firestaff on it to combine them. Getting out of this room with the complete Firestaff will activate the pressure pad at `(L13, 49, 39)`, which toggles two walls on L12 preventing you from going to the upper levels. You can avoid that by throwing the complete Firestaff through the door to the south before stepping on the pressure plate.

## モンスター（Monsters）
* **M01** (L13, 49, 41) Red Dragon
