---
title: 'Tutoriel : Intégration d’Azure Active Directory à Imagineer WebVision | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Imagineer WebVision.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b936a3f4-74c1-4437-b0f7-6d1b1de38bb1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2018
ms.author: jeedes
ms.openlocfilehash: d86004680bf13c9716b4ff4e7a41af73ea186f27
ms.sourcegitcommit: 7208bfe8878f83d5ec92e54e2f1222ffd41bf931
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2018
ms.locfileid: "39047186"
---
# <a name="tutorial-azure-active-directory-integration-with-imagineer-webvision"></a>Tutoriel : Intégration d’Azure Active Directory à Imagineer WebVision

Dans ce tutoriel, vous allez apprendre à intégrer Imagineer WebVision à Azure Active Directory (Azure AD).

L’intégration d’Imagineer WebVision à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à Imagineer WebVision.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Imagineer WebVision (via l’authentification unique) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD à Imagineer WebVision, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Imagineer WebVision pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout d’Imagineer WebVision à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-imagineer-webvision-from-the-gallery"></a>Ajout d’Imagineer WebVision à partir de la galerie
Pour configurer l’intégration d’Imagineer WebVision à Azure AD, vous devez ajouter Imagineer WebVision à votre liste d’applications SaaS gérées, à partir de la galerie.

**Pour ajouter Imagineer WebVision à partir de la galerie, effectuez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Bouton Azure Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Panneau Applications d’entreprise][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Bouton Nouvelle application][3]

4. Dans la zone de recherche, tapez **Imagineer WebVision**, sélectionnez **Imagineer WebVision** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Imagineer WebVision dans la liste des résultats](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Imagineer WebVision, avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Imagineer WebVision équivalent dans Azure AD. En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur Imagineer WebVision qui lui est associé.

Pour configurer et tester l’authentification unique Azure AD avec Imagineer WebVision, vous devez suivre les indications des sections suivantes :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Créer un utilisateur de test Imagineer WebVision](#create-an-imagineer-webvision-test-user)** pour avoir un équivalent de Britta Simon dans Imagineer WebVision qui soit lié à la représentation Azure AD associée.
4. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Imagineer WebVision.

**Pour configurer l’authentification unique Azure AD avec Imagineer WebVision, effectuez les étapes suivantes :**

1. Dans le portail Azure, dans la page d’intégration de l’application **Imagineer WebVision**, cliquez sur **Authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_samlbase.png)

3. Dans la section **Domaine et URL Imagineer WebVision**, effectuez les étapes suivantes :

    ![Informations d’authentification unique dans Domaine et URL Imagineer WebVision](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<YOUR SERVER URL>/<yourapplicationloginpage>`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<YOUR SERVER URL>/<yourapplicationloginpage>`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez [l’équipe du support technique d’Imagineer WebVision](mailto:support@itgny.com).

4. Dans la section **Certificat de signature SAML**, cliquez sur le bouton Copier pour copier **l’URL des métadonnées de fédération de l’application**, puis collez-la dans le Bloc-notes.

    ![Lien Téléchargement de certificat](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/imagineerwebvision-tutorial/tutorial_general_400.png)

6. Pour configurer l’authentification unique côté **Imagineer WebVision**, vous devez envoyer **l’URL des métadonnées de fédération de l’application** que vous avez copiée à [l’équipe du support technique Imagineer WebVision](mailto:support@itgny.com). Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

   ![Créer un utilisateur de test Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.

    ![Bouton Azure Active Directory](./media/imagineerwebvision-tutorial/create_aaduser_01.png)

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/imagineerwebvision-tutorial/create_aaduser_02.png)

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.

    ![Bouton Ajouter](./media/imagineerwebvision-tutorial/create_aaduser_03.png)

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :

    ![Boîte de dialogue Utilisateur](./media/imagineerwebvision-tutorial/create_aaduser_04.png)

    a. Dans la zone **Nom**, tapez **BrittaSimon**.

    b. Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.

    c. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="create-an-imagineer-webvision-test-user"></a>Créer un utilisateur de test Imagineer WebVision

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Imagineer WebVision. Demandez l’aide de [l’équipe du support technique Imagineer WebVision](mailto:support@itgny.com) pour ajouter des utilisateurs dans la plateforme Imagineer WebVision. Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Imagineer WebVision.

![Attribuer le rôle utilisateur][200] 

**Pour affecter Britta Simon à Imagineer WebVision, effectuez les étapes suivantes :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **Imagineer WebVision**.

    ![Lien Imagineer WebVision dans la liste des applications](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_app.png)  

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Lien « Utilisateurs et groupes »][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Volet Ajouter une attribution][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Imagineer WebVision dans le panneau d’accès, vous êtes connecté automatiquement à votre application Imagineer WebVision.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/imagineerwebvision-tutorial/tutorial_general_01.png
[2]: ./media/imagineerwebvision-tutorial/tutorial_general_02.png
[3]: ./media/imagineerwebvision-tutorial/tutorial_general_03.png
[4]: ./media/imagineerwebvision-tutorial/tutorial_general_04.png

[100]: ./media/imagineerwebvision-tutorial/tutorial_general_100.png

[200]: ./media/imagineerwebvision-tutorial/tutorial_general_200.png
[201]: ./media/imagineerwebvision-tutorial/tutorial_general_201.png
[202]: ./media/imagineerwebvision-tutorial/tutorial_general_202.png
[203]: ./media/imagineerwebvision-tutorial/tutorial_general_203.png

