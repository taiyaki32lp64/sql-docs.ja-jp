---
title: ステートメントおよび結果セットの操作 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a57ffc5c9314f8e84c077b6c15ab88ed5411f028
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025365"
---
# <a name="working-with-statements-and-result-sets"></a>ステートメントおよび結果セットの操作

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] および提供されている Statement オブジェクトと ResultSet オブジェクトを操作するときに、アプリケーションのパフォーマンスと信頼性を向上させるために使用できる手法がいくつかあります。

## <a name="use-the-appropriate-statement-object"></a>適切なステートメント オブジェクトの使用

JDBC ドライバーの Statement オブジェクト、たとえば [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) オブジェクトなどのいずれかを使用するときは、必ずジョブに対して適切なオブジェクトを使用します。

- OUT パラメーターがない場合は、SQLServerCallableStatement オブジェクトを使用する必要はありません。 代わりに、SQLServerStatement または SQLServerPreparedStatement オブジェクトを使用してください。

- ステートメントを複数回実行する予定がない場合、または IN または OUT パラメーターがない場合は、SQLServerCallableStatement または SQLServerPreparedStatement オブジェクトを使用する必要はありません。 代わりに、SQLServerStatement オブジェクトを使用します。

## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>ResultSet オブジェクトに対する適切なコンカレンシーの使用

結果セットを生成するステートメントを作成する際、実際に結果の更新を意図していない限り、更新可能なコンカレンシーを要求しないでください。 既定の順方向専用、読み取り専用のカーソル モデルは、結果セットが小さい場合に最も高速に読み取りを行います。

## <a name="limit-the-size-of-your-result-sets"></a>結果セットのサイズの制限

[setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) メソッド (あるいは SET ROWCOUNT または SELECT TOP N SQL 構文) を使用して、大きな結果セットから返される可能性がある場合に、返される行数を制限することを検討してください。 大きな結果セットを処理する必要がある場合は、接続文字列プロパティを responseBuffering=adaptive に設定して、既定のアダプティブ応答バッファリング モードを使用することを検討してください。 この方法を使用すると、アプリケーションで大きな結果セットを処理する際にサーバー側のカーソルを必要とせず、アプリケーション メモリの使用量を最小限に抑えることができます。 詳細については、「[アダプティブバッファリングの使用](../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。

## <a name="use-the-appropriate-fetch-size"></a>適切なフェッチ サイズの使用

読み取り専用のサーバー カーソルの場合、サーバーへのラウンド トリップと、ドライバーで使用されるメモリ量がトレードオフになります。 更新可能なサーバー カーソルの場合、フェッチ サイズもまた、変更に対する結果セットの応答性とサーバー上のコンカレンシーに影響します。 現在のフェッチ バッファー内の行の更新は、[refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) メソッドが明示的に発行されるか、カーソルがフェッチ バッファーを離れるまで表示されません。 フェッチ バッファーが大きいと、パフォーマンスが向上します (サーバーのラウンド トリップが少なくなります) が、変更に対する応答性が低下し、CONCUR_SS_SCROLL_LOCKS (1009) が使用されている場合、サーバー上のコンカレンシーが減少します。 変更に対する応答性を最大化するには、フェッチ サイズ 1 を使用します。 ただし、フェッチされるすべての行でサーバーへのラウンド トリップが発生する点に注意してください。

## <a name="use-streams-for-large-in-parameters"></a>大きな IN パラメーターでのストリームの使用

ストリームまたは、徐々に取り出される BLOB および CLOB を使用して、大きな列値の更新や大きな IN パラメーターの送信を処理します。 JDBC ドライバーは、これらを複数のラウンド トリップでサーバーに "チャンク化" し、メモリに収まりきらない大きな値を設定および更新できるようにします。

## <a name="see-also"></a>参照

[JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
