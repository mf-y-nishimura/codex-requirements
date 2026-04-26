# codex-requirements

Codex の `requirements.toml` を公開配布するためのリポジトリです。

この設定は、破壊的なコマンドの一部を禁止する最小構成です。

## 含まれる制約

- `rm -rf` 系の再帰削除を禁止
- `git reset --hard` を禁止
- `git checkout --` を禁止
- `git clean -fd` / `-fdx` 系を禁止

## 取得

```bash
curl -fsSL -o /tmp/requirements.toml https://raw.githubusercontent.com/mf-y-nishimura/codex-requirements/main/requirements.toml
```

## 配置

```bash
sudo mkdir -p /etc/codex
sudo install -m 644 /tmp/requirements.toml /etc/codex/requirements.toml
```

Codex を再起動すると反映されます。

## 注意

- `main` 直参照ではなく、必要ならコミット SHA を固定して取得してください。
- 実運用前に、自分の環境で禁止対象が過不足ないか確認してください。
