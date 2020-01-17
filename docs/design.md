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
contains a default chat flow, which consists of one or more topic
blocks shown on the left side of the screen. Each **topic block**
often represents a [Juji built-in mini dialog](#built-in-dialog) that
enables a chatbot to *automatically* carry on a multi-turn
conversation with users.

A chat flow is often defined for a chatbot to achieve specific
goals. For example, a typical AI sales helper chatbot is associated with
a chat flow that asks a user several questions and then use the
gathered information to offer personalized services, such as making
product recommendations.

Since each chatbot is made for its own missions, you can easily
customize a chatbot by altering the chat flow or any topic blocks
in the flow.

### Add a Topic

One can add a topic to an existing chat flow in one of the two ways:

* Click on the round green **`+`** button below the **`Welcome`** card to
  add a topic at the beginning of a chat flow. You can also use the
  same green **`+`** button above the **`Wrap-up`** card to add a topic at the end of a chat flow.

* Mouse hover any topic card (e.g., `How are you doing?`) and then
  select the round green **`+`** button to add a topic after the current
  topic card.

<p align="center"><img src="/img/design-add-topic.png" alt="add a
topic buttons" width="350"/></p>

<p align="center"><img src="/img/design-topic-type.png" alt="add a
topic buttons" width="550"/></p>

As shown above, Juji currently supports two types of topics:

#### **Chatbot Request**

This is for a chatbot to ask a user a question or perform a certain
  action. The chatbot must wait for a user to respond to such a
  request before moving the conversation forward. Currently, Juji
  supports five types of chatbot request:

<p align="center"><img src="/img/design-request-type.png" alt="add a
topic buttons" width="550"/></p>

#### **Chatbot Message**

This is for a chatbot to send a message to a user without waiting for
  a user's response. Currently, Juji supports three types of chatbot
  message.

<p align="center"><img src="/img/design-message-type.png" alt="add a
topic buttons" width="550"/></p>

**IMPORTANT TIP** If you intend to have your chatbot wait for a user input and respond to it before moving on, make sure you choose `Make a Request`. Otherwise, your chatbot simply ignores any user input even if the message is worded like a question. As the example shown below, T6 will not wait for a user's input but T5 will. Note the chat icon appearing on T5, indicating T5 is a "true" question. 

<p align="center"><img src="/img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

**IMPORTANT TIP**

To decide which chatbot request to use, please check out this [design
tip](/chatbot-design-tips-advanced#use-proper-chatbot-request).

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

## **Customize Q&A and Fallback**

In addition to driving a conversation based on the main chat flow, an
AI chatbot must handle user questions or side-talking raised any time
during a chat. To enable a chatbot to do so, Juji allows the
customization of Q&A and fallback. Such customization enables Juji
chatbots to answer user free-text questions, handle user digressions, and
even chitchat socially, anytime during a conversation.

### **Handle Free-Text Q&As**

Using the `Q&A Board`, one can support custom, natural-language Q&As,
monitor, and manage unanswered user questions encountered during a
chat. Below is an example of a Q&A board:

<p align="center"><img src="/img/design-qa.png" alt="add a
topic buttons" width="650"/></p>

On this page, one can enter a custom Q&A pair directly in the table
(using the green **`+`** button to add) or upload a CSV file
containing a Q&A list. The above screenshot also shows that there is
one unanswered user question (indicated by the red badge displayed
next to the `Q&A Board`). Juji automatically detects unanswered user
questions and displays such questions on the Q&A dashboard.

<a name="qa-tips">**IMPORTANT TIP**</a> If you decide to put all your Q&As in a CSV file and then upload, download the CSV file first as it contains the required file format to fill in your Q&As.

As shown below, each template includes four columns:

<p align="center"><img src="/img/qa-csv.png" alt="CSV file of Q&A" width="650"/></p>

All four columns must be preserved, so is their order.  Although the
first column (**`ID`**) and the last column (**`Comment`**) can be
left empty, the empty columns must still exist and cannot be deleted.

* **ID** You can use this column to give your Q&A pair a
    name/label. If you don't provide an ID, Juji will automatically
    generate one. This label is especially useful to group all varied
    question expressions into the **same question**. This way you
    don't need to duplicate the answer for each varied expression. For
    example, rows 2-3 and rows 5-6 represent two sets of
    Q&As. Moreover, they also share all the alternative answers (see
    below).

* **Question** This column holds questions and their varied expressions. 

* **Answer** This column holds answers. You can enter alternative answers to the same question. This will make your chatbot sound more intelligent. When there are alternative answers, a chatbot randomly chooses one to use when answering a matched question. 

* **Comment** This column holds your comments, which is optional.


### **Support Social Chitchat**

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

<p align="center"><img src="/img/custom-fallback.png" alt="Custom Fallback" width="650"/></p>

**IMPORTANT TIP** Juji already provides rich, built-in social chitchats. We recommend that you observe the behavior of your chatbot first before adding any custom user comment-chatbot response pairs. 

### **Tutorial Video**

Below is a very short video that shows how to create or update a Q&A
list:

<div align="center"> <iframe width="560" height="315"
src="https://www.youtube.com/embed/U0tR04xQTio" frameborder="0"
allow="accelerometer; autoplay; encrypted-media; gyroscope;
picture-in-picture" allowfullscreen></iframe> </div>

## **Customize Chatbot Settings**

In addition to customizing the main chat flow and the Q&A list, one
can also customize various chatbot settings, including the name of the project.

### Project Name

You can edit the `name` of the project by mouse hovering the project
name and then click on the `pencil` button.

### Chatbot Persona

To personalize your chatbot, you can choose a stock persona or define a custom persona.

<p align="center"><img src="/img/chatbot-settings-1.png" alt="chatbot settings" width="650"/></p>

<br>

To define a custom persona, click on the `Custom` persona icon as shown below. You can then upload your persona photo, give your custom persona a name, and enter a short bio. Once you are done, click on the green check mark to save it.

<p align="center"><img src="/img/custom-chatbot-persona.png" alt="define a custom persona" width="650"/></p>

### Conversation Parameters
You can also customer other chatbot parameters, such as setting a
`conversation pace` and `user response` requirement as shown below. 

<p align="center"><img src="/img/chatbot-settings-2.png" alt="add a
topic buttons" width="650"/></p>

* **Conversation pace** It controls how fast a chatbot transitions
    from one topic to the next.

* **Refresh duration** It controls how frequently a chatbot auto
starts itself from the beginning. In certain situations, you wish a
chatbot to start more frequently (e.g., an e-commerce chatbot) than
others (e.g., an interview chatbot) to make sure that users can
accomplish their tasks without starting over again.

* **Minimal response length** It controls the minimal number of words
a user must provide to a chatbot request. This parameter sets the
default for *all* questions and it can also be customized for a
specific chabot question/request.

<a name="default-response"></a>
* **Default response to unknown user input** This indicates what
    the chatbot should say when encountered unrecognizable user input,
    no matter whether it is a comment of question.

* **Fallback handling** This allows you to control what kind of
    fallback handling is desired for your chatbot. Juji provides a
    rich list of fallback handling functions to manage user input that
    is outside of your chatbot script. From our experience, users
    often deviate from your chatbot script and start a side
    talkng. These fallback handling functions enable your chatbot to
    handle user-initiated side talking gracefully and also keep the
    chat on track. 


## **Examples**

In this section, we use a set of concrete examples to show how to
customize a chatbot. In particular, we show how to customize a
chatbot's content and its behavior.

### Customizing Chatbot Content

Here we use a set of examples to show how to define the content
of different topics and how the content would appear in a chat on the web or
Facebook Messenger. 

#### **Plain Text Chatbot Message**

This is the simplest chatbot message that contains only plain text.

* **Add a function** Use the green function button (`fx`) below the
text bubble to add a function, such as `(user-first-name)` to
personalize the chatbot message.

* **Add a link** Use the green `link` button to add a URL (`bio`).

* **Add a paraphrase** Use the green `+` button on the right of the
    text bubble to add paraphrases of the message (see the screenshot
    below). The paraphrases will be selected by your chatbot randomly
    to send during a chat. See [best practices](/chatbot-design-tips)
    for good uses of paraphrases.

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


#### **<a name="free-text-request"></a>Free-text Request**

Perhaps the most used request for an AI chatbot is to pose free-text,
open-ended questions during a chat. Such a question can elicit diverse
and detailed user responses to gather in-depth insights and better
understand users' needs and wants.

<a name="request-label"></a>As shown below, a free-text request includes the following:

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

#### <a name="choice-request">**Choice Request**</a>

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

### Customizing Chatbot Actions

In a natural conversation, different user behavior should drive
different chatbot actions. Juji supports the customization of chatbot
behavior in many ways. This section will use a set of concrete
examples to show how to easily customize a chatbot behavior based on
application needs. 

#### <a name="built-in-dialog"></a> **Use Juji Built-in Dialog**

Unlike other chatbot platforms, Juji has a dialog library that
contains thousands of built-in mini conversations. When you [add a
topic](#add-a-topic) that is a [free-text
request](#free-text-request), Juji automatically uses the [request
label](#request-label) to search its dialog library and retrieve a
matched mini conversation for this request.

For example, if you enter `Have you ever worked at a restaurant?` as
the request label, Juji will auto retrieve the matched mini
conversation `This is to ask a user yes/no question' (see below)

<p align="center"><img src="/img/example-label-1.png" alt="add a
topic buttons" width="650"/></p>

<p align="center"><img src="/img/example-topic-1.png" alt="add a
topic buttons" width="650"/></p>

In this case, the built-in dialog will automatically process a user's
positive or negative responses and enable you use the auto-detected
expressions to direct the user to different paths. In other words, you
don't need to worry about how to define triggers to catch highly
diverse users' positive or negative expressions.

In contrast, if the request label is `What's your favorite fruit`, the
retrieved mini conversation would be `Ask a user about his/her
favorite thing` (see below)

<p align="center"><img src="/img/example-label-2.png" alt="example label" width="650"/></p>

<p align="center"><img src="/img/example-topic-2.png" alt="example topic associated with a label" width="650"/></p>

In case that Juji-retrieved mini conversation is not what you want to
use, you can always find a different built-in dialog (click on the
green search icon as shown above). Below is a screenshot showing the
Juji dialog library, where you can browse and use keywords to search
for a suitable, built-in dialog to use.

<p align="center"><img src="/img/search-a-topic.png" alt="search a
topic" width="550"/></p>

A built-in Juji dialog is very powerful as it helps handle diverse
user behavior automatically. For example, if you wish to collect
users' contact information, the built-in dialog `Ask a user contact
info` automatically handles various cases, such as user already opt-in
contact information or potentially erroneous input.

<p align="center"><img src="/img/ask-user-contact-topic.png" alt="Ask
user contact info" width="350"/></p>

#### <a name="use-built-in-attributes"></a>**Use Juji Built-in Attributes**

In certain built-in dialogs, Juji automatically creates a set of
built-in attributes to capture processed user input. For example, if a
mini dialog talks about the `weight` of something (e.g., `How much
does your dog weigh`), Juji automatically parses user input to the
question and stores the parsed user input into two attributes:
`weight-amount` and `weight-unit`.

Click on the green `attribute` icon to view the attributes associated
with a built-in dialog (see below).

<p align="center"><img src="/img/system-attribute-example.png" alt="add a
topic buttons" width="650"/></p>

You can also edit the attribute names to avoid potential conflicts. For
example, your chatbot asks two questions regarding `weight`, one for
dog and the other for cat. You would want to change the default
attribute names to `dog-weight-amount` and `cat-weight-amount`,
respectively to distinguish user answers to these two questions.

#### **Pin a Matched Dialog**

As described above, Juji uses the request label you entered to search
and find a matched built-in dialog. This means that changing your
request label will *automatically* trigger Juji to find a different
matched dialog. To avoid such situations, you can use the green `pin`
icon to pin a found dialog (see above). This means that changes in
your request label will no longer trigger Juji to search and
change the matched dialog automatically.

Besides reusing a Juji built-in dialog, you can always customize 
a built-in dialog. Next we use a set of examples to show how to
customize built-in dialogs.

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
    negative sentiment. <a name="sentiment-detection"></a>

<p align="center"><img src="/img/contain-sentiment.png" alt="add a
topic buttons" width="450"/></p>

* `matches` If a user input matches a rule specified in [Juji chatbot
    language](/reference).

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
of the choices, there is just one type of **IF** condition, the choice made by
the user.


**IMPORTANT TIP**

To decide which type of trigger (chatbot condition) to use, please
check out this [design
tip](/chatbot-design-tips-advanced#use-proper-chatbot-trigger).


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
  defines a full topic - a [message topic](#customizing-chatbot-content).

* `Follow-up Request` This defines a chatbot request that allows the
  chatbot to ask a follow-up question. This defines a full topic - a
  request topic. 

#### <a href="suspend-chat"></a>**Suspend Current Chat** 

Sometimes, you may want to pause a chatbot a bit before letting it
interact with your audience again. You can do so easily following these steps:

* Go to `Main Chat Flow` under `Design`

* Click on the **`Welcome`** card

* Click on the slider under the welcome message (on the right panel) to suspend a chat. See the screenshot below. 

* Edit the welcome message accordingly to inform users about the suspension/pause.

<p align="center"><img src="/img/suspend-chatbot.png" alt="Suspend chat" width="650"/></p>

**IMPORTANT TIP** If your chatbot is deployed via a web URL, you may also want to change the greeting message on the [web cover page](/release#deploy-to-website) to inform future users about the pause/suspension.

#### **Customize End Topic** <a href="customize-end-topic"></a>

One may want to customize a chatbot's ending behavior. For example, if
a survey chatbot needs to end a conversational survey at some point. In
contrast, a customer service chatbot must hang around to serve
customers.

To customize the ending behavior, click on the **`Wrap-up`**
topic, the last topic in the left topic panel.

<p align="center"><img src="/img/wrapup-topic.png" alt="add a
topic buttons" width="250"/></p>

Then click on the text bubble or the `pencil` icon to edit the topic:

: **Option 1: Make a chatbot stick around**

<p align="center"><img src="/img/custom-end-1.png" alt="add a
topic buttons" width="550"/></p>


: **Option 2: End a chatbot**

<p align="center"><img src="/img/custom-end-2.png" alt="add a
topic buttons" width="550"/></p>


## **What's Next**

Once a chatbot is ready, you can deploy it onto a website or a
Facebook page. Please check out [**Chatbot Deployment**](/release)
to deploy your AI chatbot.


