---
title: Importare e pubblicare la prima API in Gestione API di Azure | Microsoft Docs
description: Informazioni su come importare e pubblicare la prima API con Gestione API.
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: apimpm
ms.openlocfilehash: ffe5ee95c66eee7dccd25a1afd2fe639cbc273f5
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="import-and-publish-your-first-api"></a>Importare e pubblicare la prima API 

Questa esercitazione illustra come importare un'API back-end "Specifica OpenAPI" che si trova all'indirizzo http://conferenceapi.azurewebsites.net?format=json. Questa API back-end è fornita da Microsoft e ospitata in Azure. 

Dopo l'importazione dell'API back-end in Gestione API, l'API di Gestione API diventa una facciata per l'API back-end. Al momento dell'importazione dell'API back-end, l'API di origine e l'API di Gestione API sono identiche. Gestione API consente di personalizzare la facciata in base alle proprie esigenze senza modificare l'API back-end. Per altre informazioni, vedere [Trasformare e proteggere l'API](transform-api.md). 

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Importare la prima API
> * Testare l'API nel portale di Azure
> * Testare l'API nel portale per sviluppatori

![Nuova API](./media/api-management-get-started/created-api.png)

## <a name="prerequisites"></a>prerequisiti

Completare la guida introduttiva seguente: [Creare un'istanza di Gestione API di Azure](get-started-create-service-instance.md).

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="create-api"> </a>Importare e pubblicare un'API back-end

Questa sezione illustra come importare e pubblicare un'API back-end Specifica OpenAPI.
 
1. Selezionare **API** in **GESTIONE API**.
2. Selezionare **Specifica OpenAPI** dall'elenco.

    ![Creare un'API](./media/api-management-get-started/create-api.png)

    È possibile impostare i valori dell'API durante la creazione o successivamente andando alla scheda **Impostazioni**.  

    |Impostazione|Valore|DESCRIZIONE|
    |---|---|---|
    |**Specifica OpenAPI**|http://conferenceapi.azurewebsites.net?format=json|Fa riferimento al servizio che implementa l'API e corrisponde all'indirizzo a cui Gestione API inoltra le richieste.|
    |**Nome visualizzato**|*Demo Conference API*|Se si preme TAB dopo avere immesso l'URL del servizio, Gestione API compilerà questo campo in base al contenuto del file JSON. <br/>Questo nome viene visualizzato nel portale per sviluppatori.|
    |**Nome**|*demo-conference-api*|Fornisce un nome univoco per l'API. <br/>Se si preme TAB dopo avere immesso l'URL del servizio, Gestione API compilerà questo campo in base al contenuto del file JSON.|
    |**Descrizione**|Fornisce una descrizione facoltativa dell'API.|Se si preme TAB dopo avere immesso l'URL del servizio, Gestione API compilerà questo campo in base al contenuto del file JSON.|
    |**Suffisso dell'URL dell'API**|*conference*|Il suffisso viene aggiunto all'URL di base del servizio Gestione API. Gestione API distingue le API in base al suffisso, quindi è necessario che questo sia univoco per ciascuna API di un editore specifico.|
    |**Schema URL**|*HTTPS*|Determina i protocolli da usare per l'accesso all'API. |
    |**Prodotti**|*Illimitato*| Pubblicare l'API associandola a un prodotto. Per aggiungere facoltativamente questa nuova API a un prodotto, digitare il nome del prodotto. Questo passaggio può essere ripetuto più volte per aggiungere l'API a più prodotti.<br/>I prodotti sono associazioni di una o più API. È possibile includere diverse API e proporle agli sviluppatori tramite il portale per sviluppatori. Per avere accesso all'API, gli sviluppatori devono prima sottoscrivere un prodotto. In questo modo ottengono una chiave di sottoscrizione valida per tutte le API nel prodotto. Se si è creata l'istanza di Gestione API, si è già un amministratore e la sottoscrizione a ogni prodotto è stata effettuata per impostazione predefinita.<br/> Per impostazione predefinita, con ogni istanza di Gestione API vengono forniti due prodotti di esempio: **Starter** e **Unlimited**. |
3. Selezionare **Create**.

## <a name="test-the-new-apim-api-in-the-azure-portal"></a>Testare la nuova API di Gestione API nel portale di Azure

È possibile chiamare le operazioni direttamente dal portale di Azure, che consente di visualizzare e testare le operazioni di un'API in tutta comodità.  
1. Selezionare l'API creata nel passaggio precedente.
2. Fare clic sulla scheda **Test**.  ![Testare l'API](./media/api-management-get-started/test-api.png)
3. Fare clic su **GetSpeakers**.
    La pagina visualizza i campi per i parametri di query, ma in questo caso non ne esistono. La pagina visualizza anche i campi per le intestazioni. Una delle intestazioni è "Ocp-Apim-Subscription-Key", per la chiave di sottoscrizione del prodotto associato all'API. La chiave viene compilata automaticamente.
4. Fare clic su **Invia**.

    Il back-end risponde con **200 OK** e alcuni dati.

## <a name="call-operation"> </a>Chiamare un'operazione dal portale per sviluppatori

Le operazioni possono essere chiamate anche dal **portale per sviluppatori** per testare le API. 

1. Selezionare l'API creata nel passaggio "Importare e pubblicare un'API back-end".
2. Fare clic su **Portale per sviluppatori**.

    ![Eseguire il test nel portale per sviluppatori](./media/api-management-get-started/developer-portal.png)

    Viene aperto il sito "Portale per sviluppatori".
3. Selezionare **API**.
4. Selezionare **Demo Conference API**.
5. Fare clic su **GetSpeakers**.
    
    La pagina visualizza i campi per i parametri di query, ma in questo caso non ne esistono. La pagina visualizza anche i campi per le intestazioni. Una delle intestazioni è "Ocp-Apim-Subscription-Key", per la chiave di sottoscrizione del prodotto associato all'API. Se si è creata l'istanza di Gestione API, si è già un amministratore, quindi la chiave viene inserita automaticamente.
6. Fare clic su **Prova**.
7. Fare clic su **Invia**.
    
    Dopo aver richiamato un'operazione, nel portale per sviluppatori vengono visualizzati lo **stato della risposta**, le **intestazioni della risposta** e l'eventuale **contenuto della risposta**.

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione illustra come:

> [!div class="checklist"]
> * Importare la prima API
> * Testare l'API nel portale di Azure
> * Testare l'API nel portale per sviluppatori

Passare all'esercitazione successiva:

> [!div class="nextstepaction"]
> [Creare e pubblicare un prodotto](api-management-howto-add-products.md)
