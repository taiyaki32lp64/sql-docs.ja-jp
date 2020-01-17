---
title: ObjectType トレース イベント列 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Object Type column values
- events [SQL Server], Object Type column values
- event classes [SQL Server], Object Type column values
- Object Type column values [SQL Server]
ms.assetid: 42f85c50-34c9-49ca-955f-af9595e2707f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76675cf49ba1ac19e18b3bb4b96980aa30c4f6c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115887"
---
# <a name="objecttype-trace-event-column"></a>ObjectType トレース イベント列
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Object Type トレース イベント列は、さまざまなトレース イベントで使用されます。 このトピックでは、この列の値と、その値に関連付けられている定義について説明します。  
  
## <a name="object-type-column-values"></a>ObjectType 列の値  
  
|[値]|定義|  
|-----------|----------------|  
|8259|CHECK 制約|  
|8260|既定値 (制約またはスタンドアロン)|  
|8262|外部キー制約|  
|8272|ストアド プロシージャ|  
|8274|Rule|  
|8275|システム テーブル|  
|8276|サーバーのトリガー|  
|8277|(ユーザー定義) テーブル|  
|8278|表示|  
|8280|拡張ストアド プロシージャ|  
|16724|CLR トリガー|  
|16964|データベース|  
|16975|Object|  
|17222|フルテキスト カタログ|  
|17232|CLR ストアド プロシージャ|  
|17235|スキーマ|  
|17475|資格情報|  
|17491|DDL イベント|  
|17741|管理イベント|  
|17747|セキュリティ イベント|  
|17749|ユーザー イベント|  
|17985|CLR 集合関数|  
|17993|インライン テーブル値 SQL 関数|  
|18000|パーティション関数|  
|18002|レプリケーション フィルター プロシージャ|  
|18004|テーブル値 SQL 関数|  
|18259|サーバー ロール|  
|18263|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows グループ|  
|19265|非対称キー|  
|19277|マスター キー|  
|19280|主キー|  
|19283|ObfusKey|  
|19521|非対称キー ログイン|  
|19523|証明書ログイン|  
|19538|ロール|  
|19539|SQL ログイン|  
|19543|Windows ログイン|  
|20034|リモート サービス バインド|  
|20036|データベースに関するイベント通知|  
|20037|イベント通知|  
|20038|SQL スカラー関数|  
|20047|オブジェクトに関するイベント通知|  
|20051|シノニム|  
|20307|Sequence|  
|20549|エンドポイント|  
|20801|キャッシュされる可能性のあるアドホック クエリ|  
|20816|キャッシュされる可能性のある準備されたクエリ|  
|20819|Service Broker サービス キュー|  
|20821|UNIQUE 制約|  
|21057|アプリケーション ロール|  
|21059|Certificate|  
|21075|[サーバー]|  
|21076|Transact-SQL トリガー|  
|21313|アセンブリ|  
|21318|CLR スカラー関数|  
|21321|インライン スカラー SQL 関数|  
|21328|パーティション構成|  
|21333|ユーザー|  
|21571|Service Broker サービス コントラクト|  
|21572|データベースのトリガー|  
|21574|CLR テーブル値関数|  
|21577|内部テーブル (XML ノード テーブル、キュー テーブルなど)|  
|21581|Service Broker メッセージ型|  
|21586|Service Broker ルート|  
|21587|統計|  
|21825<br /><br /> 21827<br /><br /> 21831<br /><br /> 21843<br /><br /> 21847|ユーザー|  
|22099|Service Broker サービス|  
|22601|インデックス|  
|22604|証明書ログイン|  
|22611|XMLSchema|  
|22868|型|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
