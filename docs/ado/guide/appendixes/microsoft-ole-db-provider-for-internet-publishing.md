---
title: Microsoft OLE DB Provider for Internet Publishing |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 19d719ddb4e5a2f7851a1d12dc4abe69069a354f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926753"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet パブリッシングの概要
Microsoft OLE DB Provider for Internet Publishing は、ADO を Microsoft または Microsoft インターネット インフォメーション サーバーによって提供されるリソースにアクセスできます。 リソースには、HTML ファイル、または Windows 2000 web フォルダーなどの web ソース ファイルが含まれます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、設定、*プロバイダー*の引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```vb
MSDAIPP.DSO
```

 この値も設定またはを使用して読み取る、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)プロパティ。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 \- または -

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|OLE DB Provider for Internet Publishing を指定します。|
|**データ ソース**- または - **URL**|ファイルまたは Web フォルダーに発行されるディレクトリの URL を指定します。|
|**User ID**|ユーザー名を指定します。|
|**Password**|ユーザーのパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。

 設定した場合、 *ResourceURL*値から、"URL ="で無効な値への接続文字列、既定では、インターネット パブリッシング用プロバイダーを発生させます有効な値を要求するダイアログ ボックス。 これは、ダイアログ ボックスがオフになってされ、コンポーネントからの応答を受信していないため、固定するのには、クライアントが表示されるまで、プログラムの実行を中断しますので、アプリケーションの中間層のコンポーネントの動作が望ましくないです。

> [!NOTE]
>  場合 MSDAIPP します。DSO は、プロバイダーのいずれかの値として明示的に指定された、*プロバイダー*接続文字列キーワード、または**プロバイダー**プロパティは使用できません"URL ="接続文字列にします。 この場合、エラーが発生します。 代わりに、トピックに示すように単純に、URL を指定[ADO、OLE DB Provider for Internet Publishing とを使用して](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)します。

## <a name="see-also"></a>関連項目
 [インターネットのシナリオへの発行](../../../ado/guide/data/internet-publishing-scenario.md) [OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
