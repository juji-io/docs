# **Customize AI Chatbot**

A chatbot creator can use Juji Studio to customize an AI chatbot in
three areas:

* **Customize Main Chatflow** Every AI chatbot on Juji is driven by a
    *main chat flow*, the conversation agenda that threads one or
    more topics to drive a conversation forward. As shown below, a
    chatbot creator can add, remove, and edit a topic on a main chat flow.

* **Customize Q&A and Fallback** AI chatbots should be able to answer
    user inquiries or respond to user comments *any time* during a
    chat. To enable such capabilities, a chatbot creator can add,
    remove, and edit a Q&A list and fallback handling as shown below.

* **Customize Chatbot Persona and Beyond** A chatbot creator may also
    want to customize the chatbot persona as well as other
    chat-related settings, such as controlling the pace of a chat. 

## **Customize Main Chat Flow**

<p align="center"><img src="/img/design-main-flow.png" alt="Design page" width="650px"/></p>

As shown above, an AI chatbot created based on a template already
contains a default chat flow (see the list of topic blocks shown on
the left side of the screen). Such a chat flow is often defined for a
chatbot to achieve specific goals. For example, a typical sales helper
chatbot is associated with a chat flow that asks a user several
questions and then use the gathered information to offer personalized
services, such as making product recommendations.

Since each chatbot has its own missions, a chatbot creator can use
following operations to easily customize a main chat flow to suit
his/her needs.

### Add a Topic

One can add a topic to an existing chat flow in one of the two ways:

* Click on the round green "+" button below "Welcome" topic to add a topic at the end of a chat flow.

* Mouse hover any topic card (e.g., "How are you doing?") and then
  select the round green "+" button to add a topic after the current
  topic card.

<p align="center"><img src="/img/design-add-topic.png" alt="add a
topic buttons" width="350"/></p>

<p align="center"><img src="/img/design-topic-type.png" alt="add a
topic buttons" width="550"/></p>

As shown above, Juji currently supports two types of topics:

* **Chatbot Request**. This is for a chatbot to ask a user a question
  or perform a certain action. The chatbot must wait for a user
  to respond to such a request before moving the conversation
  forward. Currently, Juji supports five types of chatbot request:

<p align="center"><img src="/img/design-request-type.png" alt="add a
topic buttons" width="550"/></p>

* **Chatbot Message**. This is for a chatbot to send a message to a user
  without waiting for a user's response. Currently, Juji supports
  three types of chatbot message.

<p align="center"><img src="/img/design-message-type.png" alt="add a
topic buttons" width="550"/></p>

**IMPORTANT TIP:** If you intend to have your chatbot wait for a user input and respond to it before moving on, make sure you choose `Make a Request`. Otherwise, your chatbot simply ignores any user input even if the message is worded like a question. As the example shown below, T6 will not wait for a user's input but T5 will. Note the chat icon appearing on T5, indicating T5 is a "true" question. 

<p align="center"><img src="/img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

### Edit a Topic

Once a topic is added, one can then edit the topic. See the section
below on how to edit a specific topic. One can edit a topic in three sections:

