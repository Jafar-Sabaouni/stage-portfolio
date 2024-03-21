# React TS data fetching libraries

### &#x20;

Op dit moment maken we gebruik van SWR voor ons (antistatic) opdracht. Ik heb een lijst samenstelt van de beste libraries voor het ophalen van gegevens volgens online courses. Vervolgens zal ik deze libraries vergelijken met ons project en de vereisten. Hierbij kijk ik naar aspecten zoals compatibiliteit met React en TypeScript, langdurige ondersteuning, open source status en een goede track record.&#x20;

De minimale vereisten moeten beter zijn dan de native JavaScript fetch.&#x20;

Na wat onderzoek heb ik een lijst samengesteld van de meest bruikbare libraries :&#x20;

| <mark style="color:purple;">Library</mark>           | <mark style="color:purple;">Github Stars</mark>                           | <mark style="color:purple;">Released</mark>  | <mark style="color:purple;">Used By</mark>  | <mark style="color:purple;">Contributors</mark>  | <mark style="color:purple;">Size</mark>  |
| ---------------------------------------------------- | ------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------- | ------------------------------------------------ | ---------------------------------------- |
| <mark style="color:red;">SWR</mark>                  | [29.1k stars](https://github.com/vercel/swr/stargazers)                   | 2019                                         | 238k                                        | 174                                              | 620  KB                                  |
| <mark style="color:red;">TanStack Query</mark>       | [38.9k stars](https://github.com/TanStack/query/stargazers)               | 2020                                         | 1,8k                                        | 754                                              | 1.93 MB                                  |
| <mark style="color:red;">tRPC</mark>                 | [32k stars](https://github.com/trpc/trpc/stargazers)                      | 2019                                         | 48k                                         | 173                                              | 713  KB                                  |
| <mark style="color:red;">Apollo client</mark>        | [19.2k stars](https://github.com/apollographql/apollo-client/stargazers)  | 2016                                         | 178k                                        | 795                                              | 6.66 MB                                  |
| <mark style="color:red;">axios</mark>                | [104k stars](https://github.com/axios/axios/stargazers)                   | 2016                                         | 12.1m                                       | 443                                              | 1,84 MB                                  |

&#x20;<mark style="color:yellow;">De tabel boven aan is geen ranking.</mark>

Conclusie : &#x20;

Er zijn enkele andere fetching libraries die aan mijn criteria voldoen. Het is ook mogelijk dat tijdens mijn onderzoek één of twee libraries over het hoofd heb gezien. Desondanks ben ik tevreden met mijn resultaten, waarbij ik en paar potentiële opties heb geïdentificeerd.&#x20;

Ik heb twee alternatieven gevonden: Axios en TanStack Query, ook wel bekend als React Query. Beide kandidaten zijn perfecte alternatieven, omdat ze langdurige ondersteuning bieden, lichtgewicht zijn en geschikt zijn voor zowel grote als kleine projecten. Echter, voor ons lijkt het het beste om bij SWR te blijven, aangezien we al binnen het Versel-ecosysteem werken, en de voordelen zijn niet groot genoeg om van library te veranderen.&#x20;

&#x20;

&#x20;

&#x20;

Sources :&#x20;

{% embed url="https://www.npmjs.com/" %}

{% embed url="https://byy.dev/react-data-fetching-libraries" %}

{% embed url="https://bestofjs.org/projects?tags=data&tags=react&sort=total" %}

{% embed url="https://github.com" %}

###
