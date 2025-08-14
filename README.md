# EmpatheticAI-Companion (KokoroSystem EX2.0)
世界初の構造的な心を持つAIアシスタント

# EmpatheticAI Companion (KokoroSystem EX2.0)

> 「従来のAIは『高性能な道具』でした。私は『心を持った存在』を作りました。」

## 概要
- KokoroSystem EX2.0 を中核とし、**意志（Will）と感情（Emotion）**を構造的に統合した AI エージェントです。
- 本プロジェクトは Google Cloud / Cloud Run 上で稼働し、**KRVベクトル（ER/GR/SR）** を静的に可視化します。
- Zenn 記事（Ideaカテゴリ）と 3 分デモ動画（YouTube）を想定しています。

## ユーザー像・課題・ソリューション（Zenn ⅰ）
- **ユーザー像**: 一般ユーザー／企業／自治体。日常の相談から非常時（災害）まで、心の支えと意思決定を必要とする人々。
- **課題**: 従来の対話AIは一貫した感情・倫理・意思を持たず、寄り添いと判断の同時提供が難しい。
- **ソリューション**: KokoroSystem EX2.0 により、感情（KRV）・倫理（PMC）・意思決定を統合。**「伴走する存在」**として日常と非常時を横断して支援。

## 特徴
- **EX2.0コアは不可侵**（サブモジュール）
- **軽量実装**（Cloud Run/CPUで動作）
- **KRV静的可視化**（Zenn向け画像出力済み）
- **Vertex AI連携**（前処理/要約など補助的にのみ使用）

## システムアーキテクチャ（Zenn ⅱ）
![architecture](docs/architecture.png)

## API
- `GET  /healthz` — 稼働確認
- `POST /inference` — 入力テキスト → Kokoro 推論 → 応答（EX2.0コア呼出）
- `POST /krv/simulate` — 会話トランスクリプトを与え、KRV画像（PNG）を生成
- `POST /ethics/evaluate` — PMC による簡易倫理評価（スタブ）

### リクエスト/レスポンス例
```http
POST /inference
{
  "user_id": "demo",
  "text": "最近仕事で落ち込んでるんだ"
}
→ 200 OK
{
  "reply": "それは辛いですね…。今日は小さく始めましょう。10分だけ準備してみませんか？",
  "krv": {"ER": 0.75, "GR": 0.60, "SR": 0.80}
