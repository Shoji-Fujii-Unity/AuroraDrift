# AURORA DRIFT — 極彩の回廊

Three.js 製シングルファイル 3D アクション。アセットファイル・ビルド工程なし。
A single-file Three.js arcade. No assets, no build step.

| 対応項目 | 内容 |
|---|---|
| 動作 | PC（デスクトップ）/ スマホ / タブレット。WebGL 対応ブラウザ |
| 画面 | 横長（landscape）前提。縦持ち時は回転オーバーレイ表示 |
| 入力 | タッチ（仮想スティック）/ キーボード / ゲームパッド |
| サウンド | 合成音（WebAudio）。SFX と MUSIC を個別に On/Off |
| 言語 | 日本語 / English / Español / Français / 中文 / العربية (RTL) |
| データ | localStorage。端末内にのみ保存。サーバー送信なし |

- [日本語](#日本語) · [English](#english) · [Español](#español) · [Français](#français) · [中文](#中文) · [العربية](#العربية)

---

## 日本語

自動飛行するネオン回廊を、**避けて・撃って・抜ける** 一人用アクション。
リングを連続通過して SYNC（コンボ）×8 を作り、ION を加速・射撃・パルスに割り振りながら、距離と得点を伸ばします。

### 操作

| 手段 | 移動 | 射撃 | 加速 | パルス | 一時停止 |
|---|---|---|---|---|---|
| タッチ | 画面左半分をドラッグ | FIRE 長押し | BOOST 長押し | PULSE タップ | 右上 ||
| キーボード | WASD / 矢印 | Space / K | Shift | L / J / X | Esc |
| ゲームパッド | 左スティック | X / B | RT | A | Start |

Enter でタイトル画面から即スタート。ゲームパッドは接続時に自動認識します。

### モード

| モード | 時間 | 被弾 | ION | 特徴 |
|---|---|---|---|---|
| アーケード | 無限距離 | シールド消費 | 標準 | 壁・敵の全種類が出現。距離と得点を競う |
| ラッシュ | 90 秒 | −5 秒 | やや多め | リング通過で +1.4 秒。時間をやりくりする短時間勝負 |
| 禅（ZEN） | 無限距離 | 被弾なし | 無限 | 射撃と回避だけの快晴。練習・撮影向け |

### 敵と障害

すべて「予兆 → 挙動」の順に読めます。射撃で破壊できる敵はスコアとコンボに直結します。

| 名称 | 挙動 | 射撃 |
|---|---|---|
| 回廊壁 | 発光レールが当たり判定そのもの。接触でシールド 1 枚＋減速 | 不可 |
| 絞り区間 | 距離に応じて回廊が物理的に狭くなる。手前の絞り込みで視認可 | — |
| 磁柵暴風 | 横方向へ継続的に押し付け、狭い箇所では壁へ吸い寄せる | — |
| 機雷 | 静止。触れた瞬間に被弾 | 可 |
| 感応機雷 | 赤い警戒輪が脈動。接近すると広域で爆発 | 可 |
| 上下スライド壁 | 上下からすれ違い様に迫る。隙間を通す | 不可 |
| 侵入パイロン | 上下端から突き出す柱。左右へ動く | 可 |
| 閉鎖壁 | 近づくと中央の隙間が閉じる。早めに通る | 不可 |
| 旋回鋸 | Y 軸サインカーブで横断する回転刃 | 可 |
| 追跡ドローン | プレイヤーを追って直進してくる | 可 |
| 横断スティンガー | 警戒線を示した後、横向きに突撃 | 可 |
| 砲塔 | 白色でチャージ → 照準 3 連射 | 可（HP 高） |
| WARDEN（ボス） | 約 1400 m ごとに出現。リング弾幕／照準 3 連射／ドローン展開を循環 | 撃破必須 |

### システム

- **SYNC（コンボ）**：リング通過で上昇、最大 ×8。被弾とリング縁接触で 1 に戻る。高 SYNC は得点倍率と速度を押し上げる
- **ION**：加速・射撃・パルスで共有する資源。回収で回復
- **パルス**：周囲の敵を消滅させて得点化（ION を大きく消費）。緊急回避にも使える無敵時間あり
- **拾得物**：ION（緑）／シールド（黄）／TIME +5 秒（青・ラッシュのみ）／STAR 2 倍（紫・6 秒）

### セーブデータ

ブラウザの localStorage にのみ保存されます（同期・送信なし）。
自動保存され、タイトル画面の設定から**2 度押しで全消去**できます。

| 項目 | 内容 |
|---|---|
| モード別ベスト | アーケード / ラッシュ / 禅 の最高得点 |
| 通算 | 累計得点、撃破数、RUN 数 |
| 機体 | 累計得点で自動アンロック、装備機体を記憶 |
| 設定 | SFX / MUSIC / 画面シェイク / 描画品質 / 言語 |

### 技術

- Three.js（CDN 読み込み。unpkg → cdnjs にフォールバック）
- 画像・音声ファイルは使用せず、メッシュも音もすべて手続き生成
- 敵の弾と粒子はプール管理、描画は加算合成のみで負荷を抑える設計
- フレームレートを実測して自動で描画解像度を調整（設定で固定も可）
- 音声は初回タップ後に再生を開始します（ブラウザの自動再生ポリシー対策）
- フルスクリーンボタンで横画面ロックを試みます（端末依存）

### 起動方法

1. この HTML を `index.html` として保存します
2. 保存したファイルをブラウザで開きます（ダブルクリックで可）
3. 初回読み込みは Three.js を CDN から取得するため、ネットワーク接続が必要です

### 調整

| 場所 | 変更できること |
|---|---|
| 敵の設定（CFG） | 各敵の HP・当たり半径・得点・色 |
| パターン表（PAT） | 出現パターンの重みと長さ（難易度・密度） |
| 回廊幅（bx / by） | 絞り区間の厳しさ。壁への押し付け量 |

### つまずいたとき

- 画面が黒い → CDN に到達できていない可能性があります。接続を確認してください
- 音が鳴らない → 初回タップ後に鳴動します。SFX / MUSIC の状態も確認してください
- 操作できない → ポートレート表示中は回転オーバーレイの下です。横にしてください

---

## English

A solo arcade run through a neon corridor: **dodge, shoot, slip through**.
Build SYNC (combo) up to ×8 while splitting ION between boosting, firing and pulsing.

### Controls

| Input | Move | Fire | Boost | Pulse | Pause |
|---|---|---|---|---|---|
| Touch | Drag the left half | Hold FIRE | Hold BOOST | Tap PULSE | Top right ||
| Keyboard | WASD / arrows | Space / K | Shift | L / J / X | Esc |
| Gamepad | Left stick | X / B | RT | A | Start |

Enter starts immediately from the title screen. Gamepads are detected automatically.

### Modes

| Mode | Time | Damage | ION | Notes |
|---|---|---|---|---|
| Arcade | Endless distance | Costs shields | Normal | Every hazard appears. Chase distance and score |
| Rush | 90 seconds | −5 seconds | Slightly more | Rings grant +1.4 s. Budget your clock |
| Zen | Endless distance | None | Infinite | Firing and dodging only. Good for practice |

### Enemies and hazards

Everything telegraphs before it attacks. Shooting enemies feeds score and combo.

| Name | Behaviour | Shootable |
|---|---|---|
| Corridor wall | The glowing rails are the hitbox. Touch costs one shield and speed | No |
| Pinch section | The corridor physically narrows based on distance | — |
| Magnet storm | Continuous sideways push that throws you into walls | — |
| Mine | Static. Instant damage on contact | Yes |
| Proximity mine | Pulsing warning ring, detonates on approach | Yes |
| Sliding bar | Paired bars sweeping up and down. Thread the gap | No |
| Intruder pylon | Pillars jutting from top or bottom, drifting sideways | Yes |
| Crusher | The gap slams shut as you approach | No |
| Sweeping saw | Spinning blade riding a sine path across the lane | Yes |
| Hunter drone | Steers toward the player | Yes |
| Stinger | Shows a warning line, then crosses at speed | Yes |
| Turret | Charges white, then fires a 3 shot aimed burst | Yes (tanky) |
| WARDEN (boss) | Roughly every 1400 m. Ring barrage / aimed burst / drone spawn loop | Must destroy |

### Systems

- **SYNC**: rises through rings, caps at ×8. Drops to 1 on damage or rim contact. Raises multiplier and speed
- **ION**: shared resource for boost, fire and pulse. Refilled by pickups
- **Pulse**: erases nearby enemies into score for heavy ION cost, plus a brief invulnerability window
- **Pickups**: ION (green), shield (amber), +5 s chrono (blue, Rush only), ×2 star (violet, 6 s)

### Save data

Stored only in browser localStorage — nothing is sent anywhere. Auto-saved; the settings panel clears it with a confirm press.

| Field | Contents |
|---|---|
| Per-mode best | Highest score for Arcade, Rush and Zen |
| Career | Total score, kills, run count |
| Ships | Unlocked by career score, remembers the equipped hull |
| Settings | SFX, music, screen shake, render quality, language |

### Tech

- Three.js loaded from a CDN (unpkg, with a cdnjs fallback)
- Zero asset files — all meshes and audio are generated procedurally
- Pooled enemies, bullets and particles; additive blending only, no lighting pass
- Frame time is measured so render resolution can scale down automatically
- Audio starts on the first tap, following browser autoplay rules
- A fullscreen button attempts a landscape lock (device dependent)

### Running it

1. Save this HTML file as `index.html`
2. Open it in a browser (double click works)
3. The first load needs network access to fetch Three.js from the CDN

### Tuning

| Area | What you can change |
|---|---|
| Enemy config (CFG) | HP, hit radius, score value, colour per enemy |
| Pattern table (PAT) | Spawn weights and pattern length: density and difficulty |
| Corridor width (bx / by) | How hard pinches close in and how strongly storms shove |

### Troubleshooting

- Black screen: the CDN may be unreachable. Check your connection
- No audio: sound unlocks on first interaction. Verify SFX and MUSIC toggles
- Unresponsive controls: the rotate overlay is active in portrait. Turn the device sideways

---

## Español

Corredor de neón en vuelo automático: **esquiva, dispara, atraviesa**.
Encadena SYNC (combo) hasta ×8 mientras repartes el ion entre acelerar, disparar y pulsar.

### Controles

| Entrada | Mover | Disparar | Acelerar | Pulso | Pausa |
|---|---|---|---|---|---|
| Táctil | Arrastra la mitad izquierda | Mantén FIRE | Mantén BOOST | Toca PULSE | Arriba a la derecha ||
| Teclado | WASD / flechas | Space / K | Shift | L / J / X | Esc |
| Mando | Stick izquierdo | X / B | RT | A | Start |

Enter inicia desde el menú. Los mandos se detectan solos.

### Modos

| Modo | Tiempo | Daño | Ion | Notas |
|---|---|---|---|---|
| Arcade | Distancia infinita | Gasta escudos | Normal | Aparecen todos los peligros |
| Rush | 90 segundos | −5 segundos | Un poco más | Los anillos dan +1,4 s |
| Zen | Distancia infinita | Sin daño | Infinito | Solo disparar y esquivar |

### Enemigos y peligros

Todo avisa antes de atacar. Derribar enemigos sube puntos y combo.

| Nombre | Comportamiento | Se puede disparar |
|---|---|---|
| Muro del corredor | Los rieles luminosos son la caja de golpe. Un roce cuesta escudo y velocidad | No |
| Estrechamiento | El corredor se cierra según la distancia | — |
| Tormenta magnética | Empuje lateral constante hacia las paredes | — |
| Mina | Estática. Contacto inmediato | Sí |
| Mina de proximidad | Anillo de aviso pulsante, explota al acercarse | Sí |
| Barras deslizantes | Parejas que barren arriba y abajo | No |
| Pilonos | Pilares desde el borde superior o inferior, se mueven | Sí |
| Triturador | El hueco se cierra al acercarte | No |
| Sierra giratoria | Hoja que cruza en curva | Sí |
| Dron cazador | Persigue al jugador | Sí |
| Aguijón | Muestra una línea y luego cruza rápido | Sí |
| Torreta | Carga en blanco y dispara tres apuntadas | Sí (resistente) |
| WARDEN (jefe) | Cada ~1400 m. Ráfaga en anillo, apuntado y dron | Hay que destruirlo |

### Sistemas

- **SYNC**: sube con los anillos hasta ×8, vuelve a 1 al recibir daño
- **ION**: recurso compartido para acelerar, disparar y pulsar
- **Pulso**: borra enemigos cercanos a cambio de mucho ion y da invulnerabilidad breve
- **Recogibles**: ion (verde), escudo (ámbar), +5 s (azul, solo Rush), ×2 (violeta, 6 s)

### Datos guardados

Solo en localStorage del navegador; no se envía nada. Se guarda automáticamente y se borra desde Ajustes con doble confirmación.

| Campo | Contenido |
|---|---|
| Mejor por modo | Puntuación más alta en Arcade, Rush y Zen |
| Carrera | Puntos totales, bajas, partidas |
| Naves | Desbloqueo por total, recuerda la nave equipada |
| Ajustes | SFX, música, vibración, gráficos, idioma |

### Tecnología

- Three.js desde CDN (unpkg con respaldo en cdnjs)
- Sin archivos de recursos: mallas y sonido generados por código
- Enemigos, balas y partículas en pool; solo mezcla aditiva
- Mide los fotogramas y baja la resolución automáticamente si hace falta
- El audio arranca tras el primer toque, según las reglas del navegador

### Cómo abrirlo

1. Guarda este HTML como `index.html`
2. Ábrelo en el navegador
3. La primera carga necesita internet para descargar Three.js

### Ajustes

| Zona | Qué cambia |
|---|---|
| Config de enemigos (CFG) | Vida, radio, puntos y color |
| Tabla de patrones (PAT) | Peso y longitud de cada patrón |
| Ancho del corredor (bx / by) | Cierre de los estrechamientos y fuerza de las tormentas |

### Problemas frecuentes

- Pantalla negra: quizá no llega al CDN. Revisa la conexión
- Sin sonido: se activa con el primer toque. Revisa los interruptores de SFX y música
- No responde: estás en vertical; gira el dispositivo

---

## Français

Couloir de néon en vol automatique : **esquivez, tirez, passez**.
Faites monter la SYNC (combo) jusqu'à ×8 tout en partageant l'ion entre boost, tir et onde.

### Commandes

| Entrée | Diriger | Tirer | Accélérer | Onde | Pause |
|---|---|---|---|---|---|
| Tactile | Glissez sur la moitié gauche | Maintenez FIRE | Maintenez BOOST | Touchez PULSE | En haut à droite ||
| Clavier | WASD / flèches | Space / K | Shift | L / J / X | Échap |
| Manette | Stick gauche | X / B | RT | A | Start |

Entrée lance la partie depuis le menu. Les manettes sont détectées automatiquement.

### Modes

| Mode | Temps | Dégâts | Ion | Détails |
|---|---|---|---|---|
| Arcade | Distance infinie | Coûte un bouclier | Normal | Tous les pièges sont présents |
| Rush | 90 secondes | −5 secondes | Un peu plus | Les anneaux donnent +1,4 s |
| Zen | Distance infinie | Aucun | Infini | Combat pur, pour s'entraîner |

### Ennemis et dangers

Chaque attaque est annoncée. Détruire rapporte points et combo.

| Nom | Comportement | Destructible |
|---|---|---|
| Mur du couloir | Les rails lumineux sont la zone de collision | Non |
| Rétrécissement | Le couloir se resserre avec la distance | — |
| Tempête magnétique | Poussée latérale continue vers les murs | — |
| Mine | Statique, dégâts immédiats | Oui |
| Mine à proximité | Anneau d'alerte pulsant, explose à l'approche | Oui |
| Barres coulissantes | Deux barres qui balaient le haut et le bas | Non |
| Pylône | Piliers depuis un bord, dérive latérale | Oui |
| Presse | Le passage se ferme à l'approche | Non |
| Scie | Lame tournante sur trajectoire courbe | Oui |
| Drone chasseur | Se dirige vers le joueur | Oui |
| Dard | Affiche une ligne, puis traverse vite | Oui |
| Tourelle | Charge en blanc puis tire trois tirs guidés | Oui (résistante) |
| WARDEN (boss) | Environ tous les 1400 m. Barrage en anneau, tir guidé, drones | À détruire |

### Systèmes

- **SYNC** : monte à travers les anneaux jusqu'à ×8, retombe à 1 si vous êtes touché
- **Ion** : ressource commune au boost, au tir et à l'onde
- **Onde** : efface les ennemis proches contre beaucoup d'ion et donne une brève invulnérabilité
- **Bonus** : ion (vert), bouclier (ambre), +5 s (bleu, Rush), ×2 (violet, 6 s)

### Sauvegarde

Uniquement dans le localStorage du navigateur, aucun envoi. Sauvegarde automatique ; effacement depuis les réglages après confirmation.

| Champ | Contenu |
|---|---|
| Record par mode | Meilleur score en Arcade, Rush et Zen |
| Carrière | Score total, ennemis détruits, vols |
| Vaisseaux | Débloqués par le total, mémorise le vaisseau équipé |
| Réglages | SFX, musique, tremblement, rendu, langue |

### Technique

- Three.js chargé depuis un CDN (unpkg avec repli cdnjs)
- Aucun fichier de ressource : maillages et sons générés à la volée
- Ennemis, tirs et particules en pool ; blending additif uniquement
- Mesure du temps de rendu pour réduire la résolution si besoin
- L'audio démarre au premier contact, conformément aux règles du navigateur

### Lancement

1. Enregistrez ce fichier HTML sous `index.html`
2. Ouvrez-le dans le navigateur
3. Le premier chargement nécessite une connexion pour récupérer Three.js

### Réglages

| Zone | Paramètres concernés |
|---|---|
| Ennemis (CFG) | Vie, rayon, points, couleur |
| Motifs (PAT) | Poids et longueur de chaque motif |
| Largeur du couloir (bx / by) | Fermeture des passages et force des tempêtes |

### Dépannage

- Écran noir : CDN peut-être injoignable, vérifiez le réseau
- Pas de son : il s'active au premier contact ; vérifiez SFX et musique
- Contrôles muets : l'écran de rotation est actif en portrait, pivotez l'appareil

---

## 中文

自动飞行的霓虹回廊：**闪避、射击、穿越**。
连续穿环把 SYNC（连段）堆到 ×8，把 ION 分配给加速、射击与脉冲。

### 操作

| 输入 | 移动 | 射击 | 加速 | 脉冲 | 暂停 |
|---|---|---|---|---|---|
| 触屏 | 拖动屏幕左半侧 | 长按 FIRE | 长按 BOOST | 点按 PULSE | 右上角 ||
| 键盘 | WASD / 方向键 | Space / K | Shift | L / J / X | Esc |
| 手柄 | 左摇杆 | X / B | RT | A | Start |

标题界面按 Enter 立即开始。手柄插入后自动识别。

### 模式

| 模式 | 时间 | 受击 | ION | 说明 |
|---|---|---|---|---|
| 无限（Arcade） | 距离无尽 | 消耗护盾 | 标准 | 全部障碍与敌人，比拼距离与分数 |
| 限时（Rush） | 90 秒 | 扣 5 秒 | 略多 | 穿环 +1.4 秒，考验时间管理 |
| 禅（Zen） | 距离无尽 | 不会受伤 | 无限 | 纯射击与走位，适合练习 |

### 敌人与障碍

所有敌人都遵循“先预警、后行动”的规则；击破直接换算分数与连段。

| 名称 | 行为 | 可否射击 |
|---|---|---|
| 回廊壁 | 发光墙线就是判定本体，碰到掉盾并减速 | 否 |
| 收窄区 | 回廊随距离物理变窄，可从前方趋势预判 | — |
| 磁柵暴風 | 持续横向推力，在窄道里会把玩家拍向墙面 | — |
| 水雷 | 静止，接触即受伤 | 可 |
| 感应水雷 | 红色警戒环脉动，接近后大范围爆炸 | 可 |
| 滑动墙 | 上下成对逼近，需从缝隙穿过 | 否 |
| 侵入桩 | 从上下端伸出的立柱，会横向移动 | 可 |
| 闭锁壁 | 靠近时中央缺口关闭，要提前通过 | 否 |
| 旋转锯 | 沿正弦轨迹横穿的旋转刀刃 | 可 |
| 追踪无人机 | 朝玩家方向追击 | 可 |
| 横向刺客 | 先显示预警线，再横向突进 | 可 |
| 炮塔 | 白色蓄力后三连瞄准射击 | 可（较耐打） |
| WARDEN（Boss） | 约每 1400 m 出现，环形弹幕／三连射击／放无人机循环 | 必须击破 |

### 系统

- **SYNC**：穿环上涨，上限 ×8；受伤或擦到环边即回到 ×1，影响得分倍率与速度
- **ION**：加速、射击、脉冲共用资源，靠拾取回复
- **脉冲**：清除周围敌人并换算得分，消耗大量 ION，附带短暂无敌
- **拾取物**：ION（绿）、护盾（黄）、+5 秒（蓝，仅限时）、×2（紫，6 秒）

### 存档

仅保存在浏览器 localStorage，不上传任何数据。自动保存；在设置里二次确认即可清空。

| 项目 | 内容 |
|---|---|
| 模式最佳 | 三种模式各自的最高分 |
| 生涯 | 累计得分、击破数、局数 |
| 机体 | 按累计得分解锁，记住当前使用机体 |
| 设置 | 音效、音乐、画面震动、画质、语言 |

### 技术

- Three.js 通过 CDN 加载（unpkg，失败则切换 cdnjs）
- 不依赖任何素材文件，模型与声音全部程序生成
- 敌人、子弹、粒子均使用对象池；仅用叠加混合，无光照通道
- 实时监测帧率，可自动下调渲染分辨率
- 首次触摸后才启动音频（遵循浏览器自动播放策略）
- 全屏按钮会尝试锁定横屏（依设备而定）

### 运行

1. 把该 HTML 另存为 `index.html`
2. 用浏览器打开（双击即可）
3. 首次加载需要联网获取 Three.js

### 调参

| 位置 | 可改内容 |
|---|---|
| 敌人数值（CFG） | 每种敌人的 HP、判定半径、得分、颜色 |
| 关卡模式表（PAT） | 各模式的权重与长度，即密度与难度 |
| 回廊宽度（bx / by） | 收窄区强度与风暴推力 |

### 常见问题

- 黑屏：多半取不到 CDN，请检查网络
- 没有声音：首次交互后才出声，并检查音效与音乐开关
- 无法操作：竖屏时显示旋转提示，请横置设备

---

## العربية

ممر نيوني يطير تلقائيًا: **تفادَ وأطلق النار واخترق**.
ارفع التزامن (كومبو) حتى ×8 مع تقسيم المؤيّن بين التسارع وإطلاق النار والنبضة.

ملاحظة: هذه الواجهة تعمل من اليمين إلى اليسار، بينما تبقى اللعبة أفقية التوجيه.

### التحكّم

| الوسيلة | التوجيه | إطلاق | تسارع | نبضة | إيقاف |
|---|---|---|---|---|---|
| اللمس | اسحب النصف الأيسر | استمر على FIRE | استمر على BOOST | اضغط PULSE | أعلى اليمين ||
| لوحة المفاتيح | WASD أو الأسهم | Space أو K | Shift | L أو J أو X | Esc |
| يد التحكم | العصا اليسرى | X أو B | RT | A | Start |

مفتاح Enter يبدأ اللعب فورًا، ويد التحكم تُكتشف تلقائيًا.

### الأوضاع

| الوضع | الوقت | الضرر | المؤيّن | ملاحظات |
|---|---|---|---|---|
| أركيد | مسافة لا محدودة | ينقص درعًا | عادي | تظهر كل العوائق |
| اندفاع | ٩٠ ثانية | −٥ ثوانٍ | أكثر قليلًا | الحلقات تمنح ١٫٤ ثانية |
| زِن | مسافة لا محدودة | بلا أضرار | لا نهائي | طيران ورمي فقط |

### الأعداء والعوائق

كل شيء يعلن عن نفسه قبل الهجوم، وإسقاط الأعداء يزيد النقاط والكومبو.

| الاسم | السلوك | قابل للإسقاط |
|---|---|---|
| جدار الممر | القضبان المتوهجة هي منطقة الارتطام | لا |
| الاختناق | الممر يضيق فعليًا مع المسافة | — |
| عاصفة مغناطيسية | دفع جانبي مستمر يدفعك نحو الجدران | — |
| لغم | ثابت، ألم فوري عند الملامسة | نعم |
| لغم proximity | حلقة تحذير نابضة تنفجر عند الاقتراب | نعم |
| قضبان منزلقة | زوج يتحرك للأعلى والأسفل | لا |
| عمود غازي | أعمدة من الأعلى أو الأسفل تنزلق | نعم |
| الكابوس | الفجوة تُغلق عند الاقتراب | لا |
| منشار دوّار | شفرة تدور وتقطع الممر | نعم |
| مسيّرة مطاردة | تتجه نحو اللاعب | نعم |
| لسعة | تعرض خط تحذير ثم تعبر بسرعة | نعم |
| برج | يشحن باللون الأبيض ثم يطلق ثلاث رصاصات موجهة | نعم (قوي) |
| الحارس WARDEN | كل ~١٤٠٠ م. وابل حلقي وطلقات موجهة ومسيّرات | يجب تدميره |

### الأنظمة

- **التزامن**: يرتفع مع الحلقات حتى ×8 ويعود إلى ١ عند الإصابة
- **المؤيّن**: مورد مشترك للتسارع والإطلاق والنبضة
- **النبضة**: تمسح الأعداء القريبين مقابل مؤيّن كبير وتعطي مناعة قصيرة
- **المقتنيات**: مؤيّن (أخضر)، درع (كهرماني)، +٥ ثوانٍ (أزرق في الاندفاع)، ×٢ (بنفسجي، ٦ ثوانٍ)

### البيانات المحفوظة

تُحفظ فقط داخل localStorage في المتصفح دون أي إرسال، وتُمسح من الإعدادات بعد تأكيد.

| البند | المحتوى |
|---|---|
| الأفضل لكل وضع | أعلى نقاط في الأركيد والاندفاع والزِن |
| المسيرة | المجموع، الإسقاطات، عدد الجولات |
| السفن | تُفتح بالمجموع ويُحفظ السفينة المختارة |
| الإعدادات | المؤثرات، الموسيقى، الاهتزاز، الجودة، اللغة |

### التقنية

- Three.js من CDN مع بديل cdnjs
- لا ملفات أصول؛ المجسمات والصوت مولّدة برمجيًا
- تجميع الأعداء والرصاص والجسيمات في مجموعات معاد استخدامها
- قياس معدل الإطارات وخفض الدقة تلقائيًا عند الحاجة
- الصوت يبدأ بعد أول تفاعل التزامًا بسياسة المتصفح
- زر ملء الشاشة يحاول تثبيت الوضع الأفقي حسب الجهاز

### التشغيل

1. احفظ هذا الملف باسم `index.html`
2. افتحه في المتصفح
3. التحميل الأول يحتاج إنترنت لتنزيل Three.js

### الضبط

| الموضع | ما يمكن تغييره |
|---|---|
| إعدادات الأعداء (CFG) | الصحة ونصف القطر والنقاط واللون |
| جدول الأنماط (PAT) | أوزان وأنماط الظهور |
| عرض الممر (bx / by) | شدة الاختناق وقوة دفع العواصف |

### استكشاف الأخطاء

- شاشة سوداء: قد لا يتم الوصول إلى CDN، تحقق من الاتصال
- لا صوت: يعمل بعد أول تفاعل، وراجع مفتاحي المؤثرات والموسيقى
- لا استجابة: تظهر شاشة تدوير الجهاز في الوضع الرأسي، أدر الجهاز أفقيًا

---

## Credits

- محرك الرسم: Three.js — MIT
- الخطوط: Michroma, Chakra Petch, Noto Sans JP (Google Fonts, OFL)
- الصوت: توليف مباشر عبر Web Audio API، بدون ملفات صوتية

## License / 権利表記 / Lizenz / Лицензия

本ファイル（1 つの HTML）とその README は、自作配布用として自由に改変・再配布できます。
第三者資産は含まれません（Three.js と Google Fonts は各自のライセンスに従ってください）。
This single HTML file and this README may be freely modified and redistributed. No third-party assets are bundled; Three.js and Google Fonts remain under their own licenses.