---
title: ファイルを含める
description: ファイルを含める
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 0e7d549c2f3b02349007815019cc47647f172f73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213532"
---
## <a name="specifying-application-intent"></a>アプリケーション インテントの指定

キーワード**ApplicationIntent**接続文字列で指定できます。 割り当て可能な値は**ReadWrite**または**ReadOnly**します。 既定値は**ReadWrite**します。

ときに**ApplicationIntent = ReadOnly**クライアントが接続するときに、読み取りワークロードを要求します。 サーバーは接続時と中に、インテントを適用する**使用**ステートメントをデータベースします。

**ApplicationIntent** キーワードは、従来の読み取り専用データベースに対しては無効です。  


#### <a name="targets-of-readonly"></a>読み取り専用のターゲット

接続が選択したときに**ReadOnly**接続がデータベースに存在する可能性のある特別な構成の次のいずれかに割り当てられています。

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 対象の AlwaysOn データベースのワークロードの読み取りを許可または禁止できます。 使用してこの選択を制御、 **ALLOW_CONNECTIONS**の句、 **PRIMARY_ROLE**と**前に示した SECONDARY_ROLE** TRANSACT-SQL ステートメント。

- [geo レプリケーション](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [読み取りスケールアウト](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

使用可能なこれらの特別なターゲットの場合は、通常のデータベースから読み取られます。

&nbsp;

**ApplicationIntent**キーワードを使用*読み取り専用ルーティング*します。


## <a name="read-only-routing"></a>読み取り専用ルーティング

読み取り専用ルーティングは、データベースの読み取り専用レプリカの可用性を実現する機能です。 読み取り専用ルーティングを有効にするのには、次のすべて適用されます。

- AlwaysOn 可用性グループ リスナーに接続する必要があります。

- **ApplicationIntent** 接続文字列キーワードを **ReadOnly**に設定する必要があります。

- データベース管理者が可用性グループを構成し、読み取り専用のルーティングを有効にする必要があります。

複数の接続は、同じ読み取り専用レプリカに接続を満たさない可能性があります、読み取り専用ルーティングを使用します。 データベース同期の変更やサーバーのルーティング構成の変更によって、クライアントが別の読み取り専用レプリカに接続される場合があります。 すべての読み取り専用の要求が同じ読み取り専用レプリカに接続することを確認できます。 によってこの類似性を確認します。*いない*可用性グループ リスナーを渡すこと、**サーバー**接続文字列キーワードです。 代わりに、読み取り専用インスタンスの名前を指定します。

読み取り専用ルーティングは、プライマリに接続するよりも長くかかる場合があります。 待機時間が長くなるのは、読み取り専用ルーティングがまずプライマリに接続し、次に使用できる読み取り可能なセカンダリを検索するためです。 これらの複数の staps のためには、少なくとも 30 秒間に、ログイン タイムアウトを増やす必要があります。

