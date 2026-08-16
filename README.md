# 探せないファイル ― 企業内ファイル到達性の実測データセット

**Unreachable Files: A Measured Dataset of Enterprise File Retrieval Reachability**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21963182.svg)](https://doi.org/10.5281/zenodo.21963182)

社内に保存されているのに、キーワード検索では出てこないファイル。この問題を10業種で整理し、138ファイル・35課題で到達性を実測した調査報告の、**評価コーパス定義・課題と正解・課題別の測定結果・AI生成品質の全件判定**です。

調査報告の全文（日本語・HTML）:
**https://necfru.com/blog/security/unreachable-files/**

---

## 要旨

企業のファイル保管環境では、ファイルは保存されているのに、担当者が思いつく言葉では取り出せない状態が生じます。本調査はこれを「到達不能ファイル」と定義し、4つの類型（命名の不一致・語彙の不一致・内容の非露出・判断情報の不在）に整理したうえで、AI が生成した概要・タグを検索対象に含めた場合に到達性がどこまで変わるかを、事前登録型のプロトコルに従って測定しました。

コーパスは合成データ138ファイル（うち39%はファイル名が内容と乖離）、検索母集団は209件、課題は35問です。

## 主要な測定結果（2026-07-31）

| 条件 | Top-1正解率 | Recall@10 | 圏外率 |
|---|---|---|---|
| ファイル名検索（ベースライン） | 0.333 | 0.553 | 0.400 |
| メタデータ検索（AIタグ絞り込み） | 0.533 | 0.435 | 0.400 |
| 会話型AI検索 | 0.967 | 0.948 | 0.000 |
| AI構造検索 | 0.567 | 0.864 | — |

AI 生成メタデータの品質は、概要生成率 138/138（100.0%）、概要の事実誤り率 0.0%（96言明中0件、判定不能6件）、タグ適合率 98.2%（167件中164件）でした。

**ただし、正確であることと、見分けられることは別です。** 138件中26件（18.8%）はタグ集合が他ファイルと完全に一致し、概要の40.6%は数字を1つも含みません。メタデータ検索はベースラインを統計的に有意に上回りませんでした（Top-1 p=0.109）。改善した系統と、改善が検出できなかった系統の両方を公開しています。

## このリポジトリの内容

```
data/    評価コーパス構成表（138件・ゴールド記述つき）
         課題定義（35問・正解ファイルID）
         課題別の測定結果
         AI生成品質の判定結果（概要の言明判定・タグ判定・全件記述統計）
```

各ファイルの説明は `data/README.md` にあります。

**含まれていないもの**: クエリ1回ごとの生ログ、コーパス生成スクリプト、および検索系統の内部実装に関する情報は、本リポジトリには含まれていません。公開しているのは課題単位に集計した結果と、その判定根拠です。

## 測定の限界（重要）

本測定は、以下の条件下で行われたものです。数値を引用される場合は、あわせて明示してください。

- **自社製品の評価を自社が実施しています。** コーパス作成者・課題作成者・判定者・執筆者は同一人物であり、独立した第三者判定者はいません。
- **大規模環境に外挿できません。** コーパスは138ファイル・約3.6MBであり、実際の企業環境（数十万ファイル・数十TB規模）とは規模が異なります。
- **課題は35問であり、業務全体の探索行動を代表するとは限りません。**
- **人間の探索行動を測っていません。** 「探すのが速くなる」という主張は本測定の射程外です。
- **ベースライン（条件A）は上界として測定しています。** 機械抽出した全キーワードを1語ずつ検索し、最良順位を採用しました。現実の利用者はこれより不利になります。すなわち本測定はベースラインに有利な設計です。
- **検索結果の取得は上位20件を上限としています。**
- 緩和策は、プロトコルの事前登録、リトライ禁止、課題別結果と判定根拠の全件公開、集計とは独立の再計算検証の4点にとどまります。

失敗した課題、ゼロ件となった課題、入力自体が構成できなかった課題、および不適合と判定したタグは、すべて件数ではなく個別の行として含めています。

## 引用

```
草薙俊介 (2026). 探せないファイル ― 企業内ファイル到達性の実測データセット
（v1.0.0）. 株式会社ネクフル. https://doi.org/10.5281/zenodo.21963183
```

バージョンを問わず最新版を指す DOI は `10.5281/zenodo.21963182` です。
特定のバージョンを指定する必要がない場合は、こちらを使ってください。

調査報告の本文を引用する場合はこちらです。

```
草薙俊介 (2026). 探せないファイル ― 保存されているのにキーワードでは到達できない
企業内文書・画像・動画に関する業種横断調査と、自然文による到達性の実測.
株式会社ネクフル. https://necfru.com/blog/security/unreachable-files/
```

`CITATION.cff` を同梱しています。GitHub 右側の「Cite this repository」からも取得できます。

## ライセンス

[CC BY 4.0](LICENSE)

出典を明示していただければ、再利用・再配布・改変は自由です。

## 発行者

株式会社ネクフル（necfru Inc.） https://necfru.com/
著者: 草薙 俊介（代表取締役）

---

# English

Files are stored, yet nobody can retrieve them with the words they would naturally use. This repository contains the evaluation corpus definition, task set with ground truth, per-task measurement results and full quality judgements behind a Japanese-language field study of that problem across ten industries.

Full report (Japanese, HTML): https://necfru.com/blog/security/unreachable-files/

## Summary

We define *unreachable files* — files that exist in corporate storage but cannot be reached through keyword search — and classify them into four types: naming mismatch, vocabulary mismatch, non-exposed content, and absence of decision-relevant information. We then measured how much AI-generated summaries and tags change retrieval reachability, following a pre-registered protocol.

Corpus: 138 synthetic files (39% with filenames that diverge from content), retrieval pool of 209 items, 35 tasks. Measured 2026-07-31.

| Condition | Top-1 accuracy | Recall@10 | Miss rate |
|---|---|---|---|
| Filename search (baseline) | 0.333 | 0.553 | 0.400 |
| Metadata search (AI tag filtering) | 0.533 | 0.435 | 0.400 |
| Conversational AI search | 0.967 | 0.948 | 0.000 |
| Structured AI search | 0.567 | 0.864 | — |

AI metadata quality: 100.0% summary generation, 0.0% factual error rate (0 of 96 claims), 98.2% tag precision. **However, accuracy is not the same as distinguishability.** 26 of 138 files (18.8%) share an identical tag set with another file, and 40.6% of summaries contain no numbers at all. Metadata search did not significantly outperform the baseline (Top-1 p=0.109).

## Limitations

This is a vendor self-evaluation. The corpus author, task author, judge and report author are the same person; there is no independent third-party judge. The corpus is 138 files / approx. 3.6 MB and does not extrapolate to real enterprise environments of hundreds of thousands of files. The task set is 35 items and may not represent search behaviour as a whole. Human search behaviour was not measured. The baseline condition was measured as an upper bound: every mechanically extracted keyword was issued separately and the best rank was taken, which is more favourable than a real user. Result retrieval was capped at the top 20 items. Mitigations are limited to pre-registration, a no-retry rule, full publication of per-task results and judgement rationale, and independent re-computation of all reported figures.

Failed tasks, zero-result queries, tasks for which no query could be constructed, and every tag judged non-conforming are included as individual rows, not as aggregate counts.

**Not included**: per-query raw logs, the corpus generation script, and any information about the internal implementation of the retrieval systems.

## Citation

```
Kusanagi, S. (2026). Unreachable Files: A Measured Dataset of Enterprise File
Retrieval Reachability (v1.0.0) [Data set]. necfru Inc.
https://doi.org/10.5281/zenodo.21963183
```

The concept DOI `10.5281/zenodo.21963182` always resolves to the latest version.

To cite the report itself:

```
Kusanagi, S. (2026). Unreachable Files: A Cross-Industry Study of Enterprise Documents,
Images and Video That Cannot Be Reached by Keyword Search, and a Measurement of
Natural-Language Retrieval Reachability. necfru Inc.
https://necfru.com/blog/security/unreachable-files/
```

## License

CC BY 4.0.
