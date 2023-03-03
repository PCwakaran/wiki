# Stable Diffusionを始める

すべて自己責任で作業すること。
執筆時時点での動作確認は取っているが、
今後の更新で不適切なコードに差し変わったり、
動かなくなったりする可能性がある。

Stable Diffusionを自前環境で実行する。

## インストール

最低限おすすめの拡張機能を含めたインストールスクリプトを提示する。
筆者おすすめのインストールスクリプトは[ここ]((https://gist.github.com/mkaraki/685d8c4e34ce59df5ddaeb95aeaa6e1b))から最新のものを見れる。

```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git stable-diffusion-webui --depth 1
git clone https://github.com/DominikDoom/a1111-sd-webui-tagcomplete.git stable-diffusion-webui/extensions/tag-autocomplete --depth 1
git clone https://github.com/toriato/stable-diffusion-webui-daam.git stable-diffusion-webui/extensions/daam --depth 1
```

### 設定

Windowsの場合のみ記述する。

#### GTX 10xx 以上を利用している場合

`webui-user.bat`の`set COMMANDLINE_ARGS`を下記のように編集する。

```
set COMMANDLINE_ARGS=--xformers
```

### モデルのインストール

[このWiki (外部)](https://wikiwiki.jp/sd_toshiaki/%E3%83%A2%E3%83%87%E3%83%AB%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)に詳しく書いてある。
筆者は[BloodOrangeMix](https://huggingface.co/WarriorMama777/OrangeMixs/blob/main/Models/BloodOrangeMix/BloodOrangeMix.safetensors)を利用している。

ファイルをダウンロードし、`models/Stable-diffusion`に入れる。

### VAEのインストール

上記と同じページを参考にするよとい。
筆者は[vae-ft-ema-560000-ema](https://huggingface.co/stabilityai/sd-vae-ft-ema-original/blob/main/vae-ft-ema-560000-ema-pruned.safetensors)を利用している。

ファイルをダウンロードし、`models/VAE`に入れる。

## 起動する

`webui-user.bat`を起動する。

### おすすめ設定

#### Saving to a directory

##### Directory name pattern

ファイル出力先をモデルごとに変更してくれる

```
[model_name]/[date]
```

## 筆者リスト

- mkaraki