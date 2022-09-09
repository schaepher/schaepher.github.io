# elasticsearch


### high disk watermark 问题

Logstash 报： index read-only / allow delete (api)

https://www.elastic.co/guide/en/elasticsearch/reference/2.1/disk-allocator.html

PUT _settings
{
  "index": {
    "blocks": {
      "read_only_allow_delete": "false"
    }
  }
}

PUT _cluster/settings
{
  "persistent": {
    "cluster.routing.allocation.disk.threshold_enabled": false
  }
}


### the `type` event field won't be used to determine the document _type 

https://www.elastic.co/guide/en/elasticsearch/reference/6.2/removal-of-types.html

https://discuss.elastic.co/t/detected-a-6-x-and-above-cluster-the-type-event-field-wont-be-used-to-determine-the-document-type-es-version-6/183471


