# YOUTUBE LIVE CHATBOT SPECIFICATION

## OVERVIEW

本プロジェクトは、Google Colab上で動作するYouTubeライブチャットボットのプロトタイプです。以下を統合しています：

- YouTubeライブチャットのリアルタイム取得
- OpenAI GPT-3.5による自動応答生成
- VoiceVox Coreを用いた日本語音声合成（TTS）
- DeepL APIによる日本語→英語翻訳
- OpenAI Whisperモデルによる音声認識
- インタラクティブUI（おしゃべり／配信モード切替）

## PURPOSE

- 視聴者とのインタラクション強化
- ボイスチャット形式での配信体験向上

## FUNCTIONAL REQUIREMENTS

- **LIVE CHAT RETRIEVAL**
  - `pytchat`を利用し、指定動画IDのチャットを非同期取得
- **AI RESPONSE GENERATION**
  - OpenAI GPT-3.5 APIで自然な応答を生成
- **TEXT-TO-SPEECH (TTS)**
  - VoiceVox Coreで応答をWAV形式に変換・再生
  - GPU利用時はONNX Runtime GPU版、失敗時はCPUフォールバック
- **TRANSLATION**
  - DeepL APIで日本語応答を英語へ自動翻訳
- **SPEECH-TO-TEXT**
  - ブラウザ録音データをWhisperモデルでテキスト化
- **INTERACTIVE UI**
  - Colabノートブック上に録音・実行ボタンとHTML表示領域を設置
  - 「おしゃべりモード」と「配信モード」を切り替え可能

## NON-FUNCTIONAL REQUIREMENTS

- Python 3.7以上
- Google Colab環境（GPUランタイム推奨）
- APIキー管理：環境変数またはColabユーザーデータで設定
- ネットワーク接続必須（YouTube API、OpenAI、DeepL等）

## REPOSITORY STRUCTURE

```text
/repository
├─ chatbot.ipynb       # メインノートブック
├─ character.txt       # システムプロンプト定義
├─ README.md           # 本仕様書（Markdown）
└─ .gitignore          # 除外設定
```

## SETUP

1. リポジトリをクローン
   ```bash
   ```

git clone \<REPO\_URL> cd \<REPO\_NAME>

````
2. VoiceVox Core取得＆配置
   ```bash
git clone https://github.com/VOICEVOX/voicevox_core -b 0.13.2
cd voicevox_core/
# ONNX Runtimeやコアバイナリ、OpenJTalk辞書をダウンロード・配置
````

3. 依存ライブラリのインストール
   ```bash
   ```

pip install -r requirements.txt

```
4. ColabでDriveマウント & APIキー設定
   - Colab「ユーザーデータ設定」に `OPENAI_API_KEY`, `DEEPL_API_KEY` を登録
   - Driveをマウントし、`character.txt` のパスを指定

## USAGE
### - CHAT MODE
1. `chat_mode` セルを実行
2. 録音ボタンで音声入力→AI応答→TTS再生を対話形式で実行

### - STREAM MODE
1. `stream_mode` セルで `video_id` と `important_words` を設定
2. ライブチャット監視＆キーワードに応じたAI応答を自動実行

## LICENSE
MIT License

```
