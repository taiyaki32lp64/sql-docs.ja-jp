---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDevice::SendCommand コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c75cd206557547f55d47eec0a7aec52cc0069b71
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847513"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**SendCommand** 関数は、IServerVirtualDeviceSet2::OpenDevice から返された仮想デバイス オブジェクトを使用して、クライアントにコマンドを送信します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>パラメーター

*pCmd*: これはコマンド要求ブロックへのポインターです。 詳細については、コマンドを参照してください。 completionFunction フィールドは、次のシグネチャを持つ関数のアドレスを指すように設定する必要があります。

```c
void callbackFunction ( VDS_Command *pCmd);
```

このコールバックは、コマンドが完了したことをクライアントが示すと、完了エージェントによって作成されます。 SQL Server により、pCmd の completionContext フィールドが設定されます。 その目的は、コールバック関数にコンテキストを提供することです。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | コマンドがクライアントへのキューに正常に登録されました。 |
| VD_E_QUEUE_FULL | デバイス キューがいっぱいです。 |
| VD_E_IO_ERROR | デバイスは IO エラー状態です。 |
| VD_E_PROTOCOL | デバイスがアクティブではありません。 |

## <a name="remarks"></a>Remarks

コマンドを送信しようとしてエラーが発生すると、コールバック関数が呼び出され、コマンド バッファー内の completionCode が次のように設定されます。

| completionCode | エラー |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。