---
title: GET_TRANSMISSION_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATUS_TSQL
- TRANSMISSION
- TRANSMISSION_TSQL
- GET_TRANSMISSION_STATUS
- STATUS
- GET_TRANSMISSION_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], transmission status
- Service Broker errors, transmission status
- transmission status information
- status information [SQL Server], conversations
- GET_TRANSMISSION_STATUS statement
ms.assetid: 621805d5-49ed-4764-b3cb-2ae4a3bf797e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bf05f923a5a7a6333bdca7278efae918aed71f32
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211420"
---
# <a name="get_transmission_status-transact-sql"></a>GET_TRANSMISSION_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  メッセージ交換の一方の側に関して、最後の転送の状態を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GET_TRANSMISSION_STATUS ( conversation_handle )  
```  
  
## <a name="arguments"></a>引数  
 *conversation_id*  
 メッセージ交換で使用するメッセージ交換ハンドルを指定します。 このパラメーターは **uniqueidentifier** 型です。  
  
## <a name="return-types"></a>戻り値の型  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 指定したメッセージ交換に関する、最後の転送試行の状態を説明する文字列を返します。 最後の転送が成功した場合、転送がまだ試行されていない場合、または *conversation_handle* が存在しない場合は、空の文字列が返されます。  
  
 この関数で返される情報は、管理ビュー sys.transmission_queue の last_transmission_error 列で表示される情報と同じです。 ただし、この関数を使用すると、転送キューに現在メッセージがないメッセージ交換の転送状態を検出できます。  
  
> [!NOTE]  
>  GET_TRANSMISSION_STATUS では、現在のインスタンスにメッセージ交換エンドポイントを持たないメッセージの情報は提供されません。 つまり、転送されるメッセージの情報は使用できません。  
  
## <a name="examples"></a>使用例  
 次の例では、メッセージ交換ハンドル `58ef1d2d-c405-42eb-a762-23ff320bddf0` とのメッセージ交換に関する転送状態がレポートされます。  
  
```  
SELECT Status =  
    GET_TRANSMISSION_STATUS('58ef1d2d-c405-42eb-a762-23ff320bddf0') ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
 ```
 Status  
 ------------------------------- 
 The Service Broker protocol transport is disabled or not configured.
 ```  
  
 この場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssSB](../../includes/sssb-md.md)] がネットワーク経由で通信を行うように構成されていません。  
  
## <a name="see-also"></a>参照  
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
