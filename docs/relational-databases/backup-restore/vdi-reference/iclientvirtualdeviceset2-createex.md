---
title: IClientVirtualDeviceSet2::CreateEx
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::CreateEx コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 90165738dfcea8818353d602f72390bb08eea792
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847353"
---
# <a name="iclientvirtualdeviceset2createex-vdi"></a>IClientVirtualDeviceSet2::CreateEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**CreateEx** 関数は、仮想デバイス セットを作成するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::CreateEx (
   LPCWSTR         lpInstanceName,
   LPCWSTR         lpName,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>パラメーター

*lpInstanceName*: この文字列により、SQL コマンドの送信先となる SQL Server インスタンスが識別されます。

*lpName*: これにより、仮想デバイス セットが識別されます。 CreateFileMapping() によって使用される命名規則に従う必要があります。 円記号 (\) 以外の任意の文字を使用できます。 これは、ワイド文字の Unicode 文字列です。 この文字列には、ユーザーの製品名または会社名とデータベース名をプレフィックスとして付けることをお勧めします。

*pCfg*: これは仮想デバイス セットの構成です。 詳細については、「構成」に関する記事を参照してください。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_NOTSUPPORTED | 構成の 1 つ以上のフィールドが無効であるか、サポートされていません。 |
| VD_E_PROTOCOL | 仮想デバイス セットが作成されました。 |

## <a name="remarks"></a>Remarks

CreateEx メソッドは、バックアップまたは復元操作ごとに 1 回だけ呼び出す必要があります。 Close メソッドを呼び出した後、クライアントでは、インターフェイスを再利用して別の仮想デバイス セットを作成できます。

インスタンス名で、Transact-SQL を発行するインスタンスを識別できるようにする必要があります。 NULL は既定のインスタンスを識別します。 "machineName\" プレフィックスは許可されていません。

CreateEx (および Create) の呼び出しによって、クライアント プロセス内のプロセス ハンドルのセキュリティ DACL が変更されます。 このため、プロセス ハンドルのその他の変更は、CreateEx の呼び出しでシリアル化される必要があります。 CreateEx では、CreateEx の他の呼び出しを使用してシリアル化が行われますが、外部処理を使用してシリアル化を行うことはできません。 SQL Server サービスを実行しているアカウントにアクセス権が付与されます。

CreateEx メソッドは、元の IClientVirtualDeviceSet で定義されている Create メソッドよりも優先されます。 元の Create メソッドは非推奨となっており、今後の開発では使用しないでください。 元の Create メソッドでは、_VIRTUAL_SERVER_NAME_ 環境変数を使用して、インスタンス名サポートの形式が実装されます。 環境内でその変数が設定されている場合、Create メソッドによって内部的に CreateEx が呼び出され、インスタンス名として _VIRTUAL_SERVER_NAME_ の値が渡されます。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。