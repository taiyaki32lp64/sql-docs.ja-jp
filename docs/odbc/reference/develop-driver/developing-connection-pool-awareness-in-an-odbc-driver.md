---
title: ODBC ドライバー対応接続プールの開発 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02577370218a799faf86a7f8986859c415962f5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897735"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC ドライバー対応接続プールの開発
このトピックでは、ドライバーが接続プールのサービスを提供する方法に関する情報を含む ODBC ドライバーの開発の詳細について説明します。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>ドライバー対応接続プールを有効にします。  
 ドライバーは、次の ODBC サービス プロバイダー インターフェイス (SPI) 関数を実装する必要があります。  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 参照してください[ODBC サービス プロバイダー インターフェイス (SPI) リファレンス](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)詳細についてはします。  
  
 ドライバー対応のプールを有効にできるようにドライバーも次の既存の関数を実装する必要があります。  
  
|関数|追加された機能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|新しいハンドル型のサポート:SQL_HANDLE_DBC_INFO_TOKEN (以下の説明を参照してください)。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|新しい設定専用の接続属性をサポートしてください。接続をリセットするための SQL_ATTR_DBC_INFO_TOKEN (以下の説明を参照してください)。|  
  
> [!NOTE]  
>  非推奨の関数など**SQLError**と**SQLSetConnectOption**ドライバー対応接続プールはサポートされていません。  
  
## <a name="the-pool-id"></a>プール ID  
 プールの ID を置き換えて使用できる接続の特定のグループを表すポインター長さドライバー固有の ID です。 接続情報を指定するドライバーは迅速に対応するプールの ID を推定することが  
  
 たとえば、プール ID は、サーバー名と資格情報をエンコードする必要があります。 ただし、ドライバーは接続を再利用し、新しい接続を作成するよりも短時間でデータベースを変更できる場合がありますので、データベース名は必要ありません。  
  
 ドライバーはプール ID を構成するキーの属性のセットを定義する必要があります。 これらのキー属性の値は、接続属性、接続文字列、および DSN から取得できます。 これらのソースでの競合がある場合は、旧バージョンとの互換性のため、既存のドライバー固有の解決ポリシーを使用してください。  
  
 ドライバー マネージャーでは、別のプールを別のプール Id を使用します。 同じプール内のすべての接続が再利用します。 ドライバー マネージャーが別のプール ID を持つ接続を再利用しません。  
  
 そのためのドライバーは、定義済みのキー属性の値が同じ接続のすべてのグループの一意のプール ID を割り当てる必要があります。 ドライバーでは、そのキー属性の値が異なる 2 つの接続に、同じプール ID を使用している場合、ドライバー マネージャーは配置に (ドライバー マネージャーを使うと、ドライバー固有のキー属性について何も知っている)、同じプールにです。 これは、ドライバーをドライバー マネージャー内で再利用可能なないさまざまな一連のキー属性との接続を報告する必要があることを意味[SQLRateConnection 関数](../../../odbc/reference/syntax/sqlrateconnection-function.md)します。 パフォーマンスが低下することができ、これは推奨されません。  
  
 ドライバー マネージャーには、すべての接続情報と一致する場合でも、別のドライバー環境から割り当てられている接続が再利用されます。 ドライバー マネージャーは、接続があるプール ID が同じ場合でもに、さまざまな環境では、別のプールが使用されます。 そのため、プール ID は、そのドライバー環境に対してローカルです。  
  
 ドライバーからプール ID を取得するための関数は[SQLGetPoolID 関数](../../../odbc/reference/syntax/sqlgetpoolid-function.md)します。  
  
