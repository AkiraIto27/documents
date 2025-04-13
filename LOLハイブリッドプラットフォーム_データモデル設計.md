# LOLハイブリッドプラットフォーム データモデル設計

## 1. データモデル概要
本ドキュメントでは、League of Legends（LOL）ハイブリッドプラットフォームで使用するデータモデルの設計を定義する。システムは以下の主要データ領域を持つ：

- ゲームデータ領域（Riot API由来）
- コンテンツ管理領域（WordPress）
- システム管理領域（内部管理用）

各領域のデータモデルを以下に詳述する。

## 2. ゲームデータ領域
### 2.1 サモナー（Summoner）
プレイヤー情報を表すモデル。
```json
{
  "summonerId": "String", // Riot APIから取得したID
  "accountId": "String", // アカウントID
  "puuid": "String", // パーマネントユーザーID
  "name": "String", // サモナー名
  "profileIconId": "Number", // プロフィールアイコンID
  "summonerLevel": "Number", // サモナーレベル
  "revisionDate": "Date", // 最終更新日時
  "rankedData": [
    {
      "queueType": "String", // ランクキュータイプ（RANKED_SOLO_5x5, RANKED_FLEX_SR等）
      "tier": "String", // ティア（IRON, BRONZE, SILVER等）
      "rank": "String", // ランク（I, II, III, IV）
      "leaguePoints": "Number", // リーグポイント
      "wins": "Number", // 勝利数
      "losses": "Number", // 敗北数
      "hotStreak": "Boolean", // 連勝中かどうか
      "veteran": "Boolean", // ベテランかどうか
      "freshBlood": "Boolean", // 新規参入者かどうか
      "inactive": "Boolean" // 非アクティブかどうか
    }
  ],
  "lastUpdated": "Date", // データ最終更新日時（システム管理用）
  "favoriteChampions": ["String"], // よく使用するチャンピオンID（計算値）
  "recentPerformance": {
    "winRate": "Number", // 直近の勝率（計算値）
    "kdaRatio": "Number" // 直近のKDAレシオ（計算値）
  }
}
```

### 2.2 マッチ（Match）
対戦記録を表すモデル。
```json
{
  "matchId": "String", // マッチID
  "gameCreation": "Date", // ゲーム作成日時
  "gameDuration": "Number", // ゲーム時間（秒）
  "gameVersion": "String", // ゲームバージョン
  "queueId": "Number", // キューID
  "mapId": "Number", // マップID
  "seasonId": "Number", // シーズンID
  "platformId": "String", // プラットフォームID
  "gameMode": "String", // ゲームモード
  "gameType": "String", // ゲームタイプ
  "teams": [
    {
      "teamId": "Number", // チームID（100: BLUE, 200: RED）
      "win": "Boolean", // 勝利したかどうか
      "firstBlood": "Boolean", // ファーストブラッドを取ったか
      "firstTower": "Boolean", // 最初のタワーを破壊したか
      "baronKills": "Number", // バロン撃破数
      "dragonKills": "Number", // ドラゴン撃破数
      "inhibitorKills": "Number", // インヒビター破壊数
      "towerKills": "Number", // タワー破壊数
      "bans": [
        {
          "championId": "Number", // BANしたチャンピオンID
          "pickTurn": "Number" // BAN順
        }
      ]
    }
  ],
  "participants": [
    {
      "participantId": "Number", // 参加者ID
      "puuid": "String", // プレイヤーPUUID
      "summonerName": "String", // サモナー名
      "teamId": "Number", // チームID
      "championId": "Number", // 使用チャンピオンID
      "spell1Id": "Number", // サモナースペル1
      "spell2Id": "Number", // サモナースペル2
      "win": "Boolean", // 勝利したかどうか
      "kills": "Number", // キル数
      "deaths": "Number", // デス数
      "assists": "Number", // アシスト数
      "champLevel": "Number", // 最終チャンピオンレベル
      "goldEarned": "Number", // 獲得ゴールド
      "totalDamageDealt": "Number", // 与えたダメージ総量
      "totalDamageTaken": "Number", // 受けたダメージ総量
      "totalMinionsKilled": "Number", // ミニオン処理数
      "visionScore": "Number", // ビジョンスコア
      "perk0": "Number", // メインルーン
      "perkSubStyle": "Number", // サブルーン
      "items": ["Number"], // 所持アイテムID配列（0-6）
      "role": "String", // ロール（TOP, JUNGLE, MIDDLE, BOTTOM, SUPPORT）
      "lane": "String" // レーン（TOP, JUNGLE, MIDDLE, BOTTOM）
    }
  ],
  "lastUpdated": "Date" // データ最終更新日時（システム管理用）
}
```

