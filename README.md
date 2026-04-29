# TikZ 経済学図版テンプレート

経済学の授業・研究発表で頻繁に使う図を **TikZ** で描き、**Beamer** スライドに埋め込むためのサンプル集です。各 TikZ ファイルは単体でコンパイルして確認することも、Beamer スライドに `\input` で直接埋め込むこともできます。

> **コンパイル環境**: upLaTeX + dvipdfmx（日本語 LaTeX 環境）

---

## 図の一覧

### ミクロ経済学

| ファイル | 内容 |
|---|---|
| `tikz/Fig_supply_demand.tex` | 需要・供給曲線（市場均衡） |

### マクロ経済学：基礎概念

| ファイル | 内容 |
|---|---|
| `tikz/Fig_45_degree.tex` | 45度線モデル（消費関数・均衡国民所得） |
| `tikz/Fig_flow_stock.tex` | フローとストックの関係（バスタブモデル） |
| `tikz/Fig_three_approaches.tex` | GDP の三面等価（生産・支出・分配） |

### 景気循環・経済成長

| ファイル | 内容 |
|---|---|
| `tikz/Fig_bc_trend.tex` | 経済成長とトレンド |
| `tikz/Fig_bc_cycle.tex` | 景気循環（拡張・後退局面のシェード付き） |
| `tikz/Fig_business_cycle.tex` | 景気循環（別バージョン） |

### AD-AS 分析

| ファイル | 内容 |
|---|---|
| `tikz/Fig_adas_lr.tex` | AD-AS 分析：長期均衡（LRAS 垂直線） |
| `tikz/Fig_adas_lr_shift.tex` | AD-AS 分析：長期均衡（AD シフト後） |
| `tikz/Fig_adas_sr.tex` | AD-AS 分析：短期均衡（SRAS 右上がり） |

### 因果推論・政策評価

| ファイル | 内容 |
|---|---|
| `tikz/Fig_causal_simple.tex` | 因果推論の根本問題（潜在的結果の枠組み） |
| `tikz/Fig_counterfactual_cycle.tex` | 政策評価の難しさ（反実仮想と時系列） |
| `tikz/Fig_did.tex` | Difference-in-Differences 分析のイメージ |

---

## ファイル構成

```
tikz-econ-figure/
├── tikz-econ-figure.tex   # Beamer メインファイル（サンプルスライド）
├── my_preamble.tex         # 共通プリアンブル（フォント・テーマ・色定義など）
└── tikz/
    ├── Fig_supply_demand.tex
    ├── Fig_45_degree.tex
    ├── Fig_flow_stock.tex
    ├── Fig_three_approaches.tex
    ├── Fig_bc_trend.tex
    ├── Fig_bc_cycle.tex
    ├── Fig_business_cycle.tex
    ├── Fig_adas_lr.tex
    ├── Fig_adas_lr_shift.tex
    ├── Fig_adas_sr.tex
    ├── Fig_causal_simple.tex
    ├── Fig_counterfactual_cycle.tex
    └── Fig_did.tex
```

---

## 動作環境・必要パッケージ

| 項目 | 内容 |
|---|---|
| TeX エンジン | upLaTeX |
| DVI ドライバ | dvipdfmx |
| TeX ディストリビューション | TeX Live 2023 以降 |

使用パッケージ: `beamer`, `tikz`, `pgfplots`, `standalone`, `newpxtext`, `newpxmath`, `otf`, `pxchfon`, `pxjahyper`, `natbib`

使用 TikZ ライブラリ: `arrows.meta`, `decorations.pathreplacing`, `shapes.geometric`, `positioning`, `calligraphy`

---

## コンパイル方法

### Beamer スライド全体をコンパイルする

```bash
uplatex  tikz-econ-figure.tex
dvipdfmx tikz-econ-figure.dvi
```

latexmk を使う場合（`.latexmkrc` を別途用意してください）:

```bash
latexmk tikz-econ-figure.tex
```

### 各 TikZ ファイルを単体で確認する

```bash
uplatex  tikz/Fig_supply_demand.tex
dvipdfmx tikz/Fig_supply_demand.dvi
```

---

## 自分のスライドへの組み込み方

1. `my_preamble.tex` をプロジェクトにコピーし、`\documentclass` の直後に `\input{my_preamble}` を記述する。
2. 必要な TikZ ファイルを `tikz/` フォルダに置く。
3. スライドの各フレームに `\input` で埋め込む。

```latex
\begin{frame}{需要と供給}
  \begin{center}
    \input{tikz/Fig_supply_demand}
  \end{center}
\end{frame}
```

図が大きすぎる場合は `\scalebox` でサイズ調整できます:

```latex
\begin{frame}{AD-AS 分析：長期均衡}
  \begin{center}
    \scalebox{0.8}{\input{tikz/Fig_adas_lr}}
  \end{center}
\end{frame}
```

---

## 日本語フォントの設定

`tikz-econ-figure.tex` では macOS 向けに**原ノ味フォント**（`haranoaji`）を設定しています。環境に合わせて `pxchfon` のオプションを変更してください。

| 環境 | オプション |
|---|---|
| macOS（原ノ味フォント） | `\usepackage[haranoaji]{pxchfon}` |
| macOS（游書体） | `\usepackage[yu-osx]{pxchfon}` |
| 環境非依存（IPAex） | `\usepackage[ipaex]{pxchfon}` |

---

## 色の定義

共通カラーは `my_preamble.tex` で定義しています。TikZ ファイルの `standalone` プリアンブルは `\input` 時に無視されるため、色定義はプリアンブルに集約しています。

| 色名 | RGB | 用途 |
|---|---|---|
| `gdpblue` | (30, 90, 180) | GDP 曲線・AD 曲線 |
| `trendred` | (190, 40, 40) | トレンド線・LRAS・対照群 |
| `srasgreen` | (30, 140, 60) | SRAS（短期総供給曲線）・分配面 |
| `expgreen` | (200, 230, 200) | 拡張局面シェード |
| `recred` | (240, 200, 200) | 後退局面シェード |
| `goldcol` | (190, 140, 10) | GDP ボックス（三面等価） |
| `obscol` | (210, 228, 255) | 観測可能（薄青）・因果推論図 |
| `cfcol` | (232, 232, 232) | 観測不可（薄灰）・反実仮想 |
| `cfgray` | (100, 140, 200) | 反事実の折れ線（DiD 図） |
| `fillcol` | (180, 215, 255) | 政策効果の差分領域 |
| `watercol` | (175, 210, 240) | バスタブモデルの水（フロー・ストック図） |

---

## ライセンス

[MIT License](LICENSE) — 自由にご利用・改変・再配布いただけます。

---

## 作者

山田 知明（明治大学 商学部）
