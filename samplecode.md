# WEB+DB PRESS Vol.110 記事「オープンデータのためのWikidata入門」サンプルコード

技術評論社刊「WEB+DB PRESS Vol.110」の記事「オープンデータのためのWikidata入門」のサンプルコードです。

当該記事に掲載したSPARQLのクエリを以下に記載します。


### 日本の都道府県の検索

```sparql
SELECT DISTINCT ?pref ?prefLabel ?code
WHERE {
    ?pref wdt:P31 wd:Q50337.
    ?pref wdt:P429 ?code.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
}} ORDER BY ?code
```

実行▶ http://tinyurl.com/y23nnto9

### 日本の市の検索

```sparql
SELECT DISTINCT ?city ?cityLabel ?code
WHERE {
    ?city wdt:P31 wd:Q494721.
    ?city wdt:P429 ?code.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
}}
```

実行▶ http://tinyurl.com/y4vybfor

### 日本の市の検索2

```sparql
SELECT DISTINCT ?city ?cityLabel ?code
WHERE {
    ?city wdt:P31/wdt:P279* wd:Q494721.
    ?city wdt:P429 ?code.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
}}
```

実行▶ http://tinyurl.com/yyaaqd7e

### 現在の都道府県知事の検索

```sparql
SELECT ?person ?personLabel
       ?role ?roleLabel ?code WHERE {
    ?person p:P39 ?st.
    ?st ps:P39 ?role.
    ?role wdt:P279 wd:Q1623534.
    ?role wdt:P1001 ?pref.
    ?pref wdt:P429 ?code.
    FILTER EXISTS { ?st pq:P580 ?begindate }
    FILTER NOT EXISTS { ?st pq:P582 ?enddate }
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
    }
} ORDER BY ?code
```

実行▶ http://tinyurl.com/y3o27keb

### 第48回衆議院議員総選挙における当選者

```sparql
SELECT ?item ?itemLabel ?groupLabel ?districtLabel
WHERE
{
    ?item p:P39 ?statement .
    ?statement ps:P39 wd:Q17506823.
    ?statement pq:P2715 wd:Q20983100.
    ?statement pq:P768  ?district.
    ?statement pq:P4100 ?group.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
    }
}
ORDER BY ?start ?end
```

実行▶ http://tinyurl.com/yyszyzey

### 第48回衆議院議員総選挙における立候補者


```sparql
SELECT ?item ?itemLabel ?groupLabel ?districtLabel
WHERE
{
    ?item p:P3602 ?statement.
    ?statement ps:P3602 wd:Q20983100.
    ?statement pq:P768  ?district.
    ?statement pq:P1268 ?group.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "ja,en".
    }
}
ORDER BY ?start ?end
```

実行▶ http://tinyurl.com/y4cssma9
