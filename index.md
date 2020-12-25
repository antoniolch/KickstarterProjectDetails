---
layout: default
---

# KickstarterProjectDetails
This project has been made during my study period abroad and concerning the rules of making a good visualisation. It is divided into three section, all of them regard a simple analysis that comes up whatching a visualisation made over a Kickstart dataset.

More secifically, the dataset that could be taken [here](https://www.kaggle.com/kemical/kickstarter-projects#ks-projects-201801.csv) contains information and details about the Kickstarter Projects  undertaken from 2009 to 2017. It is very detailed and contains information about  the money goal and those pledged, the dates of start and deadllines as well.

All the visualisations have been made using the [VegaLite](https://vega.github.io/vega-lite/) framework.

# Dataset Description
The dataset used, from the two available on the Kaggle Repository, was the "ks-project-201801.csv" because, as the title 
suggests and as well as data exploration comes up, it concerns data from 2009 to 2017. The other one available, instead, contains 
data from 2009 to 2016. Furthermore, this choice has also been made due to the presence of the columns "usd real" and 
"usd goal real" which meaning is explained below. The dataset contains information and details about the KickProjects. 
Being more specific, each line is referred to a particular project and for each one of them there are ainformation about the project 
referred. Following a brief explanation of the attributes used for the analysis:
<ul>
  <li>The <i>name</i> of the Project;</li>
  <li>The <i>main category</i>  in which the project is collocated;</li>
  <li>The <i>category</i> that represent a sub-category in the wider main category;</li>
  <li>The <i>launched</i> that represents the date in which the project was launched;</li>
  <li>The <i>state</i> that denotes if the project has been successful (i.e. the case in which the money 
    pledged were higher than the goal), failed (i.e. the case in which the money pledged were lower than the goal), cancelled, live, suspended and undefined.</li>
  <li>The <i>backers</i> which represents the number of people that support this project;</li>
  <li>The <i>usd_pledged_real</i> which is, considering that not all the projects use the same currency, the conversion of the USD dollars of the pledged column;</li>
  <li>The <i>usd_goal_real</i> which is, as the usd_pledged_real, the conversion of the USD dollars of the pledged column.</li>
</ul>
To avoid the slowness of page loading, as consequence of the weight of the whole dataset, it has been filterea Jupyter 
Python Notebook to delete the rows and the columns that have not been used in the specific visualisation. 
The data-sets of filtered data and the code used to obtain them have been uploaded [here]("https://github.com/antoniolch/KickstarterProjectDetails/blob/master/data/data_filtering.ipynb").

# Visualisation 1

#### Question
***Considering the successful projects, which is the <i>Main Category</i> with the greatest number of them? Did it also have the greatest number of <i>Backers</i> and of <i>Money Pledged</i>?***

<html>
  <div id="vis1"></div>
  <script src="https://cdn.jsdelivr.net/npm/vega@5.9.0"></script>
  <script src="https://cdn.jsdelivr.net/npm/vega-lite@4.0.2"></script>
  <script src="https://cdn.jsdelivr.net/npm/vega-embed@6.2.1"></script>
  <script type="text/javascript">
        var yourVlSpec =  {
    "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
    "data": {
      "url": "https://raw.githubusercontent.com/antoniolch/KickstarterProjectDetails/master/data/whole_kickstarter_projects_filtered_vis1.csv",
      "format": { "type": "csv" }
    },
    "title": {
      "text":"Number, Backers and Money Pledged (USD) of Successful Projects per Category",
      "anchor":"middle",
      "fontSize": 15
    },
    "hconcat":[
      { 
        "mark":"bar",
        "encoding":{
          "y":{
            "field":"main_category",
            "type": "nominal",
            "title": "Main Category",
            "sort":{
              "op": "count",
              "field":"name",
              "order":"descending"
            }
          },
          "x":{
            "field":"ID",
            "title": "Number of Successful Projects",
            "aggregate":"count",
            "type": "quantitative"
          },
          "color": {
            "condition": {
              "test": "datum.main_category == 'Music'",
              "value" : "red"
            }
          },
            "tooltip": [
        {"field": "main_category", "type": "nominal", "title": "Main Category"},
        {"field": "name", "type":"quantitative", "aggregate":"count", "title":"Number of Successful Project"}
      ]
        }
      },
      { 
        "mark":"bar",
        "encoding":{
          "y":{
            "field":"main_category",
            "type": "nominal",
            "title": "Main Category",
            "sort":{
              "op": "sum",
              "field":"backers",
              "order":"descending"
            }
          },
          "x":{
            "field":"backers",
            "title": "Number of Backers",
            "aggregate":"sum",
            "type": "quantitative"
          },
          "color": {
            "condition": {
              "test": "datum.main_category == 'Music'",
              "value" : "red"
            }
          },
          "tooltip": [
        {"field": "main_category", "type": "nominal", "title": "Main Category"},
        {"field": "backers", "type":"quantitative", "aggregate":"sum", "title":"Number of Backers"}
      ]
        }
      },
      { 
        "mark":"bar",
        "encoding":{
          "y":{
            "field":"main_category",
            "type": "nominal",
            "title": "Main Category",
            "sort":{
              "op": "sum",
              "field":"usd_pledged_real",
              "order":"descending"
            }
          },
          "x":{
            "field":"usd_pledged_real",
            "title": "Money Pledged (USD)",
            "aggregate":"sum",
            "type": "quantitative",
            "axis":{
              "labelOverlap": "greedy",
              "labelSeparation": 2
            }
          },
          "color": {
            "condition": {
              "test": "datum.main_category == 'Music'",
              "value" : "red"
            }
          },
          "tooltip": [
        {"field": "main_category", "type": "nominal", "title": "Main Category"},
        {"field": "usd_pledged_real", "type":"quantitative", "aggregate":"sum", "title":"Money Pledged (USD)"}
      ]
        }
      }
    ]
  }
            vegaEmbed("#vis1", yourVlSpec);
  </script>
</html>

#### Description
Considering the only Successful projects, these three bar charts show respectively, for each <i>Main Category</i>, the number of projects, the number of backers and the total amount of money pledged in the USD currency. Each row represents the nominal attribute <i>Main Category</i> and its length represents the related quantitative attribute (i.e. the Number of Successful project for the bar chart on the left, the Number of Backers for the bar chart on the center and the Money Pledged in USD currency for the bar chart on the right). Each bar chart is also sorted in relation to its own quantitative attribute. Hovering over a bar will also reveal the exact value of the quantitative attribute for the specific category.

#### Insight
Against the expectation involving the "Technology" category as a winner, due to the nature of Kickstarter as an online platform, the category with the highest number successful projects is Music. This may means that, although Kickstarter is an online platform (i.e. strongly related to the technology field) where people try to finance their projects, other different kind of projects have been more appreciated. However, analyzing the number of supporters, music is not in first place. From the combination of this result with the result shown by the Money Pledged (USD) bar chart, where music is in 5th place, it can be assumed that music is a field in which projects generally have a lower goal then the other categories projects.(i.e. they do nots need a huge amount of money to be successful).

#### Design considerations
The horizontal bar charts have been chosen because it is a very effective way for length comparing. This makes very easy the comparisons between categories.
Adding a bit of redundancy and according to the Colour Pre-Attentive Property, in particular with the fact that differences in hue are perceived in the pre-attention phase, 
it has been chosen the red colour for the <i>Main Category</i> with the greatest number of successful projects. 
The Chart starts at 0, as all bar charts should be, for better understanding the difference between bars and avoiding misunderstandings.
The alternative considered has been a <i>Grouped Bar Chart</i> with a group for each Main Category. The positive aspect of this alternative is the compactness of the visualisation in which all the information could be encoded in the same chart. Nevertheless, the visualisation could be very difficult to decode because of the differences in the scale range of the quantitative attributes. 
This last problem could be overcome using normalisation. Also in this case the visualization remains difficult to decode and in particular it is difficult to make comparisons between the categories.
Horizontal bar charts have also been considered, but they were been discarded to avoid the use of angled texts that are hard to read. 

#### Data filtering and transformation
The dataset for this visualisation was filtered before using the python code uploaded on the Github repository. More precisely, only the columns "ID", "Main Category", "Backers" and "USD Pledged Real" of the successful projects are present in this filtered data version because they are the only used. Obviously, the same filter can be applied directly inside the Vega-Lite code, but it has been used the python code to make the page loading much faster.
              
# Visualisation 2

#### Question
***Considering the successful and failed projects, what is the relationship between the <i>Goal</i> (USD) and the <i>Pledged</i> (USD)?***

<html>
<div id="vis2"></div>
<script src="https://cdn.jsdelivr.net/npm/vega@5.9.0"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@4.0.2"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6.2.1"></script>
<script type="text/javascript">
        var yourVlSpec =  {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "url": "https://raw.githubusercontent.com/antoniolch/KickstarterProjectDetails/master/data/whole_kickstarter_projects_filtered_vis2.csv",
    "format": {"type": "csv"}
  },
  "width": 400,
  "height": 400,
  "title": {
    "text": "Goal vs Pledged in Technology",
    "anchor": "middle",
    "fontSize": 15
  },
  "transform": [
    { "filter": "datum.usd_goal_real < 6500000" },
    {"calculate": "(datum.usd_pledged_real /  datum.usd_goal_real) * 100", "as":"% of Goal"}
  ], 
  "mark": {"type": "point", "filled": true},
  "encoding": {
    "y": {
      "field": "usd_pledged_real",
      "title": "Pledged (USD)",
      "type": "quantitative",
      "scale": {"zero": false, "domain":[0, 6500000]},
      "axis": {"grid": false}
    },
    "x": {
      "field": "usd_goal_real",
      "title": "Goal (USD)",
      "type": "quantitative",
      "scale": {"zero": false, "domain":[0, 6500000]},
      "axis": {"grid": false}
    },
    "color":{
      "field": "state",
      "type": "nominal",
      "scale": { 
        "domain": [ "Successful" , "Failed" ], 
        "range": [ "rgb(255,128,14)", "rgb(0,107,164)" ] },
        "legend":{
          "orient":"top-right",
          "title": "Project State"
        }
    },
    "shape": {
      "condition": {
        "test": "datum.usd_pledged_real > 4000000",
        "value": "triangle-up"
      },
      "value": "circle"
    },
    "size": {
      "condition": {
        "test": "datum.usd_pledged_real > 4000000",
        "value": 150
      },
      "value": 30
    },
    "opacity": {
      "condition": {
        "test": "datum.usd_pledged_real > 4000000",
        "value": 1
      },
      "value": 0.6
    },
    "tooltip": [
      { "field": "name", "title":"Project Name", "type": "nominal" },
      { "field":"category", "title": "Category", "type": "nominal" },
      { "field": "usd_pledged_real", "title":"Pledged (USD)", "type": "quantitative"},
      { "field": "usd_goal_real",  "title":"Goal (USD)","type": "quantitative"},
      { "field": "% of Goal",  "title":"% of Goal Earned","type": "quantitative"}
    ]
  }
}
            vegaEmbed("#vis2", yourVlSpec);
      </script>
</html>

#### Description
This scatterplot shows, considering the main category Technology, the relationship between the <i>goal</i>,  measured in the USD currency, which represents the objective of a specific project and the <i>pledged</i>,  measured in the USD currency as well, which represents the money that have been sent by the people for supporting  that project. Only the successful and failed project are considered in this analysis.  Hovering over a point will reveal some information about that specific project like name, category,  goal and pledged. The colours used are blue to represent the successful projects and orange to represent the failed projects.
#### Insight
The first aspect that comes up from this graph is that the projects with a high goal were failed, receiving just few moneys or nothing. 
Furthermore, the projects that have success, generally have received much more money than the prefixed goal. 
This is the reason why the points are distributed along the axis and not on the diagonal as it would have happened if the pledged money had beenmore or less equal than a target money. 
Considering a generic project, this may suggest that either the project has lot of success or it fails miserably.
There are also some interesting outliers highlighted with the orange triangle. They regard the most four successful projects 
that have been rewarded with more than 4,000,000 dollars:
<ol start="1">
  <li>"Pono Music - Where Your Soul Rediscovers with" 6,225,354.98 dollars;</li>
  <li>"Bring Reading Rainbow Back for Every Child, Everywhere!"" With 5408916.95 dollars;</li>
  <li>"ZeTime: World's first smartwatch with hands over touchscreen" with 5333792.84 dollars;</li>
  <li>"Pimax: The World's First 8K VR Headset" with 4236618.49 dollars.</li>
</ol>
The analysis of these four projects enforces the previous consideration where there are successful projects that have earned much more than thegoal aimed.

#### Design considerations
It has been used the scatterplot because it is the best way to show the relationship between two quantitative variables (i.e. the <i>pledged money</i> and the <i>goal money</i>). 
The chosen colours have been blue for failed projects, and orange for successful projects according to the 
[Colour Blind 10 palette](https://public.tableau.com/views/TableauColors/ColorPaletteswithRGBValues?%3Aembed=y&%3AshowVizHome=no&%3Adisplay_count=y%3Adisplay_static_image=y), 
to make everyone able to decode the graph.<br> For this kind of analysis, the alternative considered was a binned heatmap that it is a very goodway to show the data distribution avoiding the overlap of points. 
However, as consequence of the fact that colours in the heatmap are used to encode density and it couldn't be used to distinguish the successfulprojects from the failed projects, 
the scatterplot was preferred. Furthermore, using the scatterplot make you able to use the tooltip for seeing additional details as which of thenew measure inserted "% of Goal Earned" 
that represents the percentage of the pledges over the prefixed goal.

#### Data filtering and transformation
The failed prejects, which goal was over 6,500,000 dollars, representing extreme outliers, have been cancelled using Vegal-Lite filters to avoid the graph to be too long along the x-axes and hard to read. 
Using the python code for filtering data, only the following columns for the successful and failed projects have been maintained: "ID","name","category", "state", "usd_pledged_real", 
"usd_goal_real" to avoid slowdowns during loading as consequence of the original dataset weight. Furthermore, still using python code, only thedata concerning the Technology Main 
Category have been used as consequence of the specific question about that Category. Obviously, the same filter can be applied directly inside theVega-Lite code, 
but it has been used the python code to make the page loading much faster.
# Visualisation 3

#### Question
***Regarding the <i>Robot</i>, <i>3D Printing</i> and <i>Software</i> categories, how the number of projects launched vary across the years from 2014 to 2017? Is the pattern consistent between these three categories?***

<html>
<div id="vis3"></div>
<script src="https://cdn.jsdelivr.net/npm/vega@5.9.0"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@4.0.2"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6.2.1"></script>
<script type="text/javascript">
        var yourVlSpec =    {
  "$schema": "https://vega.github.io/schema/vega-lite/v4.json",
  "data": {
    "url": "https://raw.githubusercontent.com/antoniolch/KickstarterProjectDetails/master/data/whole_kickstarter_projects_filtered_vis3.csv",
    "format": {
      "type": "csv",
      "parse": {"launched": "utc:'%Y-%m-%d %H:%M:%S'"}
      }
  },
  "title": {
    "text": "Robot and 3D Printing Launch",
    "anchor": "middle",
    "fontSize": 15
  },
  "width": 400,
  "height": 400,
  "transform": [
    { "filter": "year(datum.launched) > 2013" },
    { "filter": "year(datum.launched) < 2018" }
  ], 
  "mark": {"type": "line"},
  "encoding": {
    "y": {
      "field": "ID",
      "title": "Number of Projects Launched",
      "aggregate":"count",
      "type": "quantitative"
    },
    "x": {
      "field": "launched",
      "timeUnit":"year",
      "title": "Year",
      "type": "ordinal",
      "axis": { "labelAngle": 0 }
    },
    "color":{
      "field": "category",
      "type": "nominal",
      "legend": {
         "title": "Category",
         "orient": "top-right"
      },
      "scale": { 
        "range": [ "rgb(255,128,14)", "rgb(0,107,164)", "rgb(171,171,171)" ] 
      }
    }
  }
}
            vegaEmbed("#vis3", yourVlSpec);
      </script>
</html>

#### Description
This line chart aims to show how the number of projects launched in the main category  <i>Technology</i> vary during the period from 2014 to 2017, considering the <i>Robot</i>, <i>3D Printing</i> and <i>Software</i> sub-category.  The tooltip is not used here because useless in this context 
#### Insight
Using this line chart, it is possible to see the trend during the years from 2014 to 2017 regarding respectively the <i>3D Printing</i>, the <i>Robots</i> and the <i>Software</i> categories. This graph shows that there was a great increase in the number of projects launched in the 2015 in each category. However, <i>Software</i> category has had a greater interesting then the other two, considering the number of projects launched in the whole period. Then, the pattern that comes up from this analysis is the general increase in the number of projects launched during 2015 followed by a slight decrease during the following years.
#### Design considerations
It has been used a line chart because it is the best way to spot and compare trends as which seen before.  Colours have been also used to encode the different analysed categories. The colours choice is made according to the  [Colour Blind 10 palette to make everyone able to decode the graph](https://public.tableau.com/views/TableauColors/ColorPaletteswithRGBValues?%3Aembed=y&%3AshowVizHome=no&%3Adisplay_count= %3Adisplay_static_image=y). The alternative that has been analysed for this kind of analysis was the Grouped Bar Chart with a group for each year. The positive aspects of the grouped bar chart is that it makes easier the comparison between the three categories for each year but it makes too hard the identification of a trend. The reason why it has been chosen the line chart is that it is more expressive to spot trends and   it is the best way to answer to the specific question above. 
#### Data filtering and transformation
As well as in the previous visualisations it has been used the python code for filtering data and build specific dataset for this visualisation.  In particular the columns that differ from "ID", "category" and "launched" for the categories <i>3D Printing</i>, <i>Robots</i> , <i>Software</i> have been deleted. Obviously, the same filter can be applied directly inside the Vega-Lite code, but it has been used the python code to make the page loading much faster. The filters used inside the Vega-Lite code made possible the restriction over the years from 2014 to 2017.                  