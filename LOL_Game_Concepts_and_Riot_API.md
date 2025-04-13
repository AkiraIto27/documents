# League of Legends ゲーム概念とRiot API概要

## 1. League of Legends (LOL) 基本概念
### 1.1 ゲーム概要
League of Legends（リーグ・オブ・レジェンド、通称LOL）は、Riot Games社が開発・運営するMOBA（Multiplayer Online Battle Arena）ジャンルのオンラインゲームである。5対5の2チームによる対戦形式が基本であり、各プレイヤーは「チャンピオン」と呼ばれるキャラクターを操作し、敵陣営の本拠地（ネクサス）を破壊することを目指す。

### 1.2 主要ゲーム要素
#### 1.2.1 サモナー
プレイヤー自身を表す概念。サモナー名はゲーム内での識別子であり、サモナーレベルはゲーム経験値を示す。

#### 1.2.2 チャンピオン
プレイヤーが操作するキャラクター。160以上の異なるチャンピオンが存在し、それぞれ独自のスキルセットと特性を持つ。チャンピオンは以下のロールに大別される：

- トップレーナー：上部レーンを担当する耐久力の高いチャンピオン
- ジャングラー：中立モンスターを倒しながら各レーンを支援するチャンピオン
- ミッドレーナー：中央レーンを担当する魔法攻撃特化型のチャンピオン
- ボットレーナー（ADC）：下部レーンを担当する物理攻撃特化型のチャンピオン
- サポート：ADCを支援する効果特化型のチャンピオン

#### 1.2.3 マップと目標
標準的な対戦（サモナーズリフト）には以下の要素がある：

- レーン：トップ、ミドル、ボトムの3つの主要経路
- ジャングル：レーン間の中立地帯
- タワー：領域を守る防衛施設
- 抑制装置（インヒビター）：破壊されると敵のスーパーミニオンが出現
- バロン・ナッシャー：倒すと全チーム員に強力なバフを付与
- ドラゴン：倒すと永続的な能力強化を得られる
- ネクサス：本拠地。破壊されると敗北

#### 1.2.4 ゲーム進行
ゲームは以下のフェーズで進行する：

- レーン期（レーニングフェーズ）：序盤、各チャンピオンがレーンでCS（Creep Score、ミニオン処理数）を稼ぎ経済を築く
- 中盤（ミッドゲーム）：小規模な集団戦やマップ目標の争奪
- 後半（レイトゲーム）：フルスケールの集団戦と決着

#### 1.2.5 経済システム

- ゴールド：ミニオン、モンスター、敵チャンピオンの撃破等で獲得
- アイテム：ゴールドを使用して購入し、チャンピオンを強化
- 経験値：レベルアップに必要、高レベルほどスキルが強力になる

#### 1.2.6 ランクシステム
競争力のあるプレイのためのティア構造：

アイアン, ブロンズ, シルバー, ゴールド, プラチナ, エメラルド, ダイアモンド, マスター, グランドマスター, チャレンジャー

各ティア（チャレンジャーより下）はさらにIV, III, II, Iの4つの区分に分かれる。

### 1.3 ゲームメカニクス
#### 1.3.1 スキルシステム
各チャンピオンは以下のスキルを持つ：

- パッシブ：常時発動する特殊能力
- Q, W, E：基本スキル（レベルアップで強化可能）
- R：アルティメットスキル（特に強力で、レベル6, 11, 16で強化可能）

#### 1.3.2 ルーンシステム
試合前に選択する特殊な強化システム：

- メインパス：主要な特性を決定
- サブパス：補助的な特性を追加
- スタットシャード：基本ステータスの微調整

#### 1.3.3 サモナースペル
各試合で2つ選択できる特殊能力：

- フラッシュ：短距離瞬間移動
- イグナイト：継続ダメージ
- テレポート：長距離移動
- ヒール：味方と自身の回復 など

#### 1.3.4 ビジョンシステム
マップ情報把握のためのシステム：

- ワード：視界を提供する設置物
- コントロールワード：敵のワードを無効化し視界を提供
- スキャナー：一時的に範囲内の不可視ユニットを検出
- 青trinket/赤trinket：ワードを設置するためのアイテム

#### 1.3.5 オブジェクティブ管理
試合を有利に進めるための重要目標：

- エレメンタルドラゴン：4種類のドラゴンによる永続バフ
- エルダードラゴン：後半に出現する強力なバフ
- リフトヘラルド：バロン出現前に出現するミニボス
- バロン・ナッシャー：後半の主要目標、強力なバフ提供

#### 1.3.6 メタゲーム
現在の環境で最も効果的とされる戦略やチャンピオン選択。パッチごとに変化する。

- ティアリスト：チャンピオンの強さのランク付け
- メタピック：現環境で評価の高いチャンピオン
- カウンターピック：特定のチャンピオンに対して有利なチャンピオン選択

### 1.4 ゲームバージョンとパッチ
Riot Gamesは定期的にゲームバランスの調整と新コンテンツ追加を行う：

