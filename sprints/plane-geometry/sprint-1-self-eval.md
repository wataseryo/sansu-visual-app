# Sprint 1 自己評価: インタラクティブトピック画面（u6-plane-screen）

## 実装日: 2026-09-03

---

## 完了条件チェック

| # | 条件 | 状態 | 備考 |
|---|------|------|------|
| 1 | 平行四辺形「変形を見る」→ 長方形アニメーション | ✅ | `pg-tri-left` に translateX(160px)、CSS transition 1.2s |
| 2 | アニメーション中に「底辺」ラベルが図に重なって表示 | ✅ | `pg-base-label` opacity 0→1 (delay 1.2s) |
| 3 | 三角形「変形を見る」→ 2つの三角形が並ぶアニメーション | ✅ | `tri-2` を画面外右から translateX(0) へ移動 |
| 4 | 台形「変形を見る」→ 台形2つが組み合わさるアニメーション | ✅ | `trap-2` を rotate(180deg) + translateX で移動 |
| 5 | 各アニメーションに「やり直す」ボタン | ✅ | `resetPlaneAnim()` 呼び出し |
| 6 | アニメーション後に公式が強調表示 | ✅ | `.formula-reveal.visible` クラストグル |
| 7 | 概念カード（学ぶこと・入試でどう出るか・よくあるミス） | ✅ | 3枚の topic-concept-card |
| 8 | 基本例題（複合図形・補助線で分割） | ✅ | SVG付き例題カード（平行四辺形 + 内部三角形） |
| 9 | スマホ（375px）でアニメーションが崩れない | ✅ | SVG に viewBox + width:100% + max-width:320px |
| 10 | 既存のナビゲーション構造と統一 | ✅ | showScreen/initTopicTrial を既存パターン通り利用 |

---

## 実装内容

### 変更ファイル

1. **`/Users/wataseryo/教育アプリ/index.html`**
   - `u6-special-screen` の直前に `u6-plane-screen` を挿入（約160行）
   - タブUI（平行四辺形・三角形・台形）、3つのSVGアニメーション、概念カード3枚、基本例題、体験問題エリア、演習導線

2. **`/Users/wataseryo/教育アプリ/js/app.js`**
   - `showScreen()` に `if (id === 'u6-plane')` 分岐を追加
   - `switchPlaneTab()` 関数を追加
   - `playPlaneAnim()` 関数を追加（3図形すべて実装）
   - `resetPlaneAnim()` 関数を追加（3図形すべて実装）

3. **`/Users/wataseryo/教育アプリ/css/style.css`**
   - `.plane-tabs`, `.plane-tab-btn`, `.plane-tab-btn.active` を追加
   - `.plane-anim-btn.play`, `.plane-anim-btn.reset` を追加
   - `.formula-reveal`, `.formula-reveal.visible` を追加

---

## アニメーション実装詳細

### 平行四辺形 → 長方形
- 左の三角形ポリゴン（40px幅）を `translateX(160px)` で右に移動
- 長方形の右側に三角形がはまり込む形で長方形が完成
- 「底辺」テキストラベルが opacity 0→1 でフェードイン

### 三角形 × 2 → 平行四辺形
- tri-2 を画面外右（translateX 200px）から所定位置（translateX 0）へ移動
- `requestAnimationFrame` 二重呼び出しでトランジション開始前の初期位置設定を確実に実行

### 台形 × 2 → 平行四辺形
- trap-2 を `rotate(180deg)` で上下反転した状態で左外から右へ移動
- 台形2の変換起点は `transform-origin: 120px 65px`（台形1の重心）

---

## 潜在的なリスク・注意事項

1. **iOS Safari の transform-origin 挙動**: SVG要素へのCSSトランジションはSafariで稀に誤動作する。`requestAnimationFrame`の二重呼び出しで緩和しているが、実機確認推奨
2. **体験問題データ（Sprint 2）**: `initTopicTrial('u6-plane')` を呼んでいるが、problems.js に u6-plane 用のトピック問題が未追加のため、現時点では体験問題エリアは空表示
3. **categories.js の `available: false`**: Sprint 3 まで単元一覧には表示されない。Sprint 1 では意図通りの状態

---

## Sprint 2 への引き継ぎ

- `trial-u6-plane` div に体験問題（4択4問）を追加する
- `data/problems.js` に `topicUnitId: 'u6-plane'` の問題を4問追加する
- 問題内容は仕様書 Sprint 2 セクションに記載済み
