---
title: Linux と macOS の ODBC ドライバー - 高可用性とディザスター リカバリー | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08fb8cc6e54fff4b315a0a98ace046a49b2673a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008767"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Linux と macOS の ODBC ドライバーでの高可用性とディザスター リカバリーのサポート
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux および macOS 用の ODBC ドライバーは [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] をサポートしています。 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]の詳細については、以下を参照してください。  
  
-   [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー (SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [可用性グループの作成と構成 (SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [フェールオーバー クラスタリングと AlwaysOn 可用性グループ (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ (AlwaysOn 可用性グループ)](https://msdn.microsoft.com/library/ff878253.aspx)  
  
接続文字列で、特定の可用性グループの可用性グループ リスナーを指定できます。 Linux または macOS 上の ODBC アプリケーションが、フェールオーバーする可用性グループ内のデータベースに接続されている場合、元の接続が切断されるため、フェールオーバー後にアプリケーションが動作を継続するには新しい接続を開く必要があります。

Linux および macOS 上の ODBC ドライバーでは、可用性グループ リスナーに接続しておらず、ホスト名に複数の IP アドレスが関連付けられている場合、DNS ホスト名に関連付けられているすべての IP アドレスが順次繰り返し処理されます。

DNS サーバーから最初に返された IP アドレスに接続できない場合、このような繰り返し処理には時間がかかる可能性があります。 可用性グループ リスナーに接続するとき、ドライバーではすべての IP アドレスに対して並列して接続の確立が試みられます。 接続試行が成功すると、ドライバーは保留状態の接続試行をすべて破棄します。

> [!NOTE]  
> 可用性グループのフェールオーバーにより接続が失敗する可能性があるため、失敗した接続が再接続されるまで再試行する接続再試行ロジックを実装します。 接続タイムアウトを長くして、接続再試行ロジックを実装すると、可用性グループに接続できる可能性が高くなります。

## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続

[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 可用性グループ リスナーまたは [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] フェールオーバー クラスター インスタンスに接続するときは、常に **MultiSubnetFailover=Yes** を指定します。 **MultiSubnetFailover** を使用すると、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] のすべての可用性グループとフェールオーバー クラスター インスタンスで高速にフェールオーバーできます。 また、**MultiSubnetFailover** によって、単一およびマルチサブネットの AlwaysOn トポロジのフェールオーバー時間が大幅に短縮されます。 マルチサブネット フェールオーバーの場合、クライアントは複数の接続を並列で試行します。 サブネット フェールオーバーの場合、ドライバーは TCP 接続を積極的に再試行します。

**MultiSubnetFailover** 接続プロパティは、可用性グループまたはフェールオーバー クラスター インスタンスにアプリケーションが配置されていることを示します。 ドライバーでは、すべての IP アドレスに対する接続を試行することで、プライマリ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上のデータベースへの接続が試みられます。 **MultiSubnetFailover=Yes** を指定して接続している場合、クライアントでは、オペレーティング システムの既定の TCP 再送信間隔より短い間隔で TCP 接続が再試行されます。 **MultiSubnetFailover=Yes** を指定すると、AlwaysOn 可用性グループまたは AlwaysOn フェールオーバー クラスター インスタンスのフェールオーバー後に、短時間で再接続できます。 **MultiSubnetFailover=Yes** は、単一およびマルチサブネットの可用性グループとフェールオーバー クラスター インスタンスの両方に適用されます。  

可用性グループ リスナーまたはフェールオーバー クラスター インスタンスに接続する場合は、 **MultiSubnetFailover=Yes** を使用します。 それ以外の場合、アプリケーションのパフォーマンスは低下する可能性があります。

可用性グループまたはフェールオーバー クラスター インスタンス内のサーバーに接続するときは、次のことに注意してください。
  
-   単一サブネットまたは複数サブネットの可用性グループに接続するときのパフォーマンスを向上するには、**MultiSubnetFailover=Yes** を指定します。

-   接続文字列でサーバーとして、可用性グループの可用性グループ リスナーを指定します。
  
-   IP アドレス数が 64 個を超える構成の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスには接続できません。

-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証または Kerberos 認証のいずれも、アプリケーションの動作に影響を与えることなく **MultiSubnetFailover=Yes** と併用できます。

-   **loginTimeout** の値を増やすことで、フェールオーバー時間に対応し、アプリケーションの接続試行回数を減らすことができます。

-   分散トランザクションはサポートされていません。  
  
読み取り専用のルーティングが無効である場合、次の状況では可用性グループのセカンダリ レプリカの場所には接続できません。  
  
1.  セカンダリ レプリカの場所が、接続を許可するように構成されていない。  
  
2.  アプリケーションに **ApplicationIntent=ReadWrite** が使用されているが、セカンダリ レプリカの場所が読み取り専用アクセスとして構成されている。  
  
プライマリ レプリカが読み取り専用ワークロードを拒否するように構成されているとき、接続文字列に **ApplicationIntent=ReadOnly**が含まれていると、接続は失敗します。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>ODBC 構文

次の 2 つの ODBC 接続文字列キーワードは、[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]をサポートしています。  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
ODBC 接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
対応する接続属性は次のとおりです。
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
ODBC 接続プロパティの詳細については、「[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)」を参照してください。  
  
[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]を使用する ODBC アプリケーションでは、2 つの関数のいずれかを使用して接続できます。  
  
|機能|[説明]|  
|------------|---------------|  
|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** では、データ ソース名 (DSN) または接続属性を介して、**ApplicationIntent** と **MultiSubnetFailover** の両方がサポートされています。|  
|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** では、DSN、接続文字列キーワード、または接続属性を介して、**ApplicationIntent** と **MultiSubnetFailover** がサポートされています。|
  
## <a name="see-also"></a>参照  

[接続文字列のキーワードとデータ ソース名 (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[プログラミング ガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)

[リリース ノート](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