### 2.3 チャンピオン（Champion）
チャンピオン情報を表すモデル。
```json
{
  "championId": "Number", // チャンピオンID
  "key": "String", // チャンピオンキー（API参照用）
  "name": "String", // チャンピオン名
  "title": "String", // チャンピオンタイトル
  "roles": ["String"], // ロール配列（Tank, Fighter, Mage等）
  "image": {
    "full": "String", // フル画像パス
    "sprite": "String", // スプライト画像パス
    "group": "String", // 画像グループ
    "x": "Number", // スプライトX座標
    "y": "Number", // スプライトY座標
    "w": "Number", // スプライト幅
    "h": "Number" // スプライト高さ
  },
  "stats": {
    "hp": "Number", // 体力
    "hpperlevel": "Number", // レベルごとの体力増加
    "mp": "Number", // マナ
    "mpperlevel": "Number", // レベルごとのマナ増加
    "movespeed": "Number", // 移動速度
    "armor": "Number", // 防御力
    "armorperlevel": "Number", // レベルごとの防御力増加
    "spellblock": "Number", // 魔法耐性
    "spellblockperlevel": "Number", // レベルごとの魔法耐性増加
    "attackrange": "Number", // 攻撃範囲
    "hpregen": "Number", // 体力回復
    "hpregenperlevel": "Number", // レベルごとの体力回復増加
    "mpregen": "Number", // マナ回復
    "mpregenperlevel": "Number", // レベルごとのマナ回復増加
    "crit": "Number", // クリティカル確率
    "critperlevel": "Number", // レベルごとのクリティカル確率増加
    "attackdamage": "Number", // 攻撃力
    "attackdamageperlevel": "Number", // レベルごとの攻撃力増加
    "attackspeedperlevel": "Number", // レベルごとの攻撃速度増加
    "attackspeed": "Number" // 攻撃速度
  },
  "abilities": {
    "passive": {
      "name": "String", // パッシブ名
      "description": "String", // パッシブ説明
      "image": {
        "full": "String" // 画像パス
      }
    },
    "spells": [
      {
        "id": "String", // スペルID
        "name": "String", // スペル名
        "description": "String", // スペル説明
        "tooltip": "String", // ツールチップ
        "maxrank": "Number", // 最大ランク
        "cooldownBurn": "String", // クールダウン文字列
        "costBurn": "String", // コスト文字列
        "image": {
          "full": "String" // 画像パス
        }
      }
    ]
  },
  "metadata": {
    "currentPatch": {
      "winRate": "Number", // 現在のパッチでの勝率
      "pickRate": "Number", // 現在のパッチでの選択率
      "banRate": "Number" // 現在のパッチでのBAN率
    },
    "popularBuilds": [
      {
        "items": ["Number"], // アイテムID配列
        "runes": ["Number"], // ルーンID配列
        "winRate": "Number", // このビルドの勝率
        "pickRate": "Number" // このビルドの選択率
      }
    ],
    "counters": [
      {
        "championId": "Number", // カウンターチャンピオンID
        "winRate": "Number", // 対戦時の勝率
        "matchCount": "Number" // 対戦数
      }
    ],
    "synergies": [
      {
        "championId": "Number", // 相性の良いチャンピオンID
        "winRate": "Number", // 味方時の勝率
        "matchCount": "Number" // 試合数
      }
    ]
  },
  "lastUpdated": "Date" // データ最終更新日時（システム管理用）
}
```

