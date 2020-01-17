---
title: SSMA for DB2 クライアントのインストール (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/07/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1623430eed752db7fa387caf33124082eb318490
ms.sourcegitcommit: 243925311cc952dd455faea3c1156e980959d6de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70774185"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>SSMA for DB2 クライアントのインストール (DB2ToSQL)

SSMA クライアントは、次のタスクを実行するプログラムファイルで構成されています。  
  
- DB2 データベースに接続します。  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する。  
  
- DB2 データベースオブジェクトを構文[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に変換します。  
  
- オブジェクトをに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]読み込みます。  
  
- データをに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行します。  
  
このトピックでは、SSMA のインストールの前提条件と手順について説明します。  
  
## <a name="prerequisites"></a>前提条件

Ssma は、for z/OS バージョン9.0 および10.0 または db2 on luw バージョン9.8 および10.1 以降のバージョンおよび[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 以降のバージョンで動作するように設計されています。  
  
SSMA をインストールする前に、コンピューターが次の要件を満たしていることを確認してください。  
  
- Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows インストーラー3.1 以降のバージョン。  
  
- バージョン[!INCLUDE[msCoName](../../includes/msconame_md.md)] 4.0 以降の[!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]バージョン。 バージョン[!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]製品メディアで入手できます。 また、 [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手することもできます。  
  
- Microsoft OLEDB Provider for DB2 version 5 以降のバージョン、および移行する DB2 データベースへの接続。  
  
- にアクセスし、データベースオブジェクトとデータの移行先となる、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB のターゲットインスタンスをホストするコンピューターに対して十分なアクセス許可を付与します。 詳細については、「 [SQL Server &#40;DB2eToSQL&#41;への接続](../../ssma/db2/connecting-to-sql-server-db2etosql.md)」を参照してください。  
  
- 4 GB の RAM を推奨します。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  

DB2 バージョン6.0 の OLEDB プロバイダーをダウンロードするには、 [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)」を参照してください。

SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmafordb2)を参照してください。  
  
最新バージョンをダウンロードしたら、SSMA をインストールできるようにインストールファイルを抽出します。  
  
SSMA クライアントをインストールするには:
  
1. SSMA for DB2 *n*をダブルクリックします。Setup.exe をインストールします。ここで、 *n*はビルド番号です。  
  
2. **[ようこそ]** ページで、 **[次へ]** を選択します。  
  
   前提条件がインストールされていない場合は、最初に必要なコンポーネントをインストールする必要があることを示すメッセージが表示されます。 すべての前提条件がインストールされていることを確認してから、インストールプログラムを再実行してください。  
  
3. 使用許諾契約書を確認します。 同意する場合は、 **[使用許諾契約書に同意]** します を選択し、 **[次へ]** を選択します。  
  
4. **[セットアップの種類の選択]** ページで、 **[標準]** を選択します。  
  
5. **[インストール]** を選択します。  
  
> [!IMPORTANT]  
> 新しいバージョンをインストールする前に、SSMA for DB2 の以前のバージョンをすべてアンインストールしてください。
  
既定のインストール場所は、DB2 の場合は C:\Program の SQL Server Migration Assistant です。  
  
## <a name="see-also"></a>関連項目

[SQL Server &#40;DB2ToSQL への Ssma コンポーネントのインストール&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[DB2 データベースの SQL Server &#40;DB2ToSQL への移行&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
