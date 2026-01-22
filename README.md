# リンクチェッカー テストページ集

CC Link Status Interval Checker 拡張機能の動作検証用テストページ集です。

## 📂 フォルダ構成

```
Page-Check-Test-Web/
├── index.html                    # テストダッシュボード（トップページ）
├── README.md                     # このファイル
├── anchor-tests/                 # アンカーリンク関連テスト
│   ├── same-page-anchors.html   # 同一ページ内アンカー
│   ├── cross-page-anchors.html  # 別ページへのアンカー
│   ├── anchor-targets.html      # アンカーターゲットページ
│   ├── encoded-anchors.html     # エンコードされたアンカー
│   └── duplicate-ids.html       # 重複ID検証
├── internal-links/               # 内部リンク関連テスト
│   ├── valid-links.html         # 正常なリンク
│   ├── valid-page-1.html        # 正常なページ1
│   ├── valid-page-2.html        # 正常なページ2
│   ├── broken-links.html        # 404エラー
│   └── relative-absolute-paths.html  # 相対/絶対パス
├── special-cases/                # 特殊ケーステスト
│   ├── empty-hrefs.html         # 空のhref
│   ├── hidden-elements.html     # 非表示要素
│   ├── special-protocols.html   # 特殊プロトコル
│   └── redirects.html           # リダイレクト
├── error-pages/                  # エラーページ
│   ├── 404.html                 # 404ページ
│   ├── soft-error-title.html    # ソフトエラー（タイトル）
│   ├── soft-error-content.html  # ソフトエラー（コンテンツ）
│   ├── meta-redirect.html       # Metaリダイレクト
│   ├── js-redirect-basic.html   # JS基本リダイレクト
│   └── js-redirect-delayed.html # JS遅延リダイレクト
└── edge-cases/                   # エッジケース（誤検知テスト）
    ├── soft-error-false-positive.html    # ソフトエラー誤検知テスト（メイン）
    ├── redirect-false-positive.html      # リダイレクト誤検知テスト（メイン）
    ├── normal-page-error-keyword.html    # 正常ページ（タイトルに「エラー」）
    ├── normal-page-404-keyword.html      # 正常ページ（タイトルに「404」）
    ├── normal-page-forbidden-keyword.html # 正常ページ（タイトルに「Forbidden」）
    ├── normal-page-content-error.html    # 正常ページ（コンテンツにエラーキーワード）
    ├── normal-page-notfound-content.html # 正常ページ（「ページが見つかりません」）
    ├── normal-page-redirect-content.html # 正常ページ（「自動的にジャンプ」）
    ├── normal-page-code-sample.html      # 正常ページ（コードサンプル内にエラーコード）
    ├── normal-page-config-sample.html    # 正常ページ（設定ファイルサンプル）
    ├── page-with-function-redirect.html  # 関数定義内のlocation操作
    ├── page-with-postback.html           # ASP.NET __doPostBack関数
    ├── page-with-onclick-redirect.html   # onclick属性内のlocation
    ├── page-with-addeventlistener.html   # addEventListener内のlocation
    ├── page-with-commented-redirect.html # コメント内のlocation
    └── page-with-string-redirect.html    # 文字列リテラル内のlocation
```

## 🚀 使い方

1. **テストダッシュボードを開く**
   - `index.html` をブラウザで開きます

2. **テストしたいカテゴリを選択**
   - ダッシュボードから目的のテストページへ移動

3. **拡張機能を起動**
   - ブラウザの拡張機能アイコンをクリック

4. **リンクチェックを実行**
   - 「Check Links」ボタンをクリック

5. **結果を確認**
   - 期待される結果と実際の結果を比較

## 📋 テストカテゴリ

### ⚓ アンカーリンク（4ページ）

同一ページおよび別ページへのアンカーリンクの検証

| ページ | 検証項目 | 期待される動作 |
|--------|---------|--------------|
| same-page-anchors.html | 同一ページ内アンカー | content.jsで処理、正常/エラーの検出 |
| cross-page-anchors.html | 別ページへのアンカー | background.jsで処理、アンカー存在確認 |
| encoded-anchors.html | エンコードされたアンカー | 日本語・特殊文字のデコード処理 |
| duplicate-ids.html | 重複ID | 重複ID警告の表示 |

**検証ポイント:**
- ページ内アンカーと別ページアンカーの処理の違い
- アンカーの存在/不在の正確な検出
- 日本語・特殊文字のエンコード/デコード
- 重複IDの警告表示

