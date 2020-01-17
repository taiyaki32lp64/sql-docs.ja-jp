---
title: 型 xs:dateTime、xs:date 型、および xs:time のストレージ形式への変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xs:date
- xs:time
- storage format
- DateTime
ms.assetid: b9f758df-030c-4aec-8ade-1bf904aa2c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f631783aad92757edd4faae41cd43c06c431887
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096604"
---
# <a name="changes-to-the-storage-format-for-types-xsdatetime-xsdate-and-xstime"></a>xs:dateTime 型、xs:date 型、および xs:time 型のストレージ形式の変更
  XMLDATETIME ルールでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのアップグレード後に無効になる型指定された XML データがデータベースに含まれているかどうかが確認されます。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 ストレージ形式[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]型 xs:dateTime、xs:date 型、および xs:time が変更された値のタイム ゾーン情報の有無をサポートし、タイム ゾーンの保存を許可します。  
  
 XML スキーマ コレクションがこのいずれかの型を参照している場合は、コレクションに関連付けられているすべての列の XML インデックスが、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのアップグレード後に無効になります。 これらの型に対しては、SELECT または XQUERIES (またはその両方) を使用してクエリを実行できますが、XML インデックスは使用されません。 負の年の値が検出された場合は、実行時エラーが発生します。  
  
 また、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では負の年の値がサポートされません。  
  
 XMLDATETIME ルールでは、影響を受ける型のいずれかを参照している XML スキーマ コレクションがあるかどうか、およびそのようなコレクションによって型指定された XML 列が存在するかどうかがチェックされます。  
  
## <a name="corrective-action"></a>修正措置  
 xs:date、xs:time、または xs:dateTime を参照するスキーマ コレクションに従って型指定された XML 列が存在することが XMLDATETIME ルールによって確認された場合は、データ内に負の年の値があるかどうかをまず見つけ出す必要があります。 このような値があると、アップグレード後に XML インデックスを再構築できません。  
  
 次に示すクエリでは、影響を受ける型を参照する XML スキーマ コレクション、および型指定された個々の XML 列を検索します。 これにより、負の年を値に持つインスタンスが存在するかどうかがわかります。  
  
```sql
CREATE PROCEDURE DateTimeInvestigation(@withdata bit)  
-- @withdata = 0: only get the affected meta data information  
-- @withdata = 1: get the affected meta data and instance information  
AS  
BEGIN  
-- First get XML containing all schema collections containing affected element and attributes  
-- components (model groups?)   
-- and columns that are affected by the schema collections.   
CREATE table #_dt_collector(x xml);   
;with dttypes as  
  (SELECT * FROM sys.xml_schema_components   
   where base_xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
      )   
   union all  
   SELECT * FROM sys.xml_schema_components  
   where xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
       or kind='N' or kind='Z')   
   ),   
dtplaced as  
  (SELECT scp.*   
   FROM sys.xml_schema_component_placements scp   
   JOIN dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
  )   
insert into #_dt_collector SELECT x FROM (SELECT  
  xsc.xml_collection_id as "@collid"  
, s.name as "@schema"  
, xscol.name as "@name"  
, count(xsc.xml_component_id) as "@affected_elems_and_attrs"  
, (SELECT S.Name as "@schema", T.Name as "@table"  
        , C.Name as "@column"   
   FROM sys.columns C   
   JOIN sys.tables T ON C.object_id = T.object_id  
   JOIN sys.schemas S ON S.schema_id = T.schema_id  
   WHERE C.xml_collection_id = xsc.xml_collection_id  
   FOR XML PATH('Columns'), TYPE  
  )   
FROM sys.xml_schema_components xsc  
JOIN dtplaced on xsc.xml_component_id=dtplaced.xml_component_id  
JOIN sys.xml_schema_collections xscol on xsc.xml_collection_id =xscol.xml_collection_id  
JOIN sys.schemas s on xscol.schema_id=s.schema_id  
group by xsc.xml_collection_id, s.name, xscol.name  
FOR XML PATH('XML_Schema_Collections'), TYPE) as T(x);   
if (@withdata = 0)    
  BEGIN  
  SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
  drop table #_dt_collector;   
  return;   
  END;   
-- Declare cursor to find all columns bound to the schema collections  
DECLARE C CURSOR FOR  
SELECT S.Name, T.Name, C.Name   
FROM sys.columns C   
JOIN sys.tables T ON C.object_id = T.object_id  
JOIN sys.schemas S ON S.schema_id = T.schema_id  
WHERE C.xml_collection_id  
IN (SELECT distinct xsc.xml_collection_id  
    FROM sys.xml_schema_components xsc  
    JOIN (SELECT scp.*   
          FROM sys.xml_schema_component_placements scp   
          JOIN (SELECT * FROM sys.xml_schema_components   
                where base_xml_component_id    
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                   )   
                union all  
                SELECT * FROM sys.xml_schema_components  
                where xml_component_id   
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                    or kind='N' or kind='Z')   
               ) dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
          ) dtplaced on xsc.xml_component_id=dtplaced.xml_component_id);   
DECLARE @SchemaName nvarchar(max);   
DECLARE @TableName nvarchar(max);   
DECLARE @ColumnName nvarchar(max);   
DECLARE @strSQL nvarchar(MAX);   
OPEN C;   
FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
WHILE (@@FETCH_STATUS = 0)   
BEGIN  
      SET @strSQL = 'INSERT INTO #_dt_collector SELECT x FROM ( ';   
      SET @strSQL = @strSQL +    
                    'SELECT ''' + @SchemaName + '.' + @TableName + '.' + @ColumnName   
                  + ''' as "@Column", ';   
      SET @strSQL = @strSQL +    
      'sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)])'', ''bigint'')) as "@dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)])'', ''bigint'')) as "@date_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_date_elements"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)  
                      where $v instance of xs:dateTime?   
                      return 1)'', ''bigint'')) as "@dT_attributes"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:dateTime?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_dt_attributes"  
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      return 1)'', ''bigint'')) as "@date_attributes"   
     , sum('+ @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_date_attributes"'  
      + ' FROM ' + @SchemaName + '.' + @TableName  
      + ' FOR XML PATH(''data''), type) T(x)';   
      --SELECT @strSQL;   
      EXEC sp_executesql @strSQL;   
      FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
END;   
CLOSE C;   
DEALLOCATE C;   
SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
drop table #_dt_collector;   
END;   
go  
-- Get the dependent columns per affected XML Schema Collection and the  
-- number of affected values  
EXECUTE DateTimeInvestigation 1;   
```  
  
 負の年の値が見つかった場合は、複数の解決策があります。  
  
-   行を削除します。  
  
-   見つかった値を更新します。  
  
-   XML 列全体をクリアします。  
  
-   xs:date または xs:dateTime を使用しないスキーマ コレクションで、XML 列の型を再指定します (たとえば xs:string を使用します)。  
  
 負の年の問題を調整したら、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードできます。  
  
 アップグレード後に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で XML インデックスを使用するには、xs:date、xs:time、または xs:dateTime を使用するすべての列について、XML インデックスを再構築するか、XML 列の型を再指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
