---
title: 3\.5 ドライバーをドライバー 3.8 にアップグレードする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97b100b1ade97e1e88cf1421f09a7723412c8b76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915497"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>ドライバー 3.5 をドライバー 3.8 にアップグレードする
このトピックでは、ガイドラインと、ODBC 3.8 ドライバーに、ODBC 3.5 ドライバーをアップグレードするための考慮事項を提供します。  
  
##### <a name="version-numbers"></a>バージョン番号  
 次のガイドラインは、バージョン番号に関連しています。  
  
-   ドライバーは、SQL_OV_ODBC2、SQL_OV_ODBC3、および SQL_OV_ODBC3_80 以外の値の SQL_ERROR を返す SQL_ATTR_ODBC_VERSION の SQL_OV_ODBC3_80 をサポートする必要があります。 将来のバージョンのドライバー マネージャーは、ドライバーでは、ドライバーはから SQL_SUCCESS を返す場合に、ODBC のコンプライアンス レベルがサポートするいると仮定して[SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)します。  
  
-   バージョン 3.8 ドライバーから 03.80 を返す必要があります**SQLGetInfo** SQL_DRIVER_ODBC_VER に渡された場合*情報の種類*します。 ただし、古いドライバー マネージャーでは、Microsoft Windows の以前のバージョンに含まれていたはバージョン 3.5 のドライバー、ドライバーを処理し、警告を発行します。  
  
     Windows 7 では、ドライバー マネージャーのバージョンは、03.80 が。 Windows 8 のドライバー マネージャーのバージョンは SQLGetInfo SQL_DM_VER を介して 03.81 (*情報の種類*パラメーター)。 SQL_ODBC_VER 03.80 Windows 7 および Windows 8 の両方でバージョンを報告します。  
  
