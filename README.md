# @ktmage/spekta-annotator-rspec

Spekta RSpec Annotator plugin. Auto-generates `[spekta:*]` annotations from RSpec / Capybara tests.

Spekta の RSpec Annotator プラグイン。RSpec / Capybara テストファイルから `[spekta:*]` コメントを自動生成する。

## Table of Contents / 目次

- [English](#english)
- [日本語](#japanese)

<a id="english"></a>
## English

> [!CAUTION]
> **Disclaimer:**
> This project is experimental. It is provided "as-is" without warranty of any kind. APIs and output format may change without notice. Use at your own risk.

### Features

Recognizes the following RSpec / Capybara syntax and generates annotations.

**Structure (section)**

| Syntax | Annotation |
|---|---|
| `feature "..." do` / `describe "..." do` | `section` (also `page` when top-level with `page_from: filename`) |
| `context "..." do` | `section` |
| `scenario "..." do` / `it "..." do` | `section` + step collection starts |

**Steps (step)**

Recognizes Capybara DSL inside `scenario` / `it` blocks.

| DSL | Generated Step |
|---|---|
| `visit` | Open page |
| `fill_in "X", with: "Y"` | Enter "Y" in "X" |
| `click_on "X"` | Click "X" |
| `select "V", from: "X"` | Select "V" from "X" |
| `expect(page).to have_content "X"` | "X" is displayed |
| `expect(page).not_to have_content "X"` | "X" is not displayed |

### Installation

> npm package is not yet published. Currently available as a submodule of the [Spekta monorepo](https://github.com/ktmage/spekta).

After npm publication:

```bash
npm install @ktmage/spekta-annotator-rspec
```

### Configuration

```yaml
annotator:
  "@ktmage/spekta-annotator-rspec":
    page_from: filename
```

### page_from

| Value | Behavior |
|---|---|
| `manual` (default) | Does not auto-generate `page` annotations. Pages are specified manually via comments. |
| `filename` | Auto-generates `page` from the top-level `feature` / `describe`. `login_spec.rb` → `login`, `user_profile_spec.rb` → `user-profile`. |

### License

[MIT](LICENSE)

---

<a id="japanese"></a>
## 日本語

> [!CAUTION]
> **免責事項：**
> 本プロジェクトは実験的な取り組みです。いかなる保証もなく「現状のまま」提供されます。API や出力形式は予告なく変更される可能性があります。ご利用は自己責任でお願いいたします。

### 機能

以下の RSpec / Capybara の構文を認識してアノテーションを生成する。

**構造 (section)**

| 構文 | アノテーション |
|---|---|
| `feature "..." do` / `describe "..." do` | `section`（トップレベルかつ `page_from: filename` の場合は `page` も生成） |
| `context "..." do` | `section` |
| `scenario "..." do` / `it "..." do` | `section` + ステップ収集開始 |

**ステップ (step)**

`scenario` / `it` ブロック内の Capybara DSL を認識する。

| DSL | 生成されるステップ |
|---|---|
| `visit` | ページを開く |
| `fill_in "X", with: "Y"` | 「X」に「Y」と入力 |
| `click_on "X"` | 「X」をクリック |
| `select "V", from: "X"` | 「X」から「V」を選択 |
| `expect(page).to have_content "X"` | 「X」が表示される |
| `expect(page).not_to have_content "X"` | 「X」が表示されない |

### インストール

> npm パッケージは未公開です。現在は [Spekta モノレポ](https://github.com/ktmage/spekta) のサブモジュールとして利用できます。

npm 公開後は以下でインストールできるようになる予定です。

```bash
npm install @ktmage/spekta-annotator-rspec
```

### 設定例

```yaml
annotator:
  "@ktmage/spekta-annotator-rspec":
    page_from: filename
```

### page_from

| 値 | 動作 |
|---|---|
| `manual` (デフォルト) | `page` アノテーションを自動生成しない。ソース内のコメント等で手動指定する想定。 |
| `filename` | トップレベルの `feature` / `describe` で、ファイル名から `page` を自動生成する。`login_spec.rb` → `login`、`user_profile_spec.rb` → `user-profile`（`_spec` 除去、`_` を `-` に変換）。 |

### ライセンス

[MIT](LICENSE)
