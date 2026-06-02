# Offline CRAN Snapshot

SDE3 does not have Internet access. An offline snapshot of CRAN is created with name sdeCRAN that can be used to install R packages by any general user. It could be accessed by setting up 
***repos = "file:///software/sdeCRAN"***
<br><br/>
As an example, to install dplyr
```R
install.packages("dplyr", repos = "file:///software/sdeCRAN", type = "source", dependencies = TRUE)
```