- 通常パッチ：約2週間ごとのバランス調整（例：13.10）
- メジャーパッチ：シーズン変更時の大規模更新
- ホットフィックス：緊急のバグ修正や調整

### 1.5 プロシーン
組織化された競技シーン：

- LCS（北米）, LEC（欧州）, LCK（韓国）, LPL（中国）などの地域リーグ
- MSI（Mid-Season Invitational）：春季の国際大会
- World Championship：年間最大の国際大会

## 2. Riot API の概要
### 2.1 API 構造
Riot Games APIは複数のエンドポイントに分けられている：
#### 2.1.1 SUMMONER-V4
サモナー（プレイヤー）情報を取得するAPI。
`GET /lol/summoner/v4/summoners/by-name/{summonerName}`
主要パラメータ：

- summonerName: 検索するプレイヤー名

主要レスポンス：

- id: サモナーID
- accountId: アカウントID
- puuid: プレイヤーの永続的ユニークID
- name: サモナー名
- profileIconId: プロフィールアイコンID
- revisionDate: 最終更新日時
- summonerLevel: サモナーレベル

#### 2.1.2 MATCH-V5
試合情報を取得するAPI。
`GET /lol/match/v5/matches/by-puuid/{puuid}/ids`
`GET /lol/match/v5/matches/{matchId}`
主要パラメータ：

- puuid: プレイヤーの永続的ユニークID
- matchId: 特定の試合ID

主要レスポンス：

- 試合参加者情報
- チーム構成
- ビルド情報
- 試合統計
- タイムライン情報

#### 2.1.3 LEAGUE-V4
ランク情報を取得するAPI。
`GET /lol/league/v4/entries/by-summoner/{summonerId}`
主要パラメータ：

- summonerId: サモナーID

主要レスポンス：

- queueType: キュータイプ（RANKED_SOLO_5x5, RANKED_FLEX_SR等）
- tier: ティア（IRON, BRONZE, SILVER等）
- rank: ランク（I, II, III, IV）
- leaguePoints: リーグポイント
- wins: 勝利数
- losses: 敗北数

#### 2.1.4 CHAMPION-MASTERY-V4
チャンピオン熟練度情報を取得するAPI。
`GET /lol/champion-mastery/v4/champion-masteries/by-summoner/{summonerId}`
主要パラメータ：

- summonerId: サモナーID

主要レスポンス：

- championId: チャンピオンID
- championLevel: チャンピオン熟練度レベル
- championPoints: 累積ポイント
- lastPlayTime: 最後にプレイした時間

#### 2.1.5 SPECTATOR-V4
現在進行中のゲーム情報を取得するAPI。
`GET /lol/spectator/v4/active-games/by-summoner/{summonerId}`
主要パラメータ：

- summonerId: サモナーID

主要レスポンス：

- 現在の試合情報
- 参加プレイヤーとチャンピオン選択
- バン情報
- ルーンとサモナースペル

### 2.2 データドラゴン（Data Dragon）
ゲーム内静的データを提供するCDNサービス。
`https://ddragon.leagueoflegends.com/cdn/{version}/data/{language}/champion.json`
提供データ：

- チャンピオン情報
- アイテム情報
- ルーン情報
- サモナースペル情報
- アイコンと画像リソース

### 2.3 API 利用制限
Riot APIには以下の制限がある：
#### 2.3.1 レート制限

- アプリケーションレート制限：開発者キー単位の制限
- メソッドレート制限：特定APIエンドポイントへのリクエスト制限

レート制限ヘッダー：

- X-App-Rate-Limit: アプリケーション制限（例："20:1,100:120"）
- X-Method-Rate-Limit: メソッド制限（例："100:120"）
- X-Rate-Limit-Count: 現在の使用状況

#### 2.3.2 API キー

- 開発キー：開発用、厳しい制限あり（24時間ごとに再生成）
- 本番キー：申請により取得、より高いレート制限

#### 2.3.3 利用規約

- 商用利用に関するガイドライン
- Riot APIポリシー準拠要件
- ユーザーデータ取り扱い要件

### 2.4 API 使用のベストプラクティス
#### 2.4.1 効率的なAPI利用

- キャッシュの活用（TTLを考慮）
- バッチリクエストの活用
- 不要なリクエストの削減

#### 2.4.2 データ処理

- 生データの適切な変換と集約
- 意味のある派生データの計算
- 時系列データのトレンド分析

#### 2.4.3 エラーハンドリング

- レート制限対応（429エラー）
- サービス不可時のフォールバック戦略
- リトライ戦略（指数バックオフなど）

### 2.5 一般的な実装パターン
#### 2.5.1 基本フロー

1. サモナー名からPUUID取得
2. PUUIDから最近のマッチID取得
3. マッチIDから詳細情報取得
4. サモナーIDからランク情報取得
5. データ集約・分析

#### 2.5.2 データ更新戦略

- 最新パッチのマスターデータ取得
- 定期的なプレイヤーデータ更新
- イベント駆動型の更新トリガー

