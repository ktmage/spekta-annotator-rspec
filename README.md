# @ktmage/spekta-annotator-rspec

RSpec / Capybara で書かれたテストファイル (`*_spec.rb`) を解析し、Spekta アノテーションを自動生成するプラグイン。

## 機能

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

## 設定例

```yaml
annotators:
  - name: rspec
    page_from: filename
```

## page_from

| 値 | 動作 |
|---|---|
| `manual` (デフォルト) | `page` アノテーションを自動生成しない。ソース内のコメント等で手動指定する想定。 |
| `filename` | トップレベルの `feature` / `describe` で、ファイル名から `page` を自動生成する。`login_spec.rb` → `login`、`user_profile_spec.rb` → `user-profile`（`_spec` 除去、`_` を `-` に変換）。 |
