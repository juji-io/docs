
# **Monitor AI Chatbot**

Once a chatbot is deployed, the `Reports` dashboard displays the chat
stats and the audience information.

## **Chat Stats**

This dashboard currently shows the number of users who chatted with
the chatbot. One can use the date slider below the chart to view the
number of users per selected time period.

<p align="center"><img src="/img/Report-Overview.png" alt="Chat Stats" width="650"/></p>

## **Audience Dashboard**

Juji reports audience information in real time in two sections. In
particular, the [audience overview](#audience-overview) section gives
an overview of audience information and key fields.  The [audience
analytics](#audience-analytics) section provides more detailed data
analytics based on conversation topics or attributes. You can also
[export audience data](#export-audience-data) to a CSV file for
additional analysis or third-party integration.

### **Audience Overview**

Audience overview is displayed in a table. The table is updated in
real time to show several pieces of basic information related to users,
such as `name`, `location`, and `channel`.

<p align="center"><img src="/img/Report-Audience.png" alt="Audience Overview" width="650"/></p>

<br>

### **Audience Analytics**

Juji automatically analyzes audience information, such as user answers
to specific chatbot questions or distribution of custom attribute
values. Such analytic results are organized and displayed by
chatbot questions or custom attribute.

Below is an example displaying the distribution of user choices by
percentile to the question `What's your favorite color`.

<p align="center"><img src="/img/audience-analytics-piechart.png"
alt="Audience Analytics" width="650"/></p>

<br> For an open-ended question, Juji summarizes the free-text user
answers to the question by auto-discovered *semantic themes* and
displays the discovered themes with the top-3 highest coverages. Below
is an example showing the themes discovered for the question `What
subject do you teach`:

<p align="center"><img src="/img/audience-analytics-text.png"
alt="Audience Analytics" width="650"/></p>

### **Export Audience Data**

In certain cases, you may wish to export the audience data for further
analysis or to another application, such as your in-house CRM
application. To do so, you can always export the data by downloading 
the CSV file.

As shown below, click on the `download CSV` button to download the
file.

<p align="center"><img src="/img/download-report.png" alt="Chat Stats" width="650"/></p>

## **Types of Audience Data**

An AI chatbot can actively listen to users and elicit in-depth
information and/or questions from the users. Not only does such an AI
chatbot capture incredibly rich and insightful information from a
conversation, but it can also automatically infer deeper insights
about users from such information. In general, Juji AI chatbots
capture several types of information from conversations. 

### Explicit User Input

This type of information includes **user responses** to chatbot
questions and **user questions** asked during a chat. Like a survey
platform, Juji *automatically* records user responses to every chatbot
question/request.  There are two types of user responses:
free-text input to open-ended questions and choice input to structured
questions.

As shown below, the first two columns record users' free-text input to
two open-ended questions, while the last two columns record user
choices to two choice questions (radio-button questions).

<p align="center"><img src="/img/user-input-example.png" alt="add a
topic buttons" width="650"/></p>

Moreover, users often ask questions during a chat. Juji also
automatically records such user-asked questions. Both user responses and
questions can be found in the CSV file (see how to [download a CSV
file](#export-audience-data)).

### Custom Attributes

In addition to recording user responses and user questions as is, Juji
allows chatbot creators to define custom attributes and record such
attributes as part of audience data.

Currently, Juji supports four types of custom attributes:

* **detected user sentiment** As described in [designing a chatbot](/design),
one can detect user sentiment by adding a custom chatbot action as
below and store the detected sentiment in a custom attribute.


<p align="center"><img src="/img/contain-sentiment-attr.png" alt="add a
topic buttons" width="450"/></p>


<p align="center"><img src="/img/sentiment-attr-1.png" alt="add a
topic buttons" width="450"/></p>

* **extracted keywords** On can define a `contain-keywords` condition
    and store one of the matched keywords into a custom
    attribute. Defining such custom attributes is useful since these
    attributes store extracted keywords instead of the *entire* user
    input to a chatbot question.

<p align="center"><img src="/img/keyword-attr.png" alt="add a
topic buttons" width="450"/></p>

<p align="center"><img src="/img/keyword-attr-1.png" alt="add a
topic buttons" width="450"/></p>


* **is-similar-to condition** One can define a `is-similar-to` condition and
    store the matched condition into a custom attribute -- a binary
    value (true/false) storing whether if the condition is met. 

<p align="center"><img src="/img/is-similar-to-attr.png" alt="add a
topic buttons" width="450"/></p>

<p align="center"><img src="/img/is-similar-to-attr-1.png" alt="add a
topic buttons" width="450"/></p>

* **matched variables** One can define a `matches` condition with a
    specific matched pattern and then store one or more matched
    variables into custom attributes.

<p align="center"><img src="/img/match-attr.png" alt="add a
topic buttons" width="450"/></p>

<p align="center"><img src="/img/match-attr-1.png" alt="add a
topic buttons" width="450"/></p>


### Inferred User Characteristics

In addition to storing [explicit user input](#explicit-user-input) and
[extracting semantic meanings](#custom-attributes) of such input, Juji
automatically infers user characteristics from user
input. Currently, Juji infers about 150 user characteristics, including
`Big 5 personality`, `reader DNA` and `gamer DNA`.


## **Uses of Audience Data**

Because AI chatbots produce rich audience information, which can be
used to serve the audience in a hyper-personalized manner. Below we
share several typical usages of such data.  

### Customer Segmentation

A business can use one or more types of audience information mentioned
above to create customer segments and serve different segments
accordingly. For example, custom attributes recording sentiment
information can help create two segments: satisfied and unsatisfied
customers. Similarly, custom attributes that record matched keywords
naturally divide customers into different segments, e.g., customers
who like `blueberries' and customers who prefer `strawberries`.

### Retargeting Marketing

Based on user explicit input or extracted custom attributes,
businesses can retarget one or more specific customer segment. Using
the above example, a farm that specilizes in growing blueberries can
engage only those who like blueberries. Similarly, a business may want
to follow up with unsatisfied customers to learn more about their
pain points and use such insights to improve products/services. 


### Hyper-Personalized Services

Audience information can also be used to provide hyper-personalized
services and deliver superior customer experience.

First, **explicit user input** can be used to find match products
and services. The short video below shows such a use case:

<div align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Uvvo6fm5GU8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

In addition to user explicit input, **inferred user characteristics** can
be used to offer hyper-personalized services even in the absence of
purchasing behavior. For example, book vendors may recommend edgy
sci-fi books to users with a reader DNA that indicates their
adventurousness and intellectual curiosity, while recommending
self-help books to those who are always eager to improve oneselves.


## **What's Next**

Based on your needs, you may want to create multiple chatbots, e.g.,
one for helping customers and the other for helping employees. You
need practice.  To make your chatbot making and management tasks more
productive, here are some [**design tips**](/chatbot-design-tips).

