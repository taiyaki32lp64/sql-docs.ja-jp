---
title: Source プロパティ (ADO Record) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1870d8cd8253e1b6de74ce093d51ca6e33c5c6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930934"
---
# <a name="source-property-ado-record"></a>Source プロパティ (ADO Record)
データ ソースまたはによって表されるオブジェクトを示す、[レコード](../../../ado/reference/ado-api/record-object-ado.md)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**バリアント**によって表されるエンティティを示す値、**レコード**します。  
  
## <a name="remarks"></a>コメント  
 **ソース**プロパティが返す、*ソース*の引数、**レコード**オブジェクト[オープン](../../../ado/reference/ado-api/open-method-ado-record.md)メソッド。 絶対または相対 URL 文字列であるを含めることができます。 絶対 URL を設定せずに使用できます、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティを直接開くことを**レコード**オブジェクト。 暗黙的な**接続**オブジェクトがここで作成されます。  
  
 **ソース**プロパティは、既に開いているへの参照を含めることもできます**レコード セット**を開いて、**レコード**の現在の行を表すオブジェクト、 **レコード セット**します。  
  
 **ソース**プロパティでしたへの参照を含めることも、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト プロバイダーから 1 行のデータが返されます。  
  
 場合、 **ActiveConnection**プロパティが設定されても、**ソース**プロパティは、その接続のスコープ内に存在するいくつかのオブジェクトを指す必要があります。 ツリー構造の名前空間では、たとえばの場合、**ソース**プロパティが絶対 URL を含む、接続文字列内の URL で識別されるノードのスコープ内に存在するノードを指す必要があります。 場合、**ソース**プロパティには、相対 URL が含まれていますで設定されたコンテキスト内では、検証、 **ActiveConnection**プロパティ。  
  
 **ソース**プロパティが読み取り/書き込み中に、**レコード**オブジェクトが閉じられるし、は読み取り専用中に、**レコード**オブジェクトが開いています。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ソースのプロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source プロパティ (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
