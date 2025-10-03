# Bedisynk - Minecraft Bedrock Edition Discord連携アドオン

Minecraft Bedrock EditionサーバーとDiscordを連携させる高度なアドオンです。BAN管理機能、レート制限対策、安定した通信を実現します。

## 🚀 機能

### 主要機能
- **リアルタイムチャット連携**: MinecraftとDiscord間の双方向チャット
- **プレイヤー参加/退出通知**: 詳細なデバイス情報付きで通知
- **BAN管理システム**: DiscordからサーバーのBAN管理が可能
- **レート制限対策**: エクスポネンシャルバックオフによる安定したAPI通信
- **マルチプラットフォーム対応**: 各種デバイス・入力方式の自動検出

### BAN管理コマンド
- `!ban <プレイヤー名> [理由]` - プレイヤーをBAN
- `!unban <プレイヤー名>` - BANを解除
- `!banlist` - BANリストを表示
- `!help` - ヘルプを表示

## ⚙️ セットアップ

### 前提条件
- Minecraft Bedrock Edition サーバー
- Discord サーバー管理権限
- Bot トークン

### インストール手順

1. **Discord Botの作成**
   - [Discord Developer Portal](https://discord.com/developers/applications)で新しいアプリケーションを作成
   - Botを作成し、トークンを取得
   - 以下の権限を付与:
     - `Send Messages`
     - `Read Message History`
     - `Embed Links`
     - `Use Slash Commands`

2. **チャンネル設定**
   - メイン通知用チャンネルを作成（IDを取得）
   - チャット連携用チャンネルを作成（IDを取得）
   - 管理者用チャンネルを作成（IDを取得）

3. **アドオン設定**
   ```javascript
   // 設定値を実際の値に置き換え
   const channelID = "メイン通知チャンネルID";
   const chatChannelID = "チャット連携チャンネルID";
   const adminChannelID = "管理者チャンネルID";
   const botToken = "Botトークン";
   ```

4. **サーバーへの導入**
   - `mcbe.js`をサーバーのbehavior_packsフォルダに配置
   - サーバーを再起動

## 🔧 設定

### チャンネル設定
| 変数名 | 説明 |
|--------|------|
| `channelID` | 参加/退出通知など基本通知用 |
| `chatChannelID` | Minecraft⇔Discordチャット連携用 |
| `adminChannelID` | BAN管理コマンド用 |

### レート制限設定
```javascript
const RATE_LIMIT_CONFIG = {
    maxRetries: 3,              // 最大リトライ回数
    baseDelay: 100,             // 基本遅延（5秒 = 100 ticks）
    maxDelay: 600,              // 最大遅延（30秒 = 600 ticks）
    consecutiveErrorThreshold: 5, // 連続エラー閾値
    backoffMultiplier: 2        // 遅延倍率
};
```

## 🎮 使用方法

### 自動機能
- **プレイヤー参加**: 自動検知され、デバイス情報付きで通知
- **チャット連携**: 両方向でメッセージが同期
- **BANチェック**: 参加時に自動的にBANリストを確認

### 管理者コマンド例
```
!ban Steve 不正行為
!unban Alex
!banlist
!help
```

## 🛡️ エラー処理

### レート制限対策
- エクスポネンシャルバックオフアルゴリズム採用
- 429/503エラー時の自動リトライ
- 連続エラー時の一時停止機能

### フォールバック機能
- プレイヤー状態の追跡とリトライ
- JSONレスポンスの妥当性チェック
- ネットワークエラー時の回復処理

## 🔍 トラブルシューティング

### よくある問題

1. **Botがメッセージを送信しない**
   - チャンネル権限を確認
   - Botトークンが正しいか確認
   - チャンネルIDが正しいか確認

2. **BANコマンドが動作しない**
   - 管理者チャンネルで実行しているか確認
   - Botに管理者権限があるか確認

3. **接続エラーが頻発する**
   - サーバーのインターネット接続を確認
   - レート制限設定を調整

### ログ確認
コンソールで以下のプレフィックスを検索:
- `【Bedisynk】` - システムメッセージ
- `レート制限エラー` - API制限関連
- `HTTP エラー` - 通信エラー

## 📊 パフォーマンス

### 最適化機能
- メッセージIDの追跡による重複防止
- 動的プロパティによるデータ永続化
- 効率的なプレイヤー状態管理
- メモリ使用量の最適化

### 推奨環境
- Minecraft Bedrock Edition 1.21+
- 安定したインターネット接続
- 十分なメモリ容量

## 🆘 サポート

問題が発生した場合:
1. コンソールのエラーメッセージを確認
2. Discordの権限設定を再確認
3. 設定値が正しいか確認
4. サーバーログを確認
