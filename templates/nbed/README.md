# nbed / PlatformIO の共有設定

部活の共有設定を既存プロジェクトへ導入するための設定一式です。
2026-10-23 に確認した共有元と `nbed-project-template` の設定を基にしています。
ファームウェアのソースコードや HAL の設定は含みません。

新規プロジェクトは [アプリケーション用テンプレート](https://github.com/nnctroboticsclub/nbed-project-template)
または [ライブラリ用テンプレート](https://github.com/nnctroboticsclub/nbed-library-template)
から作成してください。
この2つのテンプレートは組織メンバー向けの非公開リポジトリで、アクセス権限が必要です。

## ファイルの役割

| ファイル | 用途 |
| --- | --- |
| `.clang-format` | C/C++ の整形。Google 基準・2 スペース・80文字幅 |
| `.clangd` | 補完・診断・命名、組み込み向け例外 |
| `.vscode/settings.json` | 自動保存・整形・補完・ルート限定の検索と監視の除外 |
| `.vscode/tasks.json` | ビルド・書き込み・DB生成・クリーン・全削除・完全再ビルド |
| `.vscode/extensions.json` | 推奨拡張。自動インストールは行わない |
| `.vscode/clean.py` | 固定した生成物のパスだけを削除 |
| `compiledb.py` | ビルド時・DB生成時にコンパイルDBを更新 |
| `.gitignore` | 生成物や PC 固有のデバッグ設定の除外例 |
| `platformio.ini` | NUCLEO-F446RE / nbed v0.6.0 の設定例 |
| `LICENSE` | この配布設定一式の既存の MIT ライセンス |

clangd / clang-format **23.1.0** を想定します。古いバージョンでは読み込めない
整形オプションが含まれます。実際の C/C++ 規格・CPU・include パスはコンパイルDBに従います。
`.clang-format` の `Standard` は整形時の構文判定用です。

## 既存プロジェクトへ統合する

最初に作業用ブランチを作り、既存の変更を確認してください。
このフォルダーを丸ごと上書きする方法は使わず、次の単位で差分を統合します。

1. `.clang-format` と `.clangd` を比較し、プロジェクトの規約に合わせて配置します。
   校正済みの共通設定を使う場合は、そのまま利用してください。
2. `.vscode/settings.json`・`tasks.json`・`extensions.json` を統合し、
   `.vscode/clean.py` を配置します。独自タスクやデバッグ設定は維持してください。
3. `compiledb.py` をプロジェクトルートに配置し、`platformio.ini` の利用する環境へ
   次の登録を追加します。既にコンパイルDB生成スクリプトがある場合は二重登録しません。

   ```ini
   extra_scripts =
     pre:compiledb.py
   ```

   `scripts/compiledb.py` に置く場合は登録も `pre:scripts/compiledb.py` に変更します。
   既存の `extra_scripts` に別のスクリプトがあれば、その行も保持します。
4. `.gitignore` の必要な規則を既存ファイルへ追加します。
   `/build/`・`/.cache/`・`/.pio/` はルート直下のみを除外します。
   `__pycache__/`・`*.pyc`・`*.tar.gz` は階層を問わない規則です。
   ソースとして追跡する同名ファイルがある場合は、プロジェクトに合わせて範囲を限定します。
5. `platformio.ini` の既存のボード・環境名・依存ライブラリ・追加スクリプトを保持し、
   `default_envs`、`build_dir = build`、`build_cache_dir = .cache` を確認します。
   添付の `platformio.ini` は設定例として参照してください。

この配布物には MIT ライセンスが付属します。コピーした設定一式のライセンス・
著作権表示は保持し、既存プロジェクト全体のライセンスを置き換えないでください。

## 利用する

プロジェクトのルートを VS Code で開き、PlatformIO と clangd 拡張を準備します。
タスクは標準の `${userHome}/.platformio/penv/` を使用し、Windows は `Scripts/`、
macOS/Linux は `bin/` を参照します。Core の保存先を変えている場合は、
プロジェクトのタスクと `clangd.arguments` を実際の配置に合わせてください。

- `Ctrl+Shift+B`: `platformio.ini` の `default_envs` をビルド
- 「nbed: clangd用ビルド情報を更新（既定環境）」: `compile_commands.json` を生成
- 「nbed: 完全再ビルド（既定環境）」: 生成物を削除した後に既定環境をビルド

コンパイルDBは利用する PC で再生成します。共有するソースへ固定のユーザーパスや
生成済みDBを追加しないでください。DB の変更は監視対象に残し、clangd が再起動します。
詳細は [.vscode/README.md](.vscode/README.md) を参照してください。

この設定だけではビルドできません。アプリケーションソース、依存物、対象ボードに応じた
HAL・クロックなどの設定が別途必要です。

## 更新

このフォルダーはスナップショットです。このリポジトリを更新しても導入先へは自動反映されません。
更新時は [運用ガイド](../../docs/maintenance.md) に従い、導入先の差分を確認してください。
