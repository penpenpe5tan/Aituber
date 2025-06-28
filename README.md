# YOUTUBE LIVE CHATBOT SPECIFICATION

## OVERVIEW

本プロジェクトは、Google Colab上で動作するYouTubeライブチャットボットのプロトタイプです。以下を統合しています：

- YouTubeライブチャットのリアルタイム取得（pytchat）
- OpenAI GPT-3.5 APIによる自動応答生成
- VoiceVox Coreを用いた日本語音声合成（TTS）
- DeepL APIによる日本語→英語翻訳
- OpenAI Whisperモデルによる音声認識
- インタラクティブUI（おしゃべりモード／配信モード切替）

## PURPOSE

- 視聴者とのインタラクション強化
- ボイスチャット形式での配信体験向上

## FUNCTIONAL REQUIREMENTS

- **LIVE CHAT RETRIEVAL**\
  `pytchat`を利用し、指定動画IDのチャットを非同期取得

- **AI RESPONSE GENERATION**\
  OpenAI GPT-3.5 APIで自然な応答を生成

- **TEXT-TO-SPEECH (TTS)**\
  VoiceVox Coreで応答をWAV形式に変換・再生\
  GPU利用時はONNX Runtime GPU版、失敗時はCPUフォールバック

- **TRANSLATION**\
  DeepL APIで日本語応答を英語へ自動翻訳

- **SPEECH-TO-TEXT**\
  ブラウザ録音データをWhisperモデルでテキスト化

- **INTERACTIVE UI**\
  Colabノートブック上に録音・実行ボタンとHTML表示領域を設置\
  「おしゃべりモード」と「配信モード」を切り替え可能

## NON-FUNCTIONAL REQUIREMENTS

- Python 3.7以上
- Google Colab環境（GPUランタイム推奨）
- ネットワーク接続必須（YouTube API、OpenAI、DeepL等）

## SETUP

1. **Google Driveのマウント**\
   Colab上でDriveをマウントし、下記パスにファイルを配置してください：\
   `/content/drive/My Drive/AItuber/character.txt`\
   （`character.txt` はシステムプロンプトを記述したテキストファイルです）

2. **APIキーの設定**\
   Colabの「ユーザーデータ設定」または環境変数で以下を登録：

   - `OPENAI_API_KEY`
   - `DEEPL_API_KEY`

3. **依存パッケージのインストール**\
   ノートブックの先頭セルで以下を実行して必要なライブラリを導入：

   ```bash
   !pip install aiohttp pytchat numpy sounddevice nest_asyncio openai cohere tiktoken
   ```

> **Note:** 本ノートブックは2023年時点のOpenAI／DeepL API仕様を前提としています。仕様変更があった場合は各公式ドキュメントをご確認ください。

## USAGE

### CHAT MODE

1. Colabノートブックの「おしゃべりモード」セルを実行
2. 録音ボタンで音声入力→AI応答→TTS再生を対話形式で実行

### STREAM MODE

1. 「配信モード」セルで `video_id` と `important_words` を設定
2. ライブチャットを監視し、キーワードに応じたAI応答を自動実行

## LICENSE

MIT License

