---
title: Microsoft OLE DB Provider for Microsoft Active Directory サービス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e204a4f6f7f395ca93198bc560f4a216d5a70673
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926674"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft OLE DB Provider for Microsoft Active Directory サービス
Active Directory サービス インターフェイス (ADSI) プロバイダーが ADSI による異種ディレクトリ サービスに接続するための ADO を許可します。 これにより、ADO アプリケーションは Microsoft Windows NT 4.0 および Microsoft Windows 2000 directory services のすべての LDAP 準拠ディレクトリ サービスと Novell Directory Services だけでなくに読み取り専用アクセスできるようにします。 ADO アプリケーションがシームレスにアクセスできる、新しいプロバイダー アクセス権を付与する別のディレクトリがある場合、ADSI はプロバイダー モデルに基づきます。 ADSI プロバイダーは、フリー スレッドし、Unicode に対応します。  
  
## <a name="connection-string-parameters"></a>接続文字列パラメーター  
 このプロバイダーに接続するには、設定、**Provider**の引数、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)には、次のプロパティ。  
  
```vb
ADSDSOObject  
```  
  
 読み取り、[Provider](../../../ado/reference/ado-api/provider-property-ado.md)プロパティは同様に、この文字列を返します。  
  
## <a name="typical-connection-string"></a>一般的な接続文字列  
 このプロバイダーの一般的な接続文字列は次のとおりです。  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 文字列は、次のキーワードで構成されます。  
  
|Keyword|説明|  
|-------------|-----------------|  
|**Provider**|Active Directory サービス用の OLE DB プロバイダーを指定します。|  
|**User ID**|ユーザー名を指定します。 このキーワードを省略すると、現在のログオンが使用されます。|  
|**Password**|ユーザーのパスワードを指定します。 このキーワードを省略するとします。 現在のログオンが使用されます。|  
  
> [!NOTE]
>  Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうかは、する必要がありますを指定する**Trusted_Connection = yes**または**Integrated Security = SSPI**ユーザー ID とパスワードの代わりに接続文字列の情報です。  
  
## <a name="command-text"></a>コマンド テキスト  
 4 部構成のコマンド テキストの文字列は、次の構文で、プロバイダーによって認識されます。  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|値|説明|  
|-----------|-----------------|  
|*Root*|示す、 **ADsPath**オブジェクトを使用する (つまり、検索のルート) の検索を開始します。|  
|*Assert*|RFC 1960 形式で検索フィルターを示します。|  
|*Attributes*|返される属性のコンマ区切りの一覧を示します。|  
|*Scope*|任意。 **文字列**検索のスコープを指定します 次のいずれかになります。<br /><br /> ベースでは、ベース オブジェクト (検索のルート) のみを検索します。<br />-OneLevel では、1 レベルのみを検索します。<br />サブツリーには、サブツリー全体を検索します。|  
  
 例:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 プロバイダーもサポートしています SQL SELECT コマンドのテキスト。 以下に例を示します。  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>コメント  
 プロバイダーはストアド プロシージャの呼び出しまたは単純なテーブル名を受け付けません (たとえば、 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)プロパティが必ず**adCmdText**)。 コマンドのテキスト要素の詳しい説明については、Active Directory サービス インターフェイスのドキュメントを参照してください。  
  
## <a name="recordset-behavior"></a>レコード セットの動作  
 次の表で使用できる機能、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)このプロバイダーを使用して開かれたオブジェクト。 静的カーソルの種類のみ (**adOpenStatic**) は使用できます。  
  
 詳細については**Recordset**実行、プロバイダーの構成の動作、[Supports](../../../ado/reference/ado-api/supports-method.md)メソッドを列挙し、[Properties](../../../ado/reference/ado-api/properties-collection-ado.md) のコレクション**RecordSet** をプロバイダーに固有の動的なプロパティが存在するかどうかを判断します。  
  
 **標準の ADO レコード セットのプロパティの可用性:**  
  
|プロパティ|可用性|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|読み取り/書き込み|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|読み取り/書き込み|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|読み取り専用|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|  
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|読み取り/書き込み|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|読み取り/書き込み|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|読み取り専用|  
|[Assert](../../../ado/reference/ado-api/filter-property.md)|読み取り/書き込み|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|読み取り/書き込み|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|使用できません。|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|読み取り/書き込み|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|読み取り専用|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|読み取り/書き込み|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|読み取り専用|  
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|読み取り/書き込み|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|読み取り専用|  
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|読み取り専用|  
  
 **標準の ADO レコード セット メソッドの可用性:**  
  
|方法|使用できるでしょうか。|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|いいえ|  
|[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)|いいえ|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|いいえ|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|いいえ|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|はい|  
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|はい|  
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|いいえ|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|はい|  
|[Move](../../../ado/reference/ado-api/move-method-ado.md)|はい|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|はい|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|はい|  
|[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)|はい|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|はい|  
|[Resync](../../../ado/reference/ado-api/resync-method.md)|はい|  
|[Supports](../../../ado/reference/ado-api/supports-method.md)|はい|  
|[Update](../../../ado/reference/ado-api/update-method.md)|いいえ|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|いいえ|  
  
 ADSI とプロバイダーの詳細については、Active Directory サービス インターフェイスのマニュアルを参照または ADSI Web ページを参照してください。  
  
## <a name="see-also"></a>参照  
 [CommandType プロパティ (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Provider プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Supports メソッド](../../../ado/reference/ado-api/supports-method.md)
