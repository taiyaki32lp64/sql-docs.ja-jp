---
title: スキーマ行セットのサポート (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b6ea8594d22527f2f9b87a77d70671c5724111
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625967"
---
# <a name="schema-rowset-support-ole-db"></a>スキーマ行セットのサポート (OLE DB)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、処理するときにも、リンク サーバーから返されるスキーマ情報をサポート[!INCLUDE[tsql](../../../includes/tsql-md.md)]分散クエリ。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではシノニムがサポートされていますが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ではシノニムのメタデータは返されません。  
  
 スキーマ行セットの一覧とでサポートされる制限列を以下に示します、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。  
  
|スキーマ行セット|制限列|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME、GRANTOR、GRANTEE|  
|DBSCHEMA_COLUMNS|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME<br /><br /> 次の追加の列は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に固有のものです。<br /><br /> -COLUMN_LCID。 照合順序のロケール ID です。 COLUMN_LCID の値は Windows LCID と同じです。<br />-照合順序のサポートされる比較 COLUMN_COMPFLAGS を定義します。 データ形式は DBPROB_FINDCOMPAREOPS と同じです。<br />-COLUMN_SORTID は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]並べ替えの照合順序のスタイル。<br />-COLUMN_TDSCOLLATION は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]列の照合順序。<br />-IS_COMPUTED、計算列と VARIANT_FALSE がそれ以外の場合は、列の場合は VARIANT_TRUE をします。|  
|DBSCHEMA_FOREIGN_KEYS|すべての制限がサポートされます。<br /><br /> PK_TABLE_CATALOG、PK_TABLE_SCHEMA、PK_TABLE_NAME、FK_TABLE_CATALOG、FK_TABLE_SCHEMA、FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|制限 1、2、3、および 5 がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、INDEX_NAME、TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|すべての制限がサポートされます。<br /><br /> PROCEDURE_CATALOG、PROCEDURE_SCHEMA、PROCEDURE_NAME、PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|制限 1、2、および 3 がサポートされます。<br /><br /> PROCEDURE_CATALOG、PROCEDURE_SCHEMA、PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES は、現在のユーザーによって実行可能なプロシージャまたは現在のユーザーに VIEW DEFINITION 権限が付与されているプロシージャのみを返します。|  
|DBSCHEMA_PROVIDER_TYPES|すべての制限がサポートされます。<br /><br /> DATA_TYPE、BEST_MATCH|  
|DBSCHEMA_SCHEMATA|すべての制限がサポートされます。<br /><br /> CATALOG_NAME、SCHEMA_NAME、SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|すべての制限がサポートされます。<br /><br /> CONSTRAINT_CATALOG、CONSTRAINT_SCHEMA、CONSTRAINT_NAME、TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、GRANTOR、GRANTEE|  
|DBSCHEMA_TABLES|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|すべての制限がサポートされます。<br /><br /> TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、TABLE_TYPE|  
  
## <a name="in-this-section"></a>このセクションの内容  
 [スキーマ行セットでの分散クエリのサポート](schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 行セット&#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)   
 [ユーザー定義型の使用](../features/using-user-defined-types.md)  
  
  
