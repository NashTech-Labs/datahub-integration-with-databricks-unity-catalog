## Ingesting Databricks Unity Catalog Data to DataHub

**By Ingesting our Unity Catalog data to data-hub it is good for data observability, quality check, policies, lineage
etc.**

### Steps to set up ingestion:

1. Install the python library in local.

```sh
   pip install 'acryl-datahub[unity-catalog]'
```

```sh
   pip install acryl-datahub
```

2. Create a yaml file in that specify the type of ingestion and databricks url and token of databricks.

```yaml
     type: unity-catalog
     config:
        workspace_url: https://55801*********.4.azure.databricks.com
        token: "dapia1711ad*******************"
```

3. After that specify the metastore id, catalog pattern, schema pattern and table pattern to ingest the specific data
   from databricks:

```yaml
      metastore_id_pattern:
      allow:
        - metastore-id
      catalog_pattern:
        allow:
          - metastore-id.catalog_name
        deny:
          - metastore-id.catalog_name
      schema_pattern:
        allow:
          - metastore-id.catalog_name.schema_name
        deny:
          - metastore-id.catalog_name.schema_name
      table_pattern:
        allow:
          - catalog_name.schema_name.table_name
```

4. You can also specify more terms in yaml file. Refer below link for more configuration

> https://datahubproject.io/docs/generated/ingestion/sources/databricks/

5. Define the name of pipeline

```yaml
   pipeline_name: ingesting-databricks-unity-catalog-data
```

5. After that run the below command to ingest databricks data to data-hub platform **by moving to recipe directory**

```shell
   DATAHUB_GMS_URL="http://35.***.***.***:8080" datahub ingest -c cartrecipe.dhub.yaml
```
