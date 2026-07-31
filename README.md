# renovate-config

共有 Renovate プリセット。

## 使い方

各リポジトリの `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>5ym/renovate-config"]
}
```

## 設定内容

| 設定 | 効果 |
| --- | --- |
| `matchPackageNames: ["*"]` + `groupName` | 全依存の更新を1つのPRにまとめる |
| `separateMajorMinor: false` | メジャー更新も同じPRに含める |
| `automerge: true` / `platformAutomerge: true` | GitHub の auto-merge でマージする |
| `reviewers: ["5ym"]` | PR のレビュワーに `5ym` を指定する |

`platformAutomerge` を使うため、対象リポジトリ側で **Settings → General → Allow auto-merge** を有効にしておく必要があります。
