# Data-Analysis---Cyclistics-

## Scenario

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,
your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives
must approve your recommendations, so they must be backed up with compelling data insights and professional data
visualizations.

## Obiettivo

Driving question: How do annual members and casual riders use Cyclistic bikes differently?

Cyclistic Bike-Share wants to increase member subscriptions for their services because annual members are more profitable than casual riders. Therefore they would like to know how member and casual riders use Cyclistic services differently. The results from this analysis may be used to guide future marketing programs to increase member subscriptions.

## Preparazione dei dati

Ho scaricato i seguenti file da Divvy Bike's trip data:

* 202101-divvy-tripdata
* 202102-divvy-tripdata
* 202103-divvy-tripdata
* 202104-divvy-tripdata
* 202105-divvy-tripdata
* 202111-divvy-tripdata
* 202112-divvy-tripdata

I dati comprendono dunque i periodi **gennaio-maggio 2021** e **novembre-dicembre 2021**. I mesi estivi sono infatti stati esclusi perchè i file ad essi associati risultavano troppo grandi per essere caricati su BigQuery Sandbox.

Come prima cosa ho aperto i file scaricati come foglio di calcolo Excel. Essendo le dimensioni delle tabelle abbastanza estese, ho deciso di lavorare in SQL durante le prime fasi di preparazione e pulizia dei dati, per poi spostarmi su R per l'analisi e la visualizzazione dei risultati.

Si rammenta che la compagnia di bike sharing Cyclistics è una compagnia fittizia. I dati utilizzati sono stati raccolti da Motivate International Inc, la compagnia di bike sharing Divvy che opera nella città di Chicago. L'autorizzazione per l'utilizzo del presente dataset pubblico può essere esaminata al seguente [link](https://ride.divvybikes.com/data-license-agreement).









