# Sprint 2 自己評価: 体験問題（4択）

## 実装日: 2026-09-03

---

## 完了条件チェック

| # | 条件 | 状態 | 備考 |
|---|------|------|------|
| 1 | 体験問題4問がproblems.jsに追加されている | ✅ | u6_plane_trial_001〜004 |
| 2 | topicUnitId: 'u6-plane' が正しく設定されている | ✅ | 4問すべて |
| 3 | difficulty <= 2 の問題が3問以上ある | ✅ | 001:diff1, 002:diff1, 003:diff2, 004:diff2 |
| 4 | problems.jsの構文が正しい | ✅ | node new Function()でエラーなし |
| 5 | initTopicTrial('u6-plane')で問題が表示される | ✅ | difficulty<=2の問題3件がスライス取得される |
| 6 | 既存の体験問題UIと同じ見た目・操作感 | ✅ | 同一topicUnitId形式を使用 |

---

## 追加した問題

| ID | 単元 | 正解 | 難易度 |
|----|------|------|--------|
| u6_plane_trial_001 | 平行四辺形の面積 | 40cm² | ★1 |
| u6_plane_trial_002 | 三角形の面積 | 12cm² | ★1 |
| u6_plane_trial_003 | 台形の面積 | 20cm² | ★2 |
| u6_plane_trial_004 | 複合図形（三角形2つ） | 42cm² | ★2 |

## 実装メモ

- `generateChoices()` が自動でダミー選択肢を生成するため、choicesフィールドは不要
- `initTopicTrial` が `difficulty <= 2` かつ先頭3件を使うため、4問中3問が表示される
- 4問目（複合図形）は演習への橋渡しとして、公式を3つ組み合わせる問題を選択

## Sprint 3 への引き継ぎ

- categories.js の u6-plane を `available: true`、`count: 15`、`topicScreen: 'u6-plane'` に更新
- data/problems.js に演習問題15問を追加（catId: 'pc-plane'）
- 単元一覧で「平面図形の完成」が表示されることを確認
