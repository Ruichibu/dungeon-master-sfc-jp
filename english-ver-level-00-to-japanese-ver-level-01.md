# english-ver-level-00-to-japanese-ver-level-01.md


## English ver LEVEL 00 = Japanese ver Level 01 MAP

## 【階層表記（Level）に関する絶対ルール】
* 本ドキュメント内での座標表記は、すべて `(X座標, Y座標, L階層)` で統一する。
* **「Lxx」の数値は、すべて海外PC版（Dungeon Master Editor基準）の表記で統一する。**
  * **L00** = 海外版 LEVEL 00（日本SFC版の「1階：勇者の館」）
  * **L01** = 海外版 LEVEL 01（日本SFC版の「地下1階」）
  * **L02** = 海外版 LEVEL 02（日本SFC版の「地下2階」）
  ※AIは日本版の「1階」をL01と誤認してはならない。すべての計算はL00をスタート地点として処理すること。

## 【確定したマッピング言語】
. : 通路（Passage - 通れる）
@ : 通常の壁（Wall - 通れない）
F : 偽物の壁（Fake wall - 壁に見えるが、実は通れる通路）
M : 動く壁（Movable wall - スイッチを押すことで通路になる壁）
P : 落とし穴（Pit - 同じ座標の一つ下の階に落とされる。ダメージを受ける）
H : 床に見える落とし穴（Hidden pit - 見えない落とし穴）
D : 通常の扉（Door - 遠くのスイッチを押したり、レバーを下すことで開閉するドア）
L : 鍵で開くドア（Locked door - 遠くの鍵穴に鍵を挿しこむことで開くドア）
B : ボタンが付いてるドア（Door button - ドアに併設されているボタンで開閉できるドア）
K : 破壊可能なドア（Breakable door - 強力な攻撃で破壊できるドア）
X : 床スイッチ（Pressure plate - 床を踏むことで動作するスイッチ）
I : 不可視スイッチ（Invisible plate - 床を踏むことで動作する見えないほど小さなスイッチ）
U : 上り階段（Stairs up - 一つ上の階へ移動できる）
S : 下り階段（Stairs down - 一つ下の階へ移動できる）
T : テレポーター（Teleporter - 違う場所へワープする）
W : 点滅テレポーター（Blinking teleporter - 出現、消滅を交互に繰り返すテレポート）
> : 方向転換（Spinner - その場に立つと、方向転換する）

```
  0000000000111111111
  0123456789012345678
00@@@@@@@@@@@@@@@@@@@
01@@@@@@.@@@@@@@@@@@@
02@@@@...@@@@@@@@@@@@
03@.@@.@...@@@@...@@@
04@.@@.@.@........@@@
05..@@.@@@@...@...@@@
06@.@@.@@@@.@.@.....@
07@....@@@@...@@@.@.@
08@@@@@@@@@.@@@@@...@
09@@@@.DX...........@
10@@@@.@@.@@...@.@.@@
11@..@..@.@@@@@@.@.@@
12@..@.@....@@@..@.@@
13@..@.@....@@...@.@@
14@B@@.@.@@.@...@...@
15@.@S.@.......@@.@.@
16..@@.@....@@@@@.@.@
17@....@@@@@@@@@@.@.@
18@@@@@@@@@@@@@@@@@@@
```

## Items

01 (04,09) Apple
02 (05,11) Bread
03 (04,14) Torch (Charges=15)
04 (04,15) Water (Charges=3), Scroll (“Invoke Ful for a magic torch”)
05 (04,17) Scroll (“New lives for old bones”)
06 (00,16) Corn
07 (02,13) Bread
08 (02,12) Cheese
09 (02,11) Apple

## Inscriptions

I01 (08,04) “Hall Of Champions”
I02 (04,17) “Vi Altar Of Rebirth”

##Champions

C01 (10,04) Iaido Ruyito Chiburi
C02 (10,05) Zed Duke Of Banville
C03 (14,03) Chani Sayyadina Sihaya
C04 (15,04) Hawk The Fearless
C05 (14,06) Boris Wizard Of Baldor
C06 (16,08) Alex Ander
C07 (17,09) Nabi The Prophet
C08 (16,14) Hissssa Lizar Of Makan
C09 (16,17) Gothmog
C10 (14,12) Sonja She Devil
C11 (13,12) Leyla Shadowseek
C12 (13,14) Mophus The Healer
C13 (12,13) Wuuf The Bika
C14 (11,15) Stamm Bladecaster
C15 (07,16) Azizi Johari
C16 (08,15) Leif The Valiant
C17 (09,13) Tiggy Tamal
C18 (07,13) Wu Tse Son Of Heaven
C19 (06,13) Daroou
C20 (07,09) Halk The Barbarian
C21 (09,09) Syra Child Of Nature
C22 (11,10) Gando Thurfoot
C23 (12,09) Linflas
C24 (09,07) Elija Lion Of Yaitopya
