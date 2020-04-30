# **Deploy AI Chatbot**

Juji AI chatbots can be deployed to a website or to a Facebook
Messenger on a Facebook page.

## **Deploy to Website**

When deploying a chatbot to a website, one can customize the **web
cover** page. As shown below, one can edit the **welcome message** and
configure the fields to be shown on the cover page:

* First Name (required)
* Last Name (optional)
* Email (optional)


<p align="center"><img src="/img/web-cover.png" alt="Web Deployment" width="650"/></p>

Use the `Generate URL` button to generate a web URL. This URL can then
be embedded into an email or a website for target audience.

<p align="center"><img src="/img/web-url.png" alt="generate URL" width="650"/></p>

Two URLs are generated:

* **Test URL** Give this URL to testers so that the chat data can be
  identified as test data easily.

* **Regular URL** Use this URL for target audience. 

### **Customize Web URL with External Data**
In some cases, you may want to customize the generated chatbot URL
with additional information for various purposes. For example, if you
use a chatbot to conduct surveys or onboard customers, you may want to
append a unique user id to the chatbot URL and send this URL to
qualified participants or customers.  You can also append additional
information, such as source or session information, to track where the
users obtained your chatbot URL.

It's super easy to pass such external information to Juji. You just
need to append the information to the chatbot URL. For example, the
following Juji URL is appended with `?source=email` to identify that
this chatbot URL will be emailed to the target audience:

`https://juji.ai/pre-chat/5df866e6-e911-4924-b9e1-7440038825c6?source=email`

In contrast, the following indicates the URL will be posted on
Linkedin:

`https://juji.ai/pre-chat/5df866e6-e911-4924-b9e1-7440038825c6?source=linkedin`

Juji will automatically capture such *external* information in its
reports. For example, two entries below from the CSV report file show
the captured source information (see [how to download a CSV
report](/reports)).

<p align="center"><img src="/img/capture-external-info.png" alt="capture external information" width="650"/></p>

## **Deploy to Facebook Page**

One can deploy a Juji chatbot to a Facebook Messenger associated with
a Facebook page.


<p align="center"><img src="/img/facebook-deployment.png"
alt="Facebook Deployment" width="650"/></p>

Similar to deploying to a website, one can also edit the **weclome
message** shown up in a Facebook Messenger. Click on the green
`Checklist` to make a Facebook page ready to host a chatbot.

Use the blue `Connect with Facebook` button to deploy a
chatbot. Select the page(s) you want to deploy to. Then click on the
green `Deploy` button to complete the deployment.

<p align="center"><img src="/img/select-fb-page.png" alt="Select facebook page to deploy" width="650"/></p>

If there is no page listed, it means that you have not given Juji
permissions to any of your Facebook pages to host your
chatbots. In that case, click on the green `Connect More` button to
select Facebook pages and give permissions. The permitted pages should
then show up in the list and you can then select one or more to deploy a
chatbot to.  

## **Update Deployed Chatbot**
It's possible that a chatbot needs to be updated after its
deployment. For example, you may want to add a new chatbot question or
update the wording of an existing chatbot request. To push the new
updates to the deployment, Juji supports two types of update:

* **Update Existing Release** Use the `Update` button on the Facebook
    deployment page (see below) or the one under the
    `Manage` button to push the updates to the existing chatbot. The
    updated chatbot will restart and reflect the changes made.

### **Update Facebook Chatbot**
<p align="center"><img src="/img/deploy-fb-after.png" alt="After
successful facebook deployment" width="650"/></p>

<br>

### **Update Web Chatbot**
<p align="center"><img src="/img/web-update.png" alt="Update Web AI chatbot" width="650"/></p>

* **New Release** Use the `Connect with Facebook` button or `New
    Release` button under `Manage` to release a new version of the
    chatbot. A new release version will be created.


### **Best Practices**

How do you decide whether to update a chatbot vs. to make a new
release or version of the chatbot?  While the decision is completely
up to you, we recommend that you normally just `update` a chatbot
without making a new release/version of it. If you make substantial
changes, such as adding questions or attributes, to a chatbot, we
recommend that you make a new release of the chatbot
(basically with a new version number). This is because data fields
(e.g., chatbot questions or custom attributes) could be very different
between two releases and you don't wish to mix the old and new data
together. Making a new release will also facilitate easier comparison
of audience behavior under different chatbot versions.

Note that the current [Reports](/reports) page shows the audience
information for the most recent release/version of chatbot. If you
make a new release, currently you may not be able to access the audience
information for previous releases.

## **What's Next**

Once a chatbot is deployed, you can monitor its status and the
associated audience information. Please check out [**Report
Dashboard**](reports.md) to deploy your AI chatbot. 

