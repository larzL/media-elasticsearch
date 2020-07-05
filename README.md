# ElasticSearch
Install and configure ElasticSearch.

### Ansible

```yaml
- hosts: all
  become: true
  roles:
    - role: elasticsearch
      tags: elasticsearch
```

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    elasticsearch_version: '6.8.1'

The major version to use when installing Elasticsearch.

    elasticsearch_package_state: present

The `elasticsearch` package state; set to `latest` to upgrade or change versions.

    elasticsearch_service_state: started
    elasticsearch_service_enabled: true

Controls the Elasticsearch service options.

    elasticsearch_network_host: localhost

Network host to listen for incoming connections on. By default we only listen on the localhost interface. Change this to the IP address to listen on a specific interface, or `0.0.0.0` to listen on all interfaces.

    elasticsearch_http_port: 9200

The port to listen for HTTP connections on.

```elasticsearch_extra_config:
          cluster:
            name: media_contents
            routing:
              allocation:
                awareness:
                  attributes: zone
```

Use the `elasticsearch_extra_config` option to add additional config.

```ES_plugins:
  - name: elasticsearch/elasticsearch-analysis-icu
    version: 2.4.2
  - name: lmenezes/elasticsearch-kopf
    version: 1.0
```

Install plugins using `ES_plugins`.

```elasticsearch_extra_config:
          node:
            data: "{{ es_data_ensure }}"
            master: "{{ es_master_ensure }}"
```

You can set `node.{data|master}` using `group_var`. The rest config for master and data node should be pretty much identical.
