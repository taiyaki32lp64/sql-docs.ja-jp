---
title: アドレス帳のコマンド ボタン |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1aa5b628bec9399374b94a2cd78090207bf09b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922985"
---
# <a name="address-book-command-buttons"></a>アドレス帳のコマンド ボタン
アドレス帳アプリケーションには、次のコマンド ボタンが含まれます。  
  
-   A**検索**データベースにクエリを送信するボタンをクリックします。  
  
-   A**オフ**新しい検索を開始する前に、テキスト ボックスをクリアするボタンをクリックします。  
  
-   **プロファイルの更新**従業員レコードに変更を保存するボタンをクリックします。  
  
-   A**キャンセル変更**ボタンの変更を破棄します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="find-button"></a>検索ボタン  
 クリックすると、**検索** ボタンを構築および SQL クエリを送信する VBScript Find_OnClick Sub プロシージャをアクティブにします。 このボタンをクリックすると、データ グリッドが表示されます。  
  
## <a name="building-the-sql-query"></a>SQL クエリの作成  
 Find_OnClick Sub プロシージャの最初の部分では、グローバルの SQL SELECT ステートメントをテキスト文字列を追加することで、一度に 1 つの語句である SQL クエリを構築します。 変数を設定して開始`myQuery`データ ソース テーブルからすべての行のデータを要求する SQL SELECT ステートメントにします。 次に、Sub プロシージャは、4 つの入力ボックス、ページ上の各をスキャンします。  
  
 プログラムは、word を使用するため`like`SQL ステートメントを構築するで、クエリは、完全一致ではなく、部分文字列を検索します。  
  
 たとえば場合、 **Last Name**ボックスには、"Berge"エントリが含まれている、**タイトル**ボックスには、エントリ「プログラム マネージャー、」SQL ステートメントが含まれている (の値`myQuery`) のようになります。  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 クエリが成功した場合、単語「プログラム マネージャー」(たとえば、プログラム マネージャー、高度なテクノロジ) を含むタイトルとテキスト"Berge"(Berge Berger など) を含む最後の名前を持つすべての担当者は、HTML データ グリッドに表示されます。  
  
## <a name="preparing-and-sending-the-query"></a>準備と、クエリの送信  
 Find_OnClick Sub プロシージャの最後の部分は、2 つのステートメントで構成されます。 最初のステートメントは、代入、 [SQL](../../../ado/reference/rds-api/sql-property.md)のプロパティ、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)動的に作成した SQL クエリに等しいオブジェクト。 2 番目のステートメントにより、 **rds.DataControl**オブジェクト (`DC1`) をデータベースを照会し、グリッドに新しいクエリの結果を表示します。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>プロファイルの更新ボタン  
 クリックすると、**プロファイルの更新**ボタンを実行する VBScript Update_OnClick Sub プロシージャをアクティブ化、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)と[更新](../../../ado/reference/rds-api/refresh-method-rds.md)メソッド。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 ときに`DC1.SubmitChanges`実行されると、リモート データ サービスは、すべての更新情報をパッケージ化し、HTTP 経由でサーバーに送信します。 更新プログラムは、オール_オア_ナッシング;更新プログラムの一部が成功しなかった場合、変更が行われ、ステータス メッセージが返されます。 `DC1.Refresh` 後は必要はありません**SubmitChanges**でリモートのデータ サービスが新しいデータを確実にします。  
  
## <a name="cancel-changes-button"></a>[キャンセル] ボタンの変更  
 クリックすると**キャンセル変更**を実行する VBScript Cancel_OnClick Sub プロシージャをアクティブ化、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)メソッド。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 ときに`DC1.CancelUpdate`実行されると、ユーザーが行ったデータ グリッドで従業員レコードを最後のクエリまたは更新後の編集を破棄します。 元の値が復元されます。  
  
## <a name="see-also"></a>関連項目  
 [アドレス帳のナビゲーション ボタン](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


