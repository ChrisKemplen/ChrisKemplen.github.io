# Higher Education Statistics Agency (HESA) — Common Aggregation Hierarchy of Subjects

The Higher Education Statistics Agency's (HESA) Common Aggregation Hierarchy (CAH) is a standardized classification system used in the United Kingdom to group together similar subjects across higher education institutions. It is used to facilitate the collection and reporting of data related to higher education, such as student enrollment, qualifications, and research activity. The CAH is organized into three levels of increasing specificity, with each level containing a number of subject areas. 

https://www.hesa.ac.uk/support/documentation/hecos/cah


```python
# This code imports necessary packages: requests, plotly, plotly express, and pandas
# It also initializes plotly offline mode for use in a Jupyter notebook

import requests
import plotly
import plotly.express as px
import pandas as pd

plotly.offline.init_notebook_mode()


# This code takes the url for the HESA mappigns csv and uses the requests package to get the data at that url
url = "https://www.hesa.ac.uk/files/HECoS_CAH_Mappings.csv"

response = requests.get(url)

with open("HECoS_CAH_Mappings.csv", "wb") as f:
    f.write(response.content)

    
# This code reads the csv file created in the previous step into a pandas dataframe
df = pd.read_csv("HECoS_CAH_Mappings.csv")


# This code uses plotly express to create a treemap chart with the data from the dataframe
# It specifies the path to take in order to create the chart
fig = px.treemap(df,
                path=[px.Constant("All subjects"),
                     "CAH1_Label",
                     "CAH2_Label",
                     "CAH3_Label",
                     "HECoS_Label"
                     ],
                )


# This code updates the layout of the chart to remove default margins and add custom margins
fig.update_layout(
            overwrite=True,
            margin_b=20,
            margin_l=20,
            margin_r=25,
            margin_t=0,
        )

```


```python
# using following package versions
for package in [requests, plotly, pd]:
    print(package.__name__, package.__version__)
```

    requests 2.27.1
    plotly 5.14.1
    pandas 1.4.4
    


```python
fig.write_html("index.html")
```
