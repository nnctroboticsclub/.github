# 共通設定の運用

## GitHub への反映

1. このリポジトリに作業用ブランチを作り、必要なファイルを編集します。
2. 差分、Markdown のリンク、Issue フォームの YAML を確認します。
3. コミット・push し、PR で変更を確認してから既定ブランチへ統合します。
4. 個別テンプレートのない対象リポジトリで、Issue・PR の作成画面を確認します。
   確認のために実際の Issue・PR を投稿する必要はありません。

既定ブランチへ反映した共通ファイルは、公開範囲にかかわらず、組織内で独自の
対応ファイルを持たないリポジトリの既定値になります。
個別リポジトリの Git 履歴や clone に共通ファイルが追加されるわけではありません。

## 部員向けリポジトリとの分担

公開プロフィールはこのリポジトリの `profile/README.md`、メンバー向けプロフィールは
Private の `.github-private` リポジトリの `profile/README.md` で管理します。
メンバー向けプロフィールは、組織 Overview の `View as: Member` で確認します。
プロフィールを表示できても、リンク先の権限が追加されるわけではありません。

`.github-private` の内部ガイド・Issue・PR テンプレートは、他のリポジトリへ
自動継承されません。内部用として必要なプロジェクトへコピー・統合します。
一方、この公開リポジトリの共通テンプレートは非公開リポジトリにも継承されるため、
公開・非公開のどちらでも使える内容に保ちます。

## 個別リポジトリで上書きする場合

- 貢献ガイド: 対象リポジトリに `CONTRIBUTING.md` を追加します。
- PR: 対象リポジトリに `.github/PULL_REQUEST_TEMPLATE.md` を追加します。
- Issue: 対象リポジトリの `.github/ISSUE_TEMPLATE/` に必要なフォームと設定を配置します。

Issue の個別テンプレートや設定が有効な場合は、共通フォルダーの内容は利用されません。
共通フォームも併用したい場合は、必要なフォームを対象リポジトリへ明示的に配置します。

継承された文書・テンプレートからのリンクは、参照先リポジトリを取り違えないよう、
`https://github.com/nnctroboticsclub/.github/...` などの絶対 URL を使用してください。
フォームには既定のラベル・担当者・Project を指定していません。
指定する場合は、対象となる全リポジトリでその値を利用できることを確認します。

## Nbed 配布設定を更新する場合

`templates/nbed/` は導入用スナップショットです。配置しただけでは既存プロジェクトも、
既存の GitHub テンプレートリポジトリも更新されません。
共有元・Nbed プロジェクトテンプレート・ライブラリテンプレートと差分を比較し、
必要な変更をそれぞれへ反映します。

- clangd・clang-format の設定は対応するツールのバージョンと一緒に確認する。
- JSONC、YAML、Python の構文と、VS Code タスクの参照関係を確認する。
- `clean.py` を変更する場合は一時プロジェクトで検証し、ルートの生成物だけが対象になることを確認する。
- `platformio.ini` はボードとバージョンを固定した設定例。全プロジェクトへ一律に上書きしない。
- `compiledb.py` の配置先・登録と、生成DBの参照先が一致していることを確認する。
- 個人用プロファイル、ユーザーパス、接続情報、生成済みDB・ビルド結果を混入させない。
- 配布物に添付した既存のライセンス・著作権表示を保持する。

サンプルのビルド成功と実機確認の有無は、区別して記録します。
確認していない動作や、配布元で行われた過去の検証を、今回の検証として記載しないでください。

## 自動適用されないファイル

`LICENSE`、`CODEOWNERS`、`AGENTS.md`、VS Code・clangd の設定、`.gitignore`、
GitHub Actions ワークフローは各プロジェクトで管理します。
CI の共通処理には再利用可能なワークフローを別途用意し、各リポジトリから呼び出します。
セキュリティ報告先や行動規範を追加する場合は、実際の窓口・対応体制を確認してから公開します。

## 今後追加できる機能

`workflow-templates/` にワークフローとメタデータを配置すると、組織用の Actions の
開始用ひな形を用意できます。各プロジェクトが選択して導入する仕組みで、自動実行ではありません。
CI の処理を共通化する場合は再利用可能ワークフローを用意し、利用先から明示的に呼びます。
導入前にビルド手順・依存物への権限・必要な Secrets を確認してください。

Owner は組織プロフィールに公開向け・メンバー向けそれぞれ最大6件のリポジトリを
ピン留めできます。頻繁に使う入口を整理する用途に利用できます。

## 参考

- [既定のコミュニティファイル](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [Issue フォームの構文](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [PR テンプレート](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
- [公開・メンバー向けプロフィールとピン留め](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile)
- [ワークフローテンプレート](https://docs.github.com/en/actions/how-tos/reuse-automations/create-workflow-templates)
- [再利用可能ワークフロー](https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows)
