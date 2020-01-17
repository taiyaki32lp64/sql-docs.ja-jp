---
title: エラーとイベントのリファレンス (レプリケーション) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a42dc8a023e1d44e911907cc96a77017dfc69eaf
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768500"
---
# <a name="errors-and-events-reference-replication"></a>エラーとイベントのリファレンス (レプリケーション)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  ここでは、レプリケーションに関連するさまざまなエラーの原因と解決方法について説明します。  
  
|Error|メッセージ|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|一意インデックス '%.*ls' を含むオブジェクト '%.\*ls' には重複するキー行を挿入できません。|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|制約 '%.*ls' の %ls 違反。 オブジェクト '%.\*ls' には重複したキーを挿入できません。") です。|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|データベース '%ls' は復元されましたが、レプリケーションの復元または削除中にエラーが発生しました。 データベースはオフラインのままです。 SQL Server オンライン ブックのトピック「MSSQL_ENG003165」を参照してください。|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|%S_MSG '%.*ls' を %S_MSG できません。レプリケーションに使用されています。|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|%S_MSG '%.*ls' は、レプリケーションでパブリッシュされているので変更できません。|  
|MSSQL_ENG007395。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|リンク サーバー "%ls" の OLE DB プロバイダー "%ls" では入れ子になったトランザクションを開始できません。 XACT_ABORT オプションが OFF に設定されているので、入れ子になったトランザクションが必要です。|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|パブリケーションを削除できませんでした。 サブスクリプションが存在します。|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|サーバー '%s' はサブスクリプション サーバーとして定義されていません。|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%s' はディストリビューターとして構成されていません。|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%s' はディストリビューション データベースとして構成されていません。|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|ディストリビューション データベース '%s' を削除できませんでした。 このディストリビューション データベースはパブリッシャーに関連付けられています。|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|ディストリビューター '%s' を削除できませんでした。 このディストリビューターはディストリビューション データベースに関連付けられています。|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|サブスクライバー '%s' を削除できません。 そのサブスクライバーのサブスクリプションがパブリケーション データベース '%s' にあります。|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|レプリケーション-%s: エージェント %s が成功しました。 %s|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|レプリケーション-%s: エージェント %s は失敗しました。 %s|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|レプリケーション-%s: エージェント %s には再試行のスケジュールが設定されました。 %s|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|サブスクライバー '%s' によって作成された、パブリケーション '%s' に対するサブスクリプションは、有効期限が切れたので削除されました。|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 このパブリケーションに対する 1 つ以上のサブスクリプションの有効期限が切れています。|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 ログ リーダーとディストリビューション エージェントが実行されており、待機時間の要件に適合することを確認してください。|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|パブリケーション [%s] のしきい値 [%s:%s] が設定されています。 マージ エージェントが実行されており、必要な要件に適合することを確認してください。|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|ユーザー '%.*ls'.%.\*ls はログインできませんでした|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|同時にデータベースに接続できるログ リーダー エージェントまたはログ関連のプロシージャ (sp_repldone、sp_replcmds、および sp_replshowcmds) は 1 つだけです。 ログ関連のプロシージャを実行した場合、そのプロシージャが実行された接続を削除するか、その接続に対して sp_replflush を実行してから、ログ リーダー エージェントを開始するか、別のログ関連のプロシージャを実行してください。|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|レプリケーション エージェントでは、進捗状況メッセージが %ld 分間ログに記録されていません。 この現象は、エージェントの応答が止まったか、システムの使用率が高いことを示している場合があります。 レコードがレプリケーション先にレプリケートされていること、およびサブスクライバー、パブリッシャー、ディストリビューターへの接続がアクティブなままであることを確認してください。|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|エージェントがシャットダウンされました。 詳細については、ジョブ '%s' の SQL Server エージェントのジョブ履歴を参照してください。|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|パブリケーション '%s' のアーティクル '%s' に対するサブスクライバー '%s' のサブスクリプションが、検証エラーの発生後、再初期化されました。|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|パブリケーション '%s' のアーティクル '%s' に対するサブスクライバー '%s' のサブスクリプションで、データ検証に失敗しました。|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|パブリケーション '%s' のアーティクル '%s' に対するサブスクライバー '%s' のサブスクリプションが、データ検証に合格しました。|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|'%s' または db_owner のメンバーだけが匿名エージェントを削除できます。|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|レプリケートされたコマンドを適用しているときに、サブスクライバーで行が見つかりませんでした。|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|パブリケーション '%s' の初期スナップショットはまだ使用できません。|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|アーティクル '%s' の初期スナップショットはまだ使用できません。|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|競合テーブル '%s' が存在しません。|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|レプリケーション作業ディレクトリにサブディレクトリを作成できませんでした。(%ls)|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|ユーザー スクリプト ファイルをディストリビューターにコピーできませんでした。(%ls)|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|スナップショットはパブリケーション '%s' の処理に失敗しました。 アクティブなスキーマ変更または新しいアーティクルが追加されたことが原因の可能性があります。|  
|MSSQL_ENG021617。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|SQL*PLUS を実行できません。 現在のバージョンの Oracle クライアント コードがディストリビューターにインストールされていることを確認してください。|  
|MSSQL_ENG021620。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|システムの Path 変数からアクセスできる SQL*PLUS のバージョンが古いため、Oracle パブリッシングをサポートできません。 現在のバージョンの Oracle クライアント コードがディストリビューターにインストールされていることを確認してください。|  
|MSSQL_ENG021624。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|ディストリビューター '%s' に登録済みの Oracle OLEDB プロバイダー OraOLEDB.Oracle が見つかりません。 現在のバージョンの Oracle OLEDB プロバイダーがディストリビューターにインストールおよび登録されていることを確認してください。|  
|MSSQL_ENG021626。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|Oracle OLEDB プロバイダー OraOLEDB.Oracle を使用して Oracle データベース サーバー '%s' に接続できません。|  
|MSSQL_ENG021627。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|Microsoft OLEDB プロバイダー MSDAORA を使用して Oracle データベース サーバー '%s' に接続できません。|  
|MSSQL_ENG021628。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|ディストリビューター '%s' のレジストリを更新し、Oracle OLEDB プロバイダー OraOLEDB.Oracle を SQL Server と同じプロセスで実行可能にすることができません。 SQL Server が所有しているレジストリ キーの変更が現在のログインに許可されていることを確認してください。|  
|MSSQL_ENG021629。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|Oracle 用の Oracle OLEDB プロバイダー OraOLEDB.Oracle が登録されていることを示す CLSID レジストリ キーがディストリビューターに存在しません。 ディストリビューターに Oracle OLEDB プロバイダーがインストールおよび登録されていることを確認してください。|  
|MSSQL_ENG021642。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|異種パブリッシャーにはリンク サーバーが必要です。 リンク サーバー '%s' は既に存在します。 リンク サーバーを削除するか、または別のパブリッシャー名を選択してください。|  
|MSSQL_ENG021663。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|ソース テーブル [%s].[%s] に有効な主キーが見つかりません。|  
|MSSQL_ENG021684。 「 [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」を参照してください。|Oracle パブリッシャー '%s' の管理者ログインに関連付けられた権限が不十分です。|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%s' には 'MACHINE\Login' または 'DOMAIN\Login' の形式で有効な Windows ログインを指定してください。 '%s' については、マニュアルを参照してください。|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|続行する前に、'%s' エージェント ジョブを '%s' 経由で追加してください。 '%s' については、マニュアルを参照してください。|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|プロセスは、'%1' を '%2' で実行できませんでした。|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|マージ プロセスが、'%1' で生成履歴を変更できませんでした。 トラブルシューティングを行うには、詳細な履歴ログとの同期を再開して、書き込み先の出力ファイルを指定してください。|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|マージ処理で、パラメーター化された行フィルターを使用して、アーティクル内の変更情報を列挙できませんでした。 このエラーが継続して発生する場合、このプロセスのクエリ タイムアウト値を増やし、パブリケーションの保有期間を減少し、パブリッシュされたテーブルのインデックスを強化してください。|  
  
  
