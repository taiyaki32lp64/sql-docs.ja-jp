---
title: 結果セット (拡張ストアド プロシージャ API) サーバーへの送信 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a58c8eca585bbbe2c935c524840bc465992d45c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62511847"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>結果セットのサーバーへの送信 (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 結果セットを送信するときに[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、拡張ストアド プロシージャは次のように、適切な API を呼び出す必要があります。  
  
-   **Srv_sendmsg**前に、または後で送信されたすべての行 (あれば)、任意の順序で関数を呼び出すことが**srv_sendrow**します。 完了ステータスが送信される前に、クライアントにすべてのメッセージを送信する必要があります**srv_senddone**します。  
  
-   **srv_sendrow** 関数は、クライアントに送信される各行につき 1 回呼び出されます。 すべての行は、メッセージ、状態の値の前に、クライアントに送信する必要がありますまたは完了状態を送信**srv_sendmsg**、 **srv_status**の引数**srv_pfield**、または**srv_senddone**します。  
  
-   すべての列で定義されていない行を送信**srv_describe**により、アプリケーションで情報エラー メッセージが生成され、クライアントに FAIL が返されます。 この場合、その行は送信されません。  
  
## <a name="see-also"></a>参照  
 [拡張ストアド プロシージャの作成](creating-extended-stored-procedures.md)  
  
  
