---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::OpenDevice コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: af24aff4bbb8f0eefa14363453e962c0a90d610e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847213"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**OpenDevice** 関数は、仮想デバイス セットから仮想デバイス インターフェイスを取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>パラメーター

*lpName*: これは、BACKUP または RESTORE コマンドの最初の VIRTUAL_DEVICE= 句で指定されます。 この名前は、クライアントによって作成された仮想デバイス セットへのアクセスを取得するためのキーとして使用されます。

*ppVirtualDevice*: これは、仮想デバイス インターフェイスを返すために使用されます。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_OPEN |すべてのデバイスが開かれています。 |

## <a name="remarks"></a>Remarks

各呼び出しでは、次の開かれていないデバイスが返されます。 この関数は、仮想デバイス セットの構成で指定されたデバイスの数と同じ回数だけ呼び出すことができます。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。