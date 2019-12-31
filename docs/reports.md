
# **Monitor AI Chatbot**
Once a chatbot is deployed, the `Reports` dashboard displays the chat
stats and the audience information.

## **Chat Stats**
This dashboard currently shows the number of users who chatted with
the chatbot. One can use the date slider below the chart to view the
number of users per selected time period.

<p align="center"><img src="/img/Report-Overview.png" alt="Chat Stats" width="650"/></p>

## **Audience Dashboard**
Juji presents a real-time audience dashboard, which monitors and
displays audience information in two sections. In particular, the
[audience overview](#audience-overview) section gives an overview of
audience information and key fields.  The [audience
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
answers to the question by auto-discovered **semantic themes** and
displays the discovered themes with the top-3 highest coverages. Below
is an example showing the themes discovered for the question `What
subject do you teach`:

<p align="center"><img src="/img/audience-analytics-text.png"
alt="Audience Analytics" width="650"/></p>

### **Export Audience Data**

In many cases, you may wish to export the audience data for additional
uses, such as performing further analysis, incorporating into your
in-house CRM, or using them in retargeting email campaigns. To do so,
you can always export the data by downloading the corresponding CSV file.

As shown below, click on the `download CSV` button to download the
file.

<p align="center"><img src="/img/download-report.png" alt="download CSV" width="650"/></p>


## **Types of Audience Data**
An AI chatbot can actively listen to users and elicit in-depth
information and/or questions from the users. Not only does such an AI
chatbot capture incredibly rich and insightful information from a
conversation, but it can also automatically infer deeper insights
about users from such information.

As described below, Juji **automatically** captures and analyzes many
types of data during a chat. Not only does this capability eliminate
the burden of setting up and managing a database of your own, but it
also relieves you of manually recording such information, which
is often required by other chatbot platforms. The real-time, automatic
capturing and analysis of free-text user chat also provides you with
rich, instantaneous, and actionable audience insights (e.g.,
fine-grained customer segmentation and individual preferences).

Below is a sample CSV file containing various audience information
gathered from their chats with an AI chatbot.

<p align="center"><img src="/img/sample-csv.png" alt="Sample CSV"
width="650"/></p>

### Explicit User Input

As shown above, one type of audience information includes **user
responses** to chatbot questions and **user questions** asked during a
chat. Very similar to a survey platform, Juji *automatically* records
user responses to every chatbot question/request.  There are two types
of user responses: free-text input to open-ended questions and choice
input to structured questions.

As shown below, the first two columns record users' free-text input to
two open-ended questions, while the last two columns record user
choices to two choice questions (radio-button questions).

<p align="center"><img src="/img/user-input-example.png" alt="add a
topic buttons" width="650"/></p>

Moreover, users often ask questions during a chat. Juji also
automatically records such user-asked questions. Both user responses and
questions can be found in the CSV file (see how to [download a CSV
file](#export-audience-data)).

### System Attributes

Since Juji chatbots support natural, free-text chats, these chatbots
also automatically extract key information from user free-text input
and store the information into easy-to-use system attributes. 

As shown below, a chatbot asks `how heavy is your dog`. Associated
with this dialog, the chatbot will automatically parse users'
free-text input to the question and extract two pieces of information
that are stored in two attributes, `weight-amount` and `weight-unit`. 

<p align="center"><img src="/img/system-attribute-weight.png" alt="add a
topic buttons" width="650"/></p>

<p align="center"><img src="/img/system-attribute-weight-2.png" alt="add a
topic buttons" width="650"/></p>

The CSV report file will also capture these attributes automatically
(see below). Although you can [customize the names of system
attributes](/design#use-built-in-attributes), you cannot modify the
attribute types. System attributes can be used for [various
purposes](#uses-of-audience-data), such as personalized service
recommendations and retargeting marketing.


<p align="center"><img src="/img/system-attribute-weight-3.png" alt="add a
topic buttons" width="650"/></p>


### Custom Attributes

In addition to capturing and storing system attributes, you can define
custom attributes and record such attributes as part of audience
data. Currently, Juji supports **four types** of custom attributes:

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
`Big 5 personality` (see example below), `reader DNA` and `gamer DNA`.

<p align="center"><img src="/img/big5-example.png" alt="inferred user characteristics" width="650"/></p>


## **Uses of Audience Data**

Because AI chatbots produce rich audience information, which can be
used to serve the audience in a hyper-personalized manner. Below we
share several typical usages of such data.  

### Customer Segmentation

A business can use one or more types of audience information mentioned
above to create customer segments and serve different segments
accordingly. User direct input or extracted attributes often naturally
divide audience into different segments. The example below shows that
custom attribute `like-berries` divides the audience into two
segments: those who like berries and those who don't. The values
captured by the attribute further segment the audience into several
segments: people who prefer `strawberries` and those who enjoy
`blueberries`. Another custom attribute `prefer-protein" identifies
another customer segment: people who like proteins.

<p align="center"><img src="/img/segmentation.png" alt="customer segmentation" width="650"/></p> 


### Retargeting Marketing 

Based on user explicit input or extracted attributes, businesses can
retarget one or more specific customer segment. Using the above
example, a farm that specilizes in growing blueberries can engage only
those who like blueberries. Similarly, creating a custom attribute
that captures an audience's sentiment about a product, a business can
then follow up with unsatisfied customers to learn more about their
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

