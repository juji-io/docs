# **Making AI Chatbots: <br> Best Practices (Advanced)**

Here are more design tips if you want to leverage the [Juji
Platform](/index) to achieve more.

## **Give Sensible Labels**

The label of a free-text request is a very important piece of
information. It is used for multiple purposes. As
described below, it is used to

* summarize a chat topic (i.e., displayed on the topic card
in the left panel)

* search for built-in Juji dialog

* translate user inquiries in context

* index user answers in an audience report.

### **Search for Built-in Juji Dialog**

A request label is always used to find a matched Juji built-in dialog
to handle conversations around the request. For example, Juji has a
built-in dialog that handles diverse user responses to the request
`What are your hobbies`. To find such a built-in dialog, Juji uses the
label entered with the request. Giving a sensible lable can
better help Juji find the right built-in conversation, which can then
handle diverse user responses on that topic with **no or little**
customization required.

In particular, we suggest that you give short, concise labels to
distill chatbot requests, which facilitates the finding of matched 
built-in dialogs. For example, if your chatbot is intended to ask a
user about his/her opinion about an event, it might give a long
description of the event before posing the question. In such a case,
put the long and full description in the request, but keep the
request label short and concise as shown in the example below:

<p align="center"><img src="../img/good-label.png" alt="A sensible label" width="650"/></p>

Here is another example showing that the request wording is long while
the label is kept short and to the point:

<p align="center"><img src="/img/good-label-2.png" alt="A sensible
label 2" width="550"/></p>

In case you don't think the label you entered retrieves a suitable
built-in dialog, you can always browse Juji dialog library to [search
for a more suitable built-in dialog](/design#built-in-dialog).

### **Handle Context-Sensitive User Inquiries**

In a conversation, a user may pose a context-sensitive inquiry. For
example, a chatbot asks `Everyone loves movies. What's your favorite
movie?`. A user may ask a reciprocal question instead of answering the
question `What's yours`. In such a case, the chatbot must first translate
this user inquiry `What's yours` into a full inquiry `What's your
favorite movie` based on the context before processing the user inquiry.

Currently Juji automatically translates a context-sensitive user
inquiry based on the label instead of the request itself. This is
because the label often captures the core question. A translation
based on the core question can avoid unnecessary noises. Below shows
two example requests and their labels, which are used for handling
context-sensitive user inquiries.

**Example I**

In this example, the label captures the core of the request but not
additional description.

<p align="center"><img src="../img/fav-movie-label.png" alt="A sensible label" width="650"/></p>

Based on this label, below shows a chat fragment that handles a
context-sensitive user inquiry on this topic:


<p align="center"><img src="../img/context-fav-movie.png" alt="A sensible label" width="650"/></p>


**Example II**

Here is another example showing the label is just the stem of the
  question:

<p align="center"><img src="../img/hobby-label.png" alt="A sensible label" width="650"/></p>

A conversation fragment shows that how the chatbot handles a
context-sensitive inquiry on this topic:

<p align="center"><img src="../img/context-hobby.png" alt="A sensible label" width="650"/></p>

### **Index User Responses in Audience Report**

Another use of a request label is to index the user answers to the
request in the audience report. Below is an example of audience
report. It shows various user answers to the above two requests. As
shown, both labels mentioned above are used to index the corresponding
user answers.

<p align="center"><img src="../img/label-index-answers.png" alt="A
sensible label" width="650"/></p>

Since the labels are often more concise than the original requests,
using them to index user answers makes the report more consumable.

See [these instructions](/reports#export-audience-data) to download
an audience report.

## **Clone Chatbot for Different Audiences**

In some cases, you may want your chatbot to behave slightly
differently for different audiences. For example, one chatbot needs to
redirect to a different URL after it is done chatting, while the other chatbot
may generate a unique code at the end of the chat. To reuse most of
the shared chatbot content, you can easily clone a chatbot as shown
below and then deploy
different chatbots for different audiences.


<p align="center"><img src="/img/clone-a-chatbot.png" alt="Clone a
chatbot" width="650"/></p>


## **Make "Native" Juji AI Chatbot**

While [Juji Studio](/juji-studio) provides an easy way to author,
test, deploy, and manage an AI chatbot, [Juji API](/api) provides the
flexibility of integrating an authored chatbot into any third-party
applications, such as a web or a mobile application. We strongly
encourage the use of both. For example, content creators such as
social media marketers or sales personnel can use Juji Studio to enter
the content of a chatbot. On the other side, the IT or engineering
team can use the Juji API to integrate such a chatbot into business
applications to deploy a chatbot "native" to the applications. This
separation of duties gives each team the freedom to operate while
allowing them to collaborate on the same chatbot.

## **What's Next**

Want to power up your chatbot and get some more magic going? Juji has
you covered. Check out [best practices](/chatbot-design-tips) for
designing AI chatbots or venture into **[Juji IDE](/juji-ide)**.