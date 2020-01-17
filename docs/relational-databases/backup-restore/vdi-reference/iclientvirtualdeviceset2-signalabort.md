---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::SignalAbort コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0a0d53421f0928b1ebf0ba557afbd29dd8680993
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847543"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SignalAbort** 関数は、異常終了が発生することを通知するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>Remarks

クライアントでは、バックアップ操作または復元操作をいつでも中止できます。 このルーチンは、すべての操作を中止する必要があることを通知するものです。 仮想デバイス セット全体の状態が、中止状態になります。 後続のコマンドは、いずれのデバイスについても返されません。 未完了のコマンドはすべて自動的に完了し、完了コードとして ERROR_OPERATION_ABORTED が返されます。 クライアントでは、クライアントに提供されたバッファーの未処理の使用を安全に終了した後、IClientVirtualDeviceSet2::Close を呼び出す必要があります。 詳細については、「異常終了」に関する記事を参照してください。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。