# english-ver-level-00-to-japanese-ver-level-01.md


## English ver LEVEL 00 = Japanese ver Level 01 MAP

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
* I : 不可視/極小床スイッチ（Invisible / tiny plate ── 床を踏むことで作動する、見えないスイッチもしくは見えないほど小さなスイッチ）
* U : 上り階段（Stairs up - 一つ上の階へ移動できる）
* S : 下り階段（Stairs down - 一つ下の階へ移動できる）
* T : テレポーター（Teleporter - 違う場所へワープする）
* W : 点滅テレポーター（Blinking teleporter - 出現、消滅を交互に繰り返すテレポート）
* `>` : 右回転スピナー (Spinner - 進入した向きから90度時計回りに回転する)
* `<` : 左回転スピナー (Spinner - 進入した向きから90度反時計回りに回転する)
* `^` : 180度回転スピナー (Spinner - 進入した向きから180度反転する)

```
  0000000000111111111
  0123456789012345678
00@@@@@@@@@@@@@@@@@@@00
01@@@@@@.@@.@@@@@@@@@01
02@D@@...@@@@@@@@@@@@02
03@.@@.@...@@@@...@@@03
04@.@@.@.@........@@@04
05..@@.@@@@...@...@@@05
06@.@@.@@@@.@.@.....@06
07@....@@@@...@@@.@.@07
08@@@@@@@@@.@@@@@...@08
09@@@@.DX...........@09
10@@@@.@@.@@...@.@.@@10
11@..@..@.@@@@@@.@.@@11
12@..@.@....@@@..@.@@12
13@..@.@....@@...@.@@13
14@B@@.@.@@.@...@...@14
15@.@S.@.......@@.@.@15
16..@@.@....@@@@@.@.@16
17@....@@@@@@@@@@...@17
18@@@@@@@@@@@@@@@@@@@18
  0000000000111111111
  0123456789012345678
```

## Progression & Event Flags

* **G01 [Game Start]**
  * プレイヤーはグレイロードの弟子であり、現在は魂だけの存在となった**セロン（Theron）**として `(L00, 01, 03)` からスタート。
  * この時点ではセロン単体の幽体状態のため、まずは「Hall Of Champions」に並ぶ勇者たちの鏡へ向かう。
* **E01 [The Door of Champions]**
  * **発動条件:** 魂だけのセロン（体重ゼロ）では床スイッチを踏めないため、まずは勇者の館で勇者を1人以上「復活（Reincarnate）」または「転生（Resurrect）」させ、**肉体（体重）のあるパーティ**を結成する。
  * **ギミック:** その実体化したパーティの足で `(L00, 06, 09)` の床スイッチ（X）を踏むことで、その重みによって `(L00, 05, 09)` の通常ドア（D）が永久に開放される。
* **E02 [To the Next Level]**
  * `(L00, 04, 15)` にある下り階段（S）を前を向いて降りると、次の階層である `(L01, 03, 14)` の通路（上り階段の一歩手前のマス）へと移動する。このとき、階段を背にした状態になるため、向きは**「北（階段とは反対の方向）」**を向いた状態になる。

## Items

* **T01** (L00, 04, 09) Apple
* **T02** (L00, 05, 11) Bread
* **T03** (L00, 04, 14) Torch (Charges=15)
* **T04** (L00, 04, 15) Water (Charges=3), Scroll ("Invoke Ful for a magic torch")
* **T05** (L00, 04, 17) Scroll ("New lives for old bones")
* **T06** (L00, 00, 16) Corn
* **T07** (L00, 02, 13) Bread
* **T08** (L00, 02, 12) Cheese
* **T09** (L00, 02, 11) Apple

## 壁の文字（Inscriptions）

* **I01 (L00, X08, Y05, N) “Hall Of Champions”**
  * ※通路 `(L00, X08, Y04)` に立ち、南（S）の壁を向くと読める。
* **I02 (L00, X05, Y17, W) “Vi Altar Of Rebirth”**
  * ※通路 `(L00, X04, Y17)` に立ち、東（E）の壁を向くと読める。


## 特殊ギミック注記（Notes）

* **N01** (L00, 01, 04) You can use the spell “See Through Walls” in front of the door to see Lord Order. If you come back here with the Firestaff (not completed with the power gem), the door opens, then you are teleported in front of Lord Order where you can see an alternate game end.
* **N02** (L00, 09, 04) Choose four Dungeon Master Champions.


## ヴィーの祭壇 (Altar of VI)

* **A01** (L00, 04, 18, N) 


## 勇者 (Champions)

* **C01** (L00, 10, 03, S) Iaido Ruyito Chiburi
* **C02** (L00, 10, 06, N) Zed Duke Of Banville
* **C03** (L00, 14, 02, S) Chani Sayyadina Sihaya
* **C04** (L00, 16, 04, W) Hawk The Fearless
* **C05** (L00, 14, 07, N) Boris Wizard Of Baldor
* **C06** (L00, 16, 07, S) Alex Ander
* **C07** (L00, 17, 10, N) Nabi The Prophet
* **C08** (L00, 16, 15, N) Hissssa Lizar Of Makan
* **C09** (L00, 16, 16, S) Gothmog
* **C10** (L00, 15, 12, W) Sonja She Devil
* **C11** (L00, 13, 11, S) Leyla Shadowseek
* **C12** (L00, 14, 14, W) Mophus The Healer
* **C13** (L00, 11, 13, E) Wuuf The Bika
* **C14** (L00, 11, 16, N) Stamm Bladecaster
* **C15** (L00, 07, 17, N) Azizi Johari
* **C16** (L00, 08, 14, S) Leif The Valiant
* **C17** (L00, 10, 13, W) Tiggy Tamal
* **C18** (L00, 07, 14, N) Wu Tse Son Of Heaven
* **C19** (L00, 05, 13, E) Daroou
* **C20** (L00, 07, 08, S) Halk The Barbarian
* **C21** (L00, 09, 10, N) Syra Child Of Nature
* **C22** (L00, 11, 11, N) Gando Thurfoot
* **C23** (L00, 12, 08, S) Linflas
* **C24** (L00, 08, 07, E) Elija Lion Of Yaitopya
