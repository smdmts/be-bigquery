# Be-BigQuery
## Examples
### Execute a query simply
```java
BeBigQuery bbq = new BeBigQuery("project-id"
        , "servic-account"
        , new File("path/file.p12"));
Iterable tableRows = bbq.query("select * from dataset.table where condition=11").asIterable();
for (TableRow row : tableRows) {
    for (TableCell cell : row.getF()) {
        System.out.print(cell.getV().toString() + ",");
    }
    System.out.println();
}
```

### Execute a query and get large results
```java
Iterable tableRows = bbq.query("select * from dataset.table where condition=11")
    .asIterableViaGcs("temp_dataset", "temp_gcs_buckt");
```

## Use BigQuery with Apache Spark as input data
```
// scala sample
val bbq = new BeBigQuery("project-id" , "servic-account", new File("path/file.p12"))
bbq.query("select * from dataset.table where condition=11")
    .exportToGcs("tempDataset", "tempTable", "gcsBucket", "gcsPath/*")
val textFile = sc.textFile("gs://gcsBucket/gcsPath/")
```
