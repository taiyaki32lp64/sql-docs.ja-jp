---
title: SQL Server 2005 Native Client からのアプリケーションの更新 | Microsoft Docs
description: SQL Server 2005 Native Client からのアプリケーションの更新
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989249"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client からのアプリケーションの更新
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  このトピックでは、の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]Native Client 以降の OLE DB Driver for SQL Server における重大な変更について説明します。  

 Microsoft Data Access Components (MDAC) を OLE DB Driver for SQL Server にアップグレードした場合も、一部の動作で違いが生じます。 詳細については、「 [MDAC から OLE DB Driver for SQL Server にアプリケーションを更新する](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)」を参照してください。  

 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] に付属する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] に付属する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属する [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] に付属する [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0。  

|Native Client と比較して OLE DB Driver for [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SQL Server の動作が変更されました|[説明]|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB によって定義された有効桁数までしか埋め込まれない|変換されたデータがサーバーに送信される変換の場合、OLE DB Driver for SQL Server は、 **datetime**値の最大長までデータの後続のゼロを埋め込みます。 SQL Server Native Client 9.0 では、9 桁まで埋め込まれていました。|  
|ICommandWithParameter:: SetParameterInfo の DBTYPE_DBTIMESTAMP を検証します。|OLE DB Driver for SQL Server は、ICommandWithParameter:: SetParameterInfo の*Bscale*の OLE DB 要件を実装して、DBTYPE_DBTIMESTAMP の秒の小数部の精度に設定されるようにします。|  
|**Sp_columns**ストアドプロシージャでは、IS_NULLABLE 列に対して " **no** " ではなく **"no"** が返されるようになりました。|OLE DB Driver for SQL Server では、 **sp_columns**ストアドプロシージャは、IS_NULLABLE 列に対して " **no** " ではなく **"no"** を返すようになりました。|  
|日付が範囲外の場合に別のエラーが返される|**Datetime**型では、以前のバージョンで返された範囲外の日付について、OLE DB Driver によって別 SQL Server のエラー番号が返されます。<br /><br /> 具体的に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は、Native Client 9.0 は、文字列を**datetime**に変換するときに、すべての範囲の年の値が22007を返し、OLE DB Driver for SQL Server は、日付が**datetime2**でサポートされている範囲内ではなく22008を返します。**datetime**または**smalldatetime**でサポートされる範囲です。|  
|丸め処理によって日が変わる場合に **datetime** 値では秒の小数部が丸められずに切り捨てられる。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前のバージョンでは、サーバーに送信される **datetime** 値は、クライアントによって 1/300 秒単位に丸められていました。 OLE DB Driver for SQL Server では、このシナリオでは、丸め処理によって日が変化する場合、秒の小数部が切り捨てられます。|  
|**Datetime**値に使用できる切り捨て秒数。|OLE DB Driver for SQL Server でビルドしたアプリケーションが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 サーバーに接続する場合、型識別子を DBTYPE_DBTIMESTAMP (OLE DB) または SQL_TIMESTAMP (ODBC) に設定し、小数点以下桁数を 0 に設定して datetime 列にバインドすると、サーバーに送信されるデータの時刻部分の秒および秒の小数部が切り捨てられます。<br /><br /> 例:<br /><br /> 入力データ: 1994-08-21 21:21:36.000<br /><br /> 挿入されるデータ: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME から DBTYPE_DATE への OLE DB データ変換で日が変更されなくなる|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前のバージョンでは、DBTYPE_DATE の時刻部分が午前 0 時から 0.5 秒以内の場合、OLE DB の変換コードによって日が変更されました。 OLE DB Driver for SQL Server では、日は変更されません (秒の小数部は切り捨てられ、丸められません)。|  
|IBCPSession:: BCColFmt 変換の変更。|SQL Server 用の OLE DB ドライバーでは、IBCPSession:: BCOColFmt を使用して SQLDATETIME または SQLDATETIME を文字列型に変換すると、小数値がエクスポートされます。 たとえば、SQLDATETIME 型を SQLNVARCHARMAX 型に変換すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 より前のバージョンでは、<br /> 1989-02-01 00:00:00 が返されます。<br />OLE DB Driver for SQL Server では、 <br />1989-02-01 00:00:00.0000000 が返されます。|  
|BCP API を使用するカスタム アプリケーションで警告が表示される|指定されたフィールド長をデータ長が上回る場合、どの型の場合でも BCP API によって警告メッセージが生成されます。 以前のバージョンでは、この警告は、すべての型ではなく文字型についてのみ表示されました。|  
|日付型または時刻型としてバインドされた **sql_variant** に空の文字列を挿入するとエラーが生成される。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 では、日付型または時刻型としてバインドされた **sql_variant** に空の文字列を挿入してもエラーは生成されませんでした。 OLE DB Driver for SQL Server では、このような状況でエラーが正しく生成されます。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、トリガーの実行時に異なる結果を返す場合がある|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] で導入された変更により、**NOCOUNT OFF** が有効なときに、トリガーを実行させたステートメントからアプリケーションに返される結果が異なる可能性があります。 このような場合、アプリケーションでエラーが発生することがあります。 このエラーを解決するには、トリガーで**NOCOUNT on**を設定します。|  

## <a name="see-also"></a>参照   
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)