* **Chatbot Content** Use this section to customize the actual chatbot
message(s) that users will see during a chat. Please refer to
[examples](#examples-customizing-chatbot-content) and [best practices](/chatbot-design-tips)
for defining the content of a topic.

<p align="center"><img src="/img/design-content.png" alt="add a
topic buttons" width="550"/></p>


* **Chatbot Actions** Use this section to customize chatbot behavior
    under different conditions. The green "Customization" button shown
    below can be used to add a group of chatbot actions under one
    condition (trigger). Please refer to [examples](#examples-customizing-chatbot-actions)
    and [best practices](/chatbot-design-tips) for defining specific
    conditions and corresponding custom chatbot actions.

<p align="center"><img src="/img/design-chatbot-action.png" alt="add a
topic buttons" width="550"/></p>


* **Topic Settings** Use this pop-up window
    to customize one or more topic-specific parameters, such as the
    delayed start of this topic and required user response
    length. Please refer to [best practices](/chatbot-design-tips) to tune
    these parameters.
    
<a name="topic-settings"></a><p align="center"><img src="/img/design-topic-settings.png" alt="add a
topic buttons" width="550"/></p>

### Delete a Topic

To delete a topic, mouse hover the corresponding topic card listed in
the left topic panel. Then click on the red trash can icon to delete
the topic. A deletion is permanent and cannot be undone.

<p align="center"><img src="/img/design-delete-topic.png" alt="add a
topic buttons" width="350"/></p>


### Clone a Topic

To clone a topic, mouse over the corresponding topic card listed in
the left topic panel. Then click on the green clone icon to clone the
topic. The cloned topic will retain all behavior of the original topic.
 
<p align="center"><img src="/img/design-clone-topic.png" alt="add a
topic buttons" width="350"/></p>

### Examples: Customizing Chatbot Content

Here we use a set of examples to show how to define the content
of different topics and how the content would appear in a chat on the web or
Facebook Messenger. 

#### **Plain Text Chatbot Message**

This is the simplest chatbot message that contains only plain text.

* **Add a function** Use the green function button (`fx`) below the
text bubble to add a function, such as `(user-first-name)` to
personalize the chatbot message.

* **Add a link** Use the green `link` button to add a URL (`bio`).

* **Add a paraphrase** Use the gree `+` button on the right of the
    text bubble to add paraphrases of the message. The paraphrases
    will be output randomly during a chat. See [best
    practices](/chatbot-design-tips) for good uses of paraphrases.

<p align="center"><img src="/img/design-plain-remark.png" alt="add a
topic buttons" width="550"/></p>

You can always use the green `eye` icon located at the top-right
corner of the text bubble to preview the above message in a chat:

<p align="center"><br><br><img src="/img/preview-plain-remark.png" alt="add a
topic buttons" width="350"/></p>

#### **FB Media Card**

For a FB Messenger chatbot, one can define one or more FB
Media cards to display a combination of text, image, and URL links. As
shown below, each card contains:

* **Title** (required field)

* **Subtitle** (optional)

* **Image** (optional image URL)

* **URL Buttons** (up to 3 links per card) 

<p align="center"><img src="/img/design-add-FB-media.png" alt="add a
topic button" width="550"/></p>

Currently one can define up to three FB Media cards. In a Facebook
Messenger window, these cards will show up in a carousel.

<p align="center"><img src="/img/design-fb-media-desktop.png" alt="carousel" width="550"/></p>

Note that FB Media cards will ***not*** show up if the chatbot is
deployed on a website.

#### **Web Media Card**

For a website chatbot, one can also define a message with a
combination of text, image, and URL. As shown below, the web media
card contains:

* **Text Message** (required)
* **Hyper Link** (optional)
* **Image** (optional image URL)

<p align="center"><img src="/img/design-add-web-media-3.png" alt="add a
topic buttons" width="550"/></p>

Below is the preview of a web media card with an image:

<p align="center"><img src="/img/preview-web-media.png" alt="add a
topic buttons" width="550"/></p>


#### **Free-text Request**

Perhaps the most used request for an AI chatbot is to pose free-text,
open-ended questions during a chat. Such a question can elicit diverse
and detailed user responses to gather in-depth insights and better
understand users' needs and wants.

As shown below, a free-text request includes the following:

* **Label** Typically, a label is the short form ("stem") of a chatbot
request. Although it automatically takes the form of the main message,
it is good to give a sensible label as it is also used for multiple
purposes (see [best practices](/chatbot-design-tips)).

* **Main Message** (required) This is the question that users will see
    in a chat. Instead of asking a question directly, a good message
    should also contain the context or motivation of the
    asking.
    
* **Re-asking Messages** (optional) During a chat, a user may not
    always respond to a chatbot question. In such a case, a chatbot
    may want to repeat the question. One can add (green `+`)
    paraphrases of a request and indicate whether such a paraphrase
    can be used to re-ask the question by checking the `Re-asking
    Message` box.

See [best practices](/chatbot-design-tips) on how to phrase free-text
questions in a conversation.

<p align="center"><img src="/img/design-add-free-text-q.png" alt="add a
topic buttons" width="850"/></p>

#### **Choice Request**

One of the popular chatbot request is to ask a user to make a
choice. Below is an example of a single choice request, also known as
radio button question, where a user can select only one choice.

As shown below, a single choice question contains:

* **Main Message** (required)

* **Option Items** (at least one item is required)

<p align="center"><img src="/img/design-add-radio.png" alt="add a
topic buttons" width="850"/></p>

In addition to adding regular option items, `Other` option can be added to
let a user specify additional text. One can also indicate whether to
treat all the option items as numbers. Numeric choices can be used to
define chatbot conditions involving numeric operations, such as `>=`
and `<`. See [examples](#examples-customizing-chatbot-actions) below on defining chatbot conditions.

<p align="center"><img src="/img/design-add-choice-q.png" alt="add a
topic buttons" width="550"/></p>

Depending on where the chatbot is deployed, the look of a choice
question may be different.

A choice question displayed in a **web-based** chatbot:

<p align="center"><img src="/img/preview-choice-q-web.png" alt="add a
topic buttons" width="650"/></p>

A choice question displayed in a **Facebook Messenger chatbot**:

<p align="center"><img src="/img/preview-choice-q-fb.png" alt="add a
topic buttons" width="350"/></p>

In Facebook Messenger, a user may enter a text message instead of
clicking on a choice. In such a case, the chatbot will handle the user
text input first. Since a Juji AI chatbot tracks a conversation
context, it will repeat the question, if the choice question is a
required one.

Below is an example chat where the user asks a question intead of
making a color choice. The chatbot answers the user question and then
repeats the choice question.

<p align="center"><img src="/img/preview-choice-q-fb-fallback.png" alt="add a
topic buttons" width="350"/></p>


#### **Facebook Choice**

Semantically, a Facebook choice question is essentially the same as a regular
choice question except that it takes the form of Facebook buttons in a
Facebook Messenger chatbot. This type of request will ***not*** be
displayed in a web-based chatbot.

As shown below, a Facebook choice question includes:

* **Title** (required) This is the main asking message.
* **Subtitle** (optional) This adds more information to the question.
* **Button** (at least one button is required)
* **Image** (optional) An image URL can be added with the question.

<p align="center"><img src="/img/design-add-FB-choice.png" alt="add a
topic buttons" width="350"/></p>

Here is how a Facebook choice looks like in a Facebook Messenger
chatbot:

<br><p align="center"><img src="/img/preview-fb-choice.png" alt="add a
topic buttons" width="350"/></p>

#### **Facebook Email**

This special request enables a chatbot to gather opt-in user email in
a Facebook Messenger chatbot. A user must click on the displayed email
to confirm (opt-in) his/her email. A user can also text an alternative
email. To allow users to skip this question, set this question `not
required` in the [topic settings](#topic-settings).

<p align="center"><img src="/img/design-add-FB-email.png" alt="add a
topic buttons" width="650"/></p>

### Examples: Customizing Chatbot Actions

In a natural conversation, different user behavior should drive
different chatbot actions. Juji supports custom chatbot actions based
on diverse user behavior. Next we use a set of examples to show how to
customize chatbot actions based on user behavior. 

As shown below, each customization block includes two parts:

* **IF** block defines the condition (also known as trigger) under
    which the custom chatbot actions will be performed.

* **THEN** block contains one or more custom chatbot actions.

<p align="center"><img src="/img/design-action.png" alt="add a
topic buttons" width="650"/></p>

#### **Customize IF Conditions**

Since a free-text chatbot request may elicit unanticipated, diverse
user behavior, currently Juji supports five types of **IF**
conditions to capture user behavior:

* `is-similar-to` If a user input is similar to one or more
    sentences or phrases. One can also specify the similarity
    threshold. By default, the threshold is set at 80%. 

<p align="center"><img src="/img/is-similar-to.png" alt="add a
topic buttons" width="450"/></p>


* `contains-keywords` If a user input contains one or more
    keywords. Unlike `is-similar-to` condition, this condition
    requires a precise match with the stem of at least one
    specified keyword.

<p align="center"><img src="/img/contain-keywords.png" alt="add a
topic buttons" width="450"/></p>


* `contains-sentiment` If a user input contains a positive or
    negative sentiment.

<p align="center"><img src="/img/contain-sentiment.png" alt="add a
topic buttons" width="450"/></p>

* `matches` If a user input matches a rule specified in [Juji chatbot
    language](scripting.md).

<p align="center"><img src="/img/matches.png" alt="add a
topic buttons" width="450"/></p>

* `is-anything-else` If a user input matches anything else. This is
    basically the **default** condition. 

<p align="center"><img src="/img/default-cond.png" alt="add a
topic buttons" width="450"/></p>

One can check on the box next to the `STORE MATCHED INPUT` to store the
matched input into a **custom attribute**.

As shown below, if a user input contains keywords, such as `milk`,
`egg`, or `cheese`, a custom attribute `like-protein` can be created
to store the matched keyword for each user.

<p align="center"><img src="/img/custom-attribute.png" alt="add a
topic buttons" width="650"/></p>

Custom attributes can be used for many purposes, such
as customizing a chatbot message (see below) or indexing audience
information (e.g., showing all users who `like-protein`).

Note that for a **choice request**, since a user's input must be one
of the choices, there is just one **IF** condition, the choice made by
the user.

#### **Customize THEN Actions**

As shown below, when a `IF` condition is met, one or more custom
chatbot actions can be defined:

<p align="center"><img src="/img/custom-action-overview.png" alt="add a
topic buttons" width="450"/></p>

<p align="center"><img src="/img/custom-action-detail.png" alt="add a
topic buttons" width="450"/></p>

* `Quick Acknowledgement`  This defines a simple text message that a chatbot
  can use to respond to a user input.

* `Extended Reply` This defines a full chatbot message, including image and
  paraphrases, that a chatbot can use to make an extended reply. This
  defines a full topic - a message topic.

* `Follow-up Request` This defines a chatbot request that allows the
  chatbot to ask a follow-up question. This defines a full topic - a
  request topic. 

#### **Customize End Topic**

One may want to customize a chatbot's ending behavior. For example, if
a survey chatbot needs to end a conversational survey at some point. In
contrast, a customer service chatbot must hang around to serve
customers.

To customize the ending behavior, click on the `Wrap-up`
topic, the last topic in the left topic panel.

<p align="center"><img src="/img/wrapup-topic.png" alt="add a
topic buttons" width="250"/></p>

Then click on the text bubble or the `pencil` icon to edit the topic:

* Make a chatbot stick around. 

<p align="center"><img src="/img/custom-end-1.png" alt="add a
topic buttons" width="550"/></p>


* End a chatbot. 

<p align="center"><img src="/img/custom-end-2.png" alt="add a
topic buttons" width="550"/></p>

## **Customize Q&A and Fallback**

In addition to driving a conversation based on the main chat flow, an
AI chatbot must handle user questions or side-talking raised any time
during a chat. To enable a chatbot to do so, Juji allows the
customization of Q&A and fallback.  

Using the `Q&A Board`, one can customize Q&A, handle fallbacks, and
monitor unanswered user questions encountered during a chat. Below is
an example of a Q&A board:

<p align="center"><img src="/img/design-qa.png" alt="add a
topic buttons" width="650"/></p>

The above screenshot shows that there is one unanswered user question
(see the red badge displayed next to `Q&A Board`). On this page, one
can enter a Q&A pair or user comment/chatbot response pair directly in
the table or upload a CSV file containing a Q&A list. Below is a video
that shows how to create or update a Q&A list:

<div align="center"> <iframe width="560" height="315"
src="https://www.youtube.com/embed/U0tR04xQTio" frameborder="0"
allow="accelerometer; autoplay; encrypted-media; gyroscope;
picture-in-picture" allowfullscreen></iframe> </div>

## **Customize Chatbot Persona and Beyond**

In addition to customizing the main chat flow and the Q&A list, one
can also customize various chatbot settings.

* Edit the `name` of the project and the chatbot persona:

<p align="center"><img src="/img/chatbot-settings-1.png" alt="add a
topic buttons" width="650"/></p><br>

* Customize parameters to set conversation pace and user response
requirements:

<p align="center"><img src="/img/chatbot-settings-2.png" alt="add a
topic buttons" width="650"/></p>

## **What's Next**

Once a chatbot is ready, you can deploy it onto a website or a
Facebook page. Please check out [**Chatbot Deployment**](/release)
to deploy your AI chatbot.


