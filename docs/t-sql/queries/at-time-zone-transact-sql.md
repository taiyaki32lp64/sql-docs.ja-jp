---
title: AT TIME ZONE (Transact-SQL) | Microsoft Docs
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current||=azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: ff3d3db1ab4fc3d02e8710cf482225523285c0a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031525"
---
# <a name="at-time-zone-transact-sql"></a>AT TIME ZONE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  *inputdate* を対応する *datetimeoffset* 値に変換先のタイム ゾーンで変換します。 *inputdate* がオフセット情報なしで提供されると、この関数は、*inputdate* が変換先のタイム ゾーン内であるものと想定して、タイム ゾーンのオフセットを適用します。 *inputdate* が *datetimeoffset* 値として与えられる場合、**AT TIME ZONE** 句はタイム ゾーン変換規則を利用して変換先のタイム ゾーンにそれを変換します。  
  
 **AT TIME ZONE** の実装は、タイム ゾーン間で **datetime** 値を変換する Windows メカニズムに依存します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>引数  
 *inputdate*  
 **smalldatetime**、**datetime**、**datetime2**、**datetimeoffset** 値に解決できる式です。  
  
 *timezone*  
 変換先のタイム ゾーンの名前。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Windows レジストリに格納されているタイム ゾーンに依存します。 コンピューターにインストールされているタイム ゾーンは、次のレジストリ ハイブに格納されています:**KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**。 インストールされているタイム ゾーンの一覧は [sys.time_zone_info &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) ビューでも閲覧できます。  
  
## <a name="return-types"></a>戻り値の型  
 **datetimeoffset** のデータ型を返します。  
  
## <a name="return-value"></a>戻り値  
 変換先のタイム ゾーンの **datetimeoffset** 値。  
  
## <a name="remarks"></a>Remarks  
 **AT TIME ZONE** は、データ型 **smalldatetime**、**datetime**、**datetime2** の入力値が DST 変更の影響を受ける時間間隔に分類されるとき、特別な入力値変換ルールを適用します。  
  
-   時計が進んでいると、現地時刻には時計調整の継続時間と等しい隔たりが存在します。 この継続時間は通常は 1 時間ですが、タイム ゾーンによっては 30 分または 45 分の場合もあります。 DST 変更の "*後*" で、この隔たり内にある時点はオフセットで変換されます。  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- 時計が遅れていると、現地時刻の 2 時間が重なり、1 時間になります。  その場合、時計変更の*前*に、重なる時間間隔に属する時点がオフセットで表されます。  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

一部の情報 (タイム ゾーン ルールなど) は [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] の外で保守管理され、時折変更されるため、**AT TIME ZONE** 関数は非決定的として分類されます。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. オフセット情報なしで、変換先のタイム ゾーンのオフセットを datetime に追加する  
 元の **datetime** 値が同じタイム ゾーンで与えられることがわかっているとき、タイム ゾーン ルールに基づいてオフセットを追加するには、**AT TIME ZONE** を使用します。  
  
```sql
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. 異なるタイム ゾーン間で値を変換する  
 次の例では、異なるタイム ゾーン間で値を変更します。  
  
```sql
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. ローカル タイム ゾーンでテンポラル テーブルにクエリを実行する  
 次の例では、テンポラル テーブルからデータを選択します。  
  
```sql
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>参照  
 [日付型と時刻型](../../t-sql/data-types/date-and-time-types.md)   
 [日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
