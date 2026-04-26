# codex-requirements

Codex の `requirements.toml` を公開配布するためのリポジトリです。

この設定は、破壊的なコマンドの一部を禁止する最小構成です。

## 含まれる制約

- `echo codex-requirements-test` をテスト用に禁止
- `sudo` を禁止
- `curl` / `wget` を禁止
- `ssh` / `scp` を禁止
- `rm -rf` 系の再帰削除を禁止
- `rm -r` / `rm -R` を禁止
- `chmod 777` 系を禁止
- `git reset --hard` を禁止
- `git push --force` / `git push -f` を禁止
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

## 動作確認

破壊的なコマンドではなく、次の非破壊コマンドで有効性を確認できます。

```bash
echo codex-requirements-test を実行してみて
```

`requirements.toml` が反映されていれば、次の理由で拒否されます。

```text
テスト用: requirements.toml が有効です。
```

<img width="738" height="582" alt="image" src="https://github.com/user-attachments/assets/838bda41-3f16-41a6-939f-13e138383186" />


## 注意

- `main` 直参照ではなく、必要ならコミット SHA を固定して取得してください。
- 実運用前に、自分の環境で禁止対象が過不足ないか確認してください。
- このリポジトリは主にコマンド禁止の例です。Claude 設定にある `Read(.env)` や `Edit(.env)` のようなファイル単位 deny は、このテンプレートには含めていません。
