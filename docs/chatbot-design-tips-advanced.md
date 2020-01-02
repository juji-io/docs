# **Making AI Chatbots: <br> Best Practices (Advanced)**

Here are more design tips if you want to leverage the [Juji
Platform](/index) to achieve more.

## **Give Sensible Labels**

The label of a free-text request is used for multiple purposes. It is
used to summarize the topic (see the topic card on the left panel) and
also used to index user answers to the request in an audience report.

More importantly, it is used to find a matched Juji built-in dialog to
handle user responses to the request. For example, Juji has a built-in
dialog that handles diverse user responses to the request `What are
your hobbies`. To find such a built-in dialog, Juji uses the entered
label. Giving a sensible lable thus can better help Juji find the
right built-in conversation, which can then handle diverse user
responses on that topic with no or little customization required.

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