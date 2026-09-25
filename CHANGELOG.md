# ChangeLog

## [Unreleased]
### Changed
- Unity 6000.6 対応
  - インスタンスIDを保持している箇所の型を `#if UNITY_6000_3_OR_NEWER` で `EntityId` / `int` に切り替えるようにし、非推奨APIの使用を全廃
    - 6000.6 では `GetInstanceID()` / `InstanceIDToObject(int)` / `GetAssetPath(int)` が警告 (CS0618) ではなくエラー (CS0619) になるため、`#pragma warning disable` では回避できない
  - `GetLastFolderInstanceIds` を `GetFolderInstanceIDs` 経由の実装に戻した
    - 戻り値の要素型がバージョンに応じて `EntityId` / `int` になり、型エイリアスと一致するため分岐が不要
  - `SetFolderSelection` のオーバーロード検索を「引数が最も少ないもの」に変更
    - 6000.3 で引数2つのオーバーロードが無くなり、従来の検索条件では `null` になって `NullReferenceException` が発生していた
  - `#pragma warning disable CS0618` を削除

## [1.1.0] - 2026-03-28
### Changed
- Unity 6000.3 互換性対応
  - `InstanceIDToObject(int)`、`GetAssetPath(int)` の CS0618 deprecation 警告を `#pragma warning disable` で抑制
  - `GetFolderInstanceIDs` を `m_LastFolders` パスベースの実装に書き換え（6000.3 で `EntityId[]` を返すため）
  - `SetSearch` 内の `GetAssetPath` を `InstanceIDToObject` 経由に変更
  - `SetFolderSelection` に `UNITY_6000_3_OR_NEWER` 条件分岐を追加（`EntityId` 経由での選択）

## [1.0.0] - 2023-12-02
### first release
