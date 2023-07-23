
# **Customize Q&A and Fallback**

In addition to driving a conversation based on the main chat flow, an
AI chatbot must handle user questions or side-talking raised any time
during a chat. To enable a chatbot to do so, Juji allows the
customization of Q&A and fallback. Such customization enables Juji
chatbots to answer user free-text questions, handle user digressions, and
even chitchat socially, anytime during a conversation.

## Handle Free-Text Q&As

Using the `Q&A Board`, one can support custom, natural-language Q&As,
monitor, and manage unanswered user questions encountered during a
chat. Below is an example of a Q&A board:

<p align="center"><img src="https://juji.io/docs/img/design-qa.png" alt="Q&A dashboard"
width="650"/></p>

On this page, one can enter a custom Q&A pair directly in the table
(using the green **`+`** button to add) or upload a CSV file
containing a Q&A list. The above screenshot also shows that there is
one unanswered user question (indicated by the red badge displayed
next to the `Q&A Board`). Juji automatically detects unanswered user
questions and displays such questions on the Q&A dashboard.

### **Upload Q&As CSV**

<a name="qa-tips">**IMPORTANT TIP**</a> If you decide to put all your Q&As in a CSV file and then upload, download the CSV file first as it contains the required file format to fill in your Q&As.

As shown below, each template includes four columns:

<p align="center"><img src="https://juji.io/docs/img/qa-csv.png" alt="CSV file of Q&A" width="650"/></p>

First three columns must be preserved.  Although the first column (`ID`) can be left empty, it must still exist and cannot be deleted.
Besides, other optional columns can be used for additional functionality. All columns order must be reserved.

* **ID** You can use this column to give your Q&A pair a
    name/label. If you don't provide an ID, Juji will automatically
    generate one. This label is especially useful to group all varied
    question expressions into the **same question**. This way you
    don't need to duplicate the answer for each varied expression. For
    example, rows 2-3 and rows 5-6 represent two sets of
    Q&As. Moreover, they also share all the alternative answers (see
    below).

* **Question** Questions and their varied expressions. 

* **Answer** Answers. You can enter alternative answers to the same question. This will make your chatbot sound more intelligent. When there are alternative answers, a chatbot randomly chooses one to use when answering a matched question. 

* **Comment** (Optional) Comments.
* **Multi-turn Q&A** (Optional) Multi-turn Q&A key. The specified multi-turn Q&A will start when the Q&A is triggered if the Multi-turn status is `active`.
* **# of asking** (Reporting) Number of times the unanswered question get asked. Change in this column has no effect on the Q&A.
* **Tag(s)** (Optional) Tags for the Q&A.
* **Multi-turn status** (Optional) Status of the multi-turn Q&A, can be `inactive` or `active`.

It's important to make sure the CSV file is saved with `.csv` extension and `UTF-8` encoding for the best performance. The file format and encoding can be updated in `save as` or `export as` options in both `Microsoft Excel` and `Numbers`.


## Support Social Chitchat

In addition to answering user questions, you may want your chatbot to
support social chitchat, e.g., responding to user casual comments. Similar
to handling Q&As, you can enter user comments (e.g., `you are really
smart`) and corresponding chatbot responses (e.g., `Thank you, I'm
flattered`). During a chat, whenever users make matched comments, your
chatbot can then respond to them.

Below shows an example of custom social chitchat. Whenever a user
texts expressions similar to those indicated under ID `Humor`
(B8-B10), the chatbot will tell a joke by randomly picking one from
cells C8 and C9:

<p align="center"><img src="https://juji.io/docs/img/custom-fallback.png" alt="Select Custom Fallback" width="650"/></p>

**IMPORTANT TIP** Juji already provides rich, built-in social chitchats. We recommend that you observe the behavior of your chatbot first before adding any custom user comment-chatbot response pairs. 

## Additional Resources

Please refer to the additional resources listed below on how to support Q&A including complex Q&A that may require multi-turn interactions between a user and your chatbot. Since AI is far from perfect, also check out the reading on how to monitor unanswered user questions and how to improve your chatbot constantly. 

### **Video Tutorial**
Below is a very short video that shows how to create or update a Q&A
list:

<div align="center"> <iframe width="560" height="315"
src="https://www.youtube.com/embed/U0tR04xQTio" frameborder="0"
allow="accelerometer; autoplay; encrypted-media; gyroscope;
picture-in-picture" allowfullscreen></iframe> </div>

### **How-to Guides**

* [**A Step-by-Step Guide**](https://juji.io/blog/a-step-to-step-guide-to-customer-service-chatbots-with-nlp-no-coding-required/) to create an FAQ chatbot.
* [**A Guide to Define Multi-Turn QnA**](https://juji.io/blog/how-to-make-your-chatbot-to-answer-non-trivial-questions/)
* [**A Guide to Monitor and Handle Unknown User Questions**](https://juji.io/blog/q-a-dashboard/).

## What's Next

Once a chatbot is ready, you can deploy it onto a website or a
Facebook page. Please check out [**Chatbot Deployment**](../release)
to deploy your AI chatbot. If you wish to further customize your chatbot, such as its persona or other settings, please refer to [**Customize Chatbot Persona**](../customize-persona-beyond).


