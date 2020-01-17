---
title: IClientVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::OpenDevice コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: aff46d7240cf504b02e75d91b75d0ba746a24752
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847573"
---
# <a name="iclientvirtualdeviceset2opendevice-vdi"></a>IClientVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**OpenDevice** 関数により、仮想デバイス セット内のいずれかのデバイスが開かれます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::OpenDevice (
   LPCWSTR                  lpName,
   IClientVirtualDevice**   ppVirtualDevice

);
```

## <a name="parameters"></a>パラメーター

*lpName*: これにより、仮想デバイスが識別されます。

*ppVirtualDevice*: 関数が成功すると、仮想デバイスへのポインターが返されます。 このインターフェイスは、GetCommand と CompleteCommand に使用されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_ABORT | 中止が要求されました。 |
| VD_E_OPEN |すべてのデバイスが開いています。 |
| VD_E_PROTOCOL | セットが初期化中の状態ではないか、この特定のデバイスが既に開いています。 |
| VD_E_INVALID | デバイス名が無効です。 これは、セットの構成要素として認識されている名前の 1 つではありません。 |

## <a name="remarks"></a>Remarks

VD_E_OPEN は、問題なく返される場合があります。 クライアントでは、このコードが返されるまで、ループを使って OpenDevice を呼び出すことができます。
複数のデバイス (たとえば、n 個デバイス) が構成されている場合は、仮想デバイス セットから一意のデバイス インターフェイスが n 個返されます。 最初のデバイスには、仮想デバイス セットと同じ名前が付けられます。 その他のデバイスには、BACKUP/RESTORE ステートメントの VIRTUAL_DEVICE 句で指定された名前が付けられます。

GetConfiguration 関数は、デバイスが開けるようになるまで待機するために使用できます。

この関数が成功しなかった場合は、ppVirtualDevice によって null 値が返されます。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。