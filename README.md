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

| まとまり | 自動マージ | 中身 |
| --- | --- | --- |
| `all dependencies` | する | メジャー以外の全部。小さくて頻繁で、タグを戻せば済む |
| `major dependencies` | **しない** | メジャー。とくにデータベースはタグを差し替えるだけでは上がらない(PostgreSQL は別メジャーが書いたデータディレクトリでは起動を拒否する) |
| `helm charts` | **しない** | Helm の chart。更新の種類を問わない |

ほかに `reviewers: ["5ym"]` で PR のレビュワーを指定します。

### なぜ chart は種類を問わず外すのか

**chart の版は中身の大きさを表しません。** erpnext は `8.0.15` → `8.0.78` という「パッチ」で
キャッシュとキューを Dragonfly から Valkey に入れ替え、values に書いてあったメモリ上限を
丸ごと無効にしました(danything/gitops#25)。メジャーを分けるだけでは止まりません。

グループを分けてあるのは、chart を止めることで `all dependencies` の PR まで
自動マージされなくなるのを避けるためです。

`platformAutomerge` を使うため、対象リポジトリ側で **Settings → General → Allow auto-merge** を有効にしておく必要があります。
