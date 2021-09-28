# Elastic Search

## Query Examples

* Url: http://<ElasticSearchServer>/<index>/_search

```json
// Examples of json body
"query": {
  "bool": {
    "must": [
      { "term": { "post_type": "article" } },
      { "match": { "post_type": "article" } },
      { "match_phrase": { "html_content": "most important thing" } }
    ],
    "must_not": {
      "range": {
        "date_scheduled": { "gte": "2014-01-01", "lte": "2019-12-31" }
      }
    },
    "should": [
      { "term": { "name": "slander" } },
      { "term": { "slug": "slander" } }
    ],
    "filter": [
      { "term": { "post_type": "article" } },
      { "range": { "post_id": { "gte": 30 } } }       // 29 taken out
    ]
  },
  "fuzzy": {
    "description": {
      "value": "question"
    }
  },
  "match": {
    "OriginCityName": "Frankfurt am Main"     // Exact match
  },
  "match": {                                  // Or match
    "description": {
      "query": "faq question legal help injury",
      "minimum_should_match": 2,              // Notice plural Questions does not count as a match
      "operator": "or"                        // Default is 'or', can be changed to 'and'
    }
  },
  "match_phrase": {
    "html_content": "most important thing"
  },
  "multi_match": {
    "fields": [
      "name^3",                               // Per-field boosting by 3
      "description",
      "html_content"
    ],
    "query": "legal question",
    "type": "phrase"                          // Use match_phrase logic
  },
  "range": {
    "dayOfWeek": {
      "gte": 1,
      "lte": 3
    }
  },
  "wildcard": {
    "name": {
      "value": "*legal*"
    }
  }
}
```

## Aggregation Examples

```json
{
  "size": 0,              // Do not return hits
  "aggregations": {
    "group_by_ip": {      // Look for results under `aggregations.group_by_ip` instead of `hits`
      "terms": {
        "field": "updated_by_ip_address",
        "size": 100       // Up to 100 items in buckets
      }
    },
    "popular_cities": {
      "significant_text": {
        "field": "OriginCityName"
      }
    },
    "sum_active": {     // Look for results under `aggregations.sum_active` instead of `hits`
      // "avg": {
      "sum": {
        "field": "is_active"
      }
    },
    "min_date_scheduled": {
      // "max": {
      "min": {
        "field": "date_scheduled"
      }
    },
    "stats_active": {
      "stats": {
        "field": "is_active"
      }
    },
    "unique_ips": {
      "cardinality": {
        "field": "updated_by_ip_address"
      }
    },
    // === date_histogram aggregation
    "updated_at_by_8h": {
      "date_histogram": {
        // "field": "updated_at",
        // "fixed_interval": "8h"         // 8 hours
        // "calendar_interval": "1M"      // 1 month
        "field": "date_scheduled",
        "calendar_interval": "1y",        // 1 year
        "order": {                        // Optional
          "_key": "desc"
        }
      }
    },
    // === histogram aggregation
    "unit_price_per_10": {
      "histogram": {
        "field": "unit_price",
        "interval": 10
      }
    },
    // === range aggregation
    "post_id_per_custom_range": {
      "range": {
        "field": "post_id",
        "keyed": true,                        // Optional
        "ranges": [
          { "to": 500.0 },
          { "from": 500.0, "to": 1500.0 },    // to is exclusive
          { "from": 1500.0 }                  // from is inclusive
        ]
      },
      "aggs": {
        "min_post_id": {
          "min": {
            "field": "post_id"
          }
        },
        "max_post_id": {
          "max": {
            "field": "post_id"
          }
        }
      }
    },
    // === top n aggregation
    "top_2_ip_address": {
      "terms": {
        "field": "updated_by_ip_address",
        "size": 2,
        "order": {                        // Optional
          "_count": "asc"
        }
      }
    },
    // === Combo with computed field
    "date_scheduled_by_year": {
      "date_histogram": {
        "field": "date_scheduled",
        "calendar_interval": "1y",
        "order": {
          "sum_of_1_10_of_post_ids": "desc"               // Sort by sub aggregation field
        }
      },
      "aggs": {
        "sum_of_1_10_of_post_ids": {
          "sum": {
            "script": {
              "source": "doc['post_id'].value * 0.1"      // Computed field
            }
          }
        },
        "unique_ips": {                                   // Same as standard cardinality aggregation
          "cardinality": {
            "field": "updated_by_ip_address"
          }
        }
      }
    }
  }
}
```