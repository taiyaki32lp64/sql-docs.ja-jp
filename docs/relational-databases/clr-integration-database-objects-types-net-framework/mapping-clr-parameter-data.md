---
title: CLR パラメーター データのマッピング |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 530db4d31d3db4773713816f1b68404990997512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081311"
---
# <a name="mapping-clr-parameter-data"></a>CLR パラメーター データのマッピング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  次の表[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型の場合の共通言語ランタイム (CLR) の同等の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で、 **System.Data.SqlTypes**名前空間と、 、ネイティブのCLR同等物[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework です。  
  
||||  
|-|-|-|  
|**SQL Server データ型**|型 (System.Data.SqlTypes または Microsoft.SqlServer.Types)|**CLR データ型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64 では、null 許容\<Int64 >**|  
|**binary**|**SqlBytes、SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**ブール値、null 値許容\<ブール >**|  
|**char**|なし|なし|  
|**cursor**|なし|なし|  
|**date**|**SqlDateTime**|**DateTime、null 許容\<DateTime >**|  
|**datetime**|**SqlDateTime**|**DateTime、null 許容\<DateTime >**|  
|**datetime2**|なし|**DateTime、null 許容\<DateTime >**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset では、null 許容\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**10 進数、null 値許容\<Decimal >**|  
|**float**|**SqlDouble**|**Null 値は二重\<Double >**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography**は SQL Server と共にインストールされからダウンロードできます。 これには、Microsoft.SqlServer.Types.dll に定義されて、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [機能パック](https://www.microsoft.com/download/details.aspx?id=52676)します。|なし|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry**は SQL Server と共にインストールされからダウンロードできます。 これには、Microsoft.SqlServer.Types.dll に定義されて、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [機能パック](https://www.microsoft.com/download/details.aspx?id=52676)します。|なし|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**は SQL Server と共にインストールされからダウンロードできます。 これには、Microsoft.SqlServer.Types.dll に定義されて、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [機能パック](https://www.microsoft.com/download/details.aspx?id=52676)します。|なし|  
|**image**|なし|なし|  
|**int**|**SqlInt32**|**Null 許容の Int32\<Int32 >**|  
|**money**|**SqlMoney**|**10 進数、null 値許容\<Decimal >**|  
|**nchar**|**SqlChars、SqlString**|**String、char[]**|  
|**ntext**|なし|なし|  
|**numeric**|**SqlDecimal**|**10 進数、null 値許容\<Decimal >**|  
|**nvarchar**|**SqlChars、SqlString**<br /><br /> **SQLChars**データ転送とアクセスに適しているは、 **SQLString**文字列操作の実行に適しているのです。|**String、char[]**|  
|**nvarchar (1)、nchar (1)**|**SqlChars、SqlString**|**Char、String、char[]、Nullable\<char >**|  
|**real**|**SqlSingle** (範囲**SqlSingle**、ただしがより大きい**実際**)|**1 つ、null 値許容\<単一 >**|  
|**rowversion**|なし|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16 型、null 許容\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**10 進数、null 値許容\<Decimal >**|  
|**sql_variant**|なし|**Object**|  
|**table**|なし|なし|  
|**text**|なし|なし|  
|**time**|なし|**TimeSpan、null 許容\<TimeSpan >**|  
|**timestamp**|なし|なし|  
|**tinyint**|**SqlByte**|**バイトの null 許容\<バイト >**|  
|**uniqueidentifier**|**SqlGuid**|**Guid、null 許容\<Guid >**|  
|**User-defined type(UDT)**|なし|同じアセンブリまたは依存アセンブリ内のユーザー定義型にバインドされている同じクラス|  
|**varbinary**|**SqlBytes、SqlBinary**|**Byte[]**|  
|**varbinary(1)、binary(1)**|**SqlBytes、SqlBinary**|**バイトの byte[]、Nullable\<バイト >**|  
|**varchar**|なし|なし|  
|**xml**|**SqlXml**|なし|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>out パラメーターによるデータ型の自動変換  
 CLR メソッドは、呼び出し元のコードまたはプログラムに情報を入力のパラメーターをマークすることで返すことができます、**アウト**修飾子 (Microsoft Visual c#) または **\<Out() > ByRef** (Microsoft Visual Basic)入力パラメーターが CLR データ型、 **System.Data.SqlTypes**名前空間、および呼び出し元のプログラムは、等価なを指定します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型変換が自動的に行われる入力パラメーターとしてのデータの型ときに、CLR メソッドは、データ型を返します。  
  
 たとえば、次の CLR ストアド プロシージャには、入力パラメーターの**SqlInt32**でマークされている CLR データ型**アウト**(c#) または **\<Out() > ByRef** (Visual Basic の場合):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 ストアド プロシージャが作成された後、アセンブリがビルドされ、データベースが作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を指定すると、次の TRANSACT-SQL をかけ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータ型**int**出力パラメーターとして。  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR ストアド プロシージャが呼び出されると、 **SqlInt32**データ型が自動的に変換、 **int**データ型、呼び出し元のプログラムに返されます。  
  
 ただし、out パラメーターにより自動的にすべての CLR データ型を同等な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に変換できるとは限りません。 次の表に、これらの例外を示します。  
  
|||  
|-|-|  
|**CLR データ型 (SQL Server)**|**SQL Server データ型**|  
|**Decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>変更履歴  
  
|変更内容|  
|---------------------|  
|追加**SqlGeography**、 **SqlGeometry**、および**SqlHierarchyId**マッピング テーブルの種類。|  
  
## <a name="see-also"></a>参照  
 [.NET Framework での SQL Server データ型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