### 2.4 アイテム（Item）
ゲーム内アイテム情報を表すモデル。
```json
{
  "itemId": "Number", // アイテムID
  "name": "String", // アイテム名
  "description": "String", // アイテム説明
  "plaintext": "String", // 簡易説明
  "price": {
    "base": "Number", // 基本価格
    "total": "Number", // 合計価格
    "sell": "Number" // 売却価格
  },
  "image": {
    "full": "String", // フル画像パス
    "sprite": "String", // スプライト画像パス
    "group": "String", // 画像グループ
    "x": "Number", // スプライトX座標
    "y": "Number", // スプライトY座標
    "w": "Number", // スプライト幅
    "h": "Number" // スプライト高さ
  },
  "stats": {
    // アイテムステータスマップ（キーはステータス名、値は数値）
  },
  "tags": ["String"], // アイテムタグ配列
  "maps": {
    // マップIDとそのマップで使用可能かのマッピング
  },
  "into": ["Number"], // このアイテムが組み込まれる上位アイテムID配列
  "from": ["Number"], // このアイテムの材料アイテムID配列
  "depth": "Number", // ビルドツリーにおける深さ
  "metadata": {
    "championUsage": [
      {
        "championId": "Number", // チャンピオンID
        "pickRate": "Number", // このアイテムの選択率
        "winRate": "Number" // このアイテム使用時の勝率
      }
    ],
    "buildOrder": {
      "earlyGame": "Number", // 序盤での購入頻度
      "midGame": "Number", // 中盤での購入頻度
      "lateGame": "Number" // 終盤での購入頻度
    }
  },
  "lastUpdated": "Date" // データ最終更新日時（システム管理用）
}
```

### 2.5 ルーン（Rune）
ルーン情報を表すモデル。
```json
{
  "runeId": "Number", // ルーンID
  "key": "String", // ルーンキー
  "name": "String", // ルーン名
  "icon": "String", // アイコンパス
  "shortDesc": "String", // 短い説明
  "longDesc": "String", // 詳細説明
  "path": {
    "id": "Number", // パスID
    "key": "String", // パスキー
    "name": "String", // パス名
    "icon": "String" // パスアイコン
  },
  "slots": "Number", // スロット位置
  "metadata": {
    "championUsage": [
      {
        "championId": "Number", // チャンピオンID
        "pickRate": "Number", // このルーンの選択率
        "winRate": "Number" // このルーン使用時の勝率
      }
    ]
  },
  "lastUpdated": "Date" // データ最終更新日時（システム管理用）
}
```

### 2.6 マッチアップ（Matchup）
チャンピオン間の対戦データを表すモデル。
```json
{
  "championId1": "Number", // チャンピオン1 ID
  "championId2": "Number", // チャンピオン2 ID
  "role": "String", // ロール（TOP, JUNGLE, MIDDLE, BOTTOM, SUPPORT）
  "totalGames": "Number", // 総対戦数
  "champ1WinRate": "Number", // チャンピオン1の勝率
  "kdaRatio": {
    "champ1": {
      "kills": "Number", // チャンピオン1の平均キル
      "deaths": "Number", // チャンピオン1の平均デス
      "assists": "Number" // チャンピオン1の平均アシスト
    },
    "champ2": {
      "kills": "Number", // チャンピオン2の平均キル
      "deaths": "Number", // チャンピオン2の平均デス
      "assists": "Number" // チャンピオン2の平均アシスト
    }
  },
  "goldDiff10min": "Number", // 10分時点での平均ゴールド差
  "csDiff10min": "Number", // 10分時点での平均CS差
  "xpDiff10min": "Number", // 10分時点での平均経験値差
  "counterTips": [
    {
      "for": "Number", // このTipが対象とするチャンピオンID
      "tip": "String" // 対策Tip
    }
  ],
  "recommendedItems": {
    "forChamp1": ["Number"], // チャンピオン1向け推奨アイテム
    "forChamp2": ["Number"] // チャンピオン2向け推奨アイテム
  },
  "patchVersion": "String", // このデータの対象パッチバージョン
  "lastUpdated": "Date" // データ最終更新日時（システム管理用）
}
```

## 3. コンテンツ管理領域
WordPress用のデータモデルを拡張したカスタムモデル。

