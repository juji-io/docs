# Chat Scripting

The Juji platform has many built-in capabilities for creating a
full-fledged conversational agent for most common use cases. When your needs go
beyond these built-in capabilities, Juji put in your hands a simple yet expressive
language called REP, so that you can harness the full power of the platform.
Additionally, Juji platform contains an integrated development environment (IDE) for
working with REP scripts.

## Write Custom Topic

<p align="center"><img src="../img/change-wording.png" alt="Change wording" width="600"/></p>

In the editing dialog of a question, click on `Write Custom Topic`
link, a topic editor is expanded in place.

<p align="center"><img src="../img/custom-topic.png" alt="Custom topic" width="600"/></p>

The topic editor contains a skeleton of a topic that you may edit to fill in
rules to handle user's responses to this question.

Click `Compile` to compile and any syntax error will be reported.

## Work with Full REP Scripts

At https://juji.io/ide, you have access to an online scripting environment.

<p align="center"><img src="../img/ide-custom.png" alt="IDE" width="600"/></p>

### File Browser

On the left side of the environment, you have a file browser showing all your scripts
and config files. The files are organized by the bot applications you have
created, each called an `Engagement`.

Each `Engagement` contains a `Config` document, which reflects the [Design
View](design.md) of the bot; a `Preivew` release, which has the script powering
the preview chat; and a number of `Web`, `Facebook`, or `Slack` releases, which
are your production releases of the bot scripts.

### Code Editor

On the right side of the environment, there is a code editor containing the file
you select in the file browser. The editor has syntax highlighting, rainbow
parentheses, and brackets mismatch errors are detected on the fly while you are typing.

#### Custom script file

The custom script file has a namespace ending in `.custom`. Such a file is where
your custom topics are saved. You can also freely write your own topics and
functions in that file.

You can `Upload` a file to replace the file, or `Download` the file to your
local disk, or `Save` the file in the Juji platform.

#### Main script file

<p align="center"><img src="../img/ide-custom.png" alt="IDE" width="600"/></p>

The main script file of a release has a namespace ending in something like
`.web2`, where `web` the name of the release channel, and `2` means the second
release of this engagement in that channel.

In addition to `Upload`, `Download`, and `Save`, the main script also supports
`Compile` and `Preview` functionality, where you can see your script in action
immediately.

#### Config document

This document shows the high level structure and content of your engagement.
Sometimes it is easier to edit content in the config document rather than in the
script files.

When click `Generate Script` pull down menu, a new release can directly be
created right there.
