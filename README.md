# fda_charts_apacheSpark

This repo uses the entire FDA NDC drug file to process certain metrics using a notebook in AWS Athena's Spark engine.  The metrics are extracted and presented in the data folder.  

In order to see the charts, you simply download the html file to your local computer.  The html file pulls the data directly from this repo, leveraging Google's Chart API to render the charts.

The "mostchange" metric is comparing the prior 12 month period (i.e., two years ago) to this past 12 month period to determine the percentage change.  The high percentage results are largely due to the small numbers for certain labelers/ingredients/pharm classes (ex. a labeler goes from 2 drugs in one year to 10 in the next year).   

In the notebook I restrict the metrics to product_types "Human Prescription Drug' and "Human OTC Drug", but there are other less populated types.  Also, because I'm using Athena's Spark engine, the pandasDF.to_json doesn't write to S3, so I use boto's S3.put_object, but if you're in a different environment you can use the native pandas to_json.

The FDA NDC zip is located here: https://open.fda.gov/apis/drug/ndc/download/
