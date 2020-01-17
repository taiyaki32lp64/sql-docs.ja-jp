---
title: トランザクションの昇格 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
author: rothja
ms.author: jroth
ms.openlocfilehash: d75bbf1c4d468a0d6c3872a220566d667b059a5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937492"
---
# <a name="transaction-promotion"></a>トランザクションの昇格
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  トランザクション*プロモーション*に応じてに完全な分散トランザクションに自動的に昇格したことができます、軽量のローカル トランザクションを説明します。 サーバー側で実行されているデータベース トランザクション内でマネージド ストアド プロシージャが呼び出されると、CLR (共通言語ランタイム) コードはローカル トランザクションのコンテキストで実行されます。  データベース トランザクション内でリモート サーバーへの接続が開かれると、リモート サーバーへの接続が分散トランザクションに参加し、ローカル トランザクションは自動的に分散トランザクションに昇格します。 トランザクションの昇格では、必要になるまで分散トランザクションの作成を遅延し、分散トランザクションのオーバーヘッドを最小限に抑えます。 トランザクションの昇格は自動的を使用して有効にする場合、**参加**キーワードは、開発者による介入は必要ありません。 .NET Framework Data Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、.NET Framework のクラスを通して処理され、トランザクションの昇格**System.Data.SqlClient**名前空間。  
  
## <a name="the-enlist-keyword"></a>Enlist キーワード  
 **ConnectionString**のプロパティを**SqlConnection**オブジェクトのサポート、**参加**キーワードを示すかどうか**System.Data.SqlClient**トランザクション コンテキストを検出し、分散トランザクション接続を自動的に登録します。 このキーワードが true に設定されている場合 (既定の設定)、開かれているスレッドの現在のトランザクション コンテキストに接続が自動参加します。 このキーワードが false に設定されている場合、SqlClient 接続は分散トランザクションとのやり取りを行いません。 場合**参加**が指定されていない接続文字列に 1 つが、接続が開かれた時に検出された場合に、接続は分散トランザクションに参加して自動的にします。  
  
## <a name="distributed-transactions"></a>分散トランザクション  
 通常、分散トランザクションでは、大量のシステム リソースが消費されます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散トランザクション コーディネーター (MS DTC) では、分散トランザクションを管理し、それらのトランザクションでアクセスされているすべてのリソース マネージャーを統合します。 トランザクションの昇格は特殊な形式の一方では、 **System.Transactions**を単純な作業を効果的に委任するトランザクション[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トランザクション。 **System.Transactions**、 **System.Data.SqlClient**、および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に応じて完全な分散トランザクションに昇格、トランザクションの処理に関連する作業を調整します。  
  
 アクティブな接続が開かれたときにトランザクションの昇格を使用する利点は**TransactionScope**トランザクション、および他の接続を開くと、トランザクションがコミットされる軽量のトランザクションとしてではなく完全な分散トランザクションのオーバーヘッドが生じることです。 詳細については**TransactionScope**を参照してください[Using System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)します。  
  
## <a name="see-also"></a>関連項目  
 [CLR 統合とトランザクション](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
