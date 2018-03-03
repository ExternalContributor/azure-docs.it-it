---
title: Delega offerte nello Stack di Azure | Documenti Microsoft
description: Informazioni su come inserire altri utenti responsabile della creazione di offerte e iscrizione gli utenti per l'utente.
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2018
ms.author: brenduns
ms.reviewer: alfredop
ms.openlocfilehash: 287bc04660664facbe99d2cb80ae6c92e41c4111
ms.sourcegitcommit: 782d5955e1bec50a17d9366a8e2bf583559dca9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2018
---
# <a name="delegate-offers-in-azure-stack"></a>Delegare offerte in Azure Stack

*Si applica a: Azure Stack integrate di sistemi Azure Stack Development Kit*

Come l'operatore di Stack di Azure, è spesso necessario inserire altri utenti responsabile della creazione di offerte e iscrizione gli utenti. Ad esempio, se si è un provider di servizi, è possibile rivenditori per iscriversi a clienti e gestirli per conto dell'utente. O se si fa parte di un gruppo IT centrale in un'organizzazione, potrebbe essere controllate da effettuare l'iscrizione gli utenti senza l'intervento dell'utente.

La delega consente di queste attività, rendendo possibile per accedere e gestire più utenti, è possibile direttamente. La figura seguente mostra un livello di delega, ma dello Stack di Azure supporta più livelli. Provider delegato (dp) a sua volta è possibile delegare ad altri provider, fino a cinque livelli.

![Livelli di delega](media/azure-stack-delegated-provider/image1.png)

Gli operatori di Azure Stack possono delegare la creazione di offerte e gli utenti ad altri utenti tramite la funzionalità di delega.

## <a name="roles-and-steps-in-delegation"></a>Ruoli e i passaggi di delega
Per comprendere la delega, tenere presente che sono disponibili tre ruoli coinvolti:

* Il *operatore Azure Stack* gestisce l'infrastruttura di Azure Stack, crea un modello di offerta e delegati offrono agli utenti di altri utenti.

* Gli operatori di Azure Stack delegati vengono chiamati *delegato provider*. Appartengono ad altre organizzazioni, ad esempio altri utenti di Azure Active Directory (Azure AD).

* *Gli utenti* iscriversi per le offerte e utilizzarli per la gestione dei rispettivi carichi di lavoro, creazione di macchine virtuali, l'archiviazione dei dati e così via.

Come illustrato nella figura seguente, sono disponibili due passaggi per la configurazione di delega.

1. *Identificare i provider di delegati*. Questo scopo è li sottoscrivere un'offerta in base a un piano che contiene solo il servizio di sottoscrizioni. Gli utenti che sottoscrivono l'offerta acquisiscono alcune delle funzionalità dell'operatore dello Stack di Azure, inclusa la possibilità di estendere le offerte e accesso agli utenti a essi.

2. *Delegare al provider delegato un'offerta*. Questa offerta funge da modello per il provider delegato offrono. Il provider delegato ora può richiedere l'offerta. Scegliere un nome, ma non modificare i servizi e le quote e offrono ai clienti.