## <a name="the-connection-rating"></a>接続の評価  
 比較して新しい接続を確立、プールされた接続の一部の接続情報 (データベースなど) をリセットすることでパフォーマンスの向上を取得できます。 そのため、データベース名を一連のキー属性に存在しない可能性があります。 それ以外の場合、お客様がさまざまな異なる接続文字列を使用して各データベースでは、中間層アプリケーションで優れたできない可能性があります、独立したプールすることができます。  
  
 いくつかの属性の不一致を含む接続を再利用するたびに、新しいアプリケーションの要求に基づいてが一致しない属性をリセットする必要がありますように返される接続は、アプリケーションの要求と同じです (SQL_ATTR 属性の説明を参照してください。_DBC_INFO_TOKEN [SQLSetConnectAttr 関数](https://go.microsoft.com/fwlink/?LinkId=59368))。 ただし、これらの属性をリセットするとパフォーマンスが低下する可能性があります。 たとえば、データベースをリセットするには、サーバーへのネットワーク呼び出しが必要です。 そのためがある場合は、完全に一致する接続を再利用します。  
  
 ドライバーで評価関数は、新しい接続要求を既存の接続を評価できます。 たとえば、ドライバーの評価の関数を特定できます。  
  
-   場合は、既存の接続は、要求で完全に一致します。  
  
-   のみによって意味のないなどの接続タイムアウトをリセットするには、サーバーとの通信を必要としません。  
  
-   リセットするには、サーバーとの通信を必要とするが、新しい接続を確立するよりも優れたパフォーマンスにもなるいくつかの一致しない属性があります。 場合、  
  
-   不一致が発生したかどうか、属性をリセットする非常に時間がかかるの (ドライバーの開発を検討できますにプール ID の生成に使用される一連のキー属性は、この属性を追加する)。  
  
 0 ~ 100 のスコアは、可能な限り、0 の場合は再利用しないと 100 に完全に一致するとは。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)は接続を評価する関数です。  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>新しい ODBC ハンドルの SQL_HANDLE_DBC_INFO_TOKEN  
 ドライバー対応接続プールをサポートするために、ドライバーは接続については、プールの ID を計算する必要があります。 ドライバーでは、接続情報で、プールの接続の新しい接続要求を比較する必要もあります。  プール内の接続を再利用できるなし、たびに、ドライバーは接続情報を必要とするため、新しい接続を確立するためには。  
  
 接続情報は、複数のソース (接続文字列、接続属性、および DSN) から取得できます、ため、ドライバーは接続文字列を解析し、これらの関数の呼び出しを上記の各ソース間の競合を解決する必要があります。  
  
 そのため、新しい ODBC ハンドルが導入されています。SQL_HANDLE_DBC_INFO_TOKEN します。 SQL_HANDLE_DBC_INFO_TOKEN で、ドライバーは接続文字列を解析し、複数回接続情報の競合を解決する必要はありません。 これは、ドライバー固有のデータ構造であるため、ドライバーは接続情報などのデータを格納またはプールの id。  
  
 このハンドルは、ドライバー マネージャーとドライバーの間のインターフェイスとしてのみ使用されます。 アプリケーションでは、このハンドルを直接割り当てることができません。  
  
 このハンドルの親ハンドルでは、型 sql_handle_env として、つまり、ドライバーが接続情報の解決中に、HENV ハンドルから環境情報を取得できることです。  
  
 新しい接続要求を受信すると、ドライバー マネージャーはドライバー対応接続プールをサポートしていることを確認した後に、接続情報を格納するため SQL_HANDLE_DBC_INFO_TOKEN の種類のハンドルを割り当てます。 ハンドルの使用を完了すると (を返す前に、いくつかのリターン コードを SQL_STILL_EXECUTING 以外が[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)または[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))、ドライバー マネージャーは、ハンドルを解放します。 そのため、ハンドルでは、SQLAllocHandle の呼び出しの後に作成され、SQLFreeHandle 呼び出しの後に破棄されます。 ドライバー マネージャーでは、関連付けられている HENV を解放する前に、ハンドルが解放されますが保証されます (と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)または[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)エラーが返されます)。  
  
 ドライバーは、新しいハンドル型 SQL_HANDLE_DBC_INFO_TOKEN を受け入れるように、次の関数を変更する必要があります。  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 ドライバー マネージャーは、複数のスレッドが同じ SQL_HANDLE_DBC_INFO_TOKEN ハンドルを同時に使用してしないことを保証します。 そのため、このハンドルの同期モデルはドライバー内部の非常に簡単にできます。 ドライバー マネージャーでは、割り当てと SQL_HANDLE_DBC_INFO_TOKEN を解放する前に、環境のロックは実行されません。  
  
 ドライバー マネージャーの**SQLAllocHandle**と**SQLFreeHandle**この新しい種類のハンドルを受け入れません。  
  
 SQL_HANDLE_DBC_INFO_TOKEN には、資格情報などの機密情報を含めることができます。 そのため、ドライバーではメモリ バッファーをクリアに安全に (を使用して[SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) では、このハンドルを解放する前に機密性の高い情報を含む**SQLFreeHandle**します。 アプリケーションの環境ハンドルが閉じられたときにすべての関連付けられている接続プールは閉じられます。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>ドライバー マネージャーの接続プールのアルゴリズムの評価  
 このセクションでは、ドライバー マネージャーの接続プールの評価のアルゴリズムについて説明します。 ドライバー開発者は、旧バージョンとの互換性のため、同じアルゴリズムを実装できます。 このアルゴリズムは、最適なものをできない可能性があります。 これを調整する必要があります、実装に基づくアルゴリズム (それ以外の場合はこの機能を実装する理由)。  
  
 ドライバー マネージャーは、プールからの接続ごとに 100、0 から整数の評価を返します。 0 は、接続を再利用できないし、100 を指定する最適なソリューションの一致を意味します。 接続要求が hRequest をという名前し、プールから既存の接続には hCandidate という名前を想定しています。 次の条件のいずれかが false の場合、プールされた接続 hCandidate が hRequest (ドライバー マネージャーは、レベル 0 を割り当てられます) の再利用できません。  
  
-   hCandidate と hRequest (SQLDriverConnectW) などの UNICODE API、または (SQLDriverConnectA) などの ANSI API に由来します。 (UNICODE ドライバーには、ANSI API と UNICODE API (SQL_ATTR_ANSI_APP 接続属性を参照してください) とは異なる動作ことができます)。  
  
-   hCandidate と hRequest は同じこの関数によって作成されます。SQLDriverConnect または SQLConnect のいずれか。  
  
-   SQLDriverConnect を使用する場合は、hCandidate を開くために使用する接続文字列は hRequest と同じである必要があります。  
  
-   サーバー名 (または DSN) のユーザー名と hCandidate を開くために使用するパスワードには、同じ SQLConnect を使用する場合は、hRequest を開くために使用する必要があります。  
  
-   HCandidate を開くために使用する、SID とは、現在のスレッドのセキュリティ識別子 (SID) は同じである必要があります。  
  
-   参加および参加解除するにはコストがドライバー (SQL_DTC_TRANSITION_COST での説明を参照してください。 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))、再利用*hRequest* 、余分な参加または参加解除が必要としない必要があります。  
  
 次の表では、さまざまなシナリオのスコア付けの割り当てを示します。  
  
|プールされた接続と要求の間の接続属性の比較|なしの参加/参加解除|余分な参加する必要は/参加解除|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|カタログ (SQL_ATTR_CURRENT_CATALOG) が異なる|60|50|  
|いくつかの接続属性は異なりますが、カタログは、同じ|90|70|  
|完全に一致するすべての接続属性|100|80|  
  
## <a name="sequence-diagram"></a>シーケンス図  
 このシーケンス図では、このトピックで説明されている基本的なプーリング メカニズムを示します。 使用だけが表示されます[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)が、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)ケースは似ています。  
  
 ![シーケンス図](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>状態ダイアグラム  
 この状態の図は、接続情報のトークン オブジェクト、このトピックで説明を示します。 のみが表示されます、ダイアグラム[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)が、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)ケースは似ています。 ドライバー マネージャーを呼び出すことができます、ドライバー マネージャーは、いつでもエラーを処理する必要があります、ため[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)のいずれかの状態。  
  
 ![状態図](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>関連項目  
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC サービス プロバイダー インターフェイス (SPI) リファレンス](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
