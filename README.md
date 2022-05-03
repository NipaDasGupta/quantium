# Quantium starter repo

blah blah blah
</br></br>
<b>Task 1:</b> Set Up Your Local Development Environment

* Clone the quantium-starter-repo repository using this command:
<pre>
git clone https://github.com/vagabond-systems/quantium-starter-repo.git
</pre>
* Download and install Pycharm Community Edition using this link: https://www.jetbrains.com/pycharm/download/#section=windows
* Create a new virtual environment
<pre>
python -m venv quantium
</pre>
* Activate your virtual environment
<pre>
.\quantium\Scripts\activate # Windows 
</pre>
* Install dependencies and add a virtual environment to the Python Kernel
python -m pip install --upgrade pip
pip install ipykernel
python -m ipykernel install --user --name=quantiumj
* Add the dash and pandas packages as dependencies to your virtual environment
<pre>
pip install dash
pip install pandas
</pre>
* To check your installed dependencies using this command: 
<pre>
pip list
</pre>
* With your virtual environment active, install all the necessary dash testing dependencies
<pre>
pip install dash[testing]
</pre>
* Commit your changes and push them to GitHub. To add a large library in git, first download Git Large File Storage (LFS) using this link: https://git-lfs.github.com/
* Then compressed the library folder in a zip folder. Go to the command prompt and run these command: 
<pre>
git lfs install
git lfs track "*.zip" #format of the file or folder
git add .gitattributes
git add filename.zip
git commit -m "Add Zip File"
git push origin main
</pre>
* Submit a link to your repo in the right module.
</br>
<b>Task 2:</b> Data Processing

* First, combine multiple daily sales CSV files in one 'csv' file. To do that import packages and set the working directory
<pre>
import os
import glob
import pandas as pd
os.chdir("D:\quantium\quantium\data") #path of the folder
</pre>
* Use glob to match the pattern ‘csv’
<pre>
extension = 'csv'
all_filenames = [i for i in glob.glob('*.{}'.format(extension))]
</pre>
* Combine all files in the list and export as CSV
<pre>
# combine all files in the list
combined_csv = pd.concat([pd.read_csv(f) for f in all_filenames ])
# export to csv
combined_csv.to_csv( "combined_daily_sales_data.csv", index=False, encoding='utf-8-sig')
</pre>
* Remove any row which contains another type of product rather than 'pink morsel' from the product column
<pre>
df = pd.read_csv("D:\quantium\quantium\data\combined_daily_sales_data.csv") #file path
df.head()
# droping rows that contains another types of product
df = df.drop(df.index[df['product'].isin(['chartreuse morsel', 'gold morsel', 'lapis morsel', 'magenta morsel', 'periwinkle morsel', 'vermilion morsel'])])
df.value_counts('product') 
# save modified csv file
df.to_csv('combined_daily_sales_data.csv')
</pre>
* Combined "quality" and "price" into a single field, "sales", by multiplying them together
<pre>
df.info()
df['price'] = df.price.str.replace(r'$', '')\
                   .str.replace(',', '.').astype(float) # replace the $ symbol and convert the price into float
df['sales'] = df['price'] * df['quantity'] # multiply the values and combine it into a single field, 'sales'
# save modified csv file
df.to_csv('combined_daily_sales_data.csv')
</pre>
* Commit and push your changes, then submit a link to your repo
</br>
<b>Task 3:</b> Create a Dash Application

* Import dependecies
<pre>
from dash import Dash, dcc, html
# Using plotly.express
import plotly.express as px
import pandas as pd
</pre>
* Reading the csv file data
<pre>
df = pd.read_csv('D:\quantium\quantium\data\combined_data.csv')
</pre>
* Time Series Plot with Daily Sales Data in Date Range
<pre>
fig = px.line(df, x='date', y='sales', range_x=['2018-02-06','2022-02-14'], title='Dash app')
fig.show()
</pre>
![newplot](https://user-images.githubusercontent.com/89456649/166251956-494f9ed7-f800-4b92-aa2d-324c132b2e91.png)
<b>Task 4:</b> 

* Import dependecies
<pre>
import plotly.express as px
from jupyter_dash import JupyterDash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import pandas as pd
</pre>
* Loding the csv file data
<pre>
# the path to the formatted data file
DATA_PATH = "D:\quantium\quantium\data\combined_data.csv"
# load in data
df = pd.read_csv(DATA_PATH)
df = df.sort_values(by="date")
</pre>
* Making region-specific sales data for Pink Morsel
<pre>
# Build App
app = JupyterDash(__name__)

colors = {
    'background': '#111111',
    'text': '#7FDBFF'
}

fig = px.bar(df, x="date", y="sales", color="region", barmode="group")

fig.update_layout(
    plot_bgcolor=colors['background'],
    paper_bgcolor=colors['background'],
    font_color=colors['text']
)

app.layout = html.Div(style={'backgroundColor': colors['background']}, children=[
    html.H1(
        children='JupyterDash App',
        style={
            'textAlign': 'center',
            'color': colors['text']
        }
    ),

    html.Div(children='Dash: A web application framework for your data.', style={
        'textAlign': 'center',
        'color': colors['text']
    }),

    dcc.Graph(
        id='example-graph-2',
        figure=fig
    )
])


# Run app and display result inline in the notebook
app.run_server(mode='inline')
</pre>
![newplot (1)](https://user-images.githubusercontent.com/89456649/166407616-eb1304f7-2408-4b97-9c91-272f2cdbc924.png)