#### 2.5.3 キャッシュ戦略

- マスターデータ：パッチ単位でのキャッシュ
- マッチデータ：長期キャッシュ（変更なし）
- プレイヤーデータ：短期キャッシュ（頻繁に変更）
- ランキングデータ：中期キャッシュ（定期更新）

### 2.6 実装例
#### 2.6.1 基本的なAPIリクエスト（JavaScript）
```javascript
const API_KEY = 'RGAPI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx';
const REGION = 'jp1';

// サモナー情報を取得
async function getSummonerByName(summonerName) {
  try {
    const response = await fetch(
      `https://${REGION}.api.riotgames.com/lol/summoner/v4/summoners/by-name/${encodeURIComponent(summonerName)}`,
      { headers: { 'X-Riot-Token': API_KEY } }
    );
    
    if (!response.ok) {
      throw new Error(`HTTP error ${response.status}`);
    }
    
    return await response.json();
  } catch (error) {
    console.error('Error fetching summoner data:', error);
    return null;
  }
}

// 使用例
getSummonerByName('プレイヤー名')
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

#### 2.6.2 試合履歴取得（Python）
```python
import requests

API_KEY = 'RGAPI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
REGION = 'jp1'
REGIONAL_ROUTING = 'asia'

def get_match_history(puuid, count=20):
    url = f'https://{REGIONAL_ROUTING}.api.riotgames.com/lol/match/v5/matches/by-puuid/{puuid}/ids'
    params = {
        'count': count,
        'api_key': API_KEY
    }
    
    response = requests.get(url, params=params)
    
    if response.status_code != 200:
        return f"Error: {response.status_code}"
    
    match_ids = response.json()
    matches = []
    
    for match_id in match_ids:
        match_url = f'https://{REGIONAL_ROUTING}.api.riotgames.com/lol/match/v5/matches/{match_id}'
        match_response = requests.get(match_url, params={'api_key': API_KEY})
        
        if match_response.status_code == 200:
            matches.append(match_response.json())
    
    return matches

# 使用例
# puuid = '取得したプレイヤーのPUUID'
# matches = get_match_history(puuid, 5)
```

## 3. LOL分析プラットフォームの主要指標
### 3.1 プレイヤー分析指標
#### 3.1.1 基本指標

- KDA比：(キル + アシスト) ÷ デス
- CS/分：1分あたりのミニオン処理数
- ビジョンスコア：視界確保貢献度
- ダメージシェア：チーム内での与ダメージの割合

#### 3.1.2 高度な指標

- ゴールド効率：ゴールド獲得とダメージ出力の相関
- レーン支配率：序盤のCS/ゴールド差異
- チームファイト貢献度：集団戦での影響度
- オブジェクティブコントロール：主要目標の獲得率

### 3.2 チャンピオン分析指標
#### 3.2.1 勝率関連

- 全体勝率：全試合での勝率
- 熟練者勝率：特定チャンピオンの熟練プレイヤーの勝率
- 試合時間別勝率：序盤/中盤/終盤での勝率推移

#### 3.2.2 使用統計

- ピック率：選択される頻度
- バン率：禁止される頻度
- ポジション分布：各ロールでの使用率

#### 3.2.3 ビルド分析

- アイテムパス勝率：特定のビルドルートの勝率
- ルーン組み合わせ効果：ルーン選択による勝率変化
- スキルオーダー効率：スキル育成順序による影響

### 3.3 メタゲーム分析指標
#### 3.3.1 パッチ影響分析

- バランス変動度：パッチ前後の勝率変化
- メタシフト指数：ピック/バン率の変化度
- 適応難易度：新メタへの移行コスト評価

#### 3.3.2 トレンド分析

- 急上昇チャンピオン：人気急上昇の検出
- 隠れた強キャラ：低ピック率高勝率キャラの特定
- 地域間メタ差異：サーバー間のプレイスタイル分析

## 4. コンテンツ分類体系
LOLハイブリッドプラットフォームにおけるコンテンツ分類の推奨体系。
### 4.1 コンテンツタイプ

- ニュース：最新情報、パッチノート、公式発表
- ガイド：チャンピオン攻略、初心者向け解説
- 分析：統計データ解説、メタ解析、トレンド考察
- プロシーン：eスポーツ情報、試合レポート、選手分析
- コミュニティ：プレイヤー体験、面白い出来事、創作コンテンツ

### 4.2 対象ユーザー層

- 初心者：基本概念解説、入門ガイド
- 一般プレイヤー：最新情報、ティアリスト
- 熟練者：高度な戦術解説、メタ分析
- 観戦者：プロシーン情報、試合ハイライト

### 4.3 タグ体系

- パッチバージョン：13.10, 13.11など
- チャンピオン名：Ahri, Yasuo, Zedなど
- ロール：Top, Jungle, Mid, ADC, Support
- 難易度：初級, 中級, 上級
- コンテンツ形式：テキスト, 画像, 動画, データ
- 地域：NA, EU, KR, CN, JP など