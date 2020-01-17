---
title: レプリケートされたテーブルを比較して相違があるかどうかを確認する (レプリケーション プログラミング) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- tablediff utility
- comparing replicated tables
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 94d3faab4c831fe64e54a582a5f70b2ae6b664e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210787"
---
# <a name="compare-replicated-tables-for-differences-replication-programming"></a>レプリケートされたテーブルを比較して相違があるかどうかを確認する (レプリケーション プログラミング)
  テーブルのアーティクル用にパブリッシュされたデータが、パブリッシャー側とサブスクライバー側とで異なっていると、データが収束しない可能性があります。アーティクルを検証することにより、両者に相違点が存在するかどうかを確認できます。 詳細については、「[レプリケートされたデータの検証](../validate-data-at-the-subscriber.md)」をご覧ください。 ただし、検証によって返されるのは、一致しているかどうかという情報だけであり、両者のテーブル間の相違について、それ以上詳しい情報は提供されません。 **tablediff** コマンド プロンプト ユーティリティを使用すると、2 つのテーブル間の詳細な相違点を取得できるだけでなく、サブスクリプションをパブリッシャー側のデータに収束させるための [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトを生成することもできます。  
  
> [!NOTE]  
>  **tablediff** ユーティリティは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サーバーでのみサポートされます。  
  
### <a name="to-compare-replicated-tables-for-differences-using-tablediff"></a>tablediff を使用してレプリケートされたテーブルを比較し相違点を確認するには  
  
1.  レプリケーション トポロジの任意のサーバーで、コマンド プロンプトから [tablediff Utility](../../../tools/tablediff-utility.md)を実行します。 次のパラメーターを指定します。  
  
    -   **-sourceserver** - データが正しいとわかっている方のサーバー (通常はパブリッシャー) の名前。  
  
    -   **-sourcedatabase** - 正しいデータが格納されているデータベースの名前。  
  
    -   **-sourcetable** - アーティクルの比較元テーブルの名前。  
  
    -   (省略可) **-sourceschema** - 比較元テーブルのスキーマ所有者 (既定のスキーマを使用しない場合)。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合は、 **-sourceuser** および **-sourcepassword** を指定します。  
  
        > [!IMPORTANT]  
        >  可能な場合は、Windows 認証を使用します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用する必要がある場合は、セキュリティ資格情報の入力を、ユーザーに対して実行時に求めるようにしてください。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
    -   **-destinationserver** - 比較対象のデータが格納されているサーバー (通常はサブスクライバー) の名前。  
  
    -   **-destinationdatabase** - 比較対象データベースの名前。  
  
    -   **-destinationtable** - 比較対象テーブルの名前。  
  
    -   (省略可) **-destinationschema** - 比較対象テーブルのスキーマの所有者 (既定のスキーマを使用しない場合)。  
  
    -   (省略可) **認証を使用してサブスクライバーに接続する場合は、** -destinationuser **および** -destinationpassword [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。  
  
        > [!IMPORTANT]  
        >  可能な場合は、Windows 認証を使用します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用する必要がある場合は、セキュリティ資格情報の入力を、ユーザーに対して実行時に求めるようにしてください。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
    -   (省略可) 列レベルの比較を行う場合は、 **-c** を使用します。  
  
    -   (省略可) 短時間で処理が済むように行数およびスキーマのみの比較を行う場合は、 **-q** を使用します。  
  
    -   (省略可) **-o** に、結果の出力先ファイルの名前とパスを指定します。  
  
    -   (省略可) 結果を挿入するサブスクリプション データベース内のテーブルを **-et**に指定します。 テーブルが既に存在する場合は、 **-dt** を指定して、最初にテーブルを削除します。  
  
    -   (省略可) サブスクライバー側のデータをパブリッシャー側のデータと一致するように修正するための **ファイルを生成する場合は、** -f [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用します。 各ファイルの **ステートメントの数を指定するには、** -df [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用します。  
  
    -   (省略可) 操作を再試行する回数と再試行間隔を指定するには、 **-rc** および **-ri** を使用します。  
  
    -   (省略可) 比較元テーブルと比較先テーブル間の完全なスキーマの比較を実行するには、 **-strict** を使用します。  
  
## <a name="see-also"></a>関連項目  
 [サブスクライバーでのデータの検証](../validate-data-at-the-subscriber.md)  
  
  
