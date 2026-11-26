DATASET DESCRIPTION

1. File Naming Convention
-------------------------

The instance files follow the naming convention:

C208_X_24_Y.txt

where:
- C208 indicates that the instances are based on the Solomon C208 benchmark instance.
- X represents the number of freight owner groups in the instance.
- 24 represents that we consider 24 time intervals for truck-only delivery, e.g., 24h.
- Y represents the random seed number.

2. Data Description
-------------------

Each data file contains the parameters related to the marginal routing costs of freight owner groups.

Each file consists of the following seven columns:

Column          Description
GroupID         Index of the corresponding node in the original Solomon C208 instance.
early           Earliest time at which a truck can arrive at the origin barge depot.
late            Latest time at which a truck can arrive at the origin barge depot.
cost            Marginal routing cost associated with the corresponding delivery option.
isBarge         Delivery-mode indicator: 1 for truck-barge delivery and 0 for truck-only delivery.
interval        Time interval in which a truck arrives at the shopping mall for truck-only delivery.
GroupID_new     Index of the corresponding freight owner group in the generated instance.

GroupID and GroupID_new refer to the original node indices in the Solomon C208 instance and the freight owner group indices in the generated instance, respectively.

PLEASE NOTE THAT: 
Each instance also has other features, such as demand and delivery time windows. These features are specified directly in our C++ code rather than read from the data files. The way these features are set is described in our manuscript.

3. Interpretation of the Data
-----------------------------

The meaning of each row depends on the value of isBarge.

(1) Truck-barge delivery (isBarge = 1)

Each row with isBarge = 1 represents a truck-barge delivery option.

If a truck arrives at the origin barge depot within the time window [early, late], the corresponding marginal routing cost is given by cost. Note that the barge fee is not included in cost.

For these rows, interval is not applicable.

(2) Truck-only delivery (isBarge = 0)

Each row with isBarge = 0 represents a truck-only delivery option.

If a truck arrives at the shopping mall within the time interval specified by interval, the corresponding marginal routing cost is given by cost.

For these rows, early and late are not applicable.

4. Special Value
----------------

The value 10086 is used as a placeholder to indicate that a field is not applicable. It can therefore be treated as a blank or missing value when processing the data.

For example:
- For truck-barge delivery rows (isBarge = 1), interval is not applicable.
- For truck-only delivery rows (isBarge = 0), early and late are not applicable.
