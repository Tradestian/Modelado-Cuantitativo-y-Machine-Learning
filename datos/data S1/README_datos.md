# Procedencia de los datos — Sesión 1

Todo en esta carpeta es real. Nada se generó ni se simuló.

## `equities_reales_diario.parquet`

9 tickers, uno por sector, extraídos de tu carpeta
`Trading Labs/data/ohlcv`, velas de 5 minutos resampleadas a diario
(open=primero, high=máximo, low=mínimo, close=último, volume=suma).

Ver tabla completa de tickers/sectores/archivos-origen en `../../README.md`.

Los archivos de origen tienen 3 esquemas de columnas distintos (estilo Alpha
Vantage `"1. open"`, estilo IBM/broker con `symbol`/`barCount`, y un estilo
simple con `ticker`) — normalizados a `open/high/low/close/volume` por
`preparar_equities.py` (script de construcción, no incluido en esta carpeta
por simplicidad; el archivo `.parquet` ya es el resultado final).

## `order_book_real_xbtusd.parquet`

Libro de órdenes real, 20 niveles por lado, par XBT/USD.

- **Fuente:** Kraken, API pública, sin autenticación.
- **Endpoint:** `GET https://api.kraken.com/0/public/Depth?pair=XBTUSD&count=20`
- **Capturado:** 25 de agosto de 2026.
- **Spread en la captura:** $0.10 sobre ~$78,765 (≈0.013 puntos básicos).

## `trades_reales_btcusd.parquet`

300 operaciones tick-by-tick reales, BTC-USD.

- **Fuente:** Coinbase Exchange, API pública, sin autenticación.
- **Endpoint:** `GET https://api.exchange.coinbase.com/products/BTC-USD/trades`
  (paginado con el parámetro `after` sobre `trade_id`).
- **Capturado:** 21 de agosto de 2026.
- **Rango:** ~33 segundos de actividad real de mercado (09:42:50 a
  09:43:23 UTC), 300 operaciones consecutivas.

## `ticker_real_btcusd.parquet`

Un snapshot de bid/ask/último precio, para contexto (spread visto en otro
instante distinto al del libro capturado).

- **Fuente:** Coinbase Exchange, API pública.
- **Endpoint:** `GET https://api.exchange.coinbase.com/products/BTC-USD/ticker`
- **Capturado:** 25 de agosto de 2026.

## Por qué está congelado y no en vivo

El notebook de la sesión explica esto en el bloque 3. En resumen: el material
se entrega con antelación y tiene que funcionar sin depender de que el aula
tenga internet. El notebook incluye una función opcional
(`traer_libro_en_vivo()`) para refrescar el libro con tu propio internet si
quieres mostrarlo moviéndose de verdad en clase.
