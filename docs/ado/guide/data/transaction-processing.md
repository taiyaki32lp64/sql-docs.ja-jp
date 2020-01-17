---
title: トランザクション処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cab6638704856baf873274807c0e2eff9a1f92d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923862"
---
# <a name="transaction-processing"></a>トランザクション処理
A*トランザクション*先頭との接続にまたがって実行データ アクセス操作の一連の末尾を区切ります。 データ ソースのトランザクションの機能によって、**接続**オブジェクトでは作成してトランザクションを管理することもできます。 など、Microsoft OLE DB Provider for SQL Server を使用して、Microsoft SQL Server でのデータベースにアクセスする、作成を実行するコマンドの複数の入れ子になったトランザクション。  
  
 ADO では、トランザクションでの操作によってデータ ソースへの変更が正常にまとめて、またはまったく発生することです。  
  
 トランザクションをキャンセルした場合、またはその操作のいずれかが失敗した場合、結果が発生トランザクション内の操作のいずれかのようになります。 データ ソースは、トランザクションの開始前に残ります。  
  
 ADO は、トランザクションを制御する次のメソッドを提供します。**BeginTrans**、 **CommitTrans**、および**RollbackTrans**します。 これらのメソッドを使用して、**接続**オブジェクトの保存または一連の 1 つの単位としてソース データに加えられた変更をキャンセルする場合。 たとえば、お金をアカウント間で転送するに 1 つの金額を減算し、追加した同じ量他の。、 更新が失敗するか、口座の残高できなくします。 開いているトランザクション内でこれらの変更により、を介していずれかまたはすべての変更が行われる。  
  
> [!NOTE]
>  トランザクションをサポートしていないすべてのプロバイダー。 いることを確認プロバイダーによって定義されたプロパティ"**トランザクション DDL**"が表示されます、**接続**オブジェクトの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)プロバイダーをサポートしていることを示すコレクショントランザクション。 プロバイダーがトランザクションをサポートしていない場合これらのメソッドのいずれかの呼び出しはエラーを返します。  
  
 呼び出した後、 **BeginTrans**メソッド、プロバイダーが不要になった瞬時に変更がコミットを呼び出すまで**CommitTrans**または**RollbackTrans**を終了しますトランザクションです。  
  
 呼び出す、 **CommitTrans**メソッドは、開いている接続でトランザクション内で行われた変更を保存し、トランザクションを終了します。 呼び出す、 **RollbackTrans**メソッドは、開いているトランザクションで加えられた変更を反転し、トランザクションを終了します。 開いているトランザクションが存在しない場合は、いずれかの方法を呼び出すと、エラーが発生します。  
  
 に応じて、**接続**オブジェクトの[属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティのいずれかを呼び出し、 **CommitTrans**または**RollbackTrans**メソッド可能性があります新しいトランザクションを自動的に開始します。 場合、**属性**プロパティに設定されて**adXactCommitRetaining**、プロバイダーは、後に新しいトランザクションを自動的に開始、 **CommitTrans**呼び出します。 場合、**属性**プロパティに設定されて**adXactAbortRetaining**、プロバイダーは、後に新しいトランザクションを自動的に開始、 **RollbackTrans**呼び出します。  
  
## <a name="transaction-isolation-level"></a>トランザクション分離レベル  
 使用して、 **IsolationLevel**でトランザクションの分離レベルを設定するプロパティを**接続**オブジェクト。 設定は無効になります次に呼び出すまで、 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッド。 要求した分離レベルが使用できない場合、プロバイダーは、次に高い分離レベルを返す可能性があります。 参照してください、 **IsolationLevel** ADO プログラマー リファレンスの詳細については、有効な値のプロパティ。  
  
## <a name="nested-transactions"></a>入れ子になったトランザクション  
 呼び出しを入れ子になったトランザクションをサポートするプロバイダー、 **BeginTrans**開いているトランザクション内でのメソッドは、新しい入れ子になったトランザクションを開始します。 戻り値は、入れ子のレベルを示します戻り値は"1"では、最上位レベルのトランザクションを開いていることを示します (つまり、トランザクションは入れ子になっていない別のトランザクション内で)、"2"では、(2 番目のレベルのトランザクションが開いていることを示します。トランザクション内で入れ子に最上位レベルのトランザクション) など。 呼び出す**CommitTrans**または**RollbackTrans**影響のみ、最後に開いたトランザクション; を閉じるか、上位レベルのトランザクションを解決する前に、現在のトランザクションをロールバックします。
