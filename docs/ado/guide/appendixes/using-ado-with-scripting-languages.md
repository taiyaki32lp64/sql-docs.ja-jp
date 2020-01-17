---
title: スクリプト言語と ADO の併用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b322dacbf85ec24b58e315ecbbf9d547d1481f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926488"
---
# <a name="using-ado-with-scripting-languages"></a>スクリプト言語で ADO を使用する
ADO では、スクリプトの環境では、サーバー側のスクリプトを使用してデータを公開できます。 このシナリオでは、ADO では、基になる OLE DB プロバイダーを使用して、特定のデータ ストアを参照するために必要なその他のコンポーネントは、インターネット インフォメーション サービス (IIS) を実行しているサーバーにインストールされています。 Active Server Pages (ASP) を使用して、ADO は、たとえば、HTML を生成するスクリプトで参照されているコンポーネントです。 この HTML コンテンツは、クライアント Web ブラウザーに HTTP 経由で渡されることができます。 スクリプトを使用して、Web ページはサーバー側スクリプトは、更新、移動、および特定のデータを表示することができますに戻すアクションを送信できます。  
  
 ActiveX オブジェクトを使用するには、Web ページで、前に、オブジェクトが安全であるかどうかを知る必要があります。 オブジェクトがスクリプトにとって安全だと見なされると、コントロールがユーザーのコンピューターに対して有害なアクションを実行することはできず、ユーザーの承認を求められることがなく実行されることを意味します。 次の表では、ADO オブジェクトを一覧表示し、安全であるかどうかを示します。  
  
|オブジェクト|安全なスクリプトでしょうか。|  
|------------|-------------------------|  
|ADO 接続|はい|  
|ADO コマンド|いいえ|  
|ADO パラメーター|いいえ|  
|ADO レコード セット|[はい]|  
|ADO レコード|[はい]|  
|ADO Stream|[はい]|  
|ADO エラーです。|いいえ|  
|ADOX のカタログ|いいえ|  
|ADOX のセル セット|いいえ|  
|RDS DataControl|[はい]|  
|RDS DataSpace|はい|  
|RDS DataFactory|いいえ|  
  
 次の表では、Windows DAC/MDAC に含まれるプロバイダーの一覧し、安全であるかどうかを示します。  
  
|プロバイダー|安全なスクリプトでしょうか。|  
|--------------|-------------------------|  
|図形|はい|  
|永続化します。|[はい]|  
|Remote|はい|  
|OLE DB Provider for SQL Server (SQLOLEDB)|いいえ|  
|OLE DB Provider for ODBC (MSDASQL)|いいえ|  
  
## <a name="odbc-data-sources"></a>ODBC データ ソース  
 スクリプトとスクリプト以外の ADO コードの大きな違いの 1 つは、使用されている場合に、ODBC データ ソースが。 アプリケーションのスクリプト以外では、ODBC データ ソース アドミニストレーターのユーザー DSN を作成できます。 IIS で実行されているスクリプトでは、システム DSN を作成する必要があります。それ以外の場合、スクリプトには、作成したデータ ソースは認識されません。 これは、Microsoft IIS を通じて ODBC の Microsoft OLE DB プロバイダーを使用する ADO スクリプト アプリケーションに適用されます。  
  
## <a name="referencing-the-ado-library"></a>ADO ライブラリを参照します。  
 スクリプト言語では適用されません。  
  
## <a name="handling-events"></a>イベントの処理  
 スクリプト言語では適用されません。  
  
 次のトピックでは、スクリプト言語で ADO の使用に関する詳細情報を紹介します。  
  
-   [VBScript での ADO プログラミング](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [JScript での ADO プログラミング](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>関連項目  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Microsoft Visual Basic で ADO を使用します。](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Microsoft Visual C++ での ADO の使用](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
