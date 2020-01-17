---
title: 非推奨の DBCC CONCURRENCYVIOLATION コマンドへの呼び出しを削除します |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0110d4bc138ad0da953eb83d3c81ec265d2fd3ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093206"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>非推奨の DBCC CONCURRENCYVIOLATION コマンド呼び出しの削除
  アップグレード アドバイザーによって、DBCC CONCURRENCYVIOLATION コマンドの使用が検出されました。 このコマンドは使用できなくなりました。 このコマンドを実行すると、エラー 2526 が返されます。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションの新しいバージョンにはワークロード ガバナーが含まれていないため、コマンドは削除されました。  
  
## <a name="corrective-action"></a>修正措置  
 この非推奨コマンドへの参照を削除するために、アプリケーションおよびスクリプトを更新します。  
  
## <a name="external-resources"></a>外部リソース  
  
