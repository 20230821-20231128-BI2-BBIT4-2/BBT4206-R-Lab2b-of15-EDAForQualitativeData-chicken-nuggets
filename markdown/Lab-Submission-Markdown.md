Business Intelligence Lab 2b Submission Markdown
================
Chicken-nuggets
9/10/2023

- [Student Details](#student-details)
- [Setup Chunk](#setup-chunk)
- [\<Lab 2b - Visualization
  Explanations\>](#lab-2b---visualization-explanations)
  - [\<Most frequently used words in course Evaluation Likes for Male
    students\>](#most-frequently-used-words-in-course-evaluation-likes-for-male-students)
  - [\<Most Frequently Used Words in Course Evaluation Likes Per
    Gender\>](#most-frequently-used-words-in-course-evaluation-likes-per-gender)
  - [\<Most Frequently Used Words in Course Evaluation Likes for Group A
    Students\>](#most-frequently-used-words-in-course-evaluation-likes-for-group-a-students)
- [is rendered using knitR](#is-rendered-using-knitr)
  - [\<Most Frequently Used Words in Course Evaluation Likes for Group C
    Students\>](#most-frequently-used-words-in-course-evaluation-likes-for-group-c-students)
- [is rendered using knitR](#is-rendered-using-knitr-1)
  - [\<Most frequently used words in course Evaluation Wishes for Female
    students\>](#most-frequently-used-words-in-course-evaluation-wishes-for-female-students)
  - [\<Most frequently used words in course Evaluation Wishes for Male
    students\>](#most-frequently-used-words-in-course-evaluation-wishes-for-male-students)
  - [\<Most frequently used words in course Evaluation Wishes per
    Gender\>](#most-frequently-used-words-in-course-evaluation-wishes-per-gender)
  - [\<Most frequently used words in course Evaluation Wishes for Group
    B
    students\>](#most-frequently-used-words-in-course-evaluation-wishes-for-group-b-students)
- [is rendered using knitR](#is-rendered-using-knitr-2)
  - [\<Most frequently used words in course Evaluation Wishes per Class
    Group\>](#most-frequently-used-words-in-course-evaluation-wishes-per-class-group)
  - [\<Most Important words by TF-IDF Score in Course Evaluation Likes
    Per
    Gender\>](#most-important-words-by-tf-idf-score-in-course-evaluation-likes-per-gender)
  - [\<Most Important words by TF-IDF Score in Course Evaluation Likes
    Per Class
    Group\>](#most-important-words-by-tf-idf-score-in-course-evaluation-likes-per-class-group)
  - [\<Most Important words by TF-IDF Score in Course Evaluation Wishes
    Per
    Gender\>](#most-important-words-by-tf-idf-score-in-course-evaluation-wishes-per-gender)
  - [\<Most Important words by TF-IDF Score in Course Evaluation Likes
    Per Class
    Group\>](#most-important-words-by-tf-idf-score-in-course-evaluation-likes-per-class-group-1)

# Student Details

<table style="width:99%;">
<colgroup>
<col style="width: 32%" />
<col style="width: 63%" />
<col style="width: 3%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Student ID Numbers and Names of Group Members</strong></td>
<td><p><em>&lt;list one student name, group, and ID per line; you should
be between 2 and 5 members per group&gt;</em></p>
<ol type="1">
<li><p>137118 - C - Fatoumata Camara</p></li>
<li><p>127602 - C - Trevor Anjere</p></li>
<li><p>127039 - C - Ayan Ahmed</p></li>
<li><p>136869 - C - Birkanwhal Bhambra</p></li>
<li><p>133824 - C - Habiba Siba</p></li>
</ol></td>
<td></td>
</tr>
<tr class="even">
<td><strong>GitHub Classroom Group Name</strong></td>
<td colspan="2">Chicken-Nuggets</td>
</tr>
<tr class="odd">
<td><strong>Course Code</strong></td>
<td>BBT4206</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Course Name</strong></td>
<td>Business Intelligence II</td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Program</strong></td>
<td>Bachelor of Business Information Technology</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Semester Duration</strong></td>
<td>21<sup>st</sup> August 2023 to 28<sup>th</sup> November 2023</td>
<td></td>
</tr>
</tbody>
</table>

# Setup Chunk

**Note:** the following “*KnitR*” options have been set as the
defaults:  
`knitr::opts_chunk$set(echo = TRUE, warning = FALSE, eval = TRUE, collapse = FALSE, tidy.opts = list(width.cutoff = 80), tidy = TRUE)`.

More KnitR options are documented here
<https://bookdown.org/yihui/rmarkdown-cookbook/chunk-options.html> and
here <https://yihui.org/knitr/options/>.

**Note:** the following “*R Markdown*” options have been set as the
defaults:

> output:  
>   
> github_document:  
> toc: yes  
> toc_depth: 4  
> fig_width: 6  
> fig_height: 4  
> df_print: default  
>   
> editor_options:  
> chunk_output_type: console

# \<Lab 2b - Visualization Explanations\>

\#\<Course Evaluation rating per group and per Gender\>

`` {1. Course Evaluation rating per group and per gender}  # The code creates a bar plot using the ggplot2 package to visualize course evaluation ratings per group and per Gender evaluation_per_group_per_gender %>%   ggplot() + #pipes the data frame into the ggplot() function and initializes a new visualization   geom_bar(aes(x = class_group, y = average_evaluation_rating,                fill = `Student's Gender`),# Adds bars and specifies the x-axis and y-axis and the colors of different bars based on gender            stat = "identity", position = "dodge") + #values should be used as is and the bars should be placed side by side for each class group.   expand_limits(y = 0) + #sets the lower limit of the y-axis as 0   blue_grey_theme() + #applies custom theme to the plot   scale_fill_manual(values = blue_grey_colours_2) +   ggtitle("Course Evaluation Rating per Group and per Gender") + #sets the title of the plot   labs(x = "Class Group", y = "Average Rating") #sets labels for the x and y axes # is rendered using knitR library(readr) ``

\##\<Most frequently used words in course Evaluation Likes for Female
students\>

`` {2.Most frequently used words in course Evaluation Likes for Female students} # Creates a horizontal bar plot for the data  evaluation_likes_filtered %>% #pipes the data frame into a series of operations   select(`Class Group`, `Student's Gender`,          `Average Course Evaluation Rating`, `Likes (tokenized)`) %>% #selects four columns from the data frame   filter(`Student's Gender` == "Female") %>% #Filters the data to include rows where the gender is female   count(`Likes (tokenized)`, sort = TRUE) %>% #Counts the frequency of each value and sorts in descending order   top_n(9) %>% #Selects the top 9 words from the count above   mutate(`Likes (tokenized)` = reorder(`Likes (tokenized)`, n)) %>% #reorders te Likes(tokenized) column based on the frequency count   ggplot() + #Initializes a new plot   geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds bars to the plot and specifies the x and y axes  and the colors the bars should be filled in   blue_grey_theme() + #Applies a custom theme to the plot   xlab("Word in Course Evaluation") + #Sets the labels for the x axis   ylab("Number of Times Used (Term Frequency)") + #Sets the labels for the x axis   ggtitle("Most Frequently Used Words in Course Evaluation Likes for Female           Students") + # sets the title   coord_flip() #Flips the coordinates to make it a horizontal plot # file is rendered using knitR library(readr) ``

## \<Most frequently used words in course Evaluation Likes for Male students\>

`` {3.Most frequently used words in course Evaluation Likes for Male students} # Creates a horizontal bar plot for the data  evaluation_likes_filtered %>% #pipes the data frame into a series of operations   select(`Class Group`, `Student's Gender`,          `Average Course Evaluation Rating`, `Likes (tokenized)`) %>% #selects four columns from the data frame   filter(`Student's Gender` == "Male") %>% #Filters the data to include rows where the gender is Male   count(`Likes (tokenized)`, sort = TRUE) %>% #Counts the frequency of each value and sorts in descending order   top_n(9) %>% #Selects the top 9 words from the count above   mutate(`Likes (tokenized)` = reorder(`Likes (tokenized)`, n)) %>% #reorders the Likes(tokenized) column based on the frequency count   ggplot() + #Initializes a new plot   geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds bars to the plot and specifies the x and y axes  and the colors the bars should be filled in   blue_grey_theme() + #Applies a custom theme to the plot   xlab("Word in Course Evaluation") + #Sets the labels for the x axis   ylab("Number of Times Used (Term Frequency)") + #Sets the labels for the x axis   ggtitle("Most Frequently Used Words in Course Evaluation Likes for Male           Students") + # sets the title   coord_flip() #Flips the coordinates to make it a horizontal plot # file is rendered using knitR library(readr) ``

## \<Most Frequently Used Words in Course Evaluation Likes Per Gender\>

`` {4. Most Frequently Used Words in Course Evaluation Likes Per Gender} # Creates a grouped bar plot for both genders popular_words %>% #Pipes data frame   ggplot(aes(row, n, fill = `Student's Gender`)) + #Initializes a plot and specifies the x and y axes and creates grouped bars for each word and differentiates by gender   geom_col(fill = blue_grey_colours_1) + #Adds bars and specifies the colors   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation",        y = "Number of Times Used (Term Frequency)") + #Sets the label for both axes   ggtitle("Most Frequently Used Words in Course Evaluation Likes per Gender") + #Sets the plots title   facet_wrap(~`Student's Gender`, scales = "free") + #Groups the plot into separate plots for each gender   scale_x_continuous(                      breaks = popular_words$row,                      labels = popular_words$`Likes (tokenized)`) + #Specifies the breaks and labels for the x axis   coord_flip() #Flips the coordinates to make it a horizontal bar  # is rendered using knitR library(readr) ``

## \<Most Frequently Used Words in Course Evaluation Likes for Group A Students\>

\`\``{5.Most Frequently Used Words in Course Evaluation Likes for Group A Students} # Fill this with R related code that will be executed when the R markdown file evaluation_likes_filtered %>% #Pipes data into data frame   select(`Class
Group`,`Student’s Gender`,`Average Course Evaluation Rating`,`Likes
(tokenized)`) %>% # Selects 4 columns from the data frame   filter(`Class
Group`== "A") %>% # Filter data to only include rows where Class Group is A   count(`Likes
(tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order   top_n(9) %>% #selects top 9 most frequently used words based on count   mutate(`Likes
(tokenized)`= reorder(`Likes
(tokenized)`, n)) %>% #reorders column based on frequency count   ggplot() + #Initializes new plot   geom_col(aes(`Likes
(tokenized)\`, n), fill = blue_grey_colours_1) + \#Adds a bar, specifies
what the x and y axes should represent and the colors the bars should be
filled in blue_grey_theme() + \#Applies a custom theme to the plot
xlab(“Word in Course Evaluation”) + \#sets label for X axis ylab(“Number
of Times Used (Term Frequency)”) + \#sets label for the y axis
ggtitle(“Most Frequently Used Words in Course Evaluation Likes for Group
A Students”) + \#sets the title of the plot coord_flip() \#Flips the
coordinate to make a horizontal bar plot

# is rendered using knitR

library(readr)


    ## \<Most Frequently Used Words in Course Evaluation Likes for Group B Students\>

    ```{6.Most Frequently Used Words in Course Evaluation Likes for Group B Students}
    # Fill this with R related code that will be executed when the R markdown file
    evaluation_likes_filtered %>% #Pipes data into data frame
      select(`Class Group`, `Student's Gender`,
             `Average Course Evaluation Rating`, `Likes (tokenized)`) %>% # Selects 4 columns from the data frame
      filter(`Class Group` == "B") %>% # Filter data to only include rows where Class Group is B
      count(`Likes (tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order
      top_n(9) %>% #selects top 9 most frequently used words based on count
      mutate(`Likes (tokenized)` = reorder(`Likes (tokenized)`, n)) %>% #reorders column based on frequency count
      ggplot() + #Initializes new plot
      geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds a bar, specifies what the x and y axes should represent and the colors the bars should be filled in
      blue_grey_theme() + #Applies a custom theme to the plot
      xlab("Word in Course Evaluation") + #sets label for X axis
      ylab("Number of Times Used (Term Frequency)") + #sets label for the y axis
      ggtitle("Most Frequently Used Words in Course Evaluation Likes for Group B
              Students") + #sets the title of the plot
      coord_flip() #Flips the coordinate to make a  horizontal bar plot

    # is rendered using knitR
    library(readr)

## \<Most Frequently Used Words in Course Evaluation Likes for Group C Students\>

\`\``{7.Most Frequently Used Words in Course Evaluation Likes for Group C Students} # Fill this with R related code that will be executed when the R markdown file evaluation_likes_filtered %>% #Pipes data into data frame   select(`Class
Group`,`Student’s Gender`,`Average Course Evaluation Rating`,`Likes
(tokenized)`) %>% # Selects 4 columns from the data frame   filter(`Class
Group`== "C") %>% # Filter data to only include rows where Class Group is C   count(`Likes
(tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order   top_n(9) %>% #selects top 9 most frequently used words based on count   mutate(`Likes
(tokenized)`= reorder(`Likes
(tokenized)`, n)) %>% #reorders column based on frequency count   ggplot() + #Initializes new plot   geom_col(aes(`Likes
(tokenized)\`, n), fill = blue_grey_colours_1) + \#Adds a bar, specifies
what the x and y axes should represent and the colors the bars should be
filled in blue_grey_theme() + \#Applies a custom theme to the plot
xlab(“Word in Course Evaluation”) + \#sets label for X axis ylab(“Number
of Times Used (Term Frequency)”) + \#sets label for the y axis
ggtitle(“Most Frequently Used Words in Course Evaluation Likes for Group
C Students”) + \#sets the title of the plot coord_flip() \#Flips the
coordinate to make a horizontal bar plot

# is rendered using knitR

library(readr)


    ## \<Most Frequently used words inCourse Evaluation Likes per class Group\>

    ```{8. Most Frequently used words inCourse Evaluation Likes per class Group}
    # Fill this with R related code that will be executed when the R markdown file
    popular_words %>% #Pipes data frame
      ggplot(aes(row, n, fill = `Class Group`)) + #Initializes a plot and specifies the x and y axes and creates grouped bars for each word and differentiates by gender
      geom_col(fill = blue_grey_colours_1) + #Adds bars and specifies the colors
      blue_grey_theme() + #Applies a custom theme to the plot
      labs(x = "Word in Course Evaluation",
           y = "Number of Times Used (Term Frequency)") + #Sets the label for both axes
      ggtitle("Most Frequently Used Words in Course Evaluation Likes per Class Group") + #Sets the plot's title
      facet_wrap(~`Class Group`, scales = "free") + #Groups the plot into separate plots for each gender
      scale_x_continuous(
                         breaks = popular_words$row,
                         labels = popular_words$`Likes (tokenized)`) + #Specifies the breaks and labels for the x axis
      coord_flip() #Flips the coordinates to make it a horizontal bar 
    # is rendered using knitR
    library(readr)

## \<Most frequently used words in course Evaluation Wishes for Female students\>

`` {9.Most frequently used words in course Evaluation Wishes for Female students} # Fill this with R related code that will be executed when the R markdown file # Creates a horizontal bar plot for the data  evaluation_likes_filtered %>% #pipes the data frame into a series of operations   select(`Class Group`, `Student's Gender`,          `Average Course Evaluation Rating`, `Likes (tokenized)`) %>% #selects four columns from the data frame   filter(`Student's Gender` == "Female") %>% #Filters the data to include rows where the gender is female   count(`Wishes (tokenized)`, sort = TRUE) %>% #Counts the frequency of each value and sorts in descending order   top_n(9) %>% #Selects the top 9 words from the count above   mutate(`Wishes (tokenized)` = reorder(`Likes (tokenized)`, n)) %>% #reorders the Wishes(tokenized) column based on the frequency count   ggplot() + #Initializes a new plot   geom_col(aes(`Wishes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds bars to the plot and specifies the x and y axes  and the colors the bars should be filled in   blue_grey_theme() + #Applies a custom theme to the plot   xlab("Word in Course Evaluation") + #Sets the labels for the x axis   ylab("Number of Times Used (Term Frequency)") + #Sets the labels for the x axis   ggtitle("Most Frequently Used Words in Course Evaluation Wishes for Female           Students") + # sets the title   coord_flip() #Flips the coordinates to make it a horizontal plot # file is rendered using knitR # is rendered using knitR library(readr) ``

## \<Most frequently used words in course Evaluation Wishes for Male students\>

`` {10.Most frequently used words in course Evaluation Wishes for Male students} # Fill this with R related code that will be executed when the R markdown file # Creates a horizontal bar plot for the data  evaluation_likes_filtered %>% #pipes the data frame into a series of operations   select(`Class Group`, `Student's Gender`,          `Average Course Evaluation Rating`, `Likes (tokenized)`) %>% #selects four columns from the data frame   filter(`Student's Gender` == "Male") %>% #Filters the data to include rows where the gender is Male   count(`Wishes (tokenized)`, sort = TRUE) %>% #Counts the frequency of each value and sorts in descending order   top_n(9) %>% #Selects the top 9 words from the count above   mutate(`Wishes (tokenized)` = reorder(`Wishes (tokenized)`, n)) %>% #reorders the Wishes(tokenized) column based on the frequency count   ggplot() + #Initializes a new plot   geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds bars to the plot and specifies the x and y axes  and the colors the bars should be filled in   blue_grey_theme() + #Applies a custom theme to the plot   xlab("Word in Course Evaluation") + #Sets the labels for the x axis   ylab("Number of Times Used (Term Frequency)") + #Sets the labels for the x axis   ggtitle("Most Frequently Used Words in Course Evaluation Wishes for Male           Students") + # sets the title   coord_flip() #Flips the coordinates to make it a horizontal plot # file is rendered using knitR # is rendered using knitR library(readr) ``

## \<Most frequently used words in course Evaluation Wishes per Gender\>

\`\``{11.Most frequently used words in course Evaluation Wishes per Gender} # Fill this with R related code that will be executed when the R markdown file # Creates a grouped bar plot for both genders popular_words <- evaluation_wishes_filtered %>%   group_by(`Student’s
Gender`) %>%   count(`Wishes (tokenized)`,`Student’s
Gender`, sort = TRUE) %>%   slice(seq_len(10)) %>%   ungroup() %>%   arrange(`Student’s
Gender\`, n) %\>% mutate(row = row_number())

popular_words %\>% \#Pipes data frame ggplot(aes(row, n, fill =
`Student's Gender`)) + \#Initializes a plot and specifies the x and y
axes and creates grouped bars for each word and differentiates by gender
geom_col(fill = blue_grey_colours_1) + \#Adds bars and specifies the
colors blue_grey_theme() + \#Applies a custom theme to the plot labs(x =
“Word in Course Evaluation”, y = “Number of Times Used (Term
Frequency)”) + \#Sets the label for both axes ggtitle(“Most Frequently
Used Words in Course Evaluation Wishes per Gender”) + \#Sets the plots
title facet_wrap(~`Student's Gender`, scales = “free”) + \#Groups the
plot into separate plots for each gender scale_x_continuous( breaks =
popular_words$row,  labels = popular_words$`Wishes (tokenized)`) +
\#Specifies the breaks and labels for the x axis coord_flip() \#Flips
the coordinates to make it a horizontal bar \# is rendered using knitR
library(readr)


    ## \<Most frequently used words in course Evaluation Wishes for Group A students\>

    ```{12.Most frequently used words in course Evaluation Wishes for Group A students}
    # Fill this with R related code that will be executed when the R markdown file
    evaluation_likes_filtered %>% #Pipes data into data frame
      select(`Class Group`, `Student's Gender`,
             `Average Course Evaluation Rating`, `Wishes (tokenized)`) %>% # Selects 4 columns from the data frame
      filter(`Class Group` == "A") %>% # Filter data to only include rows where Class Group is A
      count(`Wishes (tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order
      top_n(9) %>% #selects top 9 most frequently used words based on count
      mutate(`Wishes (tokenized)` = reorder(`Wishes (tokenized)`, n)) %>% #reorders column based on frequency count
      ggplot() + #Initializes new plot
      geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds a bar, specifies what the x and y axes should represent and the colors the bars should be filled in
      blue_grey_theme() + #Applies a custom theme to the plot
      xlab("Word in Course Evaluation") + #sets label for X axis
      ylab("Number of Times Used (Term Frequency)") + #sets label for the y axis
      ggtitle("Most Frequently Used Words in Course Evaluation Wishes for Group A
              Students") + #sets the title of the plot
      coord_flip() #Flips the coordinate to make a  horizontal bar plot

    # is rendered using knitR
    library(readr)

## \<Most frequently used words in course Evaluation Wishes for Group B students\>

\`\``{13.Most frequently used words in course Evaluation Wishes for Group B students} # Fill this with R related code that will be executed when the R markdown file evaluation_likes_filtered %>% #Pipes data into data frame   select(`Class
Group`,`Student’s Gender`,`Average Course Evaluation Rating`,`Wishes
(tokenized)`) %>% # Selects 4 columns from the data frame   filter(`Class
Group`== "B") %>% # Filter data to only include rows where Class Group is B   count(`Wishes
(tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order   top_n(9) %>% #selects top 9 most frequently used words based on count   mutate(`Wishes
(tokenized)`= reorder(`Wishes
(tokenized)`, n)) %>% #reorders column based on frequency count   ggplot() + #Initializes new plot   geom_col(aes(`Likes
(tokenized)\`, n), fill = blue_grey_colours_1) + \#Adds a bar, specifies
what the x and y axes should represent and the colors the bars should be
filled in blue_grey_theme() + \#Applies a custom theme to the plot
xlab(“Word in Course Evaluation”) + \#sets label for X axis ylab(“Number
of Times Used (Term Frequency)”) + \#sets label for the y axis
ggtitle(“Most Frequently Used Words in Course Evaluation Wishes for
Group B Students”) + \#sets the title of the plot coord_flip() \#Flips
the coordinate to make a horizontal bar plot

# is rendered using knitR

library(readr)


    ## \<Most frequently used words in course Evaluation Wishes for Group C students\>

    ```{14.Most frequently used words in course Evaluation Wishes for Group C students}
    # Fill this with R related code that will be executed when the R markdown file
    evaluation_likes_filtered %>% #Pipes data into data frame
      select(`Class Group`, `Student's Gender`,
             `Average Course Evaluation Rating`, `Wishes (tokenized)`) %>% # Selects 4 columns from the data frame
      filter(`Class Group` == "C") %>% # Filter data to only include rows where Class Group is C
      count(`Wishes (tokenized)`, sort = TRUE) %>% # Counts frequency of each unique value in the Likes(tokenized) column and sorts in descending order
      top_n(9) %>% #selects top 9 most frequently used words based on count
      mutate(`Wishes (tokenized)` = reorder(`Wishes (tokenized)`, n)) %>% #reorders column based on frequency count
      ggplot() + #Initializes new plot
      geom_col(aes(`Likes (tokenized)`, n), fill = blue_grey_colours_1) + #Adds a bar, specifies what the x and y axes should represent and the colors the bars should be filled in
      blue_grey_theme() + #Applies a custom theme to the plot
      xlab("Word in Course Evaluation") + #sets label for X axis
      ylab("Number of Times Used (Term Frequency)") + #sets label for the y axis
      ggtitle("Most Frequently Used Words in Course Evaluation Wishes for Group C
              Students") + #sets the title of the plot
      coord_flip() #Flips the coordinate to make a  horizontal bar plot

    # is rendered using knitR
    library(readr)

## \<Most frequently used words in course Evaluation Wishes per Class Group\>

`` {15.Most frequently used words in course Evaluation Wishes per Class Group} # Fill this with R related code that will be executed when the R markdown file popular_words %>% #Pipes data frame   ggplot(aes(row, n, fill = `Class Group`)) + #Initializes a plot and specifies the x and y axes and creates grouped bars for each word and differentiates by gender   geom_col(fill = blue_grey_colours_1) + #Adds bars and specifies the colors   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation",        y = "Number of Times Used (Term Frequency)") + #Sets the label for both axes   ggtitle("Most Frequently Used Words in Course Evaluation Wishes per Gender") + #Sets the plots title   facet_wrap(~`Class Group`, scales = "free") + #Groups the plot into separate plots for each gender   scale_x_continuous(                      breaks = popular_words$row,                      labels = popular_words$`Wishes (tokenized)`) + #Specifies the breaks and labels for the x axis   coord_flip() #Flips the coordinates to make it a horizontal bar  # is rendered using knitR library(readr) ``

## \<Most Important words by TF-IDF Score in Course Evaluation Likes Per Gender\>

`` {16. Most Important words by TF-IDF Score in Course Evaluation Likes Per Gender} # Fill this with R related code that will be executed when the R markdown file top_popular_tfidf_words %>% #Pipes data into data frame   ggplot(aes(x = row, tf_idf, fill = `Student's Gender`)) + #Initializes a plot object, fills color, creates grouped bars for each word and differentiates them by gender   geom_col(fill = blue_grey_colours_1) + #Adds a bar to the plot and specifies the color.   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation", y = "TF-IDF Score") + #Sets the label for X and Y axes    ggtitle("Most Important Words by TF-IDF Score in Course Evaluation Likes per        Gender") + #Sets the title for the plot   facet_wrap(~`Student's Gender`, scales = "free") + #Groups the plot into separate for the genders    scale_x_continuous(                      breaks = top_popular_tfidf_words$row,                      labels = top_popular_tfidf_words$`Likes (tokenized)`) + # specifies the breaks and labels for the breaks and labels   coord_flip() #Flips the coordinates to make the plot horizontal # is rendered using knitR library(readr) ``

## \<Most Important words by TF-IDF Score in Course Evaluation Likes Per Class Group\>

`` {17. Most Important words by TF-IDF Score in Course Evaluation Likes Per Class Group} # Fill this with R related code that will be executed when the R markdown file top_popular_tfidf_words %>% #Pipes data into data frame   ggplot(aes(x = row, tf_idf, fill = `Class Group`)) + #Initializes a plot object, fills color, creates grouped bars for each word and differentiates them by Class Group   geom_col(fill = blue_grey_colours_1) + #Adds a bar to the plot and specifies the color.   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation", y = "TF-IDF Score") + #Sets the label for X and Y axes    ggtitle("Most Important Words by TF-IDF Score in Course Evaluation Likes per        Gender") + #Sets the title for the plot   facet_wrap(~`Class Group`, scales = "free") + #Groups the plot into separate for the genders    scale_x_continuous(                      breaks = top_popular_tfidf_words$row,                      labels = top_popular_tfidf_words$`Likes (tokenized)`) + # specifies the breaks and labels for the breaks and labels   coord_flip() #Flips the coordinates to make the plot horizontal # is rendered using knitR library(readr) ``

## \<Most Important words by TF-IDF Score in Course Evaluation Wishes Per Gender\>

`` {18. Most Important words by TF-IDF Score in Course Evaluation Wishes Per Gender} # Fill this with R related code that will be executed when the R markdown file top_popular_tfidf_words %>% #Pipes data into data frame   ggplot(aes(x = row, tf_idf, fill = `Student's Gender`)) + #Initializes a plot object, fills color, creates grouped bars for each word and differentiates them by gender   geom_col(fill = blue_grey_colours_1) + #Adds a bar to the plot and specifies the color.   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation", y = "TF-IDF Score") + #Sets the label for X and Y axes    ggtitle("Most Important Words by TF-IDF Score in Course Evaluation wishes per        Gender") + #Sets the title for the plot   facet_wrap(~`Student's Gender`, scales = "free") + #Groups the plot into separate for the genders    scale_x_continuous(                      breaks = top_popular_tfidf_words$row,                      labels = top_popular_tfidf_words$`Wishes (tokenized)`) + # specifies the breaks and labels for the breaks and labels   coord_flip() #Flips the coordinates to make the plot horizontal # is rendered using knitR library(readr) ``

## \<Most Important words by TF-IDF Score in Course Evaluation Likes Per Class Group\>

`` {19. Most Important words by TF-IDF Score in Course Evaluation Likes Per Class Group} # Fill this with R related code that will be executed when the R markdown file top_popular_tfidf_words %>% #Pipes data into data frame   ggplot(aes(x = row, tf_idf, fill = `Class Group`)) + #Initializes a plot object, fills color, creates grouped bars for each word and differentiates them by Class Group   geom_col(fill = blue_grey_colours_1) + #Adds a bar to the plot and specifies the color.   blue_grey_theme() + #Applies a custom theme to the plot   labs(x = "Word in Course Evaluation", y = "TF-IDF Score") + #Sets the label for X and Y axes    ggtitle("Most Important Words by TF-IDF Score in Course Evaluation wishes per        Gender") + #Sets the title for the plot   facet_wrap(~`Class Group`, scales = "free") + #Groups the plot into separate for the genders    scale_x_continuous(                      breaks = top_popular_tfidf_words$row,                      labels = top_popular_tfidf_words$`Wishes (tokenized)`) + # specifies the breaks and labels for the breaks and labels   coord_flip() #Flips the coordinates to make the plot horizontal # is rendered using knitR library(readr) ``
