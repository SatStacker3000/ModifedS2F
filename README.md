# ModifedS2F
PlanB's S2F model modified with a p-spline on days-to-next halving

This is an RMD file, which is an RMarkdown file.

If you "Knit" this script in RStudio, it produces a report in the form of the PDF in this repository.

The price is essenitally computed by the following code:

```
priceModel <- function(x, S2F, DaysToHalving1, DaysToHalving2, DaysToHalving3, DaysToHalving4, DaysToHalving5, DaysToHalving6) {
result <- (exp(x[1] + x[3]*DaysToHalving1 + x[4]*DaysToHalving2 + x[5]*DaysToHalving3 + x[6]*DaysToHalving4 + x[7]*DaysToHalving5 + x[8]*DaysToHalving6)*(S2F)^(x[2]))
return(result)
}
```

 The DaysToHalving1 - DaysToHalving5 columns are created with these lines of code:
 
``` 
tmp <- dat[,pspline(DaysToHalving, nterm = 4)] %>% as.matrix()
class(tmp) <- "matrix"
tmp <- as.data.table(tmp)
names(tmp) <- paste0("DaysToHalving", 1:ncol(tmp))
```
