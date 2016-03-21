Interactive web applications in R
=================================

This lesson presents an introduction to creating interactive web applications using the Shiny package in R. We will cover the following concepts:

-   [file structure template](#app-template)
-   [input objects](#input-objects)
-   [output objects](#output-objects)
-   [create a reactive object](#create-reactive-object)
-   [customizing layout design](#design-layout)
-   [upload or download files](#download-button)
-   [deploying your app](#how-to-deploy)

Make sure the shiny package is installed and loaded

``` r
# library(shiny)
```

App template
------------

A shiny app consists of two components:

-   **ui** which defines the user interface with the main function `fluidPage()`
-   **server** which defines the instructions for assembling components of the app as a function of input and output objects

There are two ways to structure an app:

1.  Create one file called `app.R`. In this file, define objects `ui` and `server` with the assignment operator `<-` and then pass them to the function `shinyApp()`.
2.  Split the template into two files named `ui.R` and `server.R`.

When the `shiny` package is installed and loaded, RStudio will identify this file structure and create a green arrow with a "Run App" button when you open a file in the app. Applications use your current R session and are displayed in a browser window.

Test this by looking at an example within the shiny package:

``` r
# runExample("01_hello")
```

Notice the stop sign that appears in the Console window while your app is running. This is because it is using the current R session. Make sure to end the app by either closing the external window or clicking the stop sign.

Input objects
-------------

The user interface and the server file interact with each other through \_\_\*Input()\_\_ and \_\_\*Output()\_\_ functions.

Input objects collect information from the user and saves them based on the name given to the `inputId =` argument. Input objects also have a `label =` which is displayed to the user, as well as other values based on the type of input widget.

Input objects are **reactive** which means that an update to this value by a user notifies the server file that its value has been changed.

Input objects are stored in a list and are therefore referred to in the server file as `input$inputID`.

Choices for inputs can be named using a list to match the display name to the value \# Male = "M", Female = "F", Both = "M" & "F"

Selectize input useful for long drop down lists

``` r
# plots <- read.csv("../Data/plots.csv", stringsAsFactors = FALSE)
# species <- read.csv("../Data/species.csv", stringsAsFactors = FALSE)
# surveys <- read.csv("../Data/surveys.csv", na.strings = "", stringsAsFactors = FALSE)
# 
# # input object to select the taxa with radio buttons or check boxes
# # use input to filter data and create a plot
# # plot how many total of that taxa in each year
# 
# bird_species <- filter(species, taxa == "Bird")$species_id #Bird is input$pick_taxa
# surveys_birds <- filter(surveys, species_id %in% bird_species)
# barplot(table(surveys_birds$year))
```

Exercise: add an input feature to choose males, females, or both hint: use either radio buttons or checkboxGroup input

Output objects
--------------

Output objects are created through the combination of pairs of `render*()` and `*Output()` functions. Define a list of output objects in the server file using render functions:

``` r
# output$my_plot <- renderPlot({})
```

Render functions build an object to display. The code inside the body of the render function will run whenever a reactive value inside the code changes.

Use the output ID to refer to that output element in the user interface file to place it in the app.

``` r
# ui.R
# fluidPage(
#   plotOutput("my_plot")
#   )
```

| render            | output               | description           |
|-------------------|----------------------|-----------------------|
| renderPlot()      | plotOutput()         | plots                 |
| renderPrint()     | verbatimTextOutput() | text                  |
| renderText()      | textOutput()         | text                  |
| renderTable()     | tableOutput()        | static table          |
| renderDataTable() | dataTableOutput()    | interactive table     |
| renderUI()        | uiOutput()           | reactive input object |

Note that you can change the size of plot outputs by defining the number of pixels

Reactive objects
----------------

Input objects that are used in multiple render functions to create different output objects can be created independently as **reactive** objects. This value is then cached to reduce computation required, since only the code to create this object is re-run when input values are updated. Use the function `reactive()` to create reactive objects and use them with function syntax, i.e. with `()`.

make the filtered data set a reactive object to use in the plot and in another place

Design layout
-------------

Page Layout or rows Panels, objects, or columns Elements

The user interface file or object is where the page layout is defined. One option for the main function is `fluidPage()` and it takes arguments that are layout functions. Organize elements within defined layouts such as `fluidRow()`, `flowLayout()`, `sidebarLayout()`, `splitLayout()`, or `verticalLayout()`.

Elements can be layered on top of each other using `tabsetPanel()`, `navlistPanel()`, or `navbarPage()`.

Input and output objects in the user interface file must be separated by commas.

change layout so there are 2 plots displayed together add a tab with the data in a data table

### Customize appearance

Add images by saving those files in a folder called **www**. Link to it with img(src="<file name>")

Use html wrapper functions to add headers and formatted text

Add text that is a title for the graph with the appropriate selected taxa in it Exercise: Below the graph, add text that says what year had the maximum number of that taxa recorded

Include markdown files

Upload or download files
------------------------

add a button to download a csv of the data or an image of the graph

Deploy your app
---------------

Shiny extensions
----------------

There are many ways to extend the functionality and sophistication of Shiny apps using existing tools and platforms.

Leaflet

Plot.ly

Additional references
---------------------
