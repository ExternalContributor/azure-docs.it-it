---
title: 'Esercitazione: Integrazione di Azure Active Directory con Image Relay | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Image Relay.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: da05da676ea160dcdaf7e9c711d5f308ac260434
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Esercitazione: Integrazione di Azure Active Directory con Image Relay

Questa esercitazione descrive come integrare Image Relay con Azure Active Directory (Azure AD).

L'integrazione di Image Relay con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Image Relay
- È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a Image Relay con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>prerequisiti

Per configurare l'integrazione di Azure AD con Image Relay, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Image Relay abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Image Relay dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-image-relay-from-the-gallery"></a>Aggiunta di Image Relay dalla raccolta
Per configurare l'integrazione di Image Relay in Azure AD, è necessario aggiungere Image Relay dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Image Relay dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

4. Nella **casella di ricerca** digitare Image Relay.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. Nel pannello dei risultati selezionare **Image Relay** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Image Relay mediante un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Image Relay corrisponde a un determinato utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Image Relay.

Per stabilire la relazione di collegamento, in Image Relay assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Image Relay, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente test di Image Relay](#creating-an-image-relay-test-user)**: per avere una controparte di Britta Simon in Image Relay collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Image Relay.

**Per configurare l'accesso Single Sign-On di Azure AD con Image Relay, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Image Relay** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Nella sezione **URL e dominio Image Relay** seguire questa procedura:

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.imagerelay.com/`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori contattare il [team di supporto clienti di Image Relay](http://support.imagerelay.com/). 
 


4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Image Relay** fare clic su **Configura Image Relay** per aprire la finestra **Configura accesso**. Copiare i valori **Sign-Out Service URL (URL servizio di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla **sezione Quick Reference** (Riferimento rapido).

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. In un'altra finestra del browser accedere al sito aziendale di Image Relay come amministratore.

8. Nel barra degli strumenti in alto fare clic sul carico di lavoro **Users & Permissions** (Utenti e autorizzazioni).
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Fare clic su **Create New Permission**(Crea nuova autorizzazione).
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. Nel carico di lavoro **Impostazioni Single Sing-On** selezionare la casella di controllo **This Group can only sign-in via Single Sign On** (Questo gruppo può accedere solo con Single Sign-On) e quindi fare clic su **Salva**.
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Passare ad **Account Settings**(Impostazioni account).
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Selezionare il carico di lavoro **Single Sign On Settings** (Impostazioni Single Sing-On).
    
     ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Nella finestra di dialogo **SAML Settings** (Impostazioni SAML) seguire questa procedura:
    
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. Nella casella di testo **URL di accesso** incollare il valore di **URL servizio Single Sign-On** copiato dal portale di Azure.

    b. Nella casella di testo **URL disconnessione** incollare il valore di **Single Sign-Out Service URL** (URL servizio Single Sign-Out) copiato dal portale di Azure.

    c. Come **Name Id Format** (Formato ID nome) selezionare**urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    d. Come **Binding Options for Requests from the Service Provider (Image Relay)** (Opzioni di associazione per le richieste dal provider di servizi - Inoltro immagini) selezionare **POST Binding** (Associazione POST).

    e. In **Certificato X.509** fare clic su **Aggiorna certificato**.

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. Aprire il certificato scaricato nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo X.509 Certificate (Certificato X.509).

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. Nella sezione **Just-In-Time User Provisioning** (Provisioning utenti Just-In-Time) selezionare la casella di controllo **Enable Just-In-Time User Provisioning** (Abilita provisioning utenti Just-In-Time).

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Selezionare il gruppo di autorizzazioni, ad esempio, **SSO Basic**(SSO di base) a cui sarà consentito l'accesso solo tramite Single Sign-On.

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    i. Fare clic su **Save**.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Crea**.
 
### <a name="creating-an-image-relay-test-user"></a>Creazione di un utente test di Image Relay

Questa sezione descrive come creare un utente chiamato Britta Simon in Image Relay.

**Per creare un utente chiamato Britta Simon in Image Relay, seguire questa procedura:**

1. Accedere al sito aziendale di Image Relay come amministratore.

2. Andare in **Users & Permissions** (Utenti e autorizzazioni) e selezionare **Create SSO User** (Crea utente SSO).
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Immettere i valori necessari nei campi **Email** (Posta elettronica), **First Name** (Nome), **Last Name** (Cognome) e **Company** (Società) dell'utente di cui si vuole effettuare il provisioning e selezionare il gruppo di autorizzazioni (ad esempio SSO Basic) che potrà eseguire l'accesso solo tramite Single Sign-On.
   
    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. Fare clic su **Crea**.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Image Relay.

![Assegna utente][200] 

**Per assegnare Britta Simon a Image Relay, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **Image Relay**.

    ![Configure Single Sign-On](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.    

Quando si fa clic sul riquadro Image Relay nel riquadro di accesso, si dovrebbe accedere automaticamente all'applicazione Image Relay.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