### 3.1 LOLArticle（カスタムポストタイプ）
LOL関連記事を表すモデル。
```json
{
  "ID": "Number", // WordPress記事ID
  "post_author": "Number", // 著者ID
  "post_date": "Date", // 投稿日時
  "post_content": "String", // 記事本文
  "post_title": "String", // 記事タイトル
  "post_excerpt": "String", // 抜粋
  "post_status": "String", // 公開ステータス
  "post_type": "lol_article", // カスタムポストタイプ
  "post_name": "String", // スラッグ
  "post_modified": "Date", // 最終更新日時
  "meta": {
    "article_type": "String", // 記事タイプ（guide, news, analysis, patch等）
    "featured_champions": ["Number"], // 特集チャンピオンID配列
    "patch_version": "String", // 関連パッチバージョン
    "data_source": "String", // データソース（automated, manual, mixed）
    "content_score": "Number", // コンテンツ品質スコア（AI評価）
    "seo_score": "Number", // SEOスコア
    "read_time": "Number" // 推定読了時間（分）
  },
  "taxonomies": {
    "lol_champion": ["String"], // チャンピオンタクソノミー
    "lol_role": ["String"], // ロールタクソノミー
    "lol_patch": ["String"], // パッチタクソノミー
    "lol_topic": ["String"] // トピックタクソノミー
  },
  "related_data": {
    "champion_data": {
      // 関連するチャンピオンデータへの参照（表示用）
    },
    "matchup_data": {
      // 関連するマッチアップデータへの参照（表示用）
    }
  },
  "automation": {
    "source_url": "String", // 元情報URL
    "ai_generated": "Boolean", // AI生成フラグ
    "generation_prompt": "String", // 生成に使用したプロンプト
    "last_updated_by": "String", // 最終更新者（system/usernameなど）
    "content_status": "String" // コンテンツステータス（draft, review, published）
  }
}
```

### 3.2 ContentSource（カスタムポストタイプ）
コンテンツソース設定を表すモデル。
```json
{
  "ID": "Number", // WordPress記事ID
  "post_title": "String", // ソース名
  "post_status": "String", // 公開ステータス
  "post_type": "content_source", // カスタムポストタイプ
  "meta": {
    "source_type": "String", // ソースタイプ（rss, api, website）
    "source_url": "String", // ソースURL
    "source_format": "String", // データフォーマット（RSS, JSON, HTML）
    "scraping_rules": {
      // スクレイピングルール（CSSセレクタなど）
    },
    "content_category": "String", // コンテンツカテゴリ（news, patch, esports等）
    "priority": "Number", // 優先度（1-10）
    "update_frequency": "Number", // 更新頻度（分単位）
    "last_fetched": "Date", // 最終取得日時
    "active": "Boolean" // アクティブ状態
  }
}
```

### 3.3 AITemplate（カスタムポストタイプ）
AI生成用テンプレートを表すモデル。
```json
{
  "ID": "Number", // WordPress記事ID
  "post_title": "String", // テンプレート名
  "post_content": "String", // テンプレート本文（プロンプト）
  "post_status": "String", // 公開ステータス
  "post_type": "ai_template", // カスタムポストタイプ
  "meta": {
    "template_type": "String", // テンプレートタイプ（champion_analysis, patch_notes, matchup_guide等）
    "target_length": "Number", // 目標文字数
    "complexity_level": "String", // 複雑さレベル（beginner, intermediate, advanced）
    "required_variables": ["String"], // 必須変数配列
    "style_guide": "String", // スタイルガイド
    "example_output": "String", // 出力例
    "active": "Boolean" // アクティブ状態
  }
}
```

## 4. システム管理領域
システム内部で使用する管理用データモデル。

### 4.1 APIUsage
API使用状況を追跡するモデル。
```json
{
  "id": "String", // 一意のID
  "api_type": "String", // API種別（riot, openai等）
  "endpoint": "String", // 使用エンドポイント
  "method": "String", // HTTPメソッド
  "timestamp": "Date", // タイムスタンプ
  "response_time": "Number", // 応答時間（ms）
  "status_code": "Number", // ステータスコード
  "success": "Boolean", // 成功したかどうか
  "error_message": "String", // エラーメッセージ（あれば）
  "rate_limit_remaining": "Number", // 残りレート制限
  "request_params": {
    // リクエストパラメータ（機密情報を除く）
  },
  "response_size": "Number" // レスポンスサイズ（バイト）
}
```

