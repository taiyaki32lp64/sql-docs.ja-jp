---
title: ActiveConnection プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae0b32385b98ac1b48688a7f89bbd7c91842a106
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911592"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection プロパティ (ADO MD)
どの ADO に[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの現在のセル セットまたは現在が属するカタログ。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**バリアント**接続を定義する文字列を格納しているまたは**接続**オブジェクト。 既定値が空です。  
  
## <a name="remarks"></a>コメント  
 このプロパティを設定するには有効な ado**接続**オブジェクトまたは有効な接続文字列にします。 新しいプロバイダーを作成、接続文字列をこのプロパティを設定すると、**接続**オブジェクトのこの定義を使用して、接続が開かれます。  
  
 使用する場合、 *ActiveConnection*の引数、[開く](../../../ado/reference/ado-md-api/open-method-ado-md.md)メソッドを開き、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)オブジェクト、 **ActiveConnection**プロパティは引数の値を継承します。  
  
 設定、 **ActiveConnection**のプロパティを[カタログ](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)オブジェクトを**Nothing**でデータを含む、関連付けられているデータを解放、 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)コレクションおよび関連[ディメンション](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)、[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)、および[メンバー](../../../ado/reference/ado-md-api/member-object-ado-md.md)オブジェクト。 閉じる、**接続**開くために使用するオブジェクト、**カタログ**設定と同じ効果があります、 **ActiveConnection**プロパティを**Nothing**.  
  
 によって参照される接続の既定のデータベースを変更する、 **ActiveConnection**のプロパティを**カタログ**オブジェクトの内容が無効になります、**カタログ**します。  
  
 変更しようとした場合、エラーが発生、 **ActiveConnection**プロパティを開いている**セルセット**オブジェクト。  
  
> [!NOTE]
>  Visual basic でを使用してください。、**設定**キーワードを設定するとき、 **ActiveConnection**プロパティを、**接続**オブジェクト。 省略した場合、**設定**キーワード、実際に設定する、 **ActiveConnection**プロパティを等しく、**接続**オブジェクトの既定のプロパティ、 **ConnectionString**します。 コードを実行します。ただし、負の値のパフォーマンスに影響があります。 データ ソースに追加の接続を作成します。  
  
 MSOLAP データ プロバイダーを使用する場合は、サーバー名への接続文字列でのデータ ソースを設定し、データ ソースからカタログの名前に、初期カタログを設定します。 サーバーから切断されているキューブ ファイルに接続する場合、場所をへの完全パスに設定します。カブ ファイルです。 どちらの場合は、プロバイダー名に、プロバイダーを設定します。 次の文字列が振りビデオ ストアという名前のサーバーという名前のカタログに接続する MSOLAP プロバイダーを使用するなど、 **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 次の文字列は、C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub の場所にあるローカル キューブ ファイルに接続します。  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Catalog オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>関連項目  
 [セルセットの例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open メソッド (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
