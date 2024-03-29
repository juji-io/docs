# **Customize Main Chat Flow**

<p align="center"><img src="https://juji.io/docs/img/design-main-flow.png" alt="Design page" width="650px"/></p>

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

## Add a Topic

One can add a topic to an existing chat flow in one of the two ways:

* Click on the round green **`+`** button below the **`Welcome`** card to
  add a topic at the beginning of a chat flow. You can also use the
  same green **`+`** button above the **`Wrap-up`** card to add a topic at the end of a chat flow.

* Mouse hover any topic card (e.g., `How are you doing?`) and then
  select the round green **`+`** button to add a topic after the current
  topic card.

<p align="center"><img src="https://juji.io/docs/img/design-add-topic.png" alt="add a
topic button" width="350"/></p>

<p align="center"><img src="https://juji.io/docs/img/design-topic-type.png" alt="add a
topic type" width="550"/></p>

As shown above, Juji currently supports two types of topics:

### **Chatbot Request**

This is for a chatbot to ask a user a question or perform a certain
  action. The chatbot must wait for a user to respond to such a
  request before moving the conversation forward. Currently, Juji
  supports [several types of chatbot request](./#type-of-chatbot-request) as described below.

### **Chatbot Message**

This is for a chatbot to send a message to a user **without** waiting for
  a user's response. Currently, Juji supports [several types of chatbot
  messages](./#type-of-chatbot-message) as explained below in detail.


**IMPORTANT TIP** If you intend to have your chatbot wait for a user input before moving on, make sure you choose `Make a Request`. Otherwise, your chatbot simply ignores any user input even if the message is worded like a question. As the example shown below, T6 will not wait for a user's input but T5 will. Note the chat icon appearing on T5, indicating T5 is a "true" question.

<p align="center">
<img src="https://juji.io/docs/img/pseudo-q.png" alt="Pseudo question" width="350"/></p>

**IMPORTANT TIP**

To decide which chatbot request to use, please check out this [design
tip](https://juji.io/docs/chatbot-design-tips-advanced#use-proper-chatbot-request).

## Edit a Topic

No matter whether you wish to configure your chatbot to make a request (aka asking users a question) or send a message, once a topic is added, you can then edit the topic in four sections:

* [Chatbot Content](./#chatbot-content). This is to customize a message that a chatbot will send to your users.

* [Chatbot Responses](./#Chatbot-responses) (only for request topics). This is to customize a chatbot's response to a user's reply to a question asked by the chatbot.

* [Chatbot Actions](./#chatbot-actions). This is to customize a chatbot's actions prior to or after the chatbot send users a message (e.g., posing a question or displaying an image).

* [Topic Settings](./#topic-settings). This is to customize various settings related to a request or a simple message.


### **Chatbot Content**

You can customize a chatbot's message(s) to users during a chat.  Please refer to [design best practices](https://juji.io/docs/quality-chatbot-design-tips) for composing the content of such a message. Below lists various message editing options.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/msg-edit-options.png" alt="chatbot message editing options" width="550"/></p>

Below we use a set of examples to show how to use each of the editing
options and how the content would appear in a chat on the web or
Facebook Messenger.

* **Add an image** Click on the "add an image" icon to insert an image into a chat message. This allows an image to be uploaded and displayed in a chat.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/insert-image-option.png" alt="insert an image into a chatbot message" width="550"/></p>

<p align="center"><img src="https://juji.io/docs/img/juji-studio/insert-image-edit.png" alt="chatbot message including an image" width="550"/></p>


The screenshot below shows how an image is displayed in a chat. It is displayed right before or after a text message.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/image-in-chat.png" alt="display an image in a chat" width="550"/></p>


* **Make a bullet list** Select part of the message text and then click on the button "Make a bullet list" to convert the highlighted text into a bullet list as shown below.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/make-bullet-list.png" alt="display an image in a chat" width="550"/></p>

* **Insert a hyperlink** A chatbot can send a message with a URL link so users can follow the link to access more information. Select part of the text message (`FAQ list`) and then click on the `Create a hyperlink of highlighted text` button to add a URL.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/add-hyperlink.png" alt="display an image in a chat" width="550"/></p>

During a chat, the content of the hyperlink can be accessed in one of the two ways: in a separate browser tab or within the same window where the chatbot sits. When you insert a hyperlink, you can select which option you'd prefer.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/add-hyperlink-options.png" alt="display an image in a chat" width="550"/></p>

The clickthroughs of any inserted hyperlinks are tracked automatically. This means that a chatbot owner can view which hyperlinks are clicked on and how frequently, which provides the indication what content your users might be interested. See ["Reports"](https://juji.io/docs/juji-studio/reports/) dashboard to view the clickthroughs of hyperlinks.


* **Call an API** A chatbot may need to access information stored in a third-party system (e.g., a CMS or CRM) in order to communicate information tailored to aspecific user. For example, if a prospective student asks about his/her application status, the chatbot needs to access Salesforce database to retrieve the requested information. To do so, you can insert an API call to access the third-party information. Specifically, just click on the "call API" button and then follow the API call pop-up to insert the API call details.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/call-api.png" alt="display an image in a chat" width="550"/></p>

Your IT personnel often knows which API is supported and the syntax of such API calls. You don't need to write any code, you just need to get the API call details from them and copy & paste them into the API pop-up window. Here is a [Youtube Video Tutorial](https://youtu.be/LNY2S3PbSAY) on how to use APIs to connect your chatbot with other systems.

* **Add a function** Use the "Insert a function" button (`fx`) to add a function, such as `(user-first-name)` to personalize the chatbot message or make a dynamic message (e.g., based on a user's input). Watch [this Youtube video tutorial](https://youtu.be/dVjvjB-bq5w) on how to use various functions including external functions to customize a chatbot message.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/insert-function.png" alt="insert a function in a chatbot message" width="550"/></p>

* **Insert an attribute** During a chat, a chatbot may gather bits and pieces of information from a user (e.g., the number of people, date and time info) in order to perform a certain task (e.g., making a reservation). As a good paractice, it is always desirable to repeat and confirm such information back to the user. To do so, you can insert an attribute in a chatbot message since user opt-in information is auto-captured in an attribute during a chat.

As shown the example below, click on the "Add attribute" button insert attributes that capture user input regarding a reservation.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/insert-attribute.png" alt="insert attribute in a chatbot message" width="550"/></p>

Attributes are very powerful elements that can be used in chatbot design and help a chatbot learn new knowledge, maintain a memory, and accomplish complex tasks. Watch [this Youtube Video Tutorial](https://youtu.be/3jxvygIvHcg) to see how attributes can be used in creating a powerful AI chatbot.

* **Add quick texting messages** In certain parts of conversation, you may want to provide users with a "quick texting" convenience. This means, when a chatbot asks a question, it also provides a couple of quick reply options, which a user can just click on the text to reply vs. type the text and then submit. This convenient reply mode is useful especially on a mobile device. The main difference between "quick texting" and radio buttons is that "quick texting" still allows users to provide other forms of responses while radio buttons take only button clicks. It provides the interaction convenience while remaining open to diverse user responses. We recommend that quick texting be used sparsely because a good conversation should not be dominated by "click to text".

Click on the button "Add quick text message" to add up to 3 quick messages.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/add-quick-reply.png" alt="enable a quick reply message for users to click to reply" width="550"/></p>

<p align="center"><img src="https://juji.io/docs/img/juji-studio/define-quick-reply.png" alt="define up to 3 quick reply messages per topic. Here two quick text messages are defined: HELP and RESTART" width="550"/></p>

Here is how "click to text" messages look like in a chat:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/quick-reply-in-chat.png" alt="how quick reply messages look like in a chat: HELP and RESTART" width="550"/></p>

* **Add a paraphrase** To create a natural and rich conversation, you can also add paraphrases of a chatbot message, especially if such a message needs to be repeated in the same conversation. For example, when a chatbot asks users a question, if the users don't anwer the question, the chatbot may need to repeat the question. In such cases, paraphrases could help make the repetitions sound more pleasant and natural.

Use the `+` button on the right of the text bubble to add paraphrases
    of the message (see the screenshot below). The paraphrases will be
    selected by your chatbot randomly to send during a chat. See [best
    practices](https://juji.io/docs/quality-chatbot-design-tips) for good uses
    of paraphrases.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/add-paraphrases.png" alt="add paraphrases of a chatbot message" width="550"/></p>

You can also view all the paraphrases using the "down arrow" button:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/view-paraphrases.png" alt="view paraphrases" width="550"/></p>




### **Chatbot Responses**

You can also customize chatbot behavior based on user responses. The green "Customization" button shown
    below can be used to add a group of chatbot actions under one
    condition (trigger). Refer to the [design best practices](https://juji.io/docs/quality-chatbot-design-tips) for defining specific conditions and corresponding custom chatbot actions.

<p align="center"><img src="https://juji.io/docs/img/design-chatbot-action.png" alt="design
chatbot actions" width="550"/></p>

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

<p align="center"><img src="https://juji.io/docs/img/example-label-1.png" alt="an example label" width="650"/></p>

<p align="center"><img src="https://juji.io/docs/img/example-topic-1.png" alt="an example label in a topic use" width="650"/></p>

In this case, the built-in dialog will automatically process a user's
positive or negative responses and enable you use the auto-detected
expressions to direct the user to different paths. In other words, you
don't need to worry about how to define triggers to catch highly
diverse users' positive or negative expressions.

In contrast, if the request label is `What's your favorite fruit`, the
retrieved mini conversation would be `Ask a user about his/her
favorite thing` (see below)

<p align="center"><img src="https://juji.io/docs/img/example-label-2.png" alt="example label" width="650"/></p>

<p align="center"><img src="https://juji.io/docs/img/example-topic-2.png" alt="example topic associated with a label" width="650"/></p>

In case that Juji-retrieved mini conversation is not what you want to
use, you can always find a different built-in dialog (click on the
green search icon as shown above). Below is a screenshot showing the
Juji dialog library, where you can browse and use keywords to search
for a suitable, built-in dialog to use.

<p align="center"><img src="https://juji.io/docs/img/search-a-topic.png" alt="search a
topic" width="550"/></p>

A built-in Juji dialog is very powerful as it helps handle diverse
user behavior automatically. For example, if you wish to collect
users' contact information, the built-in dialog `Ask a user contact
info` automatically handles various cases, such as user already opt-in
contact information or potentially erroneous input.

<p align="center"><img src="https://juji.io/docs/img/ask-user-contact-topic.png" alt="Ask
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

<p align="center"><img src="https://juji.io/docs/img/system-attribute-example.png" alt="view system attributes within a topic" width="650"/></p>

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

<p align="center"><img src="https://juji.io/docs/img/design-action.png" alt="design custom chatbot actions" width="650"/></p>

#### **Customize IF Conditions**

Since a free-text chatbot request may elicit unanticipated, diverse
user behavior, currently Juji supports five types of **IF**
conditions to capture user behavior:

* `is-similar-to` If a user input is similar to one or more
    sentences or phrases. One can also specify the similarity
    threshold. By default, the threshold is set at 80%.

<p align="center"><img src="https://juji.io/docs/img/is-similar-to.png" alt="add a is-similar-to
trigger" width="450"/></p>


* `contains-keywords` If a user input contains one or more
    keywords. Unlike `is-similar-to` condition, this condition
    requires a precise match with the stem of at least one
    specified keyword.

<p align="center"><img src="https://juji.io/docs/img/contain-keywords.png" alt="add a contains-keywords trigger" width="450"/></p>


* `contains-sentiment` If a user input contains a positive or
    negative sentiment. <a name="sentiment-detection"></a>

<p align="center"><img src="https://juji.io/docs/img/contain-sentiment.png" alt="add a contains-sentiment trigger" width="450"/></p>

* `matches` If a user input matches a rule specified in [Juji chatbot
    language](https://juji.io/docs/reference).

<p align="center"><img src="https://juji.io/docs/img/matches.png" alt="add a matches
trigger" width="450"/></p>

* `is-anything-else` If a user input matches anything else. This is
    basically the **default** condition.

<p align="center"><img src="https://juji.io/docs/img/default-cond.png" alt="use a default condition" width="450"/></p>

One can check on the box next to the `STORE MATCHED INPUT` to store the
matched input into a **custom attribute**.

As shown below, if a user input contains keywords, such as `milk`,
`egg`, or `cheese`, a custom attribute `like-protein` can be created
to store the matched keyword for each user.

<p align="center"><img src="https://juji.io/docs/img/custom-attribute.png" alt="add custom
attributes" width="650"/></p>

Custom attributes can be used for many purposes, such
as customizing a chatbot message (see below) or indexing audience
information (e.g., showing all users who `like-protein`).

Note that for a **choice request**, since a user's input must be one
of the choices, there is just one type of **IF** condition, the choice made by
the user.


**IMPORTANT TIP**

To decide which type of trigger (chatbot condition) to use, please
check out this [design tip](https://juji.io/docs/chatbot-design-tips-advanced#use-proper-chatbot-trigger).


#### **Customize THEN Actions**

As shown below, when a `IF` condition is met, one or more custom
chatbot actions can be defined:

<p align="center"><img src="https://juji.io/docs/img/custom-action-overview.png" alt="customize chatbot actions overview" width="450"/></p>

<p align="center"><img src="https://juji.io/docs/img/custom-action-detail.png" alt="customize chatbot actions overview" width="450"/></p>

* `Quick Acknowledgement` This defines a simple text message that a
  chatbot can use to acknowledge a user. This simply sends a message
  without waiting for a user's response. This means that any follow-up
  question expression in this message won't be able to elicit any user
  response (unless it is a reflective question without requiring any
  user response). If you wish to ask a follow-up question, add a
  `Follow-up Request`as described below.

* `Extended Reply` This defines a full chatbot message, including image and
  paraphrases, that a chatbot can use to make an extended reply. This
  defines a full topic - a [message topic](#customizing-chatbot-content).

* `Follow-up Request` This defines a chatbot request that allows the
  chatbot to ask a follow-up question. This defines a full topic - a
  request topic.

### **Chatbot Actions**

Besides customizing a chatbot's response to user input, you can also customize a chatbot's actions before or after the chatbot sends a message to users.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/customize-chatbot-action-1.png" alt="customize chatbot actions prior to sending a message" width="550"/></p>


<p align="center"><img src="https://juji.io/docs/img/juji-studio/customize-chatbot-action-2.png" alt="customize chatbot actions after sending a message" width="550"/></p>


Use these actions to run background options. For example, a chatbot collects a user input (e.g., date of birth) and wants to check whether such an input is consistent with the user's previous input. To do so, one can customize a chatbot's action (post action) after collecting the user's date of birth. This post action will compare the current user input with the previous input. Sometimes certain actions may need to be performed before a chatbot sends a message to user. For example, if a chatbot wants to calculate a tax on a particular purchase, it may need to retrieve the tax rate per the user location. In this case, one could define a custom action (prior action) to retrieve the tax rate before sending a message to tell the user the total purchase price.


### Topic Settings

You can also customize one or more topic-specific parameters, such as whether a "request" topic requires user response and the length of user responses. Please refer to [best practices](https://juji.io/docs/quality-chatbot-design-tips) to fine tune these parameters.

<a name="topic-settings"></a><p align="center">
<img src="https://juji.io/docs/img/design-topic-settings.png" alt="design topic settings"
width="550"/></p>


## Delete a Topic

To delete a topic, mouse hover the corresponding topic card listed in
the left topic panel. Then click on the red trash can icon to delete
the topic. A deletion is permanent and cannot be undone.

<p align="center"><img src="https://juji.io/docs/img/design-delete-topic.png" alt="delete a
topic" width="350"/></p>

## Clone a Topic

To clone a topic, mouse over the corresponding topic card listed in
the left topic panel. Then click on the green clone icon to clone the
topic. The cloned topic will retain all behavior of the original topic.

<p align="center"><img src="https://juji.io/docs/img/design-clone-topic.png" alt="clone
a topic" width="350"/></p>

## View Topic Relationship

Although the chat flow is presented a list of topics, but the inter-connected topics actually form a graph. When the complexity of the chat flow grows, the need to see the relationship among topics grows also. Juji Studio provides two convenient tools for users to visualize and examine the topic graph. The two icons on top of the topic list leads to a text and a graph view of the topic graph.

<p align="center"><img src="https://juji.io/docs/img/chatflow-topic-icons.png" alt="Chatflow topic icons" width="350"/></p>


### **View Topic Text List**

<p align="center"><img src="https://juji.io/docs/img/topic-list-text-icon.png" alt="Topic text list icon" width="350"/></p>

Click on the Topic Text List icon, you will see all the topics represented in a textual format in a new browser tab. You can copy or download these text for detailed analysis.

<p align="center"><img src="https://juji.io/docs/img/topic-list-text-view.png" alt="Topic text list view" width="700"/></p>

### **View Topic Graph**

<p align="center"><img src="https://juji.io/docs/img/topic-list-graph-icon.png" alt="Topic graph icon" width="350"/></p>

Click on the Topic Graph icon, you will see all the topics represented in a graph visualization in a new browser tab. Each node in the graph represents a topic.  You can drag the nodes around, pan and zoom in/out the graph. Click Reset button to change the graph layout. Click Center button to re-center the viewpoint. Click Legend button to toggle on/off the legend of the graph. You can also change how long you want the node label to be by choosing a Label Size.

<p align="center"><img src="https://juji.io/docs/img/topic-graph.png" alt="Topic graph" width="700"/></p>

When you click on one of the graph nodes, not only the node turns yellow, the corresponding topic editor in the design view is also selected and open. So you can use the topic graph as a convenient topic navigator for editing topics.

Here is how to do it: first drag out the topic graph tab as a window, then lay this window side by side with the design view, or lay it top and down with the design view. The idea is to show both windows at the same time, so you can use the topic graph to navigate between topics for editing.

<p align="center"><img src="https://juji.io/docs/img/topic-graph-as-navigator.png" alt="View topic graph and topic editor at the same time" width="700"/></p>


## Type of Chatbot Request

Although one can write any type of conversation topics in
Juji, below we list the types of chatbot requests currently supported in
[Juji Studio](https://juji.io/docs/juji-studio/).

<p align="center"><img src="https://juji.io/docs/img/juji-studio/chatbot-request-type.png" alt="displays a list of chatbot request types to be described below" width="550"/></p>

### **Free-text Request**

Perhaps the most used request for an AI chatbot is to pose free-text,
open-ended questions during a chat. Such a question can elicit diverse
and detailed user responses to gather in-depth insights and better
understand users' needs and wants.

<a name="request-label"></a>As shown below, a free-text request includes the following:

* **Label** Typically, a label is the short form ("stem") of a chatbot
request. Although it automatically takes the form of the main message,
it is good to give a sensible label as it is also used for multiple
purposes (see [best practices](https://juji.io/docs/quality-chatbot-design-tips)).

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

See [best practices](https://juji.io/docs/quality-chatbot-design-tips) on how to phrase free-text
questions in a conversation.

<p align="center"><img src="https://juji.io/docs/img/design-add-free-text-q.png" alt="add a
free-text question" width="850"/></p>

### **Choice Request (Radio Buttons)**

One of the popular chatbot request is to ask a user to make a
choice. Below is an example of a single answer, multiple choice
request, also known as radio button question, where a user can select
only one choice.

As shown below, this type of choice question contains:

* **Main Message** (required)

* **Option Items** (at least one item is required to be selected by user)

<p align="center"><img src="https://juji.io/docs/img/juji-studio/radio-button-definition.png" alt="define a radio button question" width="550"/></p>

<p align="center"><img src="https://juji.io/docs/img/juji-studio/choice-question-options.png" alt="define various options of a choice question" width="550"/></p>

In addition to adding regular option items, `Other` option can be added to
let a user specify additional text. One can also indicate whether to
treat all the option items as numbers. Numeric choices can be used to
define chatbot conditions involving numeric operations, such as `>=`
and `<`. See [examples](#examples-customizing-chatbot-actions) below on defining chatbot conditions. There are other options that can be set to control the display of choice items (e.g., displaying the items in a random order or horizontally).

Depending on where the chatbot is deployed, the look of a choice
question may be different.

A choice question displayed in a web-based chatbot:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/radio-button-in-chat.png" alt="preview a web-baed radio button question" width="650"/></p>

A choice question displayed in a web-based chatbot with items laid out horizontally:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/radio-buttons-in-chat-horz.png" alt="preview a web-based radio button question with a horizontal display of choice items" width="650"/></p>

A choice question displayed in a **Facebook Messenger chatbot**:

<p align="center"><img src="https://juji.io/docs/img/preview-choice-q-fb.png" alt="preview a Facebook choice question in Facebook Messenger" width="350"/></p>

In Facebook Messenger, a user may enter a text message instead of
clicking on a choice. In such a case, the chatbot will handle the user
text input first. Since a Juji AI chatbot tracks a conversation
context, it will repeat the question, if the choice question is a
required one.

Below is an example chat where the user asks a question intead of
making a color choice. The chatbot answers the user question and then
repeats the choice question.

<p align="center"><img src="https://juji.io/docs/img/preview-choice-q-fb-fallback.png" alt="Handling user digression during Facebook choice question" width="350"/></p>

### **Choice Request (Checkbox)**

Similar to the radio buttons shown above, another popular choice question is multi-answer, multiple-choice question, also known as checkbox question. This type of choice question allows users to check one or more boxes as the answer.

Below shows how to define a checkbox question.
<p align="center"><img src="https://juji.io/docs/img/juji-studio/checkbox-definition.png" alt="define a checkbox question" width="550"/></p>

This is how a checkbox question looks like in a chat:
<p align="center"><img src="https://juji.io/docs/img/juji-studio/checkbox-in-chat.png" alt="a checkbox question displayed in a chat" width="550"/></p>

### **Facebook Choice**

Semantically, a Facebook choice question is essentially the same as a regular
choice question except that it takes the form of Facebook buttons in a
Facebook Messenger chatbot. This type of request will ***not*** be
displayed in a web-based chatbot.

As shown below, a Facebook choice question includes:

* **Title** (required) This is the main asking message.
* **Subtitle** (optional) This adds more information to the question.
* **Button** (at least one button is required)
* **Image** (optional) An image URL can be added with the question.

<p align="center"><img src="https://juji.io/docs/img/design-add-FB-choice.png" alt="add
Facebook choice buttons" width="350"/></p>

Here is how a Facebook choice looks like in a Facebook Messenger
chatbot:

<br><p align="center"><img src="https://juji.io/docs/img/preview-fb-choice.png" alt="preview Facebook choice buttons" width="350"/></p>

### **Facebook Email**

This special request enables a chatbot to gather opt-in user email in
a Facebook Messenger chatbot. A user must click on the displayed email
to confirm (opt-in) his/her email. A user can also text an alternative
email. To allow users to skip this question, set this question `not
required` in the [topic settings](#topic-settings).

<p align="center"><img src="https://juji.io/docs/img/design-add-FB-email.png" alt="add a
Facebook email requestion" width="650"/></p>

## Type of Chatbot Message

Again, one can write almost any type of chatbot messages (e.g., multi-modal, information graphics, etc.), below we list the message types currently supported by Juji Studio.

<p align="center"><img src="https://juji.io/docs/img/juji-studio/chatbot-message-type.png" alt="displays a list of message types to be described below" width="550"/></p>

### **Web Media Card**

For a website chatbot, one can define a multimedia message with a
combination of text, image or video, and URLs. As shown below, the web media
card contains:

* **Image** or **Video** (required)
* **Text Message** (optional)
* **Hyper Link** (optional, up to 3 URL links)


<p align="center"><img src="https://juji.io/docs/img/juji-studio/web-media-card.png" alt="add a web
media card" width="550"/></p>

Below is the preview of a web media card with an image:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/preview-web-media.png" alt="preview web media
" width="550"/></p>

### **Web Media Carousel**

Sometimes, one may wish to display several images or videos side by side like a carousel. This can be easily done in Juji Studio by simply clicking on the "+" button at the end of a web media card to add additional cards. One can add up to 5 media cards and they will be displayed as a carousel of images/videos in a chat.

An image carousel:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/image-carousel.png" alt="an image carousel in a chat
" width="550"/></p>

A video carousel:

<p align="center"><img src="https://juji.io/docs/img/juji-studio/video-carousel.png" alt="a video carousel in a chat
" width="550"/></p>


### **FB Media Card**

For a FB Messenger chatbot, one can define one or more FB
Media cards to display a combination of text, image, and URL links. As
shown below, each card contains:

* **Title** (required field)

* **Subtitle** (optional)

* **Image** (optional image URL)

* **URL Buttons** (up to 3 links per card)

<p align="center"><img src="https://juji.io/docs/img/design-add-FB-media.png" alt="Facebook Media Card" width="550"/></p>

Currently one can define up to three FB Media cards. In a Facebook
Messenger window, these cards will show up in a carousel.

<p align="center"><img src="https://juji.io/docs/img/design-fb-media-desktop.png" alt="FB media card carousel" width="550"/></p>

Note that FB Media cards will ***not*** show up if the chatbot is
deployed on a website.


## **Special Topics**

To help jump start the design of a chatbot, Juji has made two special topics:
* [Welcome Topic](./#welcome-topic). This is the **first topic** in all Juji AI assistant templates. It cannot be removed. It sends the first chatbot message to users when a chat session starts. One can however customize the welcome message.

* [Wrap-up Topic](./#wrapup-topic). This is the **last topic** in all Juji AI assistant templates. It cannot be removed. It sends the last chatbot message to users when a chat session ends. One can customize the wrap up message as well as the chat ending options.

### Welcome Topic

No matter whether you use a blank template or a task-specific Juji template to create a chatbot, every chatbot comes with two pre-built topics, the **Welcome** topic that starts a conversation and the **Wrap-up** topic that ends a conversation.

To start a good or warm conversation, you may wish to edit the default messages in the **Welcome** topic to suit your context. Please refer to [this recorded webinar](https://youtu.be/Aw_S2-xi8Tc) to see how to phrase custom welcome messages for different use cases.

#### **Suspend Current Chat**

For various reasons, you may want to pause a chatbot before letting it
interact with your audience again. You can do so easily in the **Welcome** topic:

* Click on the **`Welcome`** card

* Click on the slider under the welcome message (on the right panel) to suspend a chat. See the screenshot below.

* Edit the welcome message accordingly to inform users about the suspension/pause.

<p align="center"><img src="https://juji.io/docs/img/suspend-chatbot.png" alt="Suspend chat" width="650"/></p>

**IMPORTANT TIP** If your chatbot is deployed via a web URL, you may also want to change the greeting message on the [web cover page](https://juji.io/docs/juji-studio/release#deploy-to-website) to inform future users about the pause/suspension.

### Wrap-up Topic

Another Juji built-in topic for every chatbot is the **Wrap-up**
topic. One may want to customize a chatbot's ending behavior. For
example, a chatbot that conducts an interview or conversational survey
may want to end the conversation once the interview or survey is
done. In contrast, a customer support chatbot must hang around all the time to
serve customers.

To customize the ending behavior, click on the **`Wrap-up`**
topic, the last topic in the left topic panel.

<p align="center"><img src="https://juji.io/docs/img/wrapup-topic.png" alt="Wrapup topic to end a chat" width="250"/></p>

Then click on the text bubble or the `pencil` icon to edit the topic:

: **Option 1: Make a chatbot stick around**

<p align="center"><img src="https://juji.io/docs/img/custom-end-1.png" alt="customize end of chat: option 1" width="550"/></p>


: **Option 2: End a chatbot**

<p align="center"><img src="https://juji.io/docs/img/custom-end-2.png" alt="customize end of chat: option 2"
topic buttons" width="550"/></p>

If you decide to end a conversation, you also have the option to redirect the ending to a custom URL of yours. Just enter the URL where you want the ending will be.



## What's Next

Once a chatbot is ready, you can deploy it onto a website or a
Facebook page. Please check out [**Chatbot Deployment**](../release)
to deploy your AI chatbot. If you wish to further customize your chatbot, such as its capabilities to handle user questions, please refer to [**Customize QA**](../customize-qa). If you wish to customize the chatbot's persona or other settings, please refer to [**Customize Chatbot Persona**](../customize-persona-beyond/).
