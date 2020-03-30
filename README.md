# Data-Mining-Cup-2019
### Fraud detection at self-checkouts in retail

The number of self-checkout stations is on the rise. This includes stationary self-checkouts, where customers take their shopping cart to a scan station and pay for their products. Secondly, there are semi-stationary self-checkouts, where customers scan their products directly and only pay at a counter. The customers either use their own smartphone for scanning or the store provides mobile scanners. 

This automated process helps avoid long lines and speeds up the paying process for individual customers. But how can retailers prevent the trust they have placed in customers from being abused? How can they decide which purchases to check in an effort to expose fraudsters without annoying innocent customers?
This was the topic of the DATA MINING CUP 2019.


### Scenario
An established food retailer has introduced a self-scanning system that allows customers to scan their items using a handheld mobile scanner while shopping. This type of payment leaves retailers open to the risk that a certain number of customers will take advantage of this freedom to commit fraud by not scanning all of the items in their cart.

Empirical research conducted by suppliers has shown that discrepancies are found in approximately 5 % of all self-scan transactions. The research does not differentiate between actual fraudulent intent of the customer, inadvertent errors or technical problems with scanners. To minimize losses, the food retailer hopes to identify cases of fraud using targeted follow-up checks. The challenge here is to keep the number of checks as low as possible to avoid unnecessary added expense as well as to avoid putting off innocent customers due to false accusations. At the same time, however, the goal is to identify as many false scans as possible.

The objective therfore was to create a model to classify the scans as fraudulent or non-fraudulent. The classification does not take into account whether the fraud was committed intentionally or inadvertently.

### Summary
| Algorithm | Test in % | Train in % | CV | Hyperp. tuning |  Weight Config  | threshold | Precision | Recall | Domain-specific exp. return |
|:---------:|:---------:|:----------:|:---------------:|:------------------:|:---------------:|:------------------:|:---------:|:------:|:---------------------------:|
|     NB (Baseline)    |     80    |     20     |        -        |          -         |        -        |          -         |    .33    |   .94  |            - 929.970 €            |
|    SVM    |     80    |     20     |        -        |          -         |  {0:1.0, 1:2.0} |          -         |    .59    |   1.0  |            - 267.760 €            |
|     LR    |     80    |     20     |        -        |          -         |  {0:1.0, 1:1.0} |          -         |    .67    |   1.0  |            -140.645 €            |
|     RF    |     80    |     20     |        -        |          -         | {0:1.0, 1:50.0} |          -         |    .85    |   .69  |             - 72.120 €            |
|    SVM    |     80    |     20     |        -        |          -         |  {0:1.0, 1:2.0} |        >0.8        |    .88    |   .94  |              53.880 €             |
|     LR    |     80    |     20     |        -        |          -         |  {0:1.0, 1:1.0} |        >0.9        |    .83    |   .62  |             55.415 €            |
|     RF    |     80    |     20     |        -        |          -         | {0:1.0, 1:10.0} |        >0.65       |    1.0    |   .69  |             - 14.340 €             |
|    SVM    |     80    |     20     |     10 Fold     |         Yes        |  {0:1.0, 1:2.0} |        >0.95        |    .82    |   .94  |             53.335 €             |
|     LR    |     80    |     20     |     10 Fold     |         Yes        |  {0:1.0, 1:1.0} |        >0.9        |    .88    |   .96  |             54.020 €            |
|     RF    |     80    |     20     |     10 Fold     |         Yes        | {0:1.0, 1:10.0} |        >0.65       |     1.    |   .44  |             - 5.770 €             |

### Remarks
1. There is more to lose then to win
The prediction model required an extreme high precision rate with low False Positive rates. Implementing a prediction model which is not generalising properly could result in catastrophic effects in returning profits. A good generalised model would however only create small increasing profit margins. Therefore, it is necessary to question if we should provide such reactive approaches in general, but rather a proactive approach:

2. Proactive vs. reactive
Our model is a reactive approach based on the customers shopping pattern. Since there is much to lose in this reactive approach, it is reasonable to consider a proactive approach. An example of such proactive approach would be staff standing at the scan ensemble to monitor a bunch of scanners. This is a common approach in for common retailers too (IKEA) that provide self-service checkouts.

Furthermore, even if the retailer implements a reactive model which generates negative returns, it might still be useful if they would consider the costs of staff savings. Since a reactive approach requires staff which is constantly monitoring, it could be that a model which is generating negative return might generate overall savings if staff could therefore be reduced.