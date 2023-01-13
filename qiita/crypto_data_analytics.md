## はじめに

ブロックチェーン上には取引の記録を始めとした無数のデータが存在します。
データがあれば分析したくなるのが人の性、海外ではCrypto Data Analystが生まれ始めています。

https://twitter.com/DuneAnalytics/status/1483071440903680002

ブロックチェーンは柔軟に分析できるデータの持ち方をしておらず初歩的な集計でも長時間を要します（[About The Graph](https://thegraph.com/docs/en/about/)）。
分析のためには、ブロックチェーン外（オフチェーン）にデータを保持するデータ分析サービスを利用するのが一般的です。
後述しますがDune Analytics、The Graph...といったサービスが存在します。

### データ分析のユースケース

C向けもB向けも問わず様々なユースケースが考えられます。

- 投資を検討するVCやヘッジファンドの意思決定サポート
- DAppsを運営する企業がKPIモニタリングに利用
- トークングラフ等のマーケティングへの活用、レコメンド
- ブロックチェーン上の犯罪追跡
- いわゆる「勝ってる」投資家の保有銘柄の閲覧
- ブロックチェーンの学習
    - 様々な切り口で眺めることで、従来は研究か取引でしか把握できなかった細かい部分まで理解できます
- その他色々


## サービス一覧

それではブロックチェーンのデータ分析サービスはどういったものがあるのでしょうか。
有名どころだと下記のようなサービスがあります。

|    | クエリの発行方法 | Web APIの対応 | データのエクスポート先 |
| :--: | :---: | :---: | :---: |
|  自前でフルノード運用 | 実装次第 | 実装次第 | 実装次第 |
| [Dune Analytics](https://dune.com/home) | SQL | ✗ | CSV（有償） |
| [Nansen](https://www.nansen.ai/) | ✗ | ○ | CSV（有償） |
| [The Graph](https://thegraph.com/en/) | GraphQL | ○ | 実装次第 |
| [BigQuery](https://cloud.google.com/bigquery?hl=ja) | SQL | ✗ | 実装次第 |

[A Comparison of Crypto Data Providers and APIs](https://blog.luabase.com/a-comparison-of-crypto-data-providers/) / [Querying Ethereum Blockchain](https://medium.com/coinmonks/xquerying-ethereum-blockchain-a25ebcaca83a) / [Blockchain analytics](https://mirror.xyz/barniker.eth/J6s7SYB4hUc90LXb7s0lmSNCIydrA2AzxHJep445_xw)

まず最も素朴な選択肢は自前でブロックチェーンのフルノードを運用する方法です。
フルノードを手元に落としてくるか、ノードホスティングサービス（ex. [Quicknode](https://www.quicknode.com/)）を利用します。
データ分析の自由度はありますがコストはとても高いです。

自前はトゥーマッチなので、一般的にはDune Analytics等のSaaSを利用します。
これらは従来のデータ分析同様、クエリ（ex. SQL）を発行することでデータ分析が可能です。

今回の記事では、日本でも紹介記事の多いBigQuery / Dune Analytics / The Graphをピックアップしてご紹介いたします。

### 補足：他のデータ分析サービスも気になる方向け

Andrew Hongの[ブログ記事](https://web3datadegens.substack.com/p/2023-guide-to-web3-data-tools)中の図がデータ分析における川上から川下まで俯瞰しやすくオススメです。
今回紹介するサービスの他にも様々なものが網羅されています。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/9eec9f39-f6ca-143e-4065-cacfbf3ff373.png)
[2023 Guide to Web3 Data Tools](https://web3datadegens.substack.com/p/2023-guide-to-web3-data-tools)

## 1. BigQueryで分析する

説明不要、Google CloudのDWHサービスです。

https://cloud.google.com/bigquery?hl=ja

BigQuery（BQ）にはイーサリアムの公開データセットが備わっています。
多少の遅延はありつつリアルタイムで更新されており、通常のBQ同様SQLを発行して分析できます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/43dc149f-05ef-5700-775b-7110830016ea.png)

普段からBQやSQLに慣れ親しんでいる場合、新たに環境を準備する必要がなくすぐに利用できるメリットがあります。
一方で生に近いデータセットしかないことやクエリの従量課金については注意が必要です。

BQについてはデータセットを利用するだけなので細かい説明はしません。
試したい方は[Query Ethereum Blockchain with SQL in Google BigQuery](https://evgemedvedev.medium.com/ethereum-blockchain-on-google-bigquery-283fb300f579)が詳しいです。

## 2. Dune Analyticsで分析する

ブロックチェーン上のデータについてSQLを用いて分析できるサービスです。

https://dune.com/home

個人的に最もオススメです。
ブラウザ上でSQLを記述し実行可能なGUI、グラフィカルなダッシュボード作成機能が付いています。
「BigQueryとLooker Studioのブロックチェーン版」のような操作感です。
他にも作成したクエリやダッシュボードを共有可能な機能もあります。

データ分析するだけなら、無料かつ無制限に利用可能です！
CSVダウンロードを行う場合やマッチョなインスタンスを利用する際は別途オカネが必要です。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/9c96d011-adbd-c652-e3aa-4afa0bbbb565.png)
[Pricing](https://dune.com/pricing)

### 利用方法

[Dune Analyticsのホームページ](https://dune.com/home)からメールアドレスで会員登録すれば準備完了です。
ログイン後`Menu > New Query`でDune AnalyticsのGUIが開きます。
ここにSQLを記述し実行します。

![Pasted Graphic.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/7ff62b93-2c2f-b161-bb74-51da6f0f7e06.png)
[Queries are the heart of Dune's magic](https://dune.com/docs/getting-started/queries/#queries-are-the-heart-of-dunes-magic)

詳細は[公式ドキュメント](https://dune.com/docs/)をご参照ください。

### 実際にデータ分析してみる

それでは実際に使ってみましょう。
今回は山古志村NFT保有者を抽出するクエリを作ってみます。

https://note.com/yamakoshi1023/n/n1ae0039aa8a4

山古志村NFTは山古志地域の「電子住民票」を兼ねたもので、正式名称は[`Nishikigoi NFT`](https://nishikigoi.on.fleek.co/)です。
ブロックチェーンエクスプローラー[Etherscan](https://etherscan.io/)で検索します。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/256034d5-e632-8798-018d-e04ae01f5724.png)

赤枠で囲ったContractがNishikigoiを表すアドレスなのでコピーします。
「現在のNishikigoi NFT所有者」を取得するべく、各トークンID毎にランク付けし、最新アドレスのみを抽出します。
[Blockchain Analytics 101 — Dune Queries for On-Chain NFT Analysis](https://medium.com/@jseid212/blockchian-analytics-101-queries-for-on-chain-nft-analysis-fe08cbfa9ec2)を参考にしました（`FROM`句に何を書くか等、既存のクエリを参考にして進めると分かりやすいです）。

```sql
WITH
  transactions AS (
    SELECT
      "tokenId" AS token_id,
      "to" AS to_address,
      ROW_NUMBER() OVER (
        PARTITION BY "tokenId"
        ORDER BY
          evt_block_time DESC
      ) AS transaction_rank
    FROM
      erc721."ERC721_evt_Transfer"
    WHERE
      contract_address = '\xF16a5B64F5a774C24218a83f6FB2C7700FB6469a'
  )
SELECT
  to_address,
  COUNT(1) AS quantity
FROM
  transactions
WHERE
  transaction_rank = 1
GROUP BY
  to_address
ORDER BY quantity DESC
```

Dune AnalyticsのGUI上にクエリを書き[Ctrl + Enter](https://dune.com/docs/getting-started/queries/query-window/#run-selection)で実行します。
重たいクエリだと相応の時間がかかるのですが今回はすぐに返ってくるかと思います。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/542d6cc3-866a-bc1d-934b-ea9e754b6667.png)

ページ下部に`1,042 rows`と記載があり、クエリの実行結果は「現在のNishikigoi NFT保有者は1042アドレス」だと示しています。
Etherscanで答え合わせをしてみましょう。
下記の図で赤枠で囲った通り、確かにHoldersは1042なので正しい分析結果が取得できていそうです。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/657ac4e6-495a-4c3a-bc5d-6c8d31b03b3d.png)

山古志村NFTの保有者一覧が取得できました。
例えばこちらのリストをもとに「山古志村NFT保有者が持っているNFT」を抽出する等、様々な切り口で分析していけそうです。

### 更に詳しく知りたい方向け

Dune Analyticsに入門したい方は、まずは充実のチュートリアルをやってみるのをオススメします。
また、Dune Analytics上に共有されたクエリを読むのも勉強になります。

- [The general process for surfacing data with Dune](https://dune.com/docs/getting-started/guides/dune-guides/#the-general-process-for-surfacing-data-with-dune)
- [Blockchain Analytics 101 — Dune Queries for On-Chain NFT Analysis](https://medium.com/@jseid212/blockchian-analytics-101-queries-for-on-chain-nft-analysis-fe08cbfa9ec2)
- [Dune Analytics: A Guide for Complete Beginners](https://mirror.xyz/phillan.eth/17VAXsMPpwJg4OQNBHKTYAQTWfJMwFuXZQDAxPStf0o)
- [Want to become a crypto data analyst?](https://twitter.com/DuneAnalytics/status/1483071440903680002)

### 補足：インフラアーキテクチャ

裏側のアーキテクチャは[コチラ](https://twitter.com/sebastian_wag/status/1545431781779939328)のスレッドが詳しいです。
[Quicknode上に構成したアーカイブノード](https://blog.quicknode.com/dune-analytics-quiknode/)から定期的にデータを取得、ELT処理後にSpark上のDWHに格納しています。
Dune Analyticsはv2に移行しつつあるのですが、[v1はPostgreSQLで構成されています](https://docs.dune.com/dune-engine-v2-beta/dunes-new-query-engine#new-query-engine)。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/e0db0c32-3204-faeb-ab6f-111f6f583dc1.png)
[Tweet](https://twitter.com/sebastian_wag/status/1545431781779939328)


### 補足：テーブル構造

Dune Analyticsを触っていると、Raw / Decoded / Spellbook...といったテーブルを目にします。

Rawテーブルはそのままずばり生データで、イーサリアム上のトランザクション等がそのまま格納されています（ex. `ethereum.transactions`）。
DecodedテーブルはRawテーブルをデコードし、人間が分かりやすい形式にしたもので、スマートコントラクトやイベント毎のテーブルが該当します。
SpellbookテーブルはRawやDecodedテーブルをSQLで加工したテーブルです。

[A Basic Wizard Guide to Dune SQL and Ethereum Data Analytics](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql) / [Dune Analytics: A Guide for Complete Beginners](https://mirror.xyz/phillan.eth/17VAXsMPpwJg4OQNBHKTYAQTWfJMwFuXZQDAxPStf0o)

## 3. The Graphで分析する

最後に紹介するThe GraphはGoogle of Blockchainsと称されるサービスです。

https://thegraph.com/en/

Dune Analytics同様クエリを発行しイーサリアムのデータにアクセスできます。
GraphQL APIのみを持つため、人間が直接クエリを実行するだけでなくDAppsのバックエンドに利用する用途も多いかもしれません。

導入事例として、[Uniswap](https://uniswap.org/)ら取引所が表示する情報（ex. トークン価格や過去の取引量、流動性）を毎月40億件以上捌いている実績があります。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/f21a4b11-88bb-9dce-4441-4edd0ea8b793.png)
[The Graph GRT Token Economics](https://thegraph.com/blog/the-graph-grt-token-economics/) / [The Journey of a Subgraph Query](https://learn.figment.io/tutorials/the-journey-of-a-subgraph-query)

### サービス誕生の背景

Dune Analyticsのように独自サーバを構築すればデータ分析サービスの提供はできますが、運営元都合でサービスを停止することも造作ありません。
The Graphは非中央集権的に運営されるオフチェーンな分散ネットワーク（[Graph Node](https://github.com/graphprotocol/graph-node)）上で動くので単一障害点を持ちません。
ブロックチェーンに近い思想を持って生まれたサービスです。

### 動作の流れ（簡略版）

EVM系（ex. イーサリアム）のスマートコントラクトはトランザクションの処理中に[イベントログを出力します](https://medium.com/coinmonks/day-5-events-log-and-introduction-about-the-graph-8254815eb95e)。
The Graphユーザは「どのイベントをキャプチャするか / イベントをどんなスキーマに変換するかの定義（サブグラフ）」を書きデプロイします。
デプロイされたGraph Nodeは[過去のブロックに遡ってイベントを収集しつつ](https://qiita.com/chomado/items/705d0a6d9ce985f1a433#7-yaml-%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E7%B7%A8%E9%9B%86)新たなイベントを監視し、定義したスキーマ通りデータベース（[PostgreSQLらしいです](https://docs.thegraph.academy/official-docs/indexer#infrastructure)）に格納します。

格納したデータに対しGraphQL APIを用いたクエリで分析を行います。

![Pasted Graphic 19.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/e69ebfb6-b5fa-fea9-72f2-9cd0e837a560.png)
[Introduction to The Graph - The "Google" of Web3](https://techfi.tech/introduction-to-the-graph-the-google-of-web3/)

イベントはスマートコントラクト毎だけではなく、例えばERC-721（NFT）全体に対しても取得可能です。

https://thegraph.com/hosted-service/subgraph/wighawag/eip721-subgraph

https://github.com/wighawag/eip721-subgraph/blob/master/subgraph.yaml

### 補足：The Graphとの関わり方

The Graphに関係する人や組織は主に4グループあります。
後述しますが、The Graphは分散ネットワークであり、インセンティブや不正防止のため複数のステークホルダーが存在します。
ただし、データ分析する上ではDeveloperとIndexer以外は知識として留めるので良いと思います。

- Developer
    - The Graphにデータ収集を依頼したりクエリを発行する主体です。データ分析する場合はこちらに該当します
- Indexer
    - Graph Nodeを運用します。データ（インデックス）を生成し、クエリに回答することでインセンティブを受け取ります
- Curator
    - このサブグラフオススメだよ！とIndexerに働きかけます
- Delegator
    - GRTをステークしてIndexerを支持し報酬を得ようとします

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/377a52bc-aaeb-05ea-94a1-8c7ebd16d66f.png)
[The Graph](https://thegraph.com/docs/en/)

https://gaiax-blockchain.com/the-graph

### 補足：The Graphの複雑さの根源

The Graphはイーサリアム上で動作するスマートコントラクトと、オフチェーンで動作するネットワークが組み合わさったサービスです。
詳しく仕組みを理解するためにはオンチェーンとオフチェーンを行き来する必要がありなかなかタフです。

The Graphは基本的にオフチェーンな分散ネットワークです。
ただし、インセンティブや不正防止の観点からオンチェーン上にスマートコントラクトやトークン（GRT）を準備しています。

例えばIndexer（Graph Node）になるためには、GRTを一定数保有する必要があります。
DeveloperがGraph Nodeを検索するための機能（Service Discovery）はスマートコントラクトであり、GRT保有者しかリストアップされないためです。
また、もし悪さをした場合GRTを召し上げられる構造になっており不正を防止しています。

![Pasted Graphic 21.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/287774/f51cba43-2cda-2d0a-5192-9d4a08d1848e.png)
[The Graph Network In Depth - Part 1](https://thegraph.com/blog/the-graph-network-in-depth-part-1/)

### 実際にデータ分析してみる

工事中👷‍♂️
下記にトライしています。

- [Learn about The Graph](https://thegraph.com/ecosystem/learn/)
- [The Graph](https://learn.figment.io/protocols/thegraph)

## 終わりに

ブロックチェーンを対象にデータ分析する方法をまとめました。
既存技術（ex. SQL）でデータ分析できるのが分かり解像度が上がりました。
