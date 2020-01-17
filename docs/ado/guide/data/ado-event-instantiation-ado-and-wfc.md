---
title: 'ADO イベントのインスタンス化: ADO および WFC |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dbbbf92c751093d2a7333b7ac1f76888d41d345
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212343"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO イベントのインスタンス化: ADO と WFC
Windows Foundation クラス用の ADO (ADO/WFC) は ADO イベントモデルに基づいて構築されており、簡略化されたアプリケーションプログラミングインターフェイスを提供します。 一般に、ADO/WFC は ADO イベントをインターセプトし、イベントパラメーターを1つのイベントクラスに統合してから、イベントハンドラーを呼び出します。  
  
### <a name="to-use-ado-events-in-adowfc"></a>Ado/WFC で ADO イベントを使用するには  
  
1.  イベントを処理する独自のイベントハンドラーを定義します。 たとえば、 **connectionevent**ファミリで**connectcomplete**イベントを処理する場合は、次のコードを使用できます。  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  イベントハンドラーを表すハンドラーオブジェクトを定義します。 ハンドラーオブジェクトは、 **Connectionevent**型のイベントの場合はデータ型**Connecteventhandler** 、 **RecordsetEvent**型のイベントの場合はデータ型**RecordsetEventHandler**である必要があります。 たとえば、 **Connectcomplete**イベントハンドラーに対して次のコードを記述します。  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     **Connectioneventhandler**コンストラクターの最初の引数は、2番目の引数で指定されたイベントハンドラーを含むクラスへの参照です。  
  
3.  特定の種類のイベントを処理するために指定されたハンドラーの一覧に、イベントハンドラーを追加します。 メソッドには、 **addOn**_EventName_(*handler*) などの名前を指定します。  
  
4.  ADO/WFC は、内部的にすべての ADO イベントハンドラーを実装します。 このため、**接続**または**レコードセット**操作によって発生したイベントは、ADO/WFC イベントハンドラーによってインターセプトされます。  
  
     Ado/WFC イベントハンドラーは、ado/wfc **connectionevent**クラスのインスタンス、または ADO/wfc **RecordsetEvent**クラスのインスタンスの ADO **RecordsetEvent**パラメーターに ado **connectionevent**パラメーターを渡します。 これらの ADO/WFC クラスは、ADO イベントパラメーターを統合します。つまり、各 ADO/WFC クラスには、すべての ADO **Connectionevent**メソッドまたは**RecordsetEvent**メソッドの一意のパラメーターごとに1つのデータメンバーが含まれています。  
  
5.  ADO/WFC は、ADO/WFC イベントオブジェクトを使用してイベントハンドラーを呼び出します。 たとえば、 **Onconnectcomplete**ハンドラーには次のようなシグネチャがあります。  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     最初の引数は、イベント ([接続](../../../ado/reference/ado-api/connection-object-ado.md)または[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)) を送信したオブジェクトの種類です。2番目の引数は、ADO/WFC イベントオブジェクト (**connectionevent**または**RecordsetEvent**) です。  
  
     イベントハンドラーのシグネチャは、ADO イベントよりも簡単です。 ただし、イベントに適用されるパラメーターと応答方法を把握するには、ADO イベントモデルを理解している必要があります。  
  
6.  イベントハンドラーから ADO イベントの ADO/WFC ハンドラーに戻ります。 Ado/WFC は、関連する ADO/WFC イベントデータメンバーを ADO イベントパラメーターにコピーしてから、ADO イベントハンドラーから戻ります。  
  
7.  処理が完了したら、ADO/WFC イベントハンドラーの一覧からハンドラーを削除します。 メソッドに**Removeon**_EventName_(*handler*) などの名前を指定します。  
  
## <a name="see-also"></a>参照  
 [ADO イベントハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 構文のインデックス](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [イベントパラメーター](../../../ado/guide/data/event-parameters.md)   
 [イベントハンドラーの連携方法](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [イベントの種類](../../../ado/guide/data/types-of-events.md)
