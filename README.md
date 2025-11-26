# novara-core

novara-core is the text-only constitutional layer for the Novara Evidence OS.  
Code, SDKs, and APIs live in the Novara implementation repositories.  
This repo defines what all of them must obey.

日本語で言うと:

Novara-core は  
「どんな実装でも絶対に破ってはいけないルール」と  
「2040 年までに満たしていないと詰む条件」を  
テキストだけで固定するためのリポジトリです。

実装や SDK は Novara 側に追い出し、  
ここでは原則、ガバナンス、プロトコルのルール、チェックポイントだけを書きます。

---

## 1. Novara リポジトリとの関係

ざっくり分担はこうです。

- Novara  
  実装リポジトリ  
  Evidence Bundle のフォーマット、検証ツール、API、PoC、ロードマップなど  
  「何がどう動いているか」を扱う場所。

- novara-core  
  憲法リポジトリ  
  原則、ガバナンス、プロトコルのルール、2040 までの殺しチェックポイント  
  「どこまで崩れたら Novara を名乗ってはいけないか」を決める場所。

ここに書かれた条件を満たさない実装は、  
たとえコードが似ていても「正統 Novara」を名乗れないものとします。

---

## 2. このリポジトリで扱うもの

novara-core が固定するのは次の四つです。

1. 原則  
   Novara がどんな状況でも捨ててはいけない核となる考え方。

2. ガバナンス  
   誰が何を変更できるか、資本や国家がどこまで介入できるか、  
   フォークが起きた時にどちらが正統かをどう判定するか。

3. プロトコルのルール  
   CTK-2 や Evidence Bundle など、各プロトコルが守るべき  
   最低限の制約と禁止事項。  
   ワイヤ仕様そのものは Novara 実装側に置き、  
   ここでは「これを抜いたら失格」というラインだけを書く。

4. 2040 チェックポイント  
   2027 / 2030 / 2033 / 2035 などの年ごとに  
   満たしていないとその世界線がほぼ詰む条件を明文化する。  
   判例本数、保険条約、行政 Pilot、ギルド規模などを含む。

---

## 3. ディレクトリ構成

初期構成のイメージは次の通りです。

```text
novara-core/
├── README.md
├── LICENSE
└── docs/
    ├── constitution/
    │   ├── 00-index-ja.md
    │   ├── 01-principles-ja.md
    │   ├── 02-evidence-sovereignty-ja.md
    │   ├── 03-independence-and-capital-ja.md
    │   ├── 04-anti-capture-anti-abuse-ja.md
    │   ├── 05-meta-asi-governance-ja.md
    │   ├── 06-standardisation-strategy-ja.md
    │   └── 90-glossary-ja.md
    ├── protocols/
    │   ├── 00-index-ja.md
    │   ├── ctk2-wire-governance-v0.1-ja.md
    │   ├── evidence-bundle-governance-v0.1-ja.md
    │   ├── incident-protocol-v0.1-ja.md
    │   ├── insurance-ratecard-governance-v0.1-ja.md
    │   └── asi-slot-governance-v0.1-ja.md
    ├── checkpoints/
    │   └── roadmap-2040-checkpoints-ja.md
    └── archive/
        └── 90-legacy-YYYY-MM-DD.md