# Google-Geo-Tests
Notebooks for the Youtube and Android Q4 Geo Tests


### Test Considerations

We are running two geo-tests at once, so in order to distribute the effects of each test across the segments of the other test, we are creating a 3x2 matrix as seen here.

![Screenshot 2024-10-17 at 5 42 31 PM](https://github.com/user-attachments/assets/222e4e6e-d63d-4a16-b75d-60badceffcb0)

The six geo buckets should be relatively evenly distributed in our KPIs (New Persons, Returning Persons, and Claims). A test-specifc consideration is that the android camapigns are split into tier 1 and tier 2 based off states, so tier 1 and tier 2 dmas should be relatively evenly distributed across our KPIs. Finally, due to election ad spend, swing state DMAs should also be distributed evenly across buckets.

### Segmentation

The DMAs are split into the two tiers (for DMAs lying within multiple states with different tiers, the DMA is placed into the state with the most claims), and quantile cut into 6 quantiles by claims (new persons and returning persons should be relatively proportional). From these quantiles, we randomly stratify the dmas into 6 groupings, performed seperately for tier 1 and tier 2. The tier 1 and tier 2 groups are combined to form 6 geo segments.

We perform checks on tier distribution across testing segments, swing state kpis across testing segments, and national representativeness.

### Mapping

For a visual check, the DMA Mapping notebook plots the testing segments on a map, so we can check for regional biases and other considerations. 

### Synthetic Control

Ultimately, we will run a Multi-Cell Geo-Lift Analysis utilizing [CausalPy](https://causalpy.readthedocs.io/en/latest/notebooks/multi_cell_geolift.html). The package creates synthetic controls, training a model using the control geos as inputs and the median of the treatment geo kpi as the target variable. This closely matches the control to the treatment, ensuring an accurate assessment of lift post-treatment. The Synthetic Control notebook creates these synthetic controls with the pre-test data, and outputs R^2 and MAPE values to ensure that it will be possible to do so post-test.
