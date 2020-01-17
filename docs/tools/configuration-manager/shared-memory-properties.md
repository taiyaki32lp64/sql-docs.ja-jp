---
title: 共有メモリのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 17a251e25eaf02ee0733f6d00a077bd4706db29a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058328"
---
# <a name="shared-memory-properties"></a>[共有メモリのプロパティ] ダイアログ ボックス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **[共有メモリのプロパティ]** ダイアログ ボックスの **[プロトコル]** ページは、共有メモリ プロトコルを有効または無効にするために使用します。 共有メモリは、使用できる最も単純なプロトコルであり、構成可能な設定はありません。 共有メモリ プロトコルを使用するクライアントは、同じコンピューター上で実行されている [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにしか接続できないため、ほとんどのデータベース操作にとって実用的ではありません。 共有メモリ プロトコルは、他のプロトコルが正しく構成されていない可能性がある場合に、トラブルシューティングを行うために使用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動しないと、このプロトコルを有効または無効にできません。  
  
## <a name="options"></a>オプション  
 **有効**  
 可能な値は、 **[はい]** と **[いいえ]** です。 既定では、共有メモリ プロトコルは有効になっています。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [共有メモリ プロトコルを使用した有効な接続文字列の作成](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
