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

## アイテム (Items)
* **T01** (L05, 22, 05) Drumstick
* **T02** (L05, 16, 06) Cheese, Bro Potion
* **T03** (L05, 12, 07) Ven Potion
* **T04** (L05, 14, 07) Torch (Charges=13)
* **T05** (L05, 17, 24) Iron Key
* **T06** (L05, 18, 34) Iron Key
* **T07** (L05, 26, 26) Iron Key, Mail Aketon
* **T08** (L05, 26, 21) Iron Key
* **T09** (L05, 15, 21) Large Shield
* **T10** (L05, 27, 28) Ros Potion, Vi Potion, Drumstick, Torch (Charges=15)
* **T11** (L05, 34, 33) Magical Box (Blue)
* **T12** (L05, 34, 19) Iron Key, Torso Plate
* **T13** (L05, 28, 15) Magical Box (Green)
* **T14** (L05, 29, 11) Drumstick (2)
* **T15** (L05, 28, 10) Yew Staff (Charges=10)
* **T16** (L05, 32, 09) Casque’n Coif
* **T17** (L05, 29, 05) Vorpal Blade (Charges=14)
* **T18** (L05, 25, 08) Solid Key
* **T19** (L05, 22, 11) Corn, Throwing Star (2)
* **T20** (L05, 18, 17) Drumstick
* **T21** (L05, 18, 18) Mithral Aketon, Slayer (2)
* **T22** (L05, 11, 15) Magical Box (Green) (2)
* **T23** (L05, 09, 17) Torch (Charges=15)
* **T24** (L05, 06, 11) Magical Box (Blue)
* **T25** (L05, 12, 21) Vorpal Blade (Charges=0)
* **T26** (L05, 16, 30) Crossbow
* **T27** (L05, 14, 33) Chest [Slayer, Water Flask, Drumstick]
* **T28** (L05, 24, 32) Mithral Mail

## 壁の文字（Inscriptions）
* **I01** (L05, 12, 25) “The riddle room”
* **I02** (L05, 13, 23) “I am all I am none”
* **I03** (L05, 16, 23) “A golden head and tail but no body”
* **I04** (L05, 13, 27) “Hard as rocks blue as sky twinkle in womans eye”
* **I05** (L05, 16, 27) “I arch yet have no back”
* **I06** (L05, 22, 26) “The grave of king Filius explorer of combinations”
* **I07** (L05, 24, 22) “The grave of king Milias the golden who even”
* **I08** (L05, 24, 23) “In death thirsts for bullion.”
* **I09** (L05, 25, 18) “If you want to stay alive you better turn and run”
* **I10** (L05, 25, 17) “I hate cowards”
* **I11** (L05, 25, 19) “I don’t like to be ignored”
* **I12** (L05, 23, 14) “Test your strength”
* **I13** (L05, 19, 09) “Ha ha ha”
* **I14** (L05, 30, 33) “Altar of Vi”

## 鍵穴（Locks）
* **L01** (L05, 22, 23) Gold Coin
* **L02** (L05, 21, 18) Iron Key
* **L03** (L05, 23, 18) Iron Key
* **L04** (L05, 27, 17) Iron Key
* **L05** (L05, 30, 16) Iron Key
* **L06** (L05, 25, 13) Stone Key
* **L07** (L05, 13, 16) Iron Key

## 特殊ギミック注記（Notes）
* **N01** (L05, 15, 17) Each of the four alcoves requires one of these four items: a Mirror Of Dawn, a Gold Coin, a Blue Gem and a Bow. Once three items are in place, the door will open. The fourth item will reveal the hidden alcove.
* **N02** (L05, 18, 31) Pull the lever, then put any item on ground in the teleporter (do not throw it) so that it gets at `(L05, 20, 33)`. The door will then open.
* **N03** You need to press the two buttons at `(L05, 24, 25)` and `(L05, 25, 28)` to open the wall. The two other buttons are already in the correct state.
* **N04** A skeleton must walk on the pressure pad to open the wall. Leaving an item on floor will not work.

## モンスター（Monsters）
* **M01** (L05, 13, 07) Skeleton
* **M02** (L05, 18, 34) Wizard Eye
* **M03** (L05, 23, 27) Wizard Eye
* **M04** (L05, 23, 22) Skeleton (2)
* **M05** (L05, 30, 23) Skeleton Generator (4)
* **M06** (L05, 34, 22) Wizard Eye Generator (2)
* **M07** (L05, 34, 20) Skeleton (2)
* **M08** (L05, 29, 07) Skeleton (4)
* **M09** (L05, 11, 15) Giant Wasp (3)
* **M10** (L05, 11, 10) Skeleton (2)
* **M11** (L05, 05, 11) to `(L05, 06, 12)` Wizard Eye (4)
* **M12** (L05, 05, 24) Wizard Eye Generator (1-4)
* **M13** (L05, 09, 25) Skeleton (2)
* **M14** (L05, 11, 21) Skeleton (4)
* **M15** (L05, 12, 19) Skeleton (1)
* **M16** (L05, 11, 27) Skeleton (4)
* **M17** (L05, 11, 23) Skeleton (2)
* **M18** (L05, 12, 33) Skeleton Generator (1-4)
* **M19** (L05, 15, 33) Giant Wasp Generator (1)
* **M20** (L05, 16, 32) Skeleton Generator (1)
* **M21** (L05, 23, 33) Wizard Eye
