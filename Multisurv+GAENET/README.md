# Multisurv+GAENET
![Multisurv+GAENET](https://user-images.githubusercontent.com/69032913/202623549-fb9ec11f-9aa4-48b1-b8a2-bc63ad044af0.PNG)
## Data
### Clinical Data
Use the following R code to download data.

```r
# Download data for all TCGA projects
project_ids <- stringr::str_subset(TCGAbiolinks::getGDCprojects()$project_id, 'TCGA')

data <- list()

for (project_id in project_ids) {
    data[[project_id]] <- TCGAbiolinks::GDCquery_clinic(project=project_id, type='clinical')
}

# Merge into single table
# (the "disease" column identifies each original table)
data <- do.call(dplyr::bind_rows, data)

# Write to file
output_path <- '/mnt/dataA/TCGA/raw/clinical_data.tsv'
readr::write_tsv(data, output_path)
```

How to copy a file from A to B:
```console
scp /path/to/file username@B:/path/to/destination
```