# MA \[46\]15 Homework 4
**`[==[`** Your Name **`]==]`**

## Question 1

**`[==[`** Download the
[`hw4_cahmi_data.zip`](https://math.bu.edu/people/sussman/data/hw4_cahmi_data.zip)
file and save or copy it to this directory and unzip it. (Make sure it
is in a subdirectory named `data`. If you put it is in a different
subdirectory you might accidentally commit it.) Now modify the `q1`
chunk below to create a new dataset called `cahc_df`. Check that there
are no errors when importing data.

Check variables `age`, `fam_pov_lev`, `sex`, and `birth_weight_oz` for
unusual values or unusually frequent values. (There is no “right” way to
do this but provide some output showing that these are or are not
present.) Quickly comment on anything unusual. **`]==]`**

My work is to perform a preliminary analysis of the Childhood and
Adolescent Health conditions data downloaded from . This data set is
derived from data that was collected in 2016 as part of the National
Survey of Children’s Health hosted by the [Data Resource Center for
Child and Adolescent
Health](https://www.childhealthdata.org/browse/archive-prior-year-nsch-and-ns-cshcn-data-resources/state-snapshot).
I read the file into a data set call `cahc_df`.

``` r
suppressPackageStartupMessages(library(tidyverse))
```

## Question 2

**`[==[`** Whether we view this data as being “tidy” depends on what we
think of as an observation. In order to ease the analysis across
different health conditions, we want to view an observation as a
distinct pair of child and potential health condition. Use
`pivot_longer` on all columns corresponding to one of the health
conditions. Specify the `cols` and then also use the parameters
`names_pattern = "(.*)_(.*)$", names_to = c(".value", "condition")`.
(This is a slightly advanced use of `pivot_longer`. Look at the help for
`pivot_longer` to better understand this.) After you `pivot_longer` you
should have 11 columns. Save this to a new variable called `cahc_long`.

Verify by outputting empty tibbles that

- `currently_has` is not `NA` only if `ever_had` is `"Yes"` and
- `severity` is not `NA` only if `currently_has` is `"Yes"`. **`]==]`**

## Question 3

**`[==[`** Using the `cahc_long` data set, first count the number of
conditions that each child currently has (which could be 0). Then for
each potential number of conditions, count how many children of each sex
have that many conditions. Make a bar chart showing the results. The
number of conditions will be on the x-axis and the number of children
will be on the y-axis with the fill indicating the sex. Comment on any
differences you see between the two sexes. **`]==]`**

## Question 4

**`[==[`** Again using the `cahc_long` data set, we’re going going to
create a table showing the proportion of children from different race
categories who have different health conditions. First, lump together
any of the race categories with fewer than 5% of the total sample into
an “Other” category. Next, compute the proportion of children for each
(remaining) race category that have each health condition. Finally, use
`pivot_wider` to create a table with rows corresponding to the health
conditions and columns corresponding to the different race categories
with the entries of the table giving the proportions. (The resulting
table will have dimensions 15x6.)

Comment on any major differences you observe between the different race
categories. **`]==]`**

``` r
tibble(condition = letters[1:4], Purple = runif(4)) |>
  gt::gt() |> 
  gt::fmt_percent(-condition) |> 
  gt::as_raw_html()
```

<div id="xnvjatdyox" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
  &#10;  <table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false" style="-webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'; display: table; border-collapse: collapse; line-height: normal; margin-left: auto; margin-right: auto; color: #333333; font-size: 16px; font-weight: normal; font-style: normal; background-color: #FFFFFF; width: auto; border-top-style: solid; border-top-width: 2px; border-top-color: #A8A8A8; border-right-style: none; border-right-width: 2px; border-right-color: #D3D3D3; border-bottom-style: solid; border-bottom-width: 2px; border-bottom-color: #A8A8A8; border-left-style: none; border-left-width: 2px; border-left-color: #D3D3D3;" bgcolor="#FFFFFF">
  <thead style="border-style: none;">
    &#10;    <tr class="gt_col_headings" style="border-style: none; border-top-style: solid; border-top-width: 2px; border-top-color: #D3D3D3; border-bottom-style: solid; border-bottom-width: 2px; border-bottom-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3;">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="condition" style="border-style: none; color: #333333; background-color: #FFFFFF; font-size: 100%; font-weight: normal; text-transform: inherit; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: bottom; padding-top: 5px; padding-bottom: 6px; padding-left: 5px; padding-right: 5px; overflow-x: hidden; text-align: left;" bgcolor="#FFFFFF" valign="bottom" align="left">condition</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Purple" style="border-style: none; color: #333333; background-color: #FFFFFF; font-size: 100%; font-weight: normal; text-transform: inherit; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: bottom; padding-top: 5px; padding-bottom: 6px; padding-left: 5px; padding-right: 5px; overflow-x: hidden; text-align: right; font-variant-numeric: tabular-nums;" bgcolor="#FFFFFF" valign="bottom" align="right">Purple</th>
    </tr>
  </thead>
  <tbody class="gt_table_body" style="border-style: none; border-top-style: solid; border-top-width: 2px; border-top-color: #D3D3D3; border-bottom-style: solid; border-bottom-width: 2px; border-bottom-color: #D3D3D3;">
    <tr style="border-style: none;"><td headers="condition" class="gt_row gt_left" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: left;" valign="middle" align="left">a</td>
<td headers="Purple" class="gt_row gt_right" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: right; font-variant-numeric: tabular-nums;" valign="middle" align="right">61.75%</td></tr>
    <tr style="border-style: none;"><td headers="condition" class="gt_row gt_left" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: left;" valign="middle" align="left">b</td>
<td headers="Purple" class="gt_row gt_right" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: right; font-variant-numeric: tabular-nums;" valign="middle" align="right">69.57%</td></tr>
    <tr style="border-style: none;"><td headers="condition" class="gt_row gt_left" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: left;" valign="middle" align="left">c</td>
<td headers="Purple" class="gt_row gt_right" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: right; font-variant-numeric: tabular-nums;" valign="middle" align="right">7.32%</td></tr>
    <tr style="border-style: none;"><td headers="condition" class="gt_row gt_left" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: left;" valign="middle" align="left">d</td>
<td headers="Purple" class="gt_row gt_right" style="border-style: none; padding-top: 8px; padding-bottom: 8px; padding-left: 5px; padding-right: 5px; margin: 10px; border-top-style: solid; border-top-width: 1px; border-top-color: #D3D3D3; border-left-style: none; border-left-width: 1px; border-left-color: #D3D3D3; border-right-style: none; border-right-width: 1px; border-right-color: #D3D3D3; vertical-align: middle; overflow-x: hidden; text-align: right; font-variant-numeric: tabular-nums;" valign="middle" align="right">87.66%</td></tr>
  </tbody>
  &#10;  
</table>
</div>