##### <a name="driver-specific-c-data-types"></a>ドライバー固有の C データ型  
 バージョン 3.8 の ODBC アプリケーションでうまく機能するときに、ドライバーが C データ型をカスタマイズしていることができます。 (詳細については、次を参照してください[ODBC における C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。)。ただし、3.8 のドライバー、ドライバー固有の C 型を実装するための要件はありません。 ドライバーは、C の型の範囲チェックを実行する必要がありますもが、ドライバー マネージャーは行いませんを 3.8 ドライバー。 ドライバーの開発を容易にドライバー固有の C データ型の値は、次の形式で定義できます。  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性  
 新しいドライバーを開発する場合は、データ型、記述子の種類、情報の種類、診断型、および属性のドライバー固有の範囲を使用する必要があります。 ドライバー固有の範囲とその基本型の値は、後ほど[ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)します。  
  
##### <a name="connection-pooling"></a>接続のプール  
 接続プールのより優れた管理は、ODBC 3.8 に SQL_ATTR_RESET_CONNECTION 接続属性が導入されています**SQLSetConnectAttr**します。 SQL_RESET_CONNECTION_YES は、この属性の唯一の有効な値です。 ドライバー マネージャーは、ドライバー、その他の接続属性を既定値にリセットすることができますの接続プール内の接続を配置する前に、SQL_ATTR_RESET_CONNECTION が設定されます。  
  
 サーバーとの不要な通信を避けるためには、ドライバーは、接続がプールから再利用後に再設定、リモート サーバーで次の通信まで、接続属性を延期できます。  
  
 SQL_ATTR_RESET_CONNECTION がドライバー マネージャーとドライバーの間の通信にのみ使用されるに注意してください。 アプリケーションでは、直接この属性を設定できません。 バージョン 3.8 のすべてのドライバーでは、この接続属性を実装する必要があります。  
  
##### <a name="streamed-output-parameters"></a>ストリームの出力パラメーター  
 ODBC バージョン 3.8 は、出力パラメーターを取得する、ストリームの出力パラメーターをよりスケーラブルな方法を紹介します。 (詳細については、次を参照してください[SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。)。この機能をサポートするドライバーをする必要があります設定 SQL_GD_OUTPUT_PARAMS 戻り値の SQL_GETDATA_EXTENSIONS が、*情報の種類*で、 **SQLGetInfo**呼び出します。 ストリームの出力パラメーターを持つ SQL の型のサポートは、ドライバーに実装する必要があります。 ドライバー マネージャーでは、無効な SQL 型のエラーは生成されません。 ストリーミングされる出力パラメーターをサポートする SQL 型は、ドライバーで定義されます。  
  
 アプリケーションが使用されている場合、ドライバーは SQL_ERROR を返す必要があります**SQLGetData**によって返されるパラメーターと同じではないパラメーターを取得する**SQLParamData**します。  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>接続操作 (ポーリング メソッド) の非同期の実行  
 ドライバーは、さまざまな接続の操作の非同期サポートを有効にできます。  
  
 ODBC では Windows 7 以降では、ポーリング メソッド (詳細については、次を参照してください。[非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)します。 接続ハンドルで非同期操作を実装するために、バージョン 3.8 の ODBC ドライバーの要件はありません。 ドライバーが、SQL_ASYNC_DBC_FUNCTIONS を実装する必要がありますも、ドライバーが接続ハンドルで非同期操作を実装していない場合でも*情報の種類*戻って**SQL_ASYNC_DBC_NOT_CAPABLE**します。  
  
 非同期接続の操作を有効にすると、接続操作の実行時間、繰り返しのすべての呼び出しの合計時間です。 最後の呼び出しは、時間の合計が、SQL_ATTR_CONNECTION_TIMEOUT 接続属性で設定された値を超えていて、操作が完了していません後に発生しますを繰り返し、場合、ドライバーは SQL_ERROR を返しますと、SQLState HYT01 を使用して診断レコードを記録し、。メッセージの「接続のタイムアウトが期限切れ」です。 操作が完了している場合、タイムアウトはありません。  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 関数  
 ODBC 3.8 サポート[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)接続とステートメントの両方の操作のキャンセルに使用されます。 サポートするドライバー **SQLCancelHandle**関数をエクスポートする必要があります。 ドライバーは、アプリケーションから呼び出す場合は、進行中の任意の同期または非同期接続関数をキャンセルしないでください**SQLCancel**または**SQLCancelHandle**ステートメント ハンドルでします。 同様に、ドライバーが、アプリケーションから呼び出す場合、進行中は任意のステートメントを同期または非同期関数をキャンセルしないでください**SQLCancelHandle**接続ハンドル。 また、ドライバーが閲覧操作をキャンセルする必要があります (**SQLBrowseConnect** SQL_NEED_DATA を返します)、アプリケーションから呼び出す場合**SQLCancelHandle**接続ハンドル。 このような場合は、ドライバーは HY010、「関数のシーケンス エラー」を返す必要があります。  
  
 両方をサポートする必要はありません**SQLCancelHandle**と同時に操作を非同期接続します。 ドライバーは、非同期接続の操作をサポートできますが**SQLCancelHandle**、またはその逆です。  
  
##### <a name="suspended-connections"></a>中断状態の接続  
 ODBC 3.8 ドライバー マネージャーは、接続を中断状態に配置できます。 アプリケーションが呼び出す**SQLDisconnect**接続に関連付けられたリソースを解放します。 この場合、ドライバーは接続の状態をチェックせず、できるだけ多くのリソースを解放するください。 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。  
  
##### <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール  
 Windows 8 での ODBC では、接続プールの動作をカスタマイズするドライバーを許可します。 詳細については、次を参照してください。[ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。  
  
##### <a name="asynchronous-execution-notification-method"></a>非同期実行 (通知方法)  
 ODBC 3.8 は、Windows 8 以降、非同期操作の通知方法をサポートします。 詳細については、次を参照してください。[非同期実行 (通知方法)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)します。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 提供の ODBC ドライバー](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
