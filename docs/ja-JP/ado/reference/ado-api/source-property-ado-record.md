---
title: Source プロパティ (ADO レコード) |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc3c0abd277bee41dc22c700d735f54c2914458a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="source-property-ado-record"></a>Source プロパティ (ADO レコード)
データ ソースまたはによって表されるオブジェクトを示す、[レコード](../../../ado/reference/ado-api/record-object-ado.md)です。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 取得または設定、**バリアント**で表されるエンティティを示す値、**レコード**です。  
  
## <a name="remarks"></a>解説  
 **ソース**プロパティから返される、*ソース*の引数、**レコード**オブジェクト[開く](../../../ado/reference/ado-api/open-method-ado-record.md)メソッドです。 絶対または相対 URL 文字列である含めることができます。 絶対 URL を設定しないで使用できる、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティを開くには直接、**レコード**オブジェクト。 暗黙的な**接続**オブジェクトはここで作成します。  
  
 **ソース**プロパティが既に開かれているへの参照を含めることができますも**Recordset**を開きます、**レコード**の現在の行を表すオブジェクトを**レコード セット**です。  
  
 **ソース**プロパティへの参照を含めることもできます、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト プロバイダーから 1 行のデータが返されます。  
  
 場合、 **ActiveConnection**プロパティが設定されても、**ソース**プロパティは、その接続のスコープ内に存在する一部のオブジェクトを指す必要があります。 たとえば、名前空間のツリー構造で場合、**ソース**プロパティが絶対 URL を含む、接続文字列内の URL で識別されるノードのスコープ内に存在するノードを指す必要があります。 場合、**ソース**プロパティが相対 URL を含むそので設定されたコンテキスト内では、検証、 **ActiveConnection**プロパティです。  
  
 **ソース**プロパティが読み取り/書き込み中に、**レコード**オブジェクトが閉じられ、中に読み取り専用、**レコード**オブジェクトが開かれています。  
  
> [!NOTE]
>  Http スキームを使用する Url が自動的に起動、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)です。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)です。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Source プロパティ (ADO エラー)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source プロパティ (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)