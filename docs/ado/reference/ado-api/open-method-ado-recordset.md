---
title: Open メソッド (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16142f200e6fd6e7c141b4f1fe6d45fe8917bc28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931905"
---
# <a name="open-method-ado-recordset"></a>Open メソッド (ADO Recordset)
カーソルをオープンする[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**バリアント**に有効な評価される[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト、SQL ステートメント、テーブル名、ストアド プロシージャの呼び出し、URL、またはファイルの名前または[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクトを含む、永続的に格納されている[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
 *ActiveConnection*  
 任意。 いずれかを**バリアント**に有効な評価される[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト変数の名前または**文字列**を格納している[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)パラメーター。  
  
 *CursorType*  
 任意。 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)を開くときに、プロバイダーが使用するカーソルの種類を決定する値、 **Recordset**します。 既定値は**adOpenForwardOnly**します。  
  
 *LockType*  
 任意。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)ロック (同時実行) の種類を開くときに、プロバイダーを使用する必要がありますを決定する値、 **Recordset**します。 既定値は**adLockReadOnly**します。  
  
 *[オプション]*  
 任意。 A**長い**プロバイダーを評価する方法を示す値、*ソース*引数ものを表します以外の場合、**コマンド**オブジェクト、または、 **Recordset**以前保存されているファイルから復元する必要があります。 1 つまたは複数指定できます[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)または[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)値で、ビットごとの OR 演算子と組み合わせて使用できます。  
  
> [!NOTE]
>  開く場合、**レコード セット**から、 **Stream**含むされた保存される**レコード セット**を使用して、 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) の値**adAsyncFetchNonBlocking**効果はありません。 同期およびブロッキングのフェッチで、になります。  
  
> [!NOTE]
>  **ExecuteOpenEnum**値**adExecuteNoRecords**または**adExecuteStream**では使用できません**オープン**します。  
  
## <a name="remarks"></a>コメント  
 ADO の既定のカーソル**Recordset**は順方向専用、読み取り専用のカーソルが、サーバー上にあります。  
  
 使用して、**オープン**メソッドを**レコード セット**オブジェクトのクエリ、または以前に保存した結果、ベース テーブルからレコードを表すカーソルを開き、**レコード セット**します。  
  
 オプションを使用して、*ソース*、次のいずれかを使用してデータ ソースを指定する引数:**コマンド**オブジェクト変数、SQL ステートメント、ストアド プロシージャ、テーブル名、URL、またはファイルの完全なパス名。 場合*ソース*ファイルのパス名は、完全なパス ("c:\dir\file.rst")、相対パスであることができます ("..\file.rst")、または URL ("<https://files/file.rst>")。  
  
 使用することはお勧めできません、*ソース*の引数、**オープン**メソッドを呼び出しが成功したかどうかを決定する簡単な方法がないためレコードを返さないアクション クエリを実行します。 **Recordset**などによって返されるクエリは閉じられます。 SQL の INSERT ステートメントなどのレコードを返さないクエリを実行して呼び出し、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)のメソッド、**コマンド**オブジェクトまたは[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) のメソッド[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの代わりにします。  
  
 *ActiveConnection*引数に対応、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティを開くには、どの接続で指定し、 **Recordset**オブジェクト。 接続の定義がこの引数を渡すと、ADO は、指定されたパラメーターを使用して新しい接続を開きます。 開いた後、 **Recordset**を設定してクライアント側カーソル、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**、送信するには、このプロパティの値を変更することができます別のプロバイダーを更新します。 このプロパティを設定することも**Nothing** (Microsoft Visual Basic で) または切断する場合は NULL、**レコード セット**任意のプロバイダー。 変更する*ActiveConnection*のサーバー側カーソル、ただし、エラーが発生します。  
  
 他の引数のプロパティに直接対応するため、**レコード セット**オブジェクト (*ソース*、 *CursorType*、および*LockType*)、プロパティへの引数の関係は次のとおりです。  
  
-   プロパティが読み取り/書き込みの前に、 **Recordset**オブジェクトを開きます。  
  
-   実行時に、対応する引数を渡さない限り、プロパティの設定が使用される、**オープン**メソッド。 引数を渡す場合は、対応するプロパティの設定が上書きされ、プロパティの設定は、引数の値で更新されます。  
  
-   開いた後、 **Recordset**オブジェクトに、これらのプロパティは読み取り専用になります。  
  
> [!NOTE]
>  **ActiveConnection**プロパティは読み取り専用の**レコード セット**オブジェクト[ソース](../../../ado/reference/ado-api/source-property-ado-recordset.md)プロパティが有効な**コマンド**オブジェクト場合でも、 **Recordset**オブジェクトが開いていません。  
  
 渡す場合、**コマンド**オブジェクト、*ソース*引数とパス、 *ActiveConnection*引数、エラーが発生します。 **ActiveConnection**のプロパティ、**コマンド**既に有効なオブジェクトを設定する必要があります**接続**オブジェクトまたは接続文字列。  
  
 以外の何か成功した場合、**コマンド**オブジェクト、*ソース*引数を使用できます、*オプション*引数の評価を最適化するために、*ソース*引数。 場合、*オプション*引数が定義されていない、ADO プロバイダーへの呼び出し、引数が SQL ステートメント、ストアド プロシージャ、URL、またはテーブル名を確認する必要があるために、パフォーマンスの低下が発生する可能性があります。 何がわかっている場合*ソース*設定を使用する型、*オプション*引数は、関連するコードに直接ジャンプする ADO を指示します。 場合、*オプション*引数と一致しません、*ソース*入力、エラーが発生します。  
  
 渡す場合、 **Stream**オブジェクト、*ソース*引数を渡さないでください情報を他の引数にします。 そうと、エラーが生成されます。 **ActiveConnection**情報が保持するときに、**レコード セット**から開いた、 **Stream**。  
  
 既定値は、*オプション*引数が**adCmdFile**に関連付けられている接続がない場合、**レコード セット**します。 これは、通常、ケースに永続的に格納されているため**Recordset**オブジェクト。  
  
 プロバイダーが両方を設定して、データ ソースにレコードが返されない場合、 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)と[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)プロパティを**True**、現在のレコードの位置が定義されていないとします。 この空に新しいデータを追加することもできます**Recordset**オブジェクトのかどうか、カーソルの種類によりします。  
  
 開いている操作が完了すると**レコード セット**オブジェクトを使用して、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メモリを解放するメソッドには、システム リソースが関連付けられています。 オブジェクトを閉じるは削除されません。 メモリからそのプロパティの設定を変更して使用できます、**開く**メソッドを後でもう一度開きます。 メモリからオブジェクトを完全に排除するに、オブジェクト変数を設定します。 *Nothing*します。  
  
 前に、 **ActiveConnection**プロパティが設定されており、呼び出す**オープン**なしのオペランドのインスタンスを作成すると、**レコード セット**フィールドを追加することによって作成された、 **レコード セット**[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクション。  
  
 設定した場合、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**、2 つの方法のいずれかで非同期に行を取得することができます。 設定するのにはお勧め*オプション*に**adAsyncFetch**します。 動的なプロパティで「非同期行セットの処理」を使用する代わりに、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)、コレクションが取得された関連するイベントを削除できますを設定しない場合、*オプション*パラメーター**adAsyncFetch**します。  
  
> [!NOTE]
>  を通してのみサポートされてバック グラウンド フェッチ MS リモート プロバイダー、**オープン**メソッドの*オプション*パラメーター。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
 特定の組み合わせの[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)と[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)値が無効です。 については、どのオプションを組み合わせることはできませんのトピックを参照して、 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)、および[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open および Close メソッドの例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open および Close メソッドの例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open および Close メソッドの例 (vc++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Save および Open メソッドの例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema メソッド](../../../ado/reference/ado-api/openschema-method.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
