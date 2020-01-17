---
title: SSMA for DB2 コンポーネント (DB2ToSQL) の削除 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 25c8222009c2ea9358c0bab2ad5ae077588fb3cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060092"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>SSMA for DB2 コンポーネント (DB2ToSQL) の削除
終了したらを DB2 からデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA コンポーネントをアンインストールしたい場合があります。 クライアント コンポーネントは、いつでもアンインストールできます。 ただしから拡張機能パックをアンインストールする必要がありますいない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、移行されたデータベースが不要になった内の関数を使用しない限り、 **ssma_DB2**のスキーマ、 **sysdb**データベース。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>SSMA を DB2 クライアントのアンインストール  
SSMA をアンインストールするにを使用して**プログラム追加と削除**します。  
  
**SSMA をアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**、 をクリックし、**削除**します。  
  
3.  SSMA をアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックをアンインストールします。  
データベースを移行は、内のオブジェクトを使用しない場合は、確認、 **sysdb.ssma_DB2**スキーマ、スキーマから削除することによって、拡張機能パックを削除することができます - Windows のアンインストールはありません  
  
## <a name="see-also"></a>関連項目  
[SSMA for DB2 クライアントのインストール&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server での SSMA コンポーネントのインストール&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
