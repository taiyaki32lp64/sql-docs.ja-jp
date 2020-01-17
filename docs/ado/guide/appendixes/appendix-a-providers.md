---
title: 付録 A:プロバイダー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926977"
---
# <a name="appendix-a-data-and-service-providers"></a>付録 A:データとサービス プロバイダー
このセクションでは、次の 3 つの種類のプロバイダーを取り上げます。 データ プロバイダー、サービス プロバイダー、およびサービスのコンポーネント。 プロバイダーは、2 つのカテゴリに分類されます。 データとサービスを提供するものを提供するものです。 A*データ プロバイダー*が独自のデータを所有し、アプリケーションに表形式で公開します。 A*サービス プロバイダー*作成や、ADO アプリケーションの機能を強化して、データの利用によって、サービスをカプセル化します。 サービス プロバイダーがさらとして定義しても、*サービス コンポーネント*、他のサービス プロバイダーまたはコンポーネントと連携する必要があります。

## <a name="data-providers"></a>データ プロバイダー
 ADO では、強力で柔軟ないくつかの異なるデータ プロバイダーのいずれかに接続し、指定されたプロバイダーの特定の機能に関係なく、同じプログラミング モデルを公開するためにします。

 ただし、各データ プロバイダーは、一意であるため、アプリケーションが ADO と対話する方法はによって多少異なりますデータ プロバイダー。 違いは、通常は 3 つのカテゴリに分類されます。

-   接続のパラメーター、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

-   [コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトの使用量。

-   プロバイダー固有[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)動作します。

 現在、Microsoft から入手できるデータ プロバイダーの詳細は次のとおりです。

|領域|トピック|
|----------|-----------|
|ODBC データベース|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft インテックス サービス|[Microsoft OLE DB Provider for Microsoft インテックス サービス](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory サービス|[Microsoft OLE DB Provider for Microsoft Active Directory サービス](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet データベース|[OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle データベース|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|インターネットへの発行|[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|単純なデータ ソース|[Microsoft OLE DB の単純なプロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>プロバイダー固有の動的プロパティ
 [プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション、[接続](../../../ado/reference/ado-api/connection-object-ado.md)、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)、および[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトに固有の動的なプロパティが含まれます、。プロバイダー。 これらのプロパティは、ADO をサポートする組み込みのプロパティ以外のプロバイダーに固有の機能に関する情報を提供します。

 接続を確立すると、これらのオブジェクトを作成、使用、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッドを**プロパティ**プロバイダー固有のプロパティを取得するオブジェクトのコレクション。 プロバイダーのマニュアルを参照してください、 [OLE DB プログラマ ガイド](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)のこれらの動的プロパティに関する詳細情報。

## <a name="service-providers"></a>サービス プロバイダー
 サービス プロバイダーを使用するには、キーワードを指定する必要があります。 各サービス プロバイダーに関連付けられているプロバイダーに固有の動的プロパティの注意する必要があります。 プロバイダー固有の詳細については、現在、Microsoft から提供されている各サービス プロバイダーのとおりです。

-   [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB の永続化プロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB のリモート処理のプロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>サービス コンポーネント
 [For OLE DB カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)サービス コンポーネントがデータ プロバイダーのカーソル サポート機能を補完します。 また、キーワードを必要しは動的なプロパティがあります。

 OLE DB プロバイダーの詳細については、次を参照してください。 [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)します。

## <a name="provider-commands"></a>プロバイダー コマンド
 プロバイダーごとに、アプリケーションがプロバイダーのコマンドとして、SQL ステートメントを入力するユーザーを許可する場合は、ここでは、一覧表示、常にユーザー入力を検証して、危険性のある SQL ステートメントを使用してハッカーの攻撃に備える`DROP TABLE t1`、ユーザー入力の一部として。

## <a name="see-also"></a>参照
 [コマンド オブジェクト (ADO) を](../../../ado/reference/ado-api/command-object-ado.md)[接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Microsoft OLE DB Provider for Microsoft Active Directory サービス](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB Provider for Microsoft インテックス サービス](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Microsoft OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [プロパティのコレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh メソッド (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
