---
title: その他の SQL Server 以外のサブスクライバー | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dce8d383ca01fd205645a18f7aa181d12cff4675
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110949"
---
# <a name="other-non-sql-server-subscribers"></a>その他の SQL Server 以外のサブスクライバー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] がサポートしている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーの一覧については、「[SQL Server 以外のサブスクライバー](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。 ここでは、ODBC ドライバーと OLE DB プロバイダーの要件について説明します。  
  
## <a name="odbc-driver-requirements"></a>ODBC ドライバーの要件  
 ODBC ドライバーは、以下の要件を満たす必要があります。  
  
-   ODBC Level-1 に準拠している  
  
-   スレッド セーフのディストリビューター環境である  
  
-   トランザクションの実行が可能である  
  
-   データ定義言語 (DDL) をサポートする  
  
-   読み取り専用にはできない  
  
-   **MSreplication_subscriptions**などの長いテーブル名をサポートしている  
  
## <a name="replicating-using-ole-db-interfaces"></a>OLE DB インターフェイスを使用するレプリケーション  
 トランザクション レプリケーションを行うには、OLE DB プロバイダーが以下のオブジェクトをサポートする必要があります。  
  
-   **DataSource** オブジェクト  
  
-   **Session** オブジェクト  
  
-   **Command** オブジェクト  
  
-   **Rowset** オブジェクト  
  
-   **Error** オブジェクト  
  
### <a name="datasource-object-interfaces"></a>DataSource オブジェクト インターフェイス  
 データ ソースに接続するためには、以下のインターフェイスが必要です。  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 プロバイダーが **IDBInfo** インターフェイスをサポートしている場合、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はこのインターフェイスを使用して、引用符で囲まれた識別子、SQL ステートメントの最大長、テーブル名と列名の最大文字数などの情報を取得します。  
  
### <a name="session-object-interfaces"></a>Session オブジェクト インターフェイス  
 以下のインターフェイスが必要です。  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Command オブジェクト インターフェイス  
 以下のインターフェイスが必要です。  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** は、パラメーター アクセサーを作成するために必要です。 プロバイダーが **IColumnRowset**をサポートしている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はこのインターフェイスを使用して列が ID 列であるかどうかを判断します。  
  
### <a name="rowset-object-interfaces"></a>Rowset オブジェクト インターフェイス  
 以下のインターフェイスが必要です。  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 アプリケーションは、サブスクリプション データベース内に作成された、レプリケートされるテーブル上の行セットを開く必要があります。 **IColumnsInfo** と **IAccessor** は、その行セット内のデータにアクセスするために必要です。  
  
### <a name="error-object-interfaces"></a>Error オブジェクト インターフェイス  
 エラーの管理には、以下のインターフェイスを使用します。  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 **ISQLErrorInfo** は、OLE DB プロバイダーが ISQLErrorInfo をサポートしている場合に使用します。  
  
 OLE DB プロバイダーの詳細については、OLE DB プロバイダー付属のマニュアルを参照してください。  
  
## <a name="see-also"></a>参照  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  
