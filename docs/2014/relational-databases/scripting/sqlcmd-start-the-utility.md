---
title: sqlcmd ユーティリティの起動
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f8f63b4ddb3e8641ef503a615d57c63be35164
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243267"
---
# <a name="start-the-sqlcmd-utility"></a>sqlcmd ユーティリティの起動
  
  `sqlcmd` を使用するには、最初にユーティリティを起動し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する必要があります。 既定のインスタンスまたは名前付きインスタンスのいずれにも接続できます。 最初の手順として、`sqlcmd` ユーティリティを起動します。  
  
> [!NOTE]  
>  
  `sqlcmd` の既定の認証は Windows 認証です。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するには、 **-U** オプションと **-P** オプションを追加して、ユーザー名とパスワードを指定する必要があります。  
  
> [!NOTE]  
>  既定では、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] は名前付きインスタンスの **sqlexpress**としてインストールされます。  
  
 
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のこのインスタンスに接続したことがない場合、接続を受け入れるには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の構成が必要になることがあります。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>sqlcmd ユーティリティを起動し、SQL Server の既定のインスタンスに接続するには  
  
1.  [**スタート**] メニューの [**実行**] をクリックします。 
  **[名前]** ボックスに「 **cmd**」と入力して、 **[OK]** をクリックします。コマンド プロンプト ウィンドウが開きます  
  
2.  コマンド プロンプトで「 `sqlcmd`」と入力します。  
  
3.  Enter キーを押します。  
  
     これで、コンピューターで実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスに、信頼できる接続を確立しました。  
  
     **1>** 行番号`sqlcmd`を指定するプロンプトです。 Enter キーを押すたびに、この番号が 1 ずつ増えます。  
  
4.  `sqlcmd`セッションを終了するには`EXIT` 、 `sqlcmd`プロンプトで「」と入力します。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>sqlcmd ユーティリティを起動し、SQL サーバーの名前付きインスタンスに接続するには  
  
1.  コマンドプロンプトウィンドウを開き、「 `sqlcmd -S` *my\ インスタンス*名」と入力します。 
  *myServer\instanceName* には、コンピューターの実際の名前と、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定してください。  
  
2.  Enter キーを押します。  
  
     プロンプト`sqlcmd` (1>) は、指定したの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに接続していることを示します。  
  
    > [!NOTE]  
    >  入力した [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはバッファーに格納されます。 GO コマンドが見つかると、ステートメントがバッチとして実行されます。  
  
## <a name="see-also"></a>参照  
 [Sqlcmd を使用した Transact-sql スクリプトファイルの実行](sqlcmd-run-transact-sql-script-files.md)  
  
  