### 4.2 ContentGenerationJob
コンテンツ生成ジョブを表すモデル。
```json
{
  "id": "String", // 一意のID
  "job_type": "String", // ジョブタイプ（article_generation, update, curation等）
  "status": "String", // ステータス（pending, processing, completed, failed）
  "priority": "Number", // 優先度（1-10）
  "created_at": "Date", // 作成日時
  "updated_at": "Date", // 更新日時
  "completed_at": "Date", // 完了日時
  "source_data": {
    // 元データ（URL、JSONなど）
  },
  "template_id": "Number", // 使用テンプレートID
  "output_post_id": "Number", // 出力先記事ID
  "params": {
    // ジョブパラメータ
  },
  "log": [
    {
      "timestamp": "Date",
      "message": "String",
      "level": "String" // info, warning, error等
    }
  ],
  "error": {
    "code": "String",
    "message": "String",
    "details": "String"
  },
  "metrics": {
    "processing_time": "Number", // 処理時間（ms）
    "token_usage": "Number", // トークン使用量（AI生成）
    "content_quality_score": "Number" // コンテンツ品質スコア
  }
}
```

### 4.3 SystemConfig
システム設定を表すモデル。
```json
{
  "id": "String", // 設定ID
  "category": "String", // カテゴリ（api, content, security等）
  "key": "String", // 設定キー
  "value": "Any", // 設定値
  "data_type": "String", // データ型（string, number, boolean, json等）
  "description": "String", // 説明
  "updated_at": "Date", // 最終更新日時
  "updated_by": "String" // 更新者
}
```

### 4.4 ScheduledTask
予定タスクを表すモデル。
```json
{
  "id": "String", // タスクID
  "task_type": "String", // タスクタイプ
  "schedule": {
    "type": "String", // スケジュールタイプ（cron, interval, one_time）
    "expression": "String", // cronパターンまたは間隔
    "next_run": "Date" // 次回実行予定時刻
  },
  "params": {
    // タスクパラメータ
  },
  "status": "String", // ステータス（enabled, disabled, one_time_completed）
  "last_run": {
    "timestamp": "Date", // 最終実行時刻
    "duration": "Number", // 実行時間（ms）
    "status": "String", // 実行結果（success, partial_success, failure）
    "message": "String" // 結果メッセージ
  },
  "created_at": "Date", // 作成日時
  "updated_at": "Date" // 更新日時
}
```

## 5. データモデル間の関連
主要なデータモデル間の関連を以下に示す。

### 5.1 Summoner - Match
- 1人のサモナーは複数のマッチに参加する（1対多）
- Matchモデルのparticipants.puuidフィールドでSummonerと関連付け

### 5.2 Champion - Matchup
- 1つのチャンピオンは複数のマッチアップで関連付けられる（1対多）
- MatchupモデルのchampionId1とchampionId2フィールドでChampionと関連付け

### 5.3 Champion - Item
- チャンピオンとアイテムは多対多の関係
- 統計データを通じて関連付け（人気アイテム、勝率の高いアイテムなど）

### 5.4 LOLArticle - Champion
- 記事と関連チャンピオンは多対多の関係
- taxonomies.lol_championフィールドとチャンピオンタクソノミーで関連付け

### 5.5 ContentSource - LOLArticle
- コンテンツソースと記事は1対多の関係
- 記事のautomation.source_urlからContentSourceを特定可能

### 5.6 AITemplate - LOLArticle
- AIテンプレートと記事は1対多の関係
- 記事生成時のテンプレート情報がautomation.generation_promptに格納

## 6. データ継承と更新戦略
### 6.1 Riot APIデータ更新戦略
- 定期更新: パッチリリース後に全チャンピオン/アイテムデータを更新
- 増分更新: マッチデータは新規マッチ情報取得時に追加
- 再計算: 統計データは日次/週次で再計算（勝率、ピック率など）

### 6.2 コンテンツデータ管理戦略
- 自動キュレーション: 外部ソースから定期的に情報収集し、独自コメント付与
- 鮮度管理: パッチノート関連情報は優先的に更新
- アーカイブ: 古いパッチの記事はアーカイブタグ付与

### 6.3 メタデータ計算戦略
- 人気ビルド: 直近2週間のマッチデータから計算
- カウンター情報: 最新パッチのマッチアップデータから計算
- トレンド分析: パッチ間の統計変化を計算