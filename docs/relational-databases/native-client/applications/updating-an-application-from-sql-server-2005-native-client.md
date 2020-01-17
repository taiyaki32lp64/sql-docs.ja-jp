---
title: Native Client、update app SQL 2005
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2eddd2284ec77a1a4979389f964baeafb6932dc5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243810"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client からのアプリケーションの更新
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以降の [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client における重大な変更について説明します。  
  
 Microsoft Data Access Components (MDAC) を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client にアップグレードした場合も、一部の動作で違いが生じます。 詳細については、「 [MDAC から SQL Server Native Client するようにアプリケーションを更新する](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)」を参照してください。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属する [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 9.0。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属する [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 10.0。  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属する [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] に付属する [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0。  
  
|
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降の SQL Server Native Client で変更された動作|説明|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB によって定義された有効桁数までしか埋め込まれない|変換されたデータがサーバーに送信される[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]変換の場合、Native [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]Client (以降) では、 **datetime**値の最大長まで、データの後続のゼロが埋め込まれます。 SQL Server Native Client 9.0 では、9 桁まで埋め込まれていました。|  
|ICommandWithParameter:: SetParameterInfo の DBTYPE_DBTIMESTAMP を検証します。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (以降[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) では、ICommandWithParameter:: Setparameterinfo の*bscale*の OLE DB 要件を DBTYPE_DBTIMESTAMP の秒の小数部の有効桁数に設定する必要があります。|  
|**Sp_columns**ストアドプロシージャは、IS_NULLABLE 列に対して " **no** " ではなく **"no"** を返すようになりました。|Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 以降では、 **sp_columns**ストアドプロシージャは、IS_NULLABLE 列に対して " **no** " ではなく **"no"** を返すようになりました。|  
|SQLSetDescRec、SQLBindParameter、SQLBindCol が整合性チェックを実行するようになりました。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前では、SQL_DESC_DATA_PTR を設定しても、SQLSetDescRec、SQLBindParameter、または SQLBindCol の記述子の種類に対して整合性チェックを行うことができませんでした。|  
|SQLCopyDesc で、記述子の一貫性チェックが行われるようになりました。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前では、SQL_DESC_DATA_PTR フィールドが特定のレコードに設定されている場合、SQLCopyDesc は整合性チェックを実行しませんでした。|  
|SQLGetDescRec では、記述子の整合性チェックは行われなくなりました。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前では、SQLGetDescRec は SQL_DESC_DATA_PTR フィールドが設定されたときに記述子の整合性チェックを実行しました。 この一貫性チェックは、ODBC 仕様では不要になったため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 以降のバージョンでは行われなくなりました。|  
|日付が範囲外の場合に別のエラーが返される|**Datetime**型の場合、以前のバージョンで返された範囲[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外の日付につい[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]ては、Native Client (以降) によって別のエラー番号が返されます。<br /><br /> 具体的に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は、native client 9.0 では、文字列を**datetime**に変換するときの年の値[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]が範囲外の場合は 22007[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]が返され、バージョン 10.0 () 以降の native client では、日付が**datetime2**でサポートされている範囲内で**datetime**または**smalldatetime**でサポートされている範囲外の場合、22008が返されます。|  
|**datetime**値は、秒の小数部を切り捨てます。丸め処理によって日が変化する場合は丸められません。|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前のバージョンでは、サーバーに送信される **datetime** 値は、クライアントによって 1/300 秒単位に丸められていました。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降では、丸め処理によって日が変わる場合、秒の小数部が切り捨てられます。|  
|**Datetime**値に使用できる切り捨て秒数。|
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 以降でビルドしたアプリケーションが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 サーバーに接続する場合、型識別子を DBTYPE_DBTIMESTAMP (OLE DB) または SQL_TIMESTAMP (ODBC) に設定し、小数点以下桁数を 0 に設定して datetime 列にバインドすると、サーバーに送信されるデータの時刻部分の秒および秒の小数部が切り捨てられます。<br /><br /> 例:<br /><br /> 入力データ: 1994-08-21 21:21:36.000<br /><br /> 挿入されるデータ: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME から DBTYPE_DATE への OLE DB データ変換で日が変更されなくなる|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前のバージョンでは、DBTYPE_DATE の時刻部分が午前 0 時から 0.5 秒以内の場合、OLE DB の変換コードによって日が変更されました。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降では、日は変更されません (秒の小数部は丸められずに切り捨てられます)。|  
|IBCPSession:: BCColFmt 変換の変更。|Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 10.0 以降では、IBCPSession:: BCOColFmt を使用して sqldatetime または sqldatetime を文字列型に変換すると、小数値がエクスポートされます。 たとえば、SQLDATETIME 型を SQLNVARCHARMAX 型に変換すると、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、<br /><br /> 1989-02-01 00:00:00 が返されます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降のバージョンでは、1989-02-01 00:00:00.0000000 が返されます。|  
|送信するデータのサイズを SQL_LEN_DATA_AT_EXEC で指定した長さと一致させる必要がある|SQL_LEN_DATA_AT_EXEC を使用する場合、データのサイズを SQL_LEN_DATA_AT_EXEC で指定した長さと一致させる必要があります。 SQL_DATA_AT_EXEC を使用することはできますが、SQL_LEN_DATA_AT_EXEC を使用するとパフォーマンスが向上する可能性があります。|  
|BCP API を使用するカスタム アプリケーションで警告が表示される|指定されたフィールド長をデータ長が上回る場合、どの型の場合でも BCP API によって警告メッセージが生成されます。 以前のバージョンでは、この警告は、すべての型ではなく文字型についてのみ表示されました。|  
|日付型または時刻型としてバインドされた **sql_variant** に空の文字列を挿入するとエラーが生成される。|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 では、日付型または時刻型としてバインドされた **sql_variant** に空の文字列を挿入してもエラーは生成されませんでした。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 以降では、この場合に正しくエラーが生成されます。|  
|SQL_C_TYPE_TIMESTAMP と DBTYPE_DBTIMESTAMP のパラメーターの検証がより厳密に行われる|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client より前で**は、datetime 値は** **datetime**列と**smalldatetime**列の小数点以下[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]桁数に合わせて丸められました。 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 以降では、秒の小数部に対して、ODBC のコア仕様で定義されている、より厳密な検証規則が適用されます。 クライアントのバインドで明示的または暗黙的に指定された桁数を使用することによって、末尾の桁を切り捨てることなくパラメーター値を SQL 型に変換できない場合は、エラーが返されます。|  
|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、トリガーの実行時に異なる結果を返す場合がある|
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] で導入された変更により、**NOCOUNT OFF** が有効なときに、トリガーを実行させたステートメントからアプリケーションに返される結果が異なる可能性があります。 このような場合、アプリケーションでエラーが発生することがあります。 このエラーを解決するには、トリガーで**NOCOUNT on**を設定するか、SQLMoreResults を呼び出して次の結果に進みます。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
