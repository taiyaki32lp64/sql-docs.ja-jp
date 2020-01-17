---
title: FILESTREAM のサポート |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75c5d2f0f04cf0692f4a6c6ca3145210fee014b3
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308064"
---
# <a name="filestream-support"></a>FILESTREAM のサポート
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  FILESTREAM を使用すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を経由するか、Windows ファイル システムに直接アクセスすることで、大きなバイナリ値の格納やアクセスが可能になります。 大きなバイナリ値とは、2 ギガバイト (GB) よりも大きい値です。 拡張された FILESTREAM サポートの詳細については、「 [filestream &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)」を参照してください。  
  
 データベース接続を開い** \@ \@** たときに、既定では、値の設定が-1 ("無制限") に設定されます。  
  
 Windows ファイル システムの API を使用して、FILESTREAM 列にアクセスし、更新することもできます。  
  
 詳細については、次のトピックを参照してください。  
  
-   [FILESTREAM サポート &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM のサポート &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [OpenSqlFilestream による FILESTREAM データへのアクセス](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>FILESTREAM 列のクエリ  
 OLE DB のスキーマ行セットでは、列が FILESTREAM 列かどうかは報告されません。 また、OLE DB の ITableDefinition を使用して FILESTREAM 列を作成することはできません。  
  
 ODBC の SQLColumns などのカタログ関数では、列が FILESTREAM 列かどうかは報告されません。  
  
 FILESTREAM 列を作成する場合や、既存の FILESTREAM 列を検出する場合は、**sys.columns** カタログ ビューの [is_filestream](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 列を使用できます。  
  
 例を次に示します。  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>下位互換性  
 クライアントが、に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]含ま[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]れていたバージョンの Native client を使用してコンパイルされ、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]アプリケーションがに接続している場合、 **varbinary (max)** の動作はと[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]互換性があります。 返されるデータの最大サイズが 2 GB に制限されます。 戻り値が 2 GB より大きい場合は切り捨てが行われ、"文字列データの右側が切り捨てられました" という警告が返されます。  
  
 データ型の互換性が 80 に設定されている場合は、クライアントの動作で下位クライアントとの互換性が維持されます。  
  
 ネイティブクライアントの[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]バージョンより前にリリースされた SQLOLEDB またはその他のプロバイダーを使用するクライアントでは、 **varbinary (max)** は image にマップされます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client 機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
