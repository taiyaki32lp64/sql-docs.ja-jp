---
title: SQL Server テーブルから列を削除する |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 919bd28a82171068349e4019bb1bd5c190d08cd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213916"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>SQL Server テーブルからの列の削除
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが公開、 **itabledefinition::dropcolumn**関数。 コンシューマーはこの関数を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルから列を削除できます。  
  
 コンシューマーはテーブル名は、*pTableID* パラメーターの *uName* 共用体の *pwszName* メンバーに Unicode 文字列で指定します。 *pTableID* の *eKind* メンバーを DBKIND_NAME にする必要があります。  
  
 コンシューマーで列の名前を示す、 *pwszName*のメンバー、 *uName*共用体の*pColumnID*パラメーター。 列名は Unicode 文字列で指定します。 *pColumnID* の *eKind* メンバーを DBKIND_NAME にする必要があります。  
  
## <a name="example"></a>例  
  
### <a name="code"></a>コード  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>参照  
 [テーブルとインデックス](tables-and-indexes.md)  
  
  
