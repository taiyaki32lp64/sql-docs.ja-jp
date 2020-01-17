---
title: データの保持 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63323fd8ed18f57a68633dce0525d1d37e4978ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924707"
---
# <a name="persisting-data"></a>データの保持
(たとえば、ラップトップを使用して)、ポータブル コンピューター、接続および切断状態の両方で実行できるアプリケーションの必要性が生成されます。 ADO には、開発者に、クライアント カーソルを保存する機能を提供することによりこのサポートが追加されて**Recordset**をディスクに後で再読み込みします。  
  
 この種の機能は、次のようを使用することがいくつかのシナリオがあります。  
  
-   **移動。** 外出先で、アプリケーションを作成する際に、変更を行い、後で、データベースに再接続してコミットできるは、新しいレコードを追加する機能を提供に不可欠です。  
  
-   **ルックアップを頻繁に更新します。** 多くの場合、アプリケーションでは、テーブルとして使用されます参照-たとえば、税のテーブルの状態します。 頻繁に更新され、読み取り専用します。 サーバーからデータをこのアプリケーションを起動するたびに、再度読み取ることではなく、アプリケーションできますだけからデータを読み込むローカルに保存される**Recordset**します。  
  
 ADO では、保存および読み込みで**レコード セット**を使用して、 **Recordset.Save**と**Recordset.Open(,,,adCmdFile)** ADO 上のメソッド**Recordset**オブジェクト。  
  
 使用することができます、**レコード セットの保存**、ADO を保持する**レコード セット**ディスク上のファイルにします。 (保存することも、 **Recordset** ADO に**Stream**オブジェクト。 **Stream**オブジェクトは、ガイドの後半で説明します)。後で、使用することができます、**オープン**メソッドを再度開く、**レコード セット**それを使用する準備ができたら。 既定では、ADO の保存、**レコード セット**専用の Microsoft 高度なデータ TableGram (adtg 形式) の形式にします。 使用してこのバイナリ形式を指定、 **adPersistADTG PersistFormatEnum**値。 また、保存を選択することができます、**レコード セット**を代わりに使用して XML として出力**adPersistXML**します。 レコード セットを XML として保存する方法の詳細については、次を参照してください。 [XML 形式で保持するレコード](../../../ado/guide/data/persisting-records-in-xml-format.md)します。  
  
 構文、**保存**メソッドを次に示します。  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 初めて保存するとき、**レコード セット**を指定する省略可能*先*します。 省略した場合*先*の値に設定の名前を持つ新しいファイルを作成するが、[ソース](../../../ado/reference/ado-api/source-property-ado-recordset.md)のプロパティ、**レコード セット**します。  
  
 省略*先*関数を呼び出すと**保存**後の最初の保存または実行時エラーが発生します。 後で呼び出す場合**保存**を新しい*先*、**レコード セット**新しい変換先に保存されます。 ただし、新しい変換先および元の送信先両方開かれます。  
  
 **保存**が閉じない、**レコード セット**または*先*で作業を続行することができますので、**レコード セット**して最新の変更を保存します。 *移行先*されるまで開いたまま、**レコード セット**を閉じると、他のアプリケーションで読み取りが、書き込みをする間*先*します。  
  
 セキュリティ上の理由から、**保存**メソッドは、Microsoft Internet Explorer によって実行されるスクリプトから低、カスタムのセキュリティ設定の使用のみを許可します。  
  
 場合、**保存**中に、非同期メソッドが呼び出される**レコード セット**フェッチ、実行、または更新操作が進行中、**保存**非同期操作になるまで待機します。完了します。  
  
 最初の行で始まるレコードの保存、 **Recordset**します。 ときに、**保存**メソッドが終了したらの最初の行に現在の行位置を移動、**レコード セット**します。  
  
 最適な結果を設定、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**で**保存**します。 かどうか、プロバイダーがサポートしないすべての機能を保存するために必要な**レコード セット**オブジェクトの場合、カーソル サービスが機能を提供します。  
  
 ときに、**レコード セット**に保存されて、 **CursorLocation**プロパティに設定**adUseServer**、更新プログラムの機能、 **Recordset**は制限されています。 通常、単一テーブルの更新、挿入、および削除 (プロバイダーの機能に依存) できるはだけです。 [再同期](../../../ado/reference/ado-api/resync-method.md)メソッドもこの構成では使用できません。  
  
 *先*パラメーターは、OLE DB をサポートする任意のオブジェクトを受け入れることができます**IStream**保存することができます、インターフェイス、**レコード セット**ASP に直接**応答**オブジェクト。  
  
 次の例では、**保存**と**オープン**メソッドを使用して永続化、**レコード セット**を後でもう一度開きます。  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>コメント  
 このセクションでは、次のトピックを扱います。  
  
-   [レコードセットの保持に関する詳細情報](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [フィルター処理されたレコードセットおよび階層レコードセットの保持](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
