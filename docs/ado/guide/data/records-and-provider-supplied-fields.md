---
title: レコードおよびフィールドのプロバイダーが指定した |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54d55926d2bec89b0764b751bf165586e8d3c6c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924514"
---
# <a name="records-and-provider-supplied-fields"></a>レコードとプロバイダーが指定したフィールド
ときに、[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトを開くと、そのソースは、オープンの現在の行を指定できます[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)、絶対 URL または相対 URL を開くと組み合わせて[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト.  
  
 場合、**レコード**から開かれる、**レコード セット**、**レコード**オブジェクト[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクションは、のすべてのフィールドを含める**レコード セット**、さらに、基になるプロバイダーによって追加されたすべてのフィールド。  
  
 プロバイダーの補助特性として機能する追加のフィールドを挿入、**レコード**します。 その結果、**レコード**ではなく、一意のフィールドを必要があります、**レコード セット**全体またはそのいずれかとして**レコード**の別の行から派生した、 **Recordset**.  
  
 すべての行など、 **Recordset**データ ソースがこのような From の列がある可能性があり、件名の電子メールから派生します。 A**レコード**そこから派生した**Recordset**フィールドを同じになります。 ただし、**レコード**をによって表される特定のメッセージに固有の他のフィールドがありますも**レコード**、添付ファイルと Cc (カーボン コピー) など。  
  
 ですが、**レコード**オブジェクトとの現在の行、**レコード セット**、同じフィールドがあるとは異なるため、**レコード**と**レコードセット**オブジェクトは、さまざまなメソッドおよびプロパティがあります。  
  
 保持している共通のフィールド、**レコード**と**Recordset**いずれかのオブジェクトで変更できます。 フィールドを削除することはできませんただし、**レコード**オブジェクトを基になるプロバイダーが、フィールドを null に設定をサポートします。  
  
 後に、**レコード**が開かれると、プログラムでフィールドを追加できます。 追加したフィールドを削除することもできますが、元のフィールドを削除することはできません、 **Recordset**します。  
  
 開くことも、**レコード**URL から直接オブジェクト。 ここでは、フィールドに追加、**レコード**基になるプロバイダーによって異なります。 現時点では、ほとんどのプロバイダーの追加によって表されるエンティティを記述するフィールドのセットを**レコード**します。 単純なファイルなどのバイトのストリームのエンティティが構成されている場合、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)通常からオブジェクトを開くことができます、**レコード**します。  
  
## <a name="special-fields-for-document-source-providers"></a>ドキュメントの特別なフィールドのソース プロバイダー  
 特殊なクラスと呼ばれるプロバイダーの*ソース プロバイダーのドキュメント*フォルダーを管理および文書化します。 ときに、**レコード**オブジェクトが表す文書または**レコード セット**オブジェクトは、ドキュメントのフォルダーを表し、ドキュメントのソース プロバイダーがそれらのオブジェクトを記述するフィールドの一意のセットを設定します特性のドキュメントの代わりに、実際のドキュメント自体にします。 通常、1 つのフィールドへの参照が含まれます。、 **Stream**ドキュメントを表します。  
  
 これらのフィールドを構成して、リソース**レコード**または**recordset**でそれらをサポートする特定のプロバイダーの一覧表示と[付録 a:プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)します。  
  
 2 つの定数のインデックス、**フィールド**リソースのコレクション**レコード**または**レコード セット**をよく使用されるフィールドのペアを取得します。 **フィールド**オブジェクト[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティは、目的のコンテンツを返します。  
  
-   使用してアクセスするフィールド、 **adDefaultStream**定数に関連付けられている既定のストリームが含まれています、**レコード**または**Recordset**オブジェクト。 プロバイダーは、既定のストリームをオブジェクトに代入します。  
  
-   使用してアクセスするフィールド、 **adRecordURL**定数には、ドキュメントを識別する絶対 URL が含まれています。  
  
 ドキュメントのソース プロバイダーがサポートしていません、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)のコレクション**レコード**と**フィールド**オブジェクト。 コンテンツ、**プロパティ**コレクションがこのようなオブジェクトは null です。  
  
 ドキュメントのソース プロバイダーがなど、プロバイダー固有のプロパティを追加することがあります**データ ソースの種類**ドキュメントのソース プロバイダーがあるかどうかを識別するためにします。 プロバイダーの種類を決定する方法の詳細については、プロバイダーのマニュアルを参照してください。  
  
## <a name="resource-recordset-columns"></a>リソース レコード セットの列  
 A*リソース レコード セット*次の列で構成されています。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|読み取り専用。 リソースの URL を示します。|  
|RESOURCE_PARENTNAME|AdVarWChar|読み取り専用。 親レコードの絶対 URL を示します。|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|読み取り専用。 PARENTNAME、PARSENAME を連結したものであると、リソースの絶対 URL を示します。|  
|RESOURCE_ISHIDDEN|adBoolean|リソースが非表示の場合は true。 行セットを明示的に作成するコマンドが RESOURCE_ISHIDDEN が True である行を選択しない限り、行は返されません。|  
|RESOURCE_ISREADONLY|adBoolean|リソースが読み取り専用である場合は true。 開こうとして DBBINDFLAG_WRITE されのこのリソースは、DB_E_READONLY で失敗します。 読み取り専用リソースで開かれた場合でも、このプロパティを編集できます。|  
|RESOURCE_CONTENTTYPE|AdVarWChar|ドキュメントの使用方法を示します-たとえば、弁護士の簡単な。 これは、ドキュメントの作成に使用した Office テンプレートに対応可能性があります。|  
|RESOURCE_CONTENTCLASS|AdVarWChar|などの形式を示す、ドキュメントの MIME の種類を示す"`text/html`"。|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|コンテンツが格納されている言語を示します。|  
|RESOURCE_CREATIONTIME|adFileTime|読み取り専用。 リソースが作成された時刻を格納する FILETIME 構造体を示します。 時刻は世界協定時刻 (UTC) 形式で報告されます。|  
|RESOURCE_LASTACCESSTIME|AdFileTime|読み取り専用。 リソースの最終アクセス時刻が含まれる FILETIME 構造体を示します。 時刻は UTC 形式です。 プロバイダーがこの時間メンバーをサポートしていない場合、FILETIME メンバーは 0 です。|  
|RESOURCE_LASTWRITETIME|AdFileTime|読み取り専用。 リソースの最終書き込み時刻を表す FILETIME 構造体を示します。 時刻は UTC 形式です。 プロバイダーがこの時間メンバーをサポートしていない場合、FILETIME メンバーは 0 です。|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|読み取り専用。 リソースの既定のストリームにバイト単位のサイズを示します。|  
|RESOURCE_ISCOLLECTION|adBoolean|読み取り専用。 True の場合、リソースがディレクトリなどのコレクション。 リソースが単純なファイルの場合は false です。|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|リソースが構造化ドキュメントの場合は true。 リソースは、構造化されたドキュメントではない場合は false。 コレクションまたは単純なファイルが考えられます。|  
|DEFAULT_DOCUMENT|AdVarWChar|読み取り専用。 このリソースに、フォルダーの既定の単純なドキュメントまたは構造化ドキュメントの URL が含まれていることを示します。 既定のストリームが、そのリソースから要求されたときに使用されます。 このプロパティは、単純なファイルの場合は空白です。|  
|CHAPTERED_CHILDREN|adChapter|読み取り専用。 任意。 リソースの子を含む行セットのチャプターを示します。 (、 *OLE DB Provider for Internet Publishing*この列は使用しません)。|  
|RESOURCE_DISPLAYNAME|AdVarWChar|読み取り専用。 リソースの表示名を示します。|  
|RESOURCE_ISROOT|adBoolean|読み取り専用。 リソース コレクションまたは構造化されたドキュメントのルートである場合は true。|  
  
## <a name="see-also"></a>関連項目  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