![Creare il provider di delegati e consentire loro di effettuare l'iscrizione gli utenti](media/azure-stack-delegated-provider/image2.png)

Per agire come provider di delegato, gli utenti devono stabilire una relazione con il provider principale. In altre parole, è necessario creare una sottoscrizione. In questo scenario, la sottoscrizione identifica i provider delegati come avente il diritto di offerte presente per conto di provider principale.

Dopo aver stabilita questa relazione, l'operatore di Stack di Azure può delegare al provider delegato un'offerta. Il provider di delegato è ora in grado di accettare l'offerta, rinominarlo (ma non modificare il principio) e offrono ai clienti.

Nelle sezioni seguenti viene descritto come stabilire un provider di delegato, un'offerta di delegato e verificare che gli utenti possono iscriversi a è.

## <a name="set-up-roles"></a>Configurare i ruoli

Per visualizzare un provider delegato al lavoro, è necessario Azure altri account di Active Directory oltre all'account di Azure Stack operatore. Se non si dispone di questi due account, è necessario crearli. Gli account possono appartenere a qualsiasi utente di Azure AD e vengono definiti per il provider di delegato e l'utente.

| **Ruolo** | **Diritti aziendali** |
| --- | --- |
| Provider di delegati |Utente |
| Utente |Utente |

## <a name="identify-the-delegated-providers"></a>Identificare i provider di delegati
1. Accedere come un operatore di Stack di Azure.

2. Creare l'offerta che consente agli utenti di diventare provider delegato:
   
   a.  [Creare un piano](azure-stack-create-plan.md).
       Questo piano deve includere solo il servizio di sottoscrizioni. Questo articolo viene usato un piano denominato **PlanForDelegation**.
   
   b.  [Creare un'offerta](azure-stack-create-offer.md) in base a questo piano. Questo articolo viene utilizzata un'offerta chiamata **OfferToDP**.
   
   c.  Una volta completata la creazione dell'offerta, aggiungere il provider di delegati come sottoscrittore per questa offerta. Eseguire questa operazione selezionando **sottoscrizioni** > **Aggiungi** > **nuova sottoscrizione di Tenant**.
   
   ![Aggiungere il provider del delegato come sottoscrittore](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> Come con tutte le offerte di Stack di Azure, è necessario l'opzione per rendere l'offerta di utenti pubblici e consentire iscriversi o di mantenere privato e consentendo di gestire l'abbonamento l'operatore di Stack di Azure. Provider di delegati sono in genere un piccolo gruppo. Si desidera controllare quali utenti sia consentito, in modo da mantenere privato questa offerta ha senso nella maggior parte dei casi.
> 
> 

## <a name="azure-stack-operator-creates-the-delegated-offer"></a>Operatore di Stack Azure crea l'offerta di delegati

Ora è stato stabilito il provider del delegato. Il passaggio successivo consiste nel creare il piano e dell'offerta che si desidera delegare e che verranno utilizzati i clienti. È consigliabile definire questa offerta, esattamente come si desidera che i clienti per visualizzarlo, perché il provider di delegato non è possibile modificare i piani e le quote che include.

1. Un operatore Azure Stack [creare un piano](azure-stack-create-plan.md) e [un'offerta](azure-stack-create-offer.md) basati su di esso. Questo articolo viene utilizzata un'offerta chiamata **DelegatedOffer.**
   
   > [!NOTE]
   > Questa offerta non deve essere pubblico. Se si sceglie, è possibile renderlo pubblico. Nella maggior parte dei casi, tuttavia, si desidera delegata ai provider di accedervi. Dopo la delega di un'offerta privata, come descritto nei passaggi seguenti, il provider delegato possa accedervi.
   > 
   > 
1. Delegare l'offerta. Passare a **DelegatedOffer.** Quindi, nel **impostazioni** riquadro, selezionare **delegato provider** > **Aggiungi**.

2. Selezionare la sottoscrizione per il provider di delegato dall'elenco a discesa, quindi **delegato**.

> ![Aggiungere un provider di delegati](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-the-offer"></a>Provider di delegati consente di personalizzare l'offerta

Accedere al portale per gli utenti come provider di delegato e quindi creare una nuova offerta tramite l'offerta delegato come modello.

1. Selezionare **nuova** > **Tenant offre + piani** > **offrono**.

    ![Creare una nuova offerta](media/azure-stack-delegated-provider/image5.png)


1. Assegnare un nome per l'offerta. Questo articolo usa **ResellerOffer**. Selezionare l'offerta delegato sul quale impostazione base e quindi selezionare **crea**.
   
   ![Assegnare un nome](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > Si noti la differenza rispetto all'offerta creazione come esperti dall'operatore dello Stack di Azure. Il provider di delegato non ne crea l'offerta da piani di base e i piani di componente aggiuntivo. Che possono scegliere solo le offerte che sono state delegate ad essi e non è possibile apportare modifiche a tali offerte.

1. Rendere pubblico l'offerta selezionando **Sfoglia**e quindi **offre**. Selezionare l'offerta, quindi **modifica dello stato**.

2. Il delegato provider espone queste offerte tramite il proprio portale URL. Queste offerte sono visibili solo tramite il portale di delegati. Per trovare e modificare l'URL:
   
    a.  Selezionare **Sfoglia** > **più servizi** > **sottoscrizioni**. Quindi selezionare la sottoscrizione del provider di delegati. Ad esempio, **DPSubscription** > **proprietà**.
   
    b.  Copiare il portale di URL in un percorso separato, ad esempio Blocco note.
   
    ![Selezionare la sottoscrizione del provider di delegati](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   Ora è stata creata un'offerta di delegati come provider di delegati. Disconnettersi come provider di delegati. Chiudere la finestra del browser che è stato utilizzato.

## <a name="sign-up-for-the-offer"></a>Effettuare l'iscrizione per l'offerta
1. In una nuova finestra del browser, passare al portale di delegati URL che è stato salvato nel passaggio precedente. Accedere al portale come utente. 
   
   >[!NOTE]
   >Le offerte di delegati non sono visibili solo se si utilizza il portale del delegato. 

2. Nel dashboard, selezionare **ottenere una sottoscrizione**. Vedrai che il delegato offerte create dal provider di delegati sono presentate all'utente:

> ![Visualizzare e selezionare le offerte](media/azure-stack-delegated-provider/image8.png)
> 
> 

Il processo di delega offerta è stato completato. L'utente può ora iscriversi all'offerta tramite il recupero di una sottoscrizione per tale.

## <a name="multiple-tier-delegation"></a>Delega a più livelli

La delega a più livelli consente al provider di delegato delegare l'offerta di altre entità. In questo modo, ad esempio, la creazione di canali di reseller più approfonditi, in cui il provider di gestione di Azure Stack delega di un'offerta a un server di distribuzione. Server di distribuzione specifico, a sua volta, delega per un rivenditore. Stack di Azure supporta fino a cinque livelli di delega.

Per creare più livelli di delega offerta, il provider delegato delega a sua volta l'offerta sul provider successivo. Il processo è lo stesso per il provider di delegato è stato per l'operatore di Stack di Azure (vedere [operatore dello Stack di Azure consente di creare l'offerta delegata](#cloud-operator-creates-the-delegated-offer)).

## <a name="next-steps"></a>Passaggi successivi
[Eseguire il provisioning di una macchina virtuale](azure-stack-provision-vm.md)

