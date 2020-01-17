---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDevice::CompleteCommand コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0fb96d94ae330fdf55d82625ed71217ba71e50ff
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847403"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**CompleteCommand** 関数は、コマンドが終了したことを SQL Server に通知するために使用されます。 コマンドについては、適切な完了情報が返される必要があります。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>パラメーター

*pCmd*: これは、以前に IClientVirtualDevice::GetCommand から返されたコマンドのアドレスです。

*dwCompletionCode*: これは完了状態を示す WIN32 状態コードです。 このパラメーターは、すべてのコマンドについて返される必要があります。 返されるコードは、実行されるコマンドに対して適切なものである必要があります。 ERROR_SUCCESS は、コマンドが正常に実行されたことを示すために、すべてのケースで使用されます。 使用可能なコードの完全な一覧については、Winerror.h ファイルを参照してください。 各コマンドの典型的な状態コードの一覧は、「コマンド」に関する記事に示されています。

*dwBytesTransferred*: これは正常に転送されたバイト数です。 この値は、データ転送コマンド Read および Write 用にのみ返されます。

*dwlPosition*: これは GetPosition コマンドのみを対象とした応答です。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 正常に完了しました。 |
| VD_E_INVALID | pCmd がアクティブなコマンドではありませんでした。 |
| VD_E_ABORT | 中止が指示されました。 |
| VD_E_PROTOCOL | デバイスが開いていません。 |

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。
