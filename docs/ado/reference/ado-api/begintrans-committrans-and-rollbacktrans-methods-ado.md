---
title: BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3a8bc22e57d91ab64bdbbc5fc694575a8aa8ff9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920523"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO)
これらのトランザクション メソッド内のトランザクション処理の管理、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの次のようにします。  
  
-   **BeginTrans**新しいトランザクションを開始します。  
  
-   **CommitTrans**変更を保存し、現在のトランザクションを終了します。 新しいトランザクションを開始する場合もします。  
  
-   **RollbackTrans**中、現在のトランザクションに加えられた変更をキャンセルし、トランザクションを終了します。 新しいトランザクションを開始する場合もします。  
  
## <a name="syntax"></a>構文  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>戻り値  
 **BeginTrans**を返す関数として呼び出すことができます、**長い**トランザクションの入れ子レベルを示す変数。  
  
#### <a name="parameters"></a>パラメーター  
 *object*  
 A**接続**オブジェクト。  
  
## <a name="connection"></a>接続  
 これらのメソッドを使用して、**接続**オブジェクトの保存または一連の 1 つの単位としてソース データに加えられた変更をキャンセルする場合。 たとえば、お金をアカウント間で転送するに 1 つの金額を減算し、追加した同じ量他の。、 更新が失敗するか、口座の残高できなくします。 開いているトランザクション内でこれらの変更により、を介していずれかまたはすべての変更が行われる。  
  
> [!NOTE]
>  トランザクションをサポートしていないすべてのプロバイダー。 いることを確認プロバイダーによって定義されたプロパティ"**トランザクション DDL**"が表示されます、**接続**オブジェクトの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)プロバイダーをサポートしていることを示すコレクショントランザクション。 プロバイダーがトランザクションをサポートしていない場合これらのメソッドのいずれかの呼び出しはエラーを返します。  
  
 呼び出した後、 **BeginTrans**メソッド、プロバイダーが不要になった瞬時に変更がコミットを呼び出すまで**CommitTrans**または**RollbackTrans**を終了しますトランザクションです。  
  
 呼び出しを入れ子になったトランザクションをサポートするプロバイダー、 **BeginTrans**開いているトランザクション内でのメソッドは、新しい入れ子になったトランザクションを開始します。 戻り値は、入れ子のレベルを示します戻り値は"1"では、最上位レベルのトランザクションを開いていることを示します (つまり、トランザクションは入れ子になっていない別のトランザクション内で)、"2"では、(2 番目のレベルのトランザクションが開いていることを示します。トランザクション内で入れ子に最上位レベルのトランザクション) など。 呼び出す**CommitTrans**または**RollbackTrans**影響のみ、最後に開いたトランザクション; を閉じるか、上位レベルのトランザクションを解決する前に、現在のトランザクションをロールバックします。  
  
 呼び出す、 **CommitTrans**メソッドは、開いている接続でトランザクション内で行われた変更を保存し、トランザクションを終了します。 呼び出す、 **RollbackTrans**メソッドは、開いているトランザクションで加えられた変更を反転し、トランザクションを終了します。 開いているトランザクションが存在しない場合は、いずれかの方法を呼び出すと、エラーが発生します。  
  
 に応じて、**接続**オブジェクトの[属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティのいずれかを呼び出し、 **CommitTrans**または**RollbackTrans**メソッド可能性があります新しいトランザクションを自動的に開始します。 場合、**属性**プロパティに設定されて**adXactCommitRetaining**、プロバイダーは、後に新しいトランザクションを自動的に開始、 **CommitTrans**呼び出します。 場合、**属性**プロパティに設定されて**adXactAbortRetaining**、プロバイダーは、後に新しいトランザクションを自動的に開始、 **RollbackTrans**呼び出します。  
  
## <a name="remote-data-service"></a>リモート データ サービス  
 **BeginTrans**、 **CommitTrans**、および**RollbackTrans**メソッドは、クライアント側で使用されていない**接続**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [BeginTrans、CommitTrans、および RollbackTrans メソッドの例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッドの例 (vc++)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes プロパティ (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
