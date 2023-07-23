# Juji Psychographic Insights API

"If you wish to persuade me, you must think my thoughts, feel my
feelings and speak my words." —Cicero

When coming to reading one's mind or understanding one's thoughts,
the closest approach perhaps is to learn about a person's unique
psychographic characteristics, such as their personality traits,
temperament,and psychological motivations.

##Introduction

Traditionally, item-based, self-report approaches (e.g., personality
tests) are used to discover one's psychographic
characteristics. However, such approaches are subjective
(self-reported) and [prone to faking due to social desirability
biases](https://cla.auburn.edu/news/articles/tydkydk-that-ai-knows-about-you/). Thus, finding a more natural, objective, and affordable approach to
accurately measure individuals' unique psychographic characteristics
at scale has become a quest for the holy grill in many industries,
including
[marketing](https://blog.hubspot.com/insiders/marketing-psychographics),
[talent
management](https://www.marketscreener.com/quote/stock/SALESFORCE-COM-INC-12180/news/Salesforce-com-Is-a-Robot-the-Key-To-Your-Next-Successful-Interview-41863174/),
[healthcare](https://www.ajmc.com/view/understanding-psychographics-and-how-all-health-care-behavior-is-local),
and
[education](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=50d4a59232d235c4526af6eb2483471e74ac73a6).

Building on our extensive experience of Computational Psychology, Juji
has built the world's only evidence-based, [most comprehensively
validated psychographic inference
engine](https://au.finance.yahoo.com/news/juji-inc-powers-auburn-led-143000709.html). Developers
can access the engine via the Juji Psychographic Insights API, 
analyzing a person's text, such as blogs, social media posts, chat text,
and voice transcripts and inferring their unique psychographic
characteristics, such as personality and psychological motivations.


Juji can automatically infer 100+ psychographic trait models,
including fundamental personality trait models and composite
psychographic models. Developers use one type of API to access all
trait models.


## Inferring Fundamental Personality Trait Models

Just like the periodical table in chemistry, which contains basic
chemical elements of our physical world, human characteristics are
made up of a set of fundmental personality traits, which can be used
to uniquely describe a person's characteristics from three broad
aspects: passions and interests (what they like to do), skills (what
they are good at), and how they handle life's challenges
(social-emotional intelligence).

Currently exposed via API, one can obtain computed trait scores of
[the Big 5 Personality
Traits](https://en.wikipedia.org/wiki/Big_Five_personality_traits)
from text. The Big 5 personality model includes 35 trait models, is
the most validated and most widely used personality trait model. Since
numerous studies have demonstrated [the power of Big 5 personality
traits](https://pubmed.ncbi.nlm.nih.gov/26151971/) in impacting one's
many important life outcomes, such as academic achievement, job
attainment, marriage, and lifespan, developers can use Juji API to
infer individuals' Big 5 personality traits at scale and use the
inferred personality insights to build hyper-personalized applications
in any domain or industry (e.g., match-making patients with doctors,
assessing the fit of candidates and job roles, predicting
entrepreneurs' likelihood of success, and recommending suitable
financial products).

## Inferring Composite Psychographic Characteristics Models

In addition to inferring fundamental personality traits, Juji enables
the measuring of composite psychographic characteristics, such as
[Holland Codes](https://en.wikipedia.org/wiki/Holland_Codes), human
soft skills, and moral characters. All such characteristics can also
be calculated via the Juji Cognitive Core API. 


## API Definition

- Endpoint URL: https://juji.ai/api/analyze
- Method: POST
- Max Size: 8MB

The current released API supports the Big 5 personality trait model
with 35 traits (5 factors and each with 6 facets), and 5 composite
psychographic models with additional 25 facets. Additional
psychographic models are also available upon request.

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTMQ4ixKZQ2NUox_OpHXcyhDz07fbSQWIulkFasipoZFFOX-t8T9FbjnWDFhuoukqx0mmkV_y3SfpyI/pubhtml?gid=1269779010&amp;single=true&amp;widget=true&amp;headers=false" width="100%" height="700"></iframe>


### The Basics

Both [JWT and API Key](api.md#authentication) autentication are supported. Account login is not required for API Key, which is recommended autentication method if your Juji Core API usage is independent from Juji Application.


| Header Parameter | Example | Description | Type |
| --- | --- | --- | --- |
| Accept | "application/json" or "text/csv" | Specify the response type | string |
| Content-Type | "application/json" or "text/csv" | Specify the input data type | string |
| Authorization | "Bearer <token\>" or "Basic <apikey:<apikey\> encrypted\>" | Specify for authentication | string |

| Query Parameter | Example | Description | Type | default |
| --- | --- | --- | --- | --- |
| version | YYYY-MM-DD e.g., 2020-01-01, 2021-12-01 | Specify Juji API version at a particular date, latest version starts on 2021-12-01. To use previous API version, please specify a date before 2021-12-01. **Note: the previous API does not affect other parameters, see the [section below](#previous-version) for more details.**  | string | latest version |
| lang | "en", "es", "fr" or "zh" | Specify language of the input data, non-English input will be translated to English for analysis | string | "en" |
| big5_factors | true/false | Whether to include big5 factor results | boolean | TRUE |
| big5_facets | true/false | Whether to include big5 facet results | boolean | FALSE |
| holland_codes | true/false | Whether to include holland code results | boolean | FALSE |
| shopper_dna | true/false | Whether to include shopper dna results | boolean | FALSE |
| soft_skills | true/false | Whether to include soft skill results | boolean | FALSE |
| moral_characters | true/false | Whether to include moral character results | boolean | FALSE |
| big5_factors_x | true/false | Whether to include big5 factor explanation that's tailored to resulting percentile | boolean | FALSE |
| big5_facets_x | true/false | Whether to include big5 facet explanation that's tailored to resulting percentile | boolean | FALSE |
| big5_factors_x_general | true/false | Whether to include big5 factor general explanation | boolean | FALSE |
| big5_facets_x_general | true/false | Whether to include big5 facet general explanation | boolean | FALSE |
| holland_codes_x_general | true/false | Whether to include holland code general explanation | boolean | FALSE |
| shopper_dna_x_general | true/false | Whether to include shopper dna general explanation | boolean | FALSE |
| soft_skills_x_general | true/false | Whether to include soft skill result general explanation | boolean | FALSE |
| moral_characters_x_general | true/false | Whether to include moral character general explanation | boolean | FALSE |

### Request Data/Body

Data can be included in the request in JSON or CSV format.

Data in JSON format should be an array of objects that each object represent a person that is identified by "id" and has "text" for analysis. JSON input can be passed directly as the body of the request or through a file. Below is an example JSON data.
```json
[         
  {                 
    "id":"1",                 
    "text":"sentence 1. sentence 2..."
  },
  {
    "id":"2",
    "text":"sentence 1. sentence 2..."
  }
]
```

Data in CSV format requires each row to represent a person with the first column being the id and the second column being the text. The CSV file should have no header. Below is an example of same data in CSV format.
```csv
1, sentence 1. sentence 2...
2, sentence 1. sentence 2...
```

### Response

Similarly, response in both JSON and CSV formats are supported.

Response in JSON format will have the following fields:

| Key | Example | Description |
| --- | --- | --- |
| trait_id | "big5_facets_imagination" | id of the trait, <category\>_<name\> |
| name | "imagination" | name of the trait |
| category | "big5_facets" | category of the trait |
| percentile | 23.42 | percentile |
| explanation | "low imagination" | explanation of the trait percentile in English |
| general_explanation | "imagination is ..." | general explanation of the trait in English |
| parent | "big5_factors_openness" | the trait_id of the parent of the trait if applicable |

```json
{
  "results": 
  [
    {
      "id": "1", 
      "personality": 
      {
        "big5_factors_openness":
        {
          "trait_id": "big5_factors_openness",
          "name": "Openness",
          "category": "big5_factors", 
          "percentile": 70.12, 
          "explanation": "high openness",
          "general_explanation": "openness is ...",
          "code": "a_7100"
        },
        "big5_facets_imagination": 
        {
          "trait_id": "big5_facets_imagination",
          "name": "Imagination",
          "category": "big5_facets",
          "percentile": 34.56, 
          "explanation": "low imagination",
          "general_explanation": "imagination is ...",
          "parent": "big5_factors_openness",
          "code": "a_7110"
        }, 
      ...
      }
    }, 
    {
      "id": "2", 
      ...
    }, 
    ...
  ]
}
```

Response in CSV has a header that provides information to each column.

### Example API calls

#### Raw JSON
```shell
curl --location --request POST 'http://localhost:8080/api/analyze?version=2021-12-10&big5_facets=true' \
--header 'Authorization: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..wN4i7DMa_k0CDe74ABYDqw.d8sBK-7JIpj_Dh6nL8SgLrzQ_aOCWsy6tngCGZHwItpsJkIY7hBueQYasOFCpbQa.fg1PZD5hcH_OfuFV6KsnZg' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data-raw '[         
        {                 
                "id":"1",                 
                "text":"When the bad times started there, in 38, he came to Spain, since he had both nationalities. "
        },
        {
                "id":"2",
                "text":"It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of light, it was the season of darkness, it was the spring of hope, it was the winter of despair."
        }
]'
```

#### JSON File
```shell
curl --location --request POST 'http://localhost:8080/api/analyze?version=2021-12-10&big5_facets=true' \
--header 'Authorization: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..wN4i7DMa_k0CDe74ABYDqw.d8sBK-7JIpj_Dh6nL8SgLrzQ_aOCWsy6tngCGZHwItpsJkIY7hBueQYasOFCpbQa.fg1PZD5hcH_OfuFV6KsnZg' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--data-binary '@juji.json'
```

#### CSV File
```shell
curl --location --request POST 'http://localhost:8080/api/analyze?version=2021-12-10' \
--header 'Authorization: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..wN4i7DMa_k0CDe74ABYDqw.d8sBK-7JIpj_Dh6nL8SgLrzQ_aOCWsy6tngCGZHwItpsJkIY7hBueQYasOFCpbQa.fg1PZD5hcH_OfuFV6KsnZg' \
--header 'Accept: application/json' \
--header 'Content-Type: text/csv' \
--data-binary '@juji.csv'
```

#### API Key
```shell
curl --request POST 'https://juji.ai/api/analyze?version=2021-12-10&big5_facets=true&holland_codes=true&big5_factors_x=true&holland_codes_x_general=true&soft_skills=true&moral_characters=true&shopper_dna=true&moral_characters_x_general=true&big5_facets_x=true&big5_facets_x_general=true' \
--header 'Accept: application/json' \
-u 'apikey:<your-api-key>' \
--header 'Content-Type: application/json' \
--data-raw '[
        {
                "id":"1",
                "text":"It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of light, it was the season of darkness, it was the spring of hope, it was the winter of despair."
        }
]'
```

### Previous version

If you have used Juji Cognitive Core API prior to 2022, you may wish
to migrate to the current version as our inference models have been
updated and improved.

The previous version personality inference can be used by specifying the version parameter to any date before 2021-12-01. However, none of the other query parameters are supported in this version. And only the big 5 factors and their facets percentile predictions will be provided in the response.

In this version, data needs to be provided throught a file. The data file is expected to be `POST` as a `file` field in `multipart/form-data`. There is no need to specify the content-type. If have to, put in `application/json` or `text/csv` respectively as the data file can be either a JSON or CSV file with corresponding file suffix.

If the data is in a CSV file, we expect the first column contains the identifier, and the
second column contains a concatenation of an individual's written text as a single string. The CSV file should *not* have header.

If the data is in JSON format, we expect an array of objects, where
each object has two fields: `id` and `text`. `text` will be a concatenation of
an individual's written text into a single string, and `id` be any string that
is unique among the input rows/objects.

The output is streamed back in a CSV file, where the first row is the header with the names of the traits. The values of the traits are percentiles.

Juji does not retain the uploaded files, as they are immediately discarded after
the output is returned.
