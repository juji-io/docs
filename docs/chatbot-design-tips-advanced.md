# **Making AI Chatbots: <br> Best Practices (Advanced)**

Here are more design tips if you want to use the [Juji
Platform](/index) to optimize your AI chatbot performance and deliver superior user experience.


## **Use Proper Chatbot Request**

Currently Juji supports two main types of chatbot request:
[choice-based](/design#choice-request) and
[free-text](/design#free-text-request). The former collects structured
user input, while the latter elicits open-ended, free-text user input.

If your goal of a request is to guide users to different directions or
gathers user input to a limited set of options, use the choice
request. It is deterministic, quick, and almost error free.

If your goal is to elicit open-ended user input, e.g., their insights
or unanticipated responses on a particular topic, use a free-text
request. Because a free-text request is intended to gather open-ended
user input, be aware of potential highly diverse user digressions. To
handle such user digressions, make sure that you [choose a right Juji
built-in dialog](/design#built-in-dialog) to handle such situations
automatically. You can of course write [custom chatbot
actions](/design#customizing-chatbot-actions) to handle specific user
input that you wish to capture and address.

## **Use Proper Chatbot Trigger**

Depending on your chatbot application, the tip below helps you
decide whether you use a `contains-keywords` or
`is-similar-to` trigger when you customize your chatbot actions.

In general, `contains-keywords` will help better match a user input
syntactically as long as the input contains the keywords. In contrast,
`is-similar-to` will help better match a user input semantically
regardless of its syntactic form.

Assume that your chatbot asks `What's your favorite fruit?`. You
define a trigger `contains-keywords` to capture particular kind of
fruit like `strawberry`.

<p align="center"><img src="/img/keywords-trigger.png" alt="Keywords Trigger" width="650"/></p>

As long as a user input contains a keyword that matches with the fruit
name you put into, the trigger will fire. For example, it will match a
user expression `I really like strawberries`:

<p align="center"><img src="/img/keywords-chat-1.png" alt="Keywords
Trigger" width="650"/></p>

It will also match a user input with very different meaning `I like
fruit except strawberries`:

<p align="center"><img src="/img/keywords-chat-2.png" alt="Keywords Trigger" width="650"/></p>

This is because both expressions contain the keyword 'strawberry`
regardless their use with different semantics. Note that Juji
automatically handles [stemming and lemmatization]
(https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html)
in keyword matching to support the matching of word variations.

However, a `contains-keyword` trigger would not match
`strawberry` with `blueberry` because these are very different keywords:

<p align="center"><img src="/img/keywords-chat-3.png" alt="Keywords Trigger" width="650"/></p>

In contrast, if you define a trigger `is-similar-to` with examples
such as `I like strawberries`:

<p align="center"><img src="/img/is-similar-to-trigger.png"
alt="is-similar-to trigger" width="650"/></p>

This trigger will match a user input `I like blueberries` because this
expression is considered **semantically** similar:

<p align="center"><img src="/img/is-similar-to-chat.png"
alt="is-similar-to trigger" width="650"/></p>

With a high enough matching threshold (e.g., `90%`), the trigger will not match
semantically different input such as `I dislike strawberries`
even though it contains the word `strawberries'.

In short, a rule of thumb is that if you care about capturing the
semantics of a user input more accurately, use `is-similar-to` where
you can give words, phrases, and full sentences as examples. If you
care about capturing a particular word/phrase regardless how it appear
syntactically in an input, use `contains-keywords`.

In the near future, we will support the use of both in **one trigger**. 


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
label 2 - short" width="550"/></p>

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
sensible label - index answers in audience report" width="650"/></p>

Since the labels are often more concise than the original requests,
using them to index user answers makes the report more consumable.

See [these instructions](/reports#export-audience-data) to download
an audience report.

## **Clone Juji Chatbots**

In some cases, you may want your chatbot to behave slightly
differently for different audiences. For example, one chatbot needs to
redirect to a different URL after it is done chatting, while the other chatbot
may generate a unique code at the end of the chat. To reuse most of
the shared chatbot content, you can easily clone a chatbot as shown
below and then deploy
different chatbots for different audiences.


<p align="center"><img src="/img/clone-a-chatbot.png" alt="Clone a
chatbot" width="650"/></p>

## **Export/Import Juji Chatbots**

Once you have created a chatbot on Juji, you may want to share it with
others, for example, a fellow chatbot designer who could help polish
the chatbot or a client who wishes to buy your chatbot but
manage the chatbot him/herself. On the other hand, you may want to
create a chatbot based on another designer's chatbot instead of
creating one from scratch.

On Juji, you can easily do so by exporting your chatbot so you can
share it with others. The following screenshot shows that you can
click on the ellipsis (...) menu button located on the top right
corner of the card representing a chatbot you wish to export. Then
click on the "Export" button. This action will automatically download
a file called *-export.juji onto your computer, where * is the project
name associated with the chatbot.

<p align="center"><img src="/img/export-a-chatbot.png" alt="Export a
chatbot" width="650"/></p>

If you wish to import a Juji chatbot, just click on the "+ AI Helper"
button. As shown below, instead of creating a chatbot from scratch,
you can use the "Import" tab to import an exported *.juji file. After
importing a chatbot, you can customize and manage the chatbot as if it
were created by you from scratch.

<p align="center"><img src="/img/create-a-chatbot-btn.png" alt="+ AI Helper
button" width="350"/></p>

<p align="center"><img src="/img/import-a-chatbot.png" alt="Import a
chatbot" width="650"/></p>

## **Difference between "Clone" and "Export"**
Although both "Clone" and "Export" allow the sharing and reuse of a
Juji chatbot, the key difference is that "Clone" allows the reuse
within the same Juji account, while "Export" allows the reuse of a
chatbot across different Juji accounts (e.g., yours and your
teammate's).

## **Embed Juji Chatbots in Third-Party Apps**

While [Juji Studio](/juji-studio) provides an easy way to author,
test, deploy, and manage an AI chatbot, [Juji API](/api) provides the
flexibility of integrating your chatbot into any third-party
applications, such as a web or a mobile application.

The Juji platform supports the seamless, combined use of Juji Studio
and Juji API. For example, content creators such as social media
marketers, product managers, and sales professionals can use Juji
Studio to customize the content of a chatbot, deploy and manage the
chatbot. On the other side, the IT or engineering team can use the
Juji API to "embed" the deployed chatbot into a brand's own business
applications, controlling the look and feel of the chatbot and making
the chatbot "native" to the application. This separation of
duties gives each team the freedom to operate while allowing them to
easily collaborate on the same chatbot.

Such integration is also straightforward: just use the Juji provided
standard API to embed a Juji chatbot into a third-party application,
without the need of downloading and installing any code or SDK. Once a
chatbot is embedded, the business team who designs the content or
workflow of a chatbot can use the Juji Studio to easily manage and
update the chatbot without requiring the IT or engineering team's
effort to update the embedded chatbot.

## **What's Next**

Want to power up your chatbot and get some more magic going? Juji has
you covered. Check out [best practices](/chatbot-design-tips) for
designing AI chatbots or venture into **[Juji IDE](/juji-ide)**.