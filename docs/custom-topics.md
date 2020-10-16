# Custom Topics

Advanced chatbot designers can create their own mini dialog to be used on the Design page through custom topics. Designers can obtain full control on those custom topics without writing the entire script. Moreover, customization performed on the Design page will be automatically put on top of the custom topics. So designers can enjoy the benefits of both worlds.

To use custom topics, there are two steps:

1. [Write the custom topics](#write-a-custom-topic)
2. [Select the custom topic you want to use on the Design page](#use-custom-topic-on-the-design-page)

## Write A Custom Topic

Custom topics can be defined inside the custom script file in the IDE for each engagement. The custom script file has a namespace ending in `.custom`. Below is an example custom script that defines one custom topic. 

```clojure
(ns juji-doc-random0.eng1.custom
  (:require 
    [juji.expressions.rep.personality :as personality]
    [juji.topics.interviewing.v4 :as interviewing]))

(deftopic ask-general-question-customed
  [?q]
  {:custom-topic
   {:description "Ask about shop experience"
    :type "request"
    :sub-type "free-text"}}
  []
  [(ask-question ?q)]
  (handle-user-response ?q))

(deftopic handle-user-response
  [?q]
  {:include-after [(interviewing/handle-interview-fallback ?q)],
   :default-rules ([(ask-for-more? ?q)]
                   [personality/_rep-ask-for-more
                    (record-answer ?q (input-text))
                    (update-ask-for-more-counter ?q)]
                   (interviewing/handle-ask-for-more 1)
                   (*recur*)
                   [+]
                   [interviewing/_rep-ack (record-answer ?q (input-text))])}
  [my first time]
  ["Welcome, please feel free to ask me questions." (record-answer ?q (input-text))])
```

A mini dialog usually consists of a topic to ask the question (asking topic) and a topic to handle the users' responses (handling topic). In order to create a custom topic for the mini dialog, simply add a `:custom-topic` field to the asking topic's option map. Inside the `:custom-topic` field, the designer needs to define the description of the custom topic (which will be show on the Design page when selecting the custom topic) and optionally the `:type` and `:sub-type` of the custom topic. Only "free-text" sub-type is supported at this moment. Make sure the namespaces used are properly declared (see `interviewing` and `personality` in the example above), otherwise the custom script will fail to compile. Once you are done defining your custom topic, click "Save" button in the IDE to save it.

## Use Custom Topic on the Design Page

Once the custom topics are defined inside the engagement's custom script and saved, they can be used on the Design Page. 
<p align="center"><img src="../img/open-mini-dialogue-selection.png" alt="Open up mini dialogue selection popup to select the custom topic" width="650px"/></p>
Simply select the "free text" topic of choice, and click on the magnifying glass to open up a popup window for mini dialogue selection. Inside the popup window, the defined custom topics can be searched and selected.
<p align="center"><img src="../img/select-defined-custom-topic.png" alt="Select defined custom topic" width="650px"/></p>
After being selected, the defined custom topic will be used for this chat topic. Further customization can be added on the Design page as usual. The customization done on the Design page on this chat topic will be combined with the defined custom topic during conversation.