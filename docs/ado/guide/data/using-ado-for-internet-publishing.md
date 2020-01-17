---
title: ADO を使用して for Internet Publishing |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: decbc7c3b377234d91fe6b3e662d9449298041c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923619"
---
# <a name="using-ado-for-internet-publishing"></a>インターネットへの発行に ADO を使用する
[OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) ADO を使用した異種データへのアクセスの具体的な例を示しています。 このセクションの例では、インターネット パブリッシング用プロバイダーを使用する特定できますは、電子メール ストアにプロバイダーなどの異種データを他のプロバイダーと ADO を使用するときに示されている原則が生成されます。  
  
## <a name="urls"></a>URL  
 Uniform Resource Locator (Url) は、データ ソースとファイルとディレクトリの場所を指定する接続文字列とコマンドのテキストの代替として使用できます。 Url を使用するには、既存の[接続](../../../ado/reference/ado-api/connection-object-ado.md)と**Recordset**オブジェクトを使用して、**レコード**と**Stream**オブジェクト。  
  
 Url を使用する方法の詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="record-fields"></a>レコードのフィールド  
 異種データと同種のデータの主な違いは、前者は、データの各行または**レコード**、異なる一連の列を持つことができますまたは**フィールド**します。 同種のデータの各行は、同じ列のセットを持ちます。 インターネット公開プロバイダーに固有のフィールドの詳細については、次を参照してください。[レコードとプロバイダー提供の余分なフィールド](../../../ado/guide/data/records-and-provider-supplied-fields.md)します。  
  
### <a name="appending-new-fields"></a>新しいフィールドを追加します。  
 組み合わせて動作するいくつかの ADO のオブジェクトが強化されています**レコード**と**Stream**オブジェクト。  
  
-   [フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクション[Append](../../../ado/reference/ado-api/append-method-ado.md)メソッドでは、作成し、追加、[フィールド](../../../ado/reference/ado-api/field-object.md)コレクションにオブジェクトの値を指定できますも、 **フィールド**.  
  
-   [Update](../../../ado/reference/ado-api/update-method.md)メソッドが追加またはコレクションにフィールドの削除を終了します。  
  
-   代わりに、ショートカットとして、 **Append**メソッド、未定義または以前に削除されたフィールドに値を割り当てることでフィールドを作成することができます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [インターネットへの発行のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絶対 URL と相対 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [レコードとプロバイダーが指定したフィールド](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>参照  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 履歴](../../../ado/guide/ado-history.md)
