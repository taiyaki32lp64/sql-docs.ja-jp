---
title: SQL ステートメントを使用してデータを変更する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9de31bad8ef2980e7322b529a6a2b68a12355c2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026751"
---
# <a name="using-an-sql-statement-to-modify-data"></a>SQL ステートメントを使用したデータの変更

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに含まれるデータを SQL ステートメントを使用して変更するには、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) メソッドを使用できます。 executeUpdate メソッドは、SQL ステートメントをデータベースに渡して処理し、影響を受けた行数を示す値を返します。

この場合、最初に [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) メソッドを使用して、SQLServerStatement オブジェクトを作成する必要があります。

次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続を関数に渡して、テーブルにデータを追加する SQL ステートメントを作成および実行し、戻り値を出力します。

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを変更するためのパラメーターを含む SQL ステートメントを使用する必要がある場合は、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) メソッドを使用する必要があります。
>
> データの挿入先の列にスペースなどの特殊文字が含まれる場合は、それが既定値である場合を含め、挿入する値を指定する必要があります。 ここで指定しないと、挿入操作が失敗します。
>
> JDBC ドライバで、発生した可能性があるすべてのトリガが返した更新数を含む、すべての更新数を返す場合、lastUpdateCount 接続文字列プロパティを "false" に設定します。 LastUpdateCount プロパティの詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。

## <a name="see-also"></a>参照

[SQL でのステートメントの使用](../../connect/jdbc/using-statements-with-sql.md)
