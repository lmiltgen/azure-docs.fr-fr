---
title: Visualiser des données Interactive Query Hive à l’aide de Power BI dans Azure HDInsight
description: Utiliser Microsoft Power BI pour visualiser des données interactives Query Hive provenant d’Azure HDInsight
services: hdinsight
ms.service: hdinsight
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/06/2018
ms.openlocfilehash: 46b5b3436a33c3f83d85cfb02028759d53d214af
ms.sourcegitcommit: da3459aca32dcdbf6a63ae9186d2ad2ca2295893
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51245271"
---
# <a name="visualize-interactive-query-hive-data-with-microsoft-power-bi-using-direct-query-in-azure-hdinsight"></a>Visualiser des données Interactive Query Hive avec Microsoft Power BI à l’aide de la requête directe dans Azure HDInsight

Cet article décrit comment connecter Microsoft Power BI à des clusters de requête interactive Azure HDInsight, et comment visualiser des données Apache Hive à l’aide d’une requête directe. L’exemple fourni charge les données d’une table Hive hivesampletable dans Power BI. La table Hive hivesampletable contient des données sur l’utilisation du téléphone mobile. Vous allez ensuite tracer ces données d’utilisation sur une carte du monde :

![rapport cartographique Power BI HDInsight](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-visualization.png)

Vous pouvez tirer parti du [pilote ODBC Hive](../hadoop/apache-hadoop-connect-hive-power-bi.md) pour importer effectivement via le connecteur ODBC générique dans Power BI Desktop. Il n’est toutefois pas recommandé pour les charges de travail décisionnelles en raison de la nature non interactive du moteur de requête Hive. Le [connecteur de requêtes interactives HDInsight](./apache-hadoop-connect-hive-power-bi-directquery.md) et le [connecteur HDInsight Spark](https://docs.microsoft.com/power-bi/spark-on-hdinsight-with-direct-connect) sont des choix plus judicieux du fait de leurs performances.

## <a name="prerequisites"></a>Prérequis
Avant de poursuivre cet article, vérifiez que vous avez les éléments suivants :

* Un **cluster HDInsight**. Cela peut être un cluster HDInsight avec Hive ou un cluster du nouveau type Interactive Query. Pour plus d’informations sur la création de clusters, consultez [Créer un cluster](../hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).
* **[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)**. Vous pouvez télécharger une copie à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=45331).

## <a name="load-data-from-hdinsight"></a>Chargement des données à partir de HDInsight

La table Hive hivesampletable est fournie avec tous les clusters HDInsight.

1. Connectez-vous à Power BI Desktop.

2. Cliquez sur l’onglet **Accueil**, cliquez sur **Obtenir des données** dans le ruban **Données externes**, puis sélectionnez **Plus...**.

    ![données affichées Power BI HDInsight](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-open-odbc.png)
    
3. À partir du volet **Get Data** (Obtenir les données), tapez **hdinsight** dans la zone de recherche. Si vous ne voyez pas **HDInsight Interactive Query (version bêta)**, vous devez mettre à jour Power BI Desktop vers la dernière version.

4. Sélectionnez **HDInsight Interactive Query (version bêta)**, puis **Se connecter**.

5. Sélectionnez **Continuer** pour fermer la boîte de dialogue d’avertissement **Connecteur en version préliminaire**.

6. À partir de **HDInsight Interactive Query**, sélectionnez ou entrez les informations suivantes :

    - **Serveur** : entrez le nom du cluster Interactive Query, par exemple *myiqcluster.azurehdinsight.net*.

    - **Base de données** : pour ce didacticiel, entrez **default**.
    
    - **Mode de connectivité des données**: pour ce didacticiel, sélectionnez **DirectQuery**.

    ![HDInsight interactive query Power BI DirectQuery connect](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-interactive-query-power-bi-connect.png)

7. Cliquez sur **OK**.

8. Saisissez les informations d’identification de l’utilisateur HTTP, puis cliquez sur **OK**. Le nom d’utilisateur par défaut est **admin**.

9. Dans le volet de gauche, sélectionnez **hivesampletale**, puis cliquez sur **Charger**.

    ![HDInsight interactive query Power BI hivesampletable](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-interactive-query-power-bi-hivesampletable.png)

## <a name="visualize-data-on-a-map"></a>Visualiser les données sur une carte

Poursuivez la procédure précédente.

1. Dans le volet Visualisations, sélectionnez **Carte**  (icône représentant un globe).

    ![personnalisation de rapport Power BI HDInsight](./media/apache-hadoop-connect-hive-power-bi-directquery/hdinsight-power-bi-customize.png)
    
2. Dans le volet Champs, sélectionnez **country** et **devicemake**. Vous pouvez voir les données tracées sur la carte.

3. Développez la carte.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris à visualiser des données de HDInsight à l’aide de Power BI.  Pour plus d’informations sur la visualisation des données, voir les articles suivants :

* [Visualiser des données Hive à l’aide de Microsoft Power BI et ODBC dans Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md). 
* [Utiliser Zeppelin pour exécuter des requêtes Hive dans Azure HDInsight](./../hdinsight-connect-hive-zeppelin.md).
* [Connecter Excel à HDInsight avec le pilote ODBC Microsoft Hive](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Connexion d’Excel à Hadoop à l’aide de Power Query](../hadoop/apache-hadoop-connect-excel-power-query.md).
* [Se connecter à Azure HDInsight et exécuter des requêtes Hive avec Data Lake Tools pour Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).
* [Utiliser Azure HDInsight Tools pour Visual Studio Code](../hdinsight-for-vscode.md).
* [Charger des données dans HDInsight](./../hdinsight-upload-data.md).
