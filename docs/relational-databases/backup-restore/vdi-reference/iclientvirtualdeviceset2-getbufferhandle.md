---
title: IClientVirtualDeviceSet2::GetBufferHandle
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::GetBufferHandle コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 844ddad21eaf3fb579d6a0981f2a042238e92372
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847333"
---
# <a name="iclientvirtualdeviceset2getbufferhandle-vdi"></a>IClientVirtualDeviceSet2::GetBufferHandle (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

アプリケーションによっては、**IClientVirtualDevice2::GetCommand** によって返されるバッファーを操作するために、複数のプロセスが必要になる場合があります。 その場合、コマンドを受け取るプロセスでは、**GetBufferHandle** を使用して、バッファーを識別するプロセス独立ハンドルを取得することができます。 その後、このハンドルによって、同じ仮想デバイス セットを開いている他のプロセスと通信することができます。 そのプロセスでは、IClientVirtualDeviceSet2::MapBufferHandle を使用して、バッファーのアドレスが取得されます。 このアドレスは、パートナーとは異なるアドレスになる可能性があります。なぜなら、各プロセスが異なるアドレスでバッファーをマッピングしている可能性があるからです。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::GetBufferHandle (
   BYTE*         pBuffer,
   DWORD*      pBufferHandle
);
```

## <a name="parameters"></a>パラメーター

*pBuffer*: これは、Read または Write コマンドから取得されたバッファーのアドレスです。

*pBufferHandle*: バッファーの一意の識別子が返されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットは現在開いていません。 |
| VD_E_INVALID | pBuffer は有効なアドレスではありません。 |

## <a name="remarks"></a>Remarks

GetBufferHandle 関数を呼び出すプロセスでは、データ転送が完了したときに IClientVirtualDevice2::CompleteCommand を呼び出す必要があります。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。