### 🔗 内部リンク（3ページ）

内部リンクの正常/エラー検証

| ページ | 検証項目 | 期待される動作 |
|--------|---------|--------------|
| valid-links.html | 正常なリンク | 200 OKの正常検出 |
| broken-links.html | 404エラー | 404エラーの正確な検出 |
| relative-absolute-paths.html | 相対/絶対パス | パスの正しい解決 |

**検証ポイント:**
- HTTPステータスコードの正確な取得
- 相対パスの正しい解決
- レスポンス時間の記録

### ⚙️ 特殊ケース（4ページ）

特殊な状況下でのリンクチェック

| ページ | 検証項目 | 期待される動作 |
|--------|---------|--------------|
| empty-hrefs.html | 空のhref | 表示/非表示による分類 |
| hidden-elements.html | 非表示要素 | 各種CSS非表示の検出 |
| special-protocols.html | 特殊プロトコル | mailto/tel/javascriptの処理 |
| redirects.html | リダイレクト | 各種リダイレクトの検出 |

**検証ポイント:**
- 空のhrefの「エラー」「保留」分類
- display:none、visibility:hidden等の検出
- 特殊プロトコルの適切な処理
- リダイレクトタイプの識別

### ⚠️ エラーページ（6ページ）

エラー検出機能の検証

| ページ | 検証項目 | 期待される動作 |
|--------|---------|--------------|
| 404.html | 404ページ | 直接表示用 |
| soft-error-title.html | ソフトエラー（タイトル） | タイトルからエラー検出 |
| soft-error-content.html | ソフトエラー（コンテンツ） | コンテンツからエラー検出 |
| meta-redirect.html | Metaリダイレクト | meta refreshの検出 |
| js-redirect-basic.html | JS基本リダイレクト | JavaScriptリダイレクト検出 |
| js-redirect-delayed.html | JS遅延リダイレクト | 遅延時間の解析 |

**検証ポイント:**
- ソフトエラーの検出精度
- リダイレクトタイプの識別
- 遅延時間の解析
- エラー理由の表示

### 🔍 エッジケース - 誤検知テスト（16ページ）

検出ロジックの**誤検知（False Positive）**を検証するテストページ群です。
これらのページは全て「正常」として検出されるべきです。

#### ソフトエラー誤検知テスト（9ページ）

エラーキーワードを含むが、実際はエラーページではない正常なページの検証

| ページ | 内容 | 誤検知リスク |
|--------|------|-------------|
| soft-error-false-positive.html | テストメインページ | - |
| normal-page-error-keyword.html | タイトルに「エラーハンドリング入門」 | `/エラー/` パターン |
| normal-page-404-keyword.html | タイトルに「404エラーの原因と対策」 | `/404/` パターン |
| normal-page-forbidden-keyword.html | タイトルに「Forbidden Fruit Recipe」 | `/forbidden/i` パターン |
| normal-page-content-error.html | コンテンツに「アクセス権限がありません」 | コンテンツ検出パターン |
| normal-page-notfound-content.html | コンテンツに「ページが見つかりません」 | コンテンツ検出パターン |
| normal-page-redirect-content.html | コンテンツに「自動的にジャンプ」 | リダイレクト検出パターン |
| normal-page-code-sample.html | コードサンプル内に403/404等 | コード内エラーコード |
| normal-page-config-sample.html | 設定ファイルにErrorDocument等 | 設定内エラー設定 |

**検証ポイント:**
- エラーキーワードが**文脈上正当**な場合は検出しないこと
- チュートリアル・ドキュメント系ページの誤検知防止
- コードサンプル・設定例の誤検知防止

#### リダイレクト誤検知テスト（7ページ）

`location.href`等のリダイレクトコードを含むが、実際には自動リダイレクトしないページの検証

| ページ | 内容 | 検出除外の仕組み |
|--------|------|-----------------|
| redirect-false-positive.html | テストメインページ | - |
| page-with-function-redirect.html | `function doRedirect() { location.href = '...' }` | 関数定義内は除外 |
| page-with-postback.html | ASP.NET `__doPostBack` 関数 | 標準関数パターン除外 |
| page-with-onclick-redirect.html | `onclick="location.href='...'"` | イベント属性内は除外 |
| page-with-addeventlistener.html | `addEventListener('click', () => { location.href })` | イベントリスナー内は除外 |
| page-with-commented-redirect.html | `// location.href = '...'` | コメント内は除外（要確認） |
| page-with-string-redirect.html | `const s = 'location.href = "..."';` | 文字列内は除外（要確認） |

