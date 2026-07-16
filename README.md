## 実行方法

### 前提条件
- Python 3.11 以上
- Git

### 環境構築（uv を使用）

#### 1. uv のインストール

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# または Homebrew を使用
brew install uv
```

詳細：https://docs.astral.sh/uv/

#### 2. リポジトリをクローン

```bash
git clone https://github.com/Michikoo29avril/temperature-finance-analysis.git
cd temperature-finance-analysis
```

#### 3. 仮想環境を作成し依存関係をインストール

```bash
# uv が自動で仮想環境を作成・管理します
uv sync
```

この 1 コマンドで以下が自動実行されます：
- Python 3.11 仮想環境の作成
- `pyproject.toml` の依存パッケージをインストール

#### 4. 仮想環境を有効化

```bash
# uv run を使う場合（推奨）
uv run jupyter notebook temperature_cpi_1970.ipynb

# または手動で有効化
source .venv/bin/activate  # macOS/Linux
# または
.venv\Scripts\activate  # Windows
```

### Jupyter Notebook を実行

#### オプション 1：uv run を使う（推奨）

```bash
# 仮想環境を自動で有効化して実行
uv run jupyter notebook temperature_cpi_1970.ipynb
```

#### オプション 2：手動で仮想環境を有効化

```bash
# 仮想環境を有効化
source .venv/bin/activate

# Jupyter を起動
jupyter notebook temperature_cpi_1970.ipynb
```

### セルの実行

Notebook が起動したら：

1. `temperature_cpi_1970.ipynb` をクリック
2. セルを上から順に実行
   - セルをクリック → `Ctrl + Enter`（または `Cell > Run All`）
3. グラフが `outputs/` に自動保存される

---

## 依存パッケージ

```toml
# pyproject.toml に記載
pandas       # データ処理
numpy        # 数値計算
matplotlib   # グラフ描画
seaborn      # 統計グラフ
prophet      # 時系列予測
scipy        # 統計分析
jupyter      # Notebook 環境
```

### パッケージを追加する場合

```bash
# 新しいパッケージを追加
uv add パッケージ名

# 例：新しい統計ライブラリを追加
uv add statsmodels

# 開発用パッケージの追加
uv add --dev pytest
```

### パッケージをアップデート

```bash
# すべてのパッケージを最新に
uv sync --upgrade

# 特定のパッケージのみ
uv update pandas
```

---

## 他のマシンで実行

別のマシンで同じ環境を再現する場合：

```bash
# リポジトリをクローン
git clone https://github.com/Michikoo29avril/temperature-finance-analysis.git
cd temperature-finance-analysis

# uv.lock から完全に同じ環境を再構築
uv sync

# Notebook を実行
uv run jupyter notebook temperature_cpi_1970.ipynb
```

`uv.lock` により、開発時と本番時で完全に同じバージョンが保証されます。

---

## トラブルシューティング

### Python のバージョンが異なる場合

```bash
# インストール済みの Python バージョンを確認
uv python list

# 特定バージョンの Python で実行
uv sync --python 3.11
```

### Jupyter が起動しない

```bash
# uv run で直接実行
uv run jupyter notebook temperature_cpi_1970.ipynb

# それでもダメな場合は手動有効化
source .venv/bin/activate
jupyter notebook temperature_cpi_1970.ipynb
```

### ModuleNotFoundError が出る

```bash
# 依存関係を再インストール
uv sync --refresh

# または
rm uv.lock
uv sync
```

---

## 開発に参加する場合

```bash
# 開発用依存パッケージもインストール
uv sync

# テストを実行
uv run pytest

# コードをフォーマット
uv run black .

# 型チェック
uv run mypy .
```

---
