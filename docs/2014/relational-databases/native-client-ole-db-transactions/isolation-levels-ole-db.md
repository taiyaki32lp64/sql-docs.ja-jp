---
title: 分離レベル (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a18986af71f652a833f413ee1fa62ca2fd44ba06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63215993"
---
# <a name="isolation-levels-ole-db"></a>分離レベル (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは、接続のトランザクション分離レベルを制御できます。 トランザクション分離レベルを制御する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーの使用。  
  
-   DBPROPSET_SESSION プロパティの DBPROP_SESS_AUTOCOMMITISOLEVELS を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーの既定の自動コミット モード。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの既定のレベルは、DBPROPVAL_TI_READCOMMITTED です。  
  
-   ローカルの手動コミット トランザクションには、**ITransactionLocal::StartTransaction** メソッドの *isoLevel* パラメーター。  
  
-   MS DTC でコーディネートされる分散トランザクションには、**ITransactionDispenser::BeginTransaction** メソッドの *isoLevel* パラメーター。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ダーティ リード分離レベルでの読み取り専用アクセスを許可します。 他のすべてのレベルでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトにロックをかけることによってコンカレンシーを制限します。 クライアントがより高度なコンカレンシー レベルを要求すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はデータへのコンカレント アクセスに対してより厳密な制限を適用します。 最高レベルのデータへの同時アクセスを維持するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーがその要求の特定の同時実行レベルを適切に制御する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ではスナップショット分離レベルが導入されました。 詳細については、「[スナップショット分離を使用した作業](../native-client/features/working-with-snapshot-isolation.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [トランザクション](transactions.md)  
  
  
