---
title: Microsoft OLE DB Provider for Oracle |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60510302525562d9c3007a6ef57213fc261b4c60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926625"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle の概要
> [!IMPORTANT]
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle の OLE DB プロバイダーを使用します。

 Microsoft OLE DB Provider for Oracle では、Oracle データベースにアクセスする ADO を使用します。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、設定、*プロバイダー*の引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。

```vb
MSDAORA
```

 読み取り、[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティは同様に、この文字列を返します。

 Oracle データベースでは、キーセット カーソルまたは動的カーソルでの結合クエリを実行する場合、エラーが発生します。 Oracle では、静的な読み取り専用のカーソルのみサポートされます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 文字列は、これらのキーワードで構成されます。

|Keyword|説明|
|-------------|-----------------|
|**Provider**|OLE DB Provider for Oracle を指定します。|
|**Data Source**|サーバーの名前を指定します。|
|**User ID**|ユーザー名を指定します。|
|**Password**|ユーザーのパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 プロバイダーは、ADO で定義されているだけでなく、いくつかのプロバイダーに固有の接続パラメーターをサポートします。 ADO 接続のプロパティでこれらのプロバイダーに固有のプロパティを使用して設定できるよう、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクションを[接続](../../../ado/reference/ado-api/connection-object-ado.md)またはの一部として、 **ConnectionString**.

 これらのパラメーターに詳しく記載、 [OLE DB プログラマーズ リファレンス](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)します。 [ADO Dynamic プロパティ インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)これらのパラメーター名と対応する OLE DB プロパティの間の相互参照を提供します。

|パラメーター|説明|
|---------------|-----------------|
|**ウィンドウ ハンドル**|使用して追加の情報を要求するウィンドウ ハンドルを示します。|
|**Locale Identifier**|一意な 32 ビットに関連するユーザーの言語の基本設定を指定する数 (たとえば、1033) を示します。 これらの設定を示す日付と時刻を書式設定方法、項目をアルファベット順に並べ替えるか、文字列が比較され具合です。|
|**OLE DB サービス**|OLE DB サービスを有効または無効を指定するビットマスクを示します。|
|**プロンプト**|接続が確立されるときにユーザーに確認するかどうかを示します。|
|**拡張プロパティ**|プロバイダー固有の拡張された接続情報を含む文字列。 このプロパティはプロパティのメカニズムでは記述できないプロバイダーに固有の接続情報にのみ使用します。|

## <a name="see-also"></a>関連項目
 [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [プロバイダー プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
