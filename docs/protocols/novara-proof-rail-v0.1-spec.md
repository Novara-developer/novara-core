# Novara proof rail v0.1 spec

目的  
支払い、権利付与、重要なステータス変更などの前に  
有効な Evidence Bundle が存在するかをチェックし、  
条件を満たさないトランザクションを止めるための最小仕様を定義する。

本 spec は v0.1 の実装用。  
将来の金融インフラ連携では v1.x で厳格化する。

## 1. 基本コンセプト

Proof rail は「支払い API ではなく、その前段に挟むフィルター」。

- 入力  
  支払いや権利変更のリクエスト  
- 内部で見るもの  
  関連する Evidence Bundle とポリシー  
- 出力  
  許可、保留、拒否 の三値と、その理由コード

支払い処理そのものは別システムが担当する。

## 2. リクエスト形式

抽象レベルの必須フィールド

- request_id  
- subject_id  
- amount または権利変更の内容  
- currency または対象リソース  
- evidence_bundle_id  
- policy_id  
- requested_at

実際のフィールド名や追加項目は各実装で拡張してよいが、  
上記に相当する情報が無いリクエストは受理してはならない。

## 3. レスポンス形式

レスポンスは次の三値のどれか。

- APPROVE  
- HOLD  
- REJECT  

共通フィールド

- request_id  
- decision  
- decision_reason_code  
- decided_at  
- evidence_summary  
  例  
  使用された Evidence Bundle のハッシュと、確認したチェックリストの結果

decision_reason_code は機械処理用の短いコードとし、  
人間向け説明は別途 human readable proof 側で扱う。

## 4. チェック項目 v0.1

最低限、次の条件をすべて満たした場合のみ APPROVE としてよい。

一 Evidence Bundle が検証成功  
  hash チェーン、anchors、署名など、当該バージョンの spec が要求する項目が全て ok。

二 bundle 内に該当トランザクションの AAL レコードが存在  
  request_id または同等のキーでひも付け可能であること。

三 適用ポリシーが有効期間内  
  policy_id に対応するポリシーが、requested_at の時点で有効である。

四 上限チェック  
  同一 subject に対する累積額や回数が、ポリシーで定めた上限内である。

いずれかが満たされない場合は HOLD または REJECT を返す。

## 5. AAL への記録

Proof rail 自身も AAL に次のレコードを残す。

- kind が proof_rail_decision  
- 対応する request_id  
- decision  
- decision_reason_code  
- evidence_bundle_id  
- policy_id  
- decided_at

このログによって  
「なぜその支払いが通ったか、または止まったか」が後から検証できる。

## 6. 失敗モード

Proof rail が正常に判定できない場合の扱いを固定する。

代表的な失敗例

- Evidence Bundle 検証に必要なライブラリの障害  
- バンドルが取得できない  
- 内部ストレージの障害

原則

- 証拠が確認できない場合はデフォルトで HOLD か REJECT  
- 「証拠が無いが通した」という状態は v0.1 では許容しない

実装側は failure_mode フィールドで  
どのクラスの障害だったかを記録すること。

## 7. SLO ボンドとの関係

Proof rail は次をトリガーとして扱う。

- REJECT や HOLD が一定割合を超えた場合  
- 特定の decision_reason_code が異常に多い場合

この情報は別途 SLO ボンドや保険の ratecard に渡される。  
本 spec v0.1 では連携の詳細までは規定しないが、  
将来の拡張で証拠として利用できるよう、  
メトリクスを継続的に AAL に流すことだけ定める。

## 8. バージョニング

Proof rail のバージョンと、対応する Evidence Bundle spec のバージョンを  
次のように管理する。

- 本文書は proof_rail v0.1  
- 対応する Evidence Bundle は v0.9 から v1.0 を想定  
- 互換性が破れる変更が入る場合は v1.x として別文書を作成する

トランザクションごとに  
使用した proof rail バージョンを AAL に記録すること。