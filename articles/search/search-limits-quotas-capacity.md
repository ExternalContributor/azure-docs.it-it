---
title: Limiti dei servizi in Ricerca di Azure | Microsoft Docs
description: "Limiti del servizio utilizzati per la pianificazione della capacità e limiti massimi per richieste e risposte in Ricerca di Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 11/09/2017
ms.author: heidist
ms.openlocfilehash: 3deb0ff81114c840798c5927ad7311d7e603813d
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="service-limits-in-azure-search"></a>Limiti dei servizi in Ricerca di Azure
I limiti massimi per archiviazione, carichi di lavoro e quantità di indici, documenti e altri oggetti dipendono dal [piano tariffario scelto per Ricerca di Azure](search-create-service-portal.md): **Gratuito**, **Basic** o **Standard**.

* **gratuito** è un servizio condiviso multi-tenant fornito con la sottoscrizione di Azure. 
* Il piano **Basic** fornisce risorse di elaborazione dedicate per carichi di lavoro di produzione di dimensioni ridotte.
* Il piano **Standard** prevede computer dedicati con maggiore capacità di elaborazione e archiviazione a ogni livello. Il piano Standard è disponibile in quattro livelli: S1, S2, S3 e ad alta densità S3 (S3 HD).

> [!NOTE]
> Il provisioning di un servizio viene eseguito in base al piano tariffario specifico. Il passaggio a un nuovo piano tariffario per ottenere più capacità prevede il provisioning di un nuovo servizio (non esiste alcun aggiornamento sul posto). Per altre informazioni, vedere [Scegliere uno SKU o un piano tariffario](search-sku-tier.md). Per altre informazioni sulla regolazione delle capacità all'interno di un servizio di cui è già stato effettuato il provisioning, vedere [Ridimensionare i livelli di risorse per le query e l'indicizzazione dei carichi di lavoro](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Limiti per sottoscrizione
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Limiti per servizio
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Limiti per indice
Esiste una corrispondenza uno a uno tra i limiti sugli indici e sugli indicizzatori. Dato un limite di 200 indici, il limite massimo per gli indicizzatori è 200 per lo stesso servizio.

| Risorsa | Gratuito | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Indice: numero massimo di campi per indice |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Numero massimo di profili di punteggio per indice |100 |100 |100 |100 |100 |100 |
| Numero massimo di funzioni per profilo |8 |8 |8 |8 |8 |8 |
| Indicizzatori: carico di indicizzazione massimo per chiamata |10.000 documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |Limitato solo da numero massimo di documenti |N/D <sup>2</sup> |
| Indicizzatori: tempo massimo di esecuzione | 1-3 minuti <sup>3</sup> |24 ore |24 ore |24 ore |24 ore |N/D <sup>2</sup> |
| Indicizzatore BLOB: dimensioni massime per un BLOB, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indicizzatore BLOB: numero massimo di caratteri di contenuto estratti da un BLOB |32.000 |64.000 |4 milioni |4 milioni |4 milioni |N/D <sup>2</sup> |

<sup>1</sup> Il livello Basic è l'unico SKU con un limite inferiore di 100 campi per indice.

<sup>2</sup> S3 HD attualmente non supporta gli indicizzatori. In caso di esigenze urgenti per questa funzionalità, contattare il supporto tecnico di Azure.

<sup>3</sup> Il tempo di esecuzione massimo degli indicizzatori per il livello gratuito è di 3 minuti per le origini BLOB e di 1 minuto per tutte le altre origini dati.

## <a name="document-size-limits"></a>Limiti per la dimensione dei documenti
| Risorsa | Gratuito | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Dimensione individuale dei documenti per l'API di indice |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

Si riferisce alla dimensione massima del documento quando si chiama un'API di indice. La dimensione del documento costituisce effettivamente un limite alla dimensione del corpo della richiesta dell'API di indice. Poiché è possibile passare all'API di indice un batch costituito da più documenti in una sola volta, il limite della dimensione dipende in effetti dal numero di documenti presenti nel batch. Per un batch con un solo documento, la dimensione massima del documento è di 16 MB di JSON.

Per limitare la dimensione del documento, è necessario escludere dalla richiesta i dati non disponibili per query. Le immagini e altri dati binari non sono direttamente disponibili per query e non devono quindi essere archiviati nell'indice. Per integrare i dati non disponibili per query nei risultati della ricerca, definire un campo non disponibile per la ricerca che consenta l'archiviazione di un riferimento URL nella risorsa.

## <a name="queries-per-second-qps"></a>Query al secondo

Le stime di query al secondo devono essere sviluppate in modo indipendente da ogni cliente. Le dimensioni e la complessità dell'indice, le dimensioni e la complessità della query e la quantità di traffico sono i fattori principali in base ai quali è possibile determinare il numero di query al secondo. Non è possibile fornire stime significative se questi fattori sono sconosciuti.

Le stime sono più prevedibili se vengono calcolate su servizi in esecuzione su risorse dedicate (livelli Basic e Standard). In questo caso, infatti, è possibile stimare in modo più preciso il numero di query al secondo, poiché si ha il controllo di un numero maggiore di parametri. Per informazioni su come eseguire la stima, vedere [Considerazioni sulle prestazioni e sull'ottimizzazione di Ricerca di Azure](search-performance-optimization.md).

## <a name="api-request-limits"></a>Limiti delle richieste API
* 16 MB al massimo per <sup>1</sup> richiesta
* 8 KB al massimo per la lunghezza dell'URL
* 1000 documenti al massimo per ogni batch di carichi, unioni o eliminazioni di indice
* 32 campi al massimo nella clausola $orderby
* 32.766 byte (32 KB meno 2 byte) di testo con codifica UTF-8 per la dimensione massima del termine di ricerca

<sup>1</sup> In Ricerca di Azure il corpo di una richiesta è soggetto a un limite massimo di 16 MB, che impone un limite pratico ai contenuti di singoli campi o raccolte non vincolati a limiti teorici. Per altre informazioni sulla composizione dei campi e sulle relative restrizioni, vedere [Supported data types](https://msdn.microsoft.com/library/azure/dn798938.aspx) (Tipi di dati supportati).

## <a name="api-response-limits"></a>Limiti delle risposte API
* 1000 documenti al massimo restituiti per pagina di risultati della ricerca
* 100 suggerimenti al massimo restituiti per richiesta di API di suggerimento

## <a name="api-key-limits"></a>Limiti delle chiavi API
Le chiavi API vengono utilizzate per l'autenticazione del servizio. Sono disponibili due tipi. Le chiavi amministratore, specificate nell'intestazione della richiesta, consentono l'accesso completo in lettura e scrittura al servizio. Le chiavi di query sono di sola lettura, sono specificate nell'URL e in genere sono distribuite ad applicazioni client.

* 2 chiavi di amministrazione al massimo per ogni servizio
* 50 chiavi di query al massimo per ogni servizio
