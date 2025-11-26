# Human-Readable Proof v0.1 ドラフト（v0.1 本文リセット）

このファイルは、旧 v0.1 の文章を **一旦すべて無効化して**、
「人間が読める証拠レポート」の仕様をゼロから書き直すための叩き台。

旧テキストは Git 履歴に残っているが、今の設計とは前提が合わないので、
ここから先は参照しない。

---

## 目的（何を解決するか）

- 被害者・裁判所・保険会社・規制当局・市民が、
  「ハッシュとJSONだけ」ではなく **意味が分かるレポート** を受け取ること
- そのレポートが、
  - Novara Evidence Bundle（AAL + anchors + meta）
  - SLO-Bond / 保険支払い
  - 補償・再発防止策
  と 1:1 に対応していること

---

## 後でここに書くべき最低項目（アウトライン）

Human-Readable Proof 1通につき、最低限:

1. 何が起きたか（Timeline）
2. 誰が関わったか（Actors / Systems / Models）
3. どのポリシーのもとで動いたか（Policy / Version）
4. どの Evidence Bundle によって裏付けられているか（Bundle IDs / Hashes）
5. 誰がいくら払うか、なぜその額か（Attribution ＋ SLO-Bound Formula）
6. 何が変わったか（再発防止策 / Config / Model / Org）

---

## 当面の方針

- 今は **本文を全部消して、骨だけ残す** フェーズ
- 条文っぽく書くのではなく、
  「2040 年に裁判所と保険会社がそのまま読める仕様書」
  にしていく
- 英語版 `human-readable-proof-v0.1-en.md` は、
  この日本語を固めてから派生させる