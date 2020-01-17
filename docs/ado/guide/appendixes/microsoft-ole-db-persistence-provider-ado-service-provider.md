---
title: Microsoft OLE DB の永続化プロバイダー (ADO サービス プロバイダー) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bd341a3af2d1fdb076312b4c0993184fb4fae39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926764"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB の永続化プロバイダーの概要
Microsoft OLE DB 永続化プロバイダーでは、保存することができます、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)ファイルにオブジェクトし、後で復元する**Recordset**ファイルからのオブジェクト。 スキーマ情報、データ、および保留中の変更は保持されます。

 保存することができます、 **Recordset**専用の高度なデータ テーブル グラム (adtg 形式) 形式またはオープン拡張マークアップ言語 (XML) 形式のいずれかでします。

## <a name="provider-keyword"></a>プロバイダーのキーワード
 このプロバイダーを起動するには、接続文字列で、次のキーワードと値を指定します。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>エラー
 アプリケーションでは、このプロバイダーによって発行された、次のエラーを検出できます。

|定数|説明|
|--------------|-----------------|
|E_BADSTREAM|開かれたファイルの有効な形式がありません (つまり、形式が adtg 形式または XML)。|
|E_CANTPERSISTROWSET|**Recordset**保存されているオブジェクトが保存されないようにする特性です。|

## <a name="remarks"></a>コメント
 Microsoft OLE DB 永続化プロバイダーは、動的プロパティを公開しません。

 現時点では、階層のみ parameterized **Recordset**オブジェクトを保存できません。

 永続的に保存の詳細については**Recordset** 、オブジェクトを参照してください[レコード セットの保持](../../../ado/guide/data/more-about-recordset-persistence.md)します。

 ストリームを開くに使用するときに、**レコード セット、** 以外の指定されたパラメーターことはありません、*ソース*のパラメーター、**開く**メソッド。

## <a name="see-also"></a>関連項目
[Microsoft OLE DB の永続化プロバイダー (サービス プロバイダーの ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
