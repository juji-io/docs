# Customize Chatbot in Design View

We have had a glance at the Chatbot Design view already in [Get Started](index.md).

<p align="center"><img src="../img/design-page.png" alt="Design page" width="550"/></p>

Now we learn how to use it to customize our chatbot.

## Customize Agenda

Unlike many chatbots that only answer user's requests, an important mission of
Juji chatbot is to ask user questions or give user guidances. Therefore, each
Juji chatbot has an agenda, which may consists of some questions to ask or
information to give.

As the Design user interface shows, the template you selected already contains a
sample agenda. You may modify it to your liking by doing the following.

### Change Wordings

Juji platform has many built-in questions that organizations may ask their
audience, such as what kind of product their customers favor, what needs their
employees have, and so on.

You may want to change the way how these questions are asked. To change the
wording of any question, just click on the bubble containing the question, it
expands into a dialog:

<p align="center"><img src="../img/change-wording.png" alt="Change wording" width="550"/></p>

The main text box contains the text of the question that you can edit. After
editing, click `Save` to save your changes.

If you `Preivew` your chat, you will find that the bot asks the question with
your new wording.

### Delete Question

If you do not want the bot to ask a question, click the question to bring up the
editing dialog. On the left corner of the dialog, there is a `Delete` link for you to
delete the question.

### Add Question

If you want the bot to ask an additional question somewhere, click the big `+`
icon between question items to bring up a popup menu:

<p align="center"><img src="../img/add-question.png" alt="Add question" width="550"/></p>

Select `Qeustion Bank`, it brings up a dialog that allows you to select the Juji
built-in questions that your bot can ask the audience.

<p align="center"><img src="../img/question-bank.png" alt="Question bank" width="550"/></p>

Juji works hard to handle the contingencies surrounding these built-in
questions, such as followup inquiries, uncooperative responses, and so on,
based on our ample experience in developing and deploying chatbots to real world
use cases. We recommend you to try these built-ins first.

If you could not find a built-in question that is close to the question you have in mind,
you may write your own topic to handle them by clicking `Write Custom Topic`
link in the editing dialog. Refers to [Juji Concepts](concept.md) to start
learning your way around writing topics.

## Customize Answer to FAQs

Juji bot can also answer user's common questions. You can customize the
bot's answers to these frequently asked questions (FAQs) by clicking on the `FAQ` link
at the right side of the red bar on top. It brings up a dialog:

<p align="center"><img src="../img/faq-edit.png" alt="FAQ edit" width="550"/></p>

On top of the dialog is a pull down menu for selecting questions to add to
the list of FAQs you bot will answer.

Juji works hard to recognize these questions in whatever form your users may
choose to ask them. Asking a similar question in completely different ways would
normally not deter Juji bot, thanks to modern natural language processing.

Once the questions are added to the list of FAQs, all you need to do is to provide
your answers to these questions. Users may ask these questions any time during
the conversation and Juji bot would answer them correctly using your answers.

You can also delete questions that are not relevant to you. After you are done
with editing the FAQs, do not forget to click `Save`.
