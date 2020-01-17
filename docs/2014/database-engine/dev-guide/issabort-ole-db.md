---
title: ISSAbort (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 801eb84df08837ec8e49b6bb0e28fc1f1115e674
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781038"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  **ISSAbort**で公開される、インターフェイス、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、提供、 [issabort::abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)現在の行セットと任意のコマンドをキャンセルするために使用するメソッドがバッチ処理最初に、行セットを生成してをまだ完了していない実行コマンド。  
  
 **ISSAbort**は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダーに固有のインターフェイスを使用して利用可能な**QueryInterface**上、 **IMultipleResults**によって返されるオブジェクト**Icommand::execute**または**iopenrowset::openrowset**します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|方法|説明|  
|------------|-----------------|  
|[Issabort::abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|現在の行セットと、現在のコマンドに関連付けられているバッチ コマンドを取り消します。|  
  
## <a name="see-also"></a>参照  
 [インターフェイス&#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
