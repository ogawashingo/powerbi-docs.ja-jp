---
title: PowerShell を使用してデータ ソース接続文字列を変更する
description: PowerShell の API を使ってデータ ソース接続文字列を変更します - Power BI Report Server。
author: maggiesMSFT
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-report-server
ms.topic: conceptual
ms.date: 10/24/2019
ms.author: maggies
ms.openlocfilehash: 77716514ffbb6dc8d3f128ada85276b46bf7af05
ms.sourcegitcommit: 17f45a81b0dcbf9e3f1fb2a551584170baecd320
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72923667"
---
# <a name="change-data-source-connection-strings-in-power-bi-reports-with-powershell---power-bi-report-server"></a>PowerShell を使って Power BI レポートのデータ ソース接続文字列を変更する - Power BI Report Server

PowerShell の API を使って、Power BI Report Server の Power BI レポートのデータ ソース接続文字列を変更できます。 

1. Power BI Report Server PowerShell コマンドレットをインストールします。 コマンドレットとインストール手順は [https://github.com/Microsoft/ReportingServicesTools](https://github.com/Microsoft/ReportingServicesTools) に記載されています。 

2. PowerShell コマンドレットを使用して、Power BI ファイルの既存のデータ ソース情報を取得します。

    ```powershell
    Get-RsRestItemDataSource -RsItem '/MyPbixReport'
    ```

    Power BI レポートに含まれている最初のデータ ソースの情報を表示するには: 

    ```powershell
    $dataSources[0]
    ```

3. 必要に応じて、接続情報と資格情報を更新します。 接続文字列とデータ ソースを更新する際に保存された資格情報を使用する場合は、そのアカウントのパスワードを入力する必要があります。 

    データ ソース接続文字列を更新するには:

    ```powershell
    $dataSources[0].ConnectionString = 'data source=myCatalogServer;initial catalog=ReportServer;persist security info=False' 
    ```

    データソースの資格情報の種類を変更するには:

    ```powershell
    $dataSources[0].DataModelDataSource.AuthType = 'Integrated'
    ```

    データ ソースのユーザー名/パスワードを変更するには:

    ```powershell
    $dataSources[0].DataModelDataSource.Username = 'domain\user
    ```
    ```powershell
    $dataSources[0].DataModelDataSource.Secret = 'password'
    ```

4. 更新した資格情報を、サーバーに保存し直します。

    ```powershell
    Set-RsRestItemDataSource -RsItem '/MyPbixReport' -RsItemType 'PowerBIReport' -DataSources $dataSources
    ```

## <a name="next-steps"></a>次の手順

[Power BI Report Server でのページ分割されたレポートのデータ ソース](connect-data-sources.md) 

他にわからないことがある場合は、 [Power BI コミュニティで質問してみてください](https://community.powerbi.com/)。