**検証ポイント:**
- **関数定義内**のリダイレクトコードは検出しないこと
- **イベントハンドラ内**のコードは検出しないこと（ユーザーアクション必要）
- **コメント内**のコードは検出しないこと
- **文字列リテラル内**のコードは検出しないこと
- ASP.NET WebFormsの`__doPostBack`等、標準パターンを除外すること

**注意:** コメント・文字列の除外は現在の実装で未対応の可能性あり。テスト結果により改善要否を判断。

## 🎯 検証項目一覧

### リンクチェック機能
- [x] 同一ページ内アンカーの検出
- [x] 別ページアンカーの検出
- [x] アンカーの存在/不在確認
- [x] エンコードされたアンカーのデコード
- [x] 重複IDの警告
- [x] 正常なリンク（200 OK）の検出
- [x] 404エラーの検出
- [x] 相対パスの解決
- [x] 空のhrefの検出（表示/非表示分類）
- [x] 非表示要素の検出（display:none等）
- [x] 特殊プロトコルの処理

### エラー検出機能
- [x] ソフトエラー（タイトルベース）の検出
- [x] ソフトエラー（コンテンツベース）の検出
- [x] Metaリダイレクトの検出
- [x] JavaScriptリダイレクトの検出
- [x] JavaScript遅延リダイレクトの検出
- [x] リダイレクト先URLの解析
- [x] 遅延時間の解析

### 誤検知防止（False Positive Prevention）
- [ ] タイトル内エラーキーワードの文脈判断
- [ ] コンテンツ内エラーキーワードの文脈判断
- [ ] コードサンプル内のエラーコード除外
- [ ] 設定ファイルサンプル内のエラー設定除外
- [x] 関数定義内のリダイレクトコード除外
- [x] ASP.NET __doPostBack等の標準パターン除外
- [ ] onclick属性内のリダイレクトコード除外
- [ ] addEventListener内のリダイレクトコード除外
- [ ] コメント内のリダイレクトコード除外
- [ ] 文字列リテラル内のリダイレクトコード除外

### UI/UX機能
- [x] エラー番号の表示
- [x] ハイライト機能（個別・一括）
- [x] ジャンプ機能
- [x] フィルター機能
- [x] 統計情報の表示
- [x] CSVエクスポート
- [x] 詳細情報の表示

## 📊 統計

- **カテゴリ数**: 5
- **テストページ数**: 35
- **検証項目数**: 70+

## 🔄 今後の拡張

新しいリンクチェック機能を追加した際は、対応するテストページをこのフォルダに追加してください。

### 推奨フォルダ構成（拡張時）

```
Page-Check-Test-Web/
├── external-links/        # 外部リンクテスト（将来）
├── performance/           # パフォーマンステスト（将来）
└── regression/            # 回帰テスト（将来）
```

## 💡 テストのヒント

### 効率的なテスト方法

1. **カテゴリ別テスト**
   - 機能追加時は関連カテゴリのページのみテスト

2. **フィルター活用**
   - 各フィルター（エラー、成功、保留など）が正しく動作するか確認

3. **統計情報確認**
   - 検出数が期待値と一致するか確認

4. **詳細情報確認**
   - エラー理由、非表示理由などの詳細が正しく表示されるか確認

### デバッグ時の確認ポイント

- ブラウザのコンソールでエラーが出ていないか
- ネットワークタブでリクエストが正しく送信されているか
- 拡張機能のバックグラウンドページでエラーログを確認

## 📝 変更履歴

### v2.1 (2026-01-23)
- エッジケース（誤検知テスト）カテゴリを追加
- ソフトエラー誤検知テスト: 9ページ追加
- リダイレクト誤検知テスト: 7ページ追加
- 検証項目を70+に拡充

### v2.0 (2025-01-XX)
- 初版リリース
- 4カテゴリ、19テストページを作成
- 50以上の検証項目をカバー

## 🤝 貢献

新しいテストケースの追加や改善案がある場合は、以下の手順でお願いします：

1. 適切なカテゴリフォルダを選択（または新規作成）
2. テストページを作成
3. index.htmlにリンクを追加
4. このREADME.mdを更新

## 📄 ライセンス

このテストページ集は拡張機能のテスト目的で作成されています。

---

**作成日**: 2025-01-XX
**最終更新**: 2025-01-XX
**対象拡張機能**: CC Link Status Interval Checker v2.0+
