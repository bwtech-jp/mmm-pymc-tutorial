# MMM（マーケティング・ミックス・モデリング）入門（ケーススタディ1）

Python とベイズ統計で、MMM（マーケティング・ミックス・モデリング）を手を動かしながら日本語で学ぶ、無料の教材です。
[PyMC-Marketing](https://www.pymc-marketing.io/) の公式ケーススタディ「[MMM End-to-End Case Study](https://www.pymc-marketing.io/en/stable/notebooks/mmm/mmm_case_study.html)」を、学ぶ順に8回のノートブックに組み立て直しました。

- 上から順に実行するだけで進められます（コードを書く必要はありません）
- 各回に、図の読み方の解説と、答えつきの小課題があります
- 解説ページ：<https://bwtech.co.jp/learn/mmm/>

作成：[Birdwing Technologies合同会社](https://bwtech.co.jp/)

## 目次

| 回 | 内容 | 所要時間 | ノートブック | Colab |
|---|---|---|---|---|
| 第0回 | 動作確認 | 5〜10分 | [00_setup_check.ipynb](00_setup_check.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/00_setup_check.ipynb) |
| 第1回 | データ理解（EDA） | 30〜45分 | [01_eda.ipynb](01_eda.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/01_eda.ipynb) |
| 第2回 | adstock と saturation | 45〜60分 | [02_adstock_saturation.ipynb](02_adstock_saturation.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/02_adstock_saturation.ipynb) |
| 第3回 | モデル定義と事前分布 | 45〜60分 | [03_model_priors.ipynb](03_model_priors.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/03_model_priors.ipynb) |
| 第4回 | 学習（MCMC）と診断 | 60分 | [04_fit_diagnostics.ipynb](04_fit_diagnostics.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/04_fit_diagnostics.ipynb) |
| 第5回 | 結果の解釈（貢献・ROAS・飽和曲線） | 60分 | [05_results.ipynb](05_results.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/05_results.ipynb) |
| 第6回 | 予測精度の検証 | 45分 | [06_out_of_sample.ipynb](06_out_of_sample.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/06_out_of_sample.ipynb) |
| 第7回 | 予算最適化 | 60分 | [07_budget_optimization.ipynb](07_budget_optimization.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/07_budget_optimization.ipynb) |
| 第8回 | 振り返り（説明資料を1枚作る） | 60分 | [08_review_onepager.ipynb](08_review_onepager.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bwtech-jp/mmm-pymc-tutorial/blob/main/08_review_onepager.ipynb) |

## 始め方

### A. Google Colab で動かす（準備不要）

上の表の「Open in Colab」を押して開き、上から順に実行します。必要なライブラリとデータは、最初のセルが自動で用意します。
開き方は、解説ページの「[第0回 環境構築](https://bwtech.co.jp/learn/mmm/00-setup)」を見てください。

- 第4回以降は、学習結果（約185MB）を Google ドライブの `mmm-pymc/models/` に保存します。初回に、ドライブへの接続を許可する画面が出ます
- ドライブを使いたくないときは、最初のセルの `USE_DRIVE = True` を `False` に変えます（その場合は、回ごとに学習し直します）

### B. 自分のPCで動かす

Python 3.11 が必要です。

```
python -m venv .venv
.venv\Scripts\activate          （Mac / Linux は source .venv/bin/activate）
pip install -r requirements.txt
```

そのあと、VS Code などでノートブックを開き、カーネルに `.venv` を選びます。
まず `00_setup_check.ipynb` を実行して、最後に「準備完了」と出ることを確かめてください。
くわしい手順は「[第0回 環境構築](https://bwtech.co.jp/learn/mmm/00-setup)」にあります。

## 動作を確かめた環境

| | 版 |
|---|---|
| OS | Windows 11 |
| Python | 3.11 |
| pymc-marketing | 0.19.2 |
| pymc | 5.28.5 |
| nutpie | 0.16.8 |

- Windows には C++ コンパイラ（g++）が入っていないことが多いので、g++ がなくても動く設定（`nuts_sampler="nutpie"`、`compile_kwargs={"mode": "NUMBA"}`）にしてあります
- Google Colab でも、全9本が最後まで動くことを確かめました（2026年11月）
- Mac / Linux での動作は確かめていません
- 版が違うと、結果の数字が少し変わることがあります

## データについて

- 本家のケーススタディと同じ、公開されている学習用のデータです（週次・209週）。特定の企業の実績として扱わないでください
- データのファイルは、このリポジトリには入っていません。ノートブックの最初のセルが、PyMC-Marketing のリポジトリから取得します

## ライセンス

Apache License 2.0（[LICENSE](LICENSE)）。もとにしたものと変更点は [NOTICE](NOTICE) に書いてあります。

## お問い合わせ

内容の誤りや、動かなかった点があれば、[お問い合わせフォーム](https://bwtech.co.jp/contact)からお知らせください。
