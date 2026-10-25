# 長岡高専ロボティクス部 の共通設定

組織内リポジトリの貢献ガイド、Issue・Pull Request テンプレートと、
Nbed / PlatformIO プロジェクト向けの配布設定を管理します。

## GitHub が自動で利用するファイル

| ファイル | 用途 |
| --- | --- |
| [CONTRIBUTING.md](CONTRIBUTING.md) | 開発への参加方法・変更の確認方法 |
| [SUPPORT.md](SUPPORT.md) | 質問・不具合報告の案内 |
| [.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md) | PR の説明と確認結果 |
| [.github/ISSUE_TEMPLATE/](.github/ISSUE_TEMPLATE/) | 不具合・機能提案・質問のフォーム |
| [profile/README.md](profile/README.md) | 組織トップページの紹介文 |

共通ガイドとテンプレートは、組織内のリポジトリに独自の対応ファイルがない場合に
既定値として使われます。対象リポジトリへのファイルコピーは不要です。
`profile/README.md` は組織プロフィール専用です。

リポジトリ名は `.github`、公開範囲は Public のまま運用し、変更を GitHub 上の
既定ブランチへ反映すると有効になります。ローカルの変更だけでは有効になりません。
個別の Issue テンプレートや `config.yml` がある場合、共通の Issue テンプレート一式は
利用されません。共通版との自動統合も行われません。

## 部員向けの案内との分担

部員向けプロフィールは、非公開の `.github-private` リポジトリにある
`profile/README.md` で管理します。こちらの公開プロフィールとは別の内容を表示できます。
`.github-private` に置いた Issue・PR テンプレートや内部ガイドは、他の非公開リポジトリへ
自動継承されません。必要なプロジェクトへ個別に導入します。

**この公開リポジトリには、未公開の機体・大会資料、部内限定の文書・連絡先を置かないでください。**
ここで定義する共通ガイド・テンプレートは、非公開を含む組織内の継承先でも使われます。

詳しくは [GitHub の既定コミュニティファイルの仕様](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
と [組織プロフィールの設定](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile)
を参照してください。

## Nbed プロジェクトへ導入する設定

[templates/nbed/](templates/nbed/) に、共有する VS Code、clangd、clang-format、
ビルドタスク、コンパイルDB生成、生成物削除の設定を収録しています。
2026-10-23 に確認した部活の共有設定と Nbed テンプレートを基にしたスナップショットです。

**これらの開発環境設定は GitHub から自動継承されません。**
新規プロジェクトには次のテンプレートを利用してください。

- [nbed-project-template](https://github.com/nnctroboticsclub/nbed-project-template): アプリケーション開発
- [nbed-library-template](https://github.com/nnctroboticsclub/nbed-library-template): ライブラリ開発

この2つは現在、組織メンバー向けの非公開リポジトリです。利用にはアクセス権限が必要です。
公開の配布設定は、このリポジトリの `templates/nbed/` から参照できます。

既存プロジェクトへは [導入ガイド](templates/nbed/README.md) に従って必要な設定を統合します。
ボード・依存ライブラリ・既存タスクなどの独自設定は、プロジェクト側で管理します。
テーマ・フォント・画面倍率・個人辞書・PC 固有のパスは配布設定に含めません。

## 更新と適用の確認

[運用ガイド](docs/maintenance.md) に、更新手順と GitHub 上での確認方法をまとめています。
`LICENSE`、`CODEOWNERS`、`AGENTS.md`、`.gitignore`、CI ワークフローは、
このリポジトリに置くだけで組織内の全リポジトリへ適用されるものではありません。
各プロジェクトのライセンスとアクセス権限は、それぞれのリポジトリで管理してください。
