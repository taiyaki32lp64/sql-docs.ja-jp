---
title: SQL Server インデックスの削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14b54b80d18b79092ab46055477b59cb4ea6d5ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046394"
---
# <a name="dropping-a-sql-server-index"></a>SQL Server インデックスの削除
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが公開、 **iindexdefinition::dropindex**関数。 コンシューマーはこの関数を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルからインデックスを削除できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、複数公開されて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インデックスと主キーと UNIQUE 制約。 テーブル所有者、データベース所有者、一部の管理ロールのメンバーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを変更して、制約を削除できます。 既定では、テーブル所有者だけが既存のインデックスを削除できます。 したがって、**DropIndex** が成功するか失敗するかは、アプリケーション ユーザーのアクセス権だけでなく、指定されたインデックスの種類によっても異なります。  
  
 コンシューマーは、*pTableID* パラメーターの *uName* 共用体の *pwszName* メンバーに Unicode 文字列としてテーブル名を指定します。 *pTableID* の *eKind* メンバーを DBKIND_NAME にする必要があります。  
  
 インデックス名は、*pIndexID* パラメーターの *uName* 共用体の *pwszName* メンバーに Unicode 文字列で指定します。 *pIndexID* の *eKind* メンバーを DBKIND_NAME にする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがテーブルのすべてのインデックスを削除するの OLE DB の機能をサポートしていないときに*pIndexID*が null です。 *pIndexID* が NULL の場合、E_INVALIDARG を返します。  
  
## <a name="see-also"></a>参照  
 [テーブルとインデックス](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
