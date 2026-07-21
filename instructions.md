# Develop your own agent with Copilot Studio

This lab teaches you how to create and enhance a custom AI-powered customer service agent using Microsoft Copilot Studio. You'll start by learning to create a new agent, add content, and explore the fundamentals of **Message** and **Question** nodes, entities, slot filling, and variables, essential for building interactive conversational agents.

As you progress, you'll integrate external data sources and services with your agent. You'll use Power Automate to request data from other sources and return it in a conversational dialog. You'll also understand the basics of the **HTTP Request** node and how to retrieve information from external services. By pointing your agent to your website and other knowledge sources, you'll make it smarter and more capable of providing accurate information, guided by custom prompt instructions.

Finally, you'll explore advanced features like using plugin actions to interact with other data sources and invoking AI Builder prompts to analyze customer feedback. These skills will enable you to create a highly functional customer service agent that handles complex tasks and provides valuable insights. By the end of this lab, you'll understand how to leverage Microsoft Copilot Studio to improve customer service efficiency and support an organization's growing needs.

## Architecture

!IMAGE [auc6ybi7.jpg](instructions353330/auc6ybi7.jpg)

## Exercises

This lab has the following exercises:

- Create your first agent in Microsoft Copilot Studio.
- Learn basic authoring.
- Build and call Power Automate cloud flows from your agent.
- Make HTTP requests to connect to an API.
- Leverage knowledge sources, AI knowledge, and custom instructions
- Use generative AI orchestration to interact with your connectors.
- Invoke AI Builder prompts


## Prerequisites

For running this lab, you'll need:

- Power Platform Environment with Dataverse enabled
- Microsoft Copilot Studio Trial Subscription activated within Power Platform environment
- Power Automate
- Access to Azure OpenAI services

## Customer story

Contoso, Inc. leases specialty medical equipment to hospitals throughout the Northwestern United States. Founded in 2005 with headquarters in Seattle, WA, the company has grown significantly over the years. They now support over 900 hospitals and more than 15,000 individuals, providing essential medical equipment.

Despite their success, Contoso has faced challenges in recent years due to a surge in demand for their services. Keeping up with their promises of excellent customer service and 24-hour turnaround on service contracts has become increasingly difficult. The company has outgrown its current customer service and service deployment tools, leading to issues such as staff capacity problems, and increased workload for Customer Service Reps.

To address these challenges and improve customer service efficiency, Contoso, Inc. decides to implement a new AI-powered customer service agent using Microsoft Copilot Studio. The goal is to create a scalable solution that can handle the current and future workload, streamline the process of managing equipment maintenance requests, and enhance the overall customer experience.

By leveraging the capabilities of Microsoft Copilot Studio, Contoso aims to reduce the workload on Customer Service Reps, improve response times, and provide more accurate and timely information to their customers. This initiative will help Contoso maintain its reputation for excellent customer service and support its continued growth in the medical equipment leasing industry.

===

# Exercise 01: Create your first agent in Microsoft Copilot Studio

> [!alert] For learners who are newer to Copilot agents and Copilot Studio, we've provided instructions (Task 01, Key Task 03) that will allow you to import a pre-built agent. This preconfigures everything built in Exercises 01-04.

## Scenario

Contoso's customer service department has been overwhelmed with increased workloads due to growing customer inquiries. To alleviate the strain on Customer Service Representatives, Contoso decides to create an AI-powered customer service agent.

In this exercise, you'll take the first steps in creating this customer support agent, customizing its tone, establishing conversation boundaries, and connecting it to essential data sources. At the end, you'll test the agent in a simulated environment, ensuring it meets Contoso's requirements for a professional and engaging customer interaction.

## Objectives

After you complete this exercise, you'll be able to:

- Create an agent for customer support, customize its tone, boundaries, and data sources.
- Create a topic, add trigger phrases, and use the authoring user interface.
- Publish your agent to a demo website for testing.
- Test your agent, validate its behavior, ensure it meets the expected criteria.

## Architecture

!IMAGE [y19cqq0m.jpg](instructions353330/y19cqq0m.jpg)

## Duration

Estimated time: 60 minutes

===

# Task 01: Set up

### Introduction

Contoso has decided to adopt an AI-driven customer support solution to address increasing customer demands and reduce the workload on customer service representatives. To start implementing this solution, you first need to set up the required environment within the Power Platform. This task involves preparing the necessary foundational components such as Dataverse, enabling you to build the AI-powered agent effectively.

### Description

In this task, you'll configure the Power Platform environment by enabling Microsoft Dataverse and deploying sample apps and data. These components provide the essential foundation for creating and deploying intelligent agents with Microsoft Copilot Studio.

### Success criteria

- You navigated to the Power Platform admin center and signed in with the provided Microsoft 365 credentials.
- You selected the correct environment ("Contoso (default)") and enabled Dataverse with sample apps and data.

===

### Navigate the lab environment


**The Type Text icon**!IMAGE [hut7bsbc.jpg](instructions353330/hut7bsbc.jpg)

Select the icon in the instructions and the Type Text feature will automatically send the specified text to the active window in the virtual machine.

Always compare the text in the instructions with the typed text in the virtual machine to verify that the expected text displays.

For larger code blocks, use the **Copy** button and then paste the text by right-clicking or using **CTRL+V** in the virtual machine.

!IMAGE [q1n1yy18.jpg](instructions353330/q1n1yy18.jpg)

---

**Lab credentials** The credentials required for accessing the virtual environment and the lab-supplied Microsoft 365 tenant are always available at the top of this instructions pane under the **Resources** tab.

---

**Saving your progress** To save your progress, select **Exit Lab** in the upper-right corner of the screen, then select **Save Progress and Exit**. This will ensure that your work is preserved for future sessions.

> [!alert] Selecting **End Lab** will terminate the lab without saving.

---

**Images**

All images in the lab instructions are clickable. By selecting them, you can open a zoomed-in view in a separate window for better clarity and analysis.

---

**Split Windows feature** If you're equipped with multiple screens, you can use the Split Windows feature to place the lab instructions on a separate screen, making better use of your screen real estate.

To enable this feature:

1. Select the **cogwheel** icon in the upper-right corner of this pane.
2. Select **Split Windows** at the bottom of the **Settings** pane.

This will help you keep the virtual machine and instructions visible simultaneously for a more efficient workflow.

===

## Key tasks

### 01: Set up Power Platform

1. [] Sign in to the virtual machine with the following credentials:

    | Item | Value |
    | ---- | ----- |
    | Username | **Admin** |
    | Password | +++@lab.VirtualMachine(Win11).Password+++ |

    > [!hint] Select the **+++Type Text+++** icon throughout the lab to enter the associated text into the virtual machine.
1. [] Open Microsoft Edge, then go to `admin.powerplatform.microsoft.com`.
1. [] Sign in with your lab credentials:

    | Item | Value |
    | ---- | ----- |
    | **Username** | `@lab.CloudPortalCredential(User1).Username` |
    | **Password** | `@lab.CloudPortalCredential(User1).AccessToken` |

    >[!alert] This password is labelled **TAP** (Temporary Access Password) in the **Resources** tab, not **Password**.

1. [] Close or skip the various dialogs.

1. [] On the left service menu, select **Manage**.

    !IMAGE[ptvw5d8o.jpg](instructions353330/ptvw5d8o.jpg)


1. [] Select **New** on the top bar.

    !IMAGE[ex5cc9z8.jpg](instructions353330/ex5cc9z8.jpg)

1. [] In the **Add Dataverse** flyout pane, enter the following:

    | Item | Value |
    | ---- | ----- |
    | **Name** | `Contoso` |
    | **Type** | **Developer** |

1. [] Select **Next** at the bottom of the flyout pane.

    !IMAGE[v9clvkr4.jpg](instructions353330/v9clvkr4.jpg)

1. [] Select the toggle for **Deploy sample apps and data?** to change to **Yes**, then select **Save**.

    !IMAGE[4s1g6wzt.jpg](instructions353330/4s1g6wzt.jpg)

    >[!alert] Sample data must be deployed for a later exercise.

    >[!Note] This environment is where Copilot Studio will store data associated with your custom agent.
    
1. [] Wait until the **Contoso** environment's **State** column shows **Ready**.

    Periodically select **Refresh** on the top bar.

    !IMAGE[5dnaso6h.jpg](instructions353330/5dnaso6h.jpg)

    > [!alert] This may take around 15 minutes.
    > 
    > If not **Ready** after 25 minutes, please exit and relaunch the lab.

<!-- 1. [] Select **Contoso**.

    !IMAGE[e5bu7qed.jpg](instructions353330/e5bu7qed.jpg)

1. [] In the URL highlight and copy the environment ID as shown in the image.

    !IMAGE[kgo4aqbx.jpg](instructions353330/kgo4aqbx.jpg)

1. [] Paste the copied value into the following text box:

    @lab.TextBox(environmentId)

    >[!alert] This value will be used for future reference in the instructions. -->

===

### 02: Configure SharePoint

1. [] Open a new browser tab, then go to `lodsprodmslearnmca.sharepoint.com/_layouts/15/sharepoint.aspx`.

1. [] On the top bar, select **Create site**.

    !IMAGE[0xrade28.jpg](instructions353330/0xrade28.jpg)

1. [] In the dialog, select **Communication site**.

    !IMAGE[slo14p0m.jpg](instructions353330/slo14p0m.jpg)

1. [] Select the **Standard communication** template.

    !IMAGE[efsn9xrx.jpg](instructions353330/efsn9xrx.jpg)

1. [] In the lower-right corner of the dialog, select **Use template**.

1. [] Enter the following details:

    | Item | Value |
    | ---- | ----- |
    | **Site name** | `Mark 8 Project Team` |
    | **Site description** | `The team dedicated to the Mark 8 Project.` |
    | **Site address** | `Mark8ProjectTeam@lab.LabInstance.Id` |

    >[!alert] This specific **Site address** will be referenced again in a future exercise.

1. [] Select **Next**.

    !IMAGE[3p4zhots.jpg](instructions353330/3p4zhots.jpg)

1. [] Select **Create site**.

1. [] On the top site navigation, select **Documents**.

    !IMAGE[vmbp21cm.jpg](instructions353330/vmbp21cm.jpg)

1. [] On the top bar, select **Upload**, then select **Folder**.

    !IMAGE[e02t4bz2.jpg](instructions353330/e02t4bz2.jpg)

1. [] Go to `F:\LabFiles`, select **SharePointFiles**, then select **Upload**.

    !IMAGE[obmhqpbt.jpg](instructions353330/obmhqpbt.jpg)

1. [] Close the tab after upload.

===

### 03: Switch to the new environment in Copilot Studio

<!-- 1. [] Open a new browser tab, then go to `copilotstudio.microsoft.com/environments/@lab.Variable(environmentId)/home`. 

    >[!alert] This URL uses the referenced environment ID from the previous step to take you directly to the new environment.
-->

1. [] Open a new browser tab, then go to `copilotstudio.microsoft.com`.

1. [] Select your region, then select **Get Started** in the dialog.

    !IMAGE[2wpmxbz5.jpg](instructions353330/2wpmxbz5.jpg)

1. [] Close or skip any additional dialogs.

1. [] In the upper-right corner of the page, select **Environment**, then select **Contoso** from the flyout pane.

    !IMAGE[9ss0n2g0.jpg](instructions353330/9ss0n2g0.jpg)

    >[!note] Depending on screen resolution, you may need to select the globe icon to select between environments.
    > 
    >!IMAGE[2vtc4d6s.jpg](instructions353330/2vtc4d6s.jpg)

    >[!alert] If you don't see **Contoso**, verify the environment is **Ready** in Power Platform, then refresh the Copilot Studio page.

===

### 04: (Optional) Use Power Apps to upload a pre-built agent

> [!alert] You can **optionally** import an agent to use as a starting point for your lab exercises. This completes all the steps from **Exercise 01** to the end of **Exercise 04**. You'll need to download and import a custom solution for this.
> 
> If you import a custom solution, please observe all the following exercises, regardless, to learn how everything is configured. Also follow along with the various tests of the agent.

1. [] In the leftmost menu of Copilot Studio, select **Agents**.

    !IMAGE[r1ke7iim.jpg](instructions353330/r1ke7iim.jpg)
1. [] In the upper-right part of the page, select **Import agent**.

    !IMAGE[sph5rnfi.jpg](instructions353330/sph5rnfi.jpg)

    > [!note] This will open the **Solutions** page in a new tab.
1. [] Select **Import solution** on the top bar.

    !IMAGE [moe1wmsq.jpg](instructions353330/moe1wmsq.jpg)
1. [] Select **Browse** in the new pane.
1. [] In the top address bar, select the empty white space to the right of **Admin >** to change the file path, then enter `F:\LabFiles\Solution`.

    !IMAGE [hm9457xm.jpg](instructions353330/hm9457xm.jpg)
    !IMAGE [azmn5hg6.jpg](instructions353330/azmn5hg6.jpg)

    > [!note] Alternatively, expand for navigating through the folders manually:
    > 1. In the left pane, move down to under **This PC**, then select **AllFiles (F:)**.
    >
    > !IMAGE [584vjaji.jpg](instructions353330/584vjaji.jpg)
    > 1. Double-click **LabFiles**.
    > 2. Double-click **Solution**.
1. [] Select **TechExcel_1_0_0_1.zip**, then select **Open**.

    !IMAGE [lgzy4xfe.jpg](instructions353330/lgzy4xfe.jpg)
1. [] Select **Next** in the lower-left corner of the pane.

    !IMAGE [2v1q61qq.jpg](instructions353330/2v1q61qq.jpg)
1. [] Select **Import** in the lower-left corner of the pane.
1. [] Wait until you see a yellow warning banner under the top bar upon completion. The warning can be safely ignored.

    !IMAGE [pzpw58yh.jpg](instructions353330/pzpw58yh.jpg)
    !IMAGE [ll25ki7o.jpg](instructions353330/ll25ki7o.jpg)

    > [!alert] It may take a couple of minutes to complete the import of the agent.

    >[!Note] This is the definition of the agent, not the running version. This comes with various internal components that you'll explore in the upcoming exercises.

1. [] After the import finishes, close the **Solutions** page tab to return to Copilot Studio.
1. [] Select **Home** in the leftmost menu.

    !IMAGE[xwnx4ab5.jpg](instructions353330/xwnx4ab5.jpg)

===

# Task 02: Create an agent

### Introduction

With the Power Platform environment prepared, your next step is to create a customer support agent for Contoso. This task involves defining the agent's purpose, customizing its tone and limitations, and specifying external knowledge sources. Completing these steps ensures the agent is tailored to Contoso's specific support scenarios and customer interactions.

### Description

In this task, you'll use Microsoft Copilot Studio to define and create your first AI-driven agent. You'll specify the agent's purpose, tone, conversational boundaries, and data sources, preparing it for initial testing.

### Success criteria

- An agent is created within Microsoft Copilot Studio.
- The agent's purpose, tone, and boundaries are clearly defined.
- External knowledge sources are successfully integrated.

===

## Key tasks

### 01: Create an agent

1. [] In the text box at the top for **What would you like to build?**, enter the following prompt, then select **Enter**:

    `I want to create an agent for my customer support. It is an assistant for Contoso customers, helping to answer common questions and helping with common tasks, like checking order status.`

    !IMAGE[etfhu0m3.jpg](instructions353330/etfhu0m3.jpg)

    >[!Note] You'll be redirected to a conversational experience to further customize your agent.

    >[!alert] If prompted to wait before submitting your request, please wait a few moments and try again. If the issue persists, expand the following dropdown menu for additional instructions on manually creating your agent.

<details markdown="block">
<summary>Select to expand for details on manually creating your agent instead.</summary>
>
> 1. [] On the leftmost pane, select **Create**.
>
>     
>     !IMAGE [1sft3n3h.jpg](instructions353330/1sft3n3h.jpg)
>
> 1. [] On the **Create** page, select **New agent** near the upper-left corner of the page.
>
>     !IMAGE [ydxyyexc.jpg](instructions353330/ydxyyexc.jpg)
> 1. [] In the upper-right corner of the page, select **Create**.
> 1. [] In the upper-right corner of the page, select **Skip to configure**.
>
>     !IMAGE [u0i18dp7.jpg](instructions353330/u0i18dp7.jpg)
> 1. [] In the upper-right corner of the page, select **Create**.
> 1. [] In the upper-right corner of the page, select **Settings**.
>
>     !IMAGE [uej9ptsa.jpg](instructions353330/uej9ptsa.jpg)
>
> 1. [] On the **Settings** pane, select **✨ Generative AI**.
> 1. [] Under **How should your agent interact with people?**, select **Generative**, then select **Save**.
>
>     !IMAGE [kuqxivm6.jpg](instructions353330/kuqxivm6.jpg)
> 1. [] Proceed to the next task.
</details>

> [!alert] Note that the following steps may be in a different order for you, as the responses will vary. The agent may not even ask some of the questions. Be sure to input all four of the following prompts, regardless of the order.

1. [] If asked, confirm the agent's main purpose, or enter the following again:

    `It is an assistant for Contoso customers, helping to answer common questions and helping with common tasks, like checking order status.`
1. [] Enter the following to set up the agent's tone:

    `Playful tone, joyful, customer focused, but definitely professional.`
1. [] Enter the following to set up its boundaries and limitations:

    `We don't want to discuss other brands like Fabrikam. Never provide product comparisons with competitor technologies.`
1. [] Enter the following prompt to set up publicly accessible data sources:

    `Information should come from https://learn.microsoft.com/en-us/microsoft-copilot-studio and from https://www.microsoft.com/en-us/microsoft-copilot.`

1. [] Select **Create** in the upper-right corner of the window.

    !IMAGE [hliew081.jpg](instructions353330/hliew081.jpg)

>[!Note] You can also choose to avoid the conversational creation experience by selecting **Skip to configure**. You can set the agent's primary language in the **Edit language** menu. For the lab, be sure to remain in English (en-US). It's best practice to always configure your agent in the context of your own solution and publisher, so that the agent is created with the desired publisher prefix, and so you can easily export the agent and deploy it to other environments.

===

# Task 03: Take a quick tour of the user interface

### Introduction

After creating your customer support agent, the next step is to familiarize yourself with the Microsoft Copilot Studio user interface. Understanding the UI is essential for effectively managing and authoring topics, configuring actions, and monitoring agent performance.

### Description

In this task, you'll explore the primary components of the Copilot Studio user interface, including key navigation areas such as agent creation, topic management, actions, analytics, channels, settings, and testing.

### Success criteria

- You've successfully navigated the main Copilot Studio pages.
- You understand the primary functions and sections of the Copilot Studio user interface.

### Learning resources

Microsoft Copilot Studio makes it easier for you to build basic to advanced agents. The following section reviews the main pages of the maker experience for Microsoft Copilot Studio.

===

## Key tasks

### 01: Learn about the main pages of Copilot Studio

!IMAGE [w7c2lfe1.jpg](instructions353330/w7c2lfe1.jpg)

!IMAGE[75cdh408.jpg](instructions353330/75cdh408.jpg)

####**A**
- **Home** - Microsoft Copilot Studio home page where you can start creating new agents from. It contains the list of recent agents, a list of agent templates to get you started, and learning resources. 
- **Create** - This menu gives you the conversational agent creation experience. 
- **Agents** - List of all the agents you have access to in the environment. 

####**B**
- **Overview** - Description of the agent, its instructions, and a quick view of its configuration (knowledge sources, topics, actions, publish status, and so on). 
- **Knowledge** - Where you manage the agent knowledge sources (such as websites or files). 
- **Tools** - Building blocks that enable your agent to interact with external systems.
- **Topics** - Where you manage custom and system topics. Topics are the core building blocks of an agent. Topics can be seen as the agent competencies: they define how a conversational dialog plays out. Topics are discrete conversation paths that, when used together, allow users to have a conversation that feels natural and flows appropriately. 
- **Analytics** - Where you can view metrics to monitor how well your agent is serving your users and identify ways to improve it. 
- **Channels** - Where you configure how your agent is made available to your users (for example, Teams or a website). 
 
####**C**
- **Environment** - Where you can identify the Power Platform environment you're working from. You would typically create and author an agent in a development environment and deploy it to test and production environments. 

####**D**
- **Publish** - Where you can make the latest version of your agent available to your users. Apart from the test pane, changes are not reflected to your end users if you haven't published the agent. 
- **Settings** - Where you can manage your agent configuration (such as advanced settings, security, and language). 

####**E**
- **Test your agent** - Where you can immediately test your agent and your customizations, even without saving. 

===

### 02: Learn about the Copilot Studio settings interface

First, go to the Settings under the Contoso environment:
!IMAGE[1nczryfz.jpg](instructions353330/1nczryfz.jpg)

This is the settings interface:
!IMAGE[b9yfql7a.jpg](instructions353330/b9yfql7a.jpg)

1. **Agent details** - Where you can update the agent display name, icon, and modify advanced settings (for example, configure the Azure Application Insights integration)
2. **Generative AI** - Where you can choose to replace the more classic natural language understanding approach for topic triggering and entity extraction with one that's based on a large language model to do multi-intent detection and more complex entity extraction. This is also where you can configure content moderation settings for knowledge sources (to reduce risks of hallucinations).
3. **Security** - Where you can share your agent with other users (to co-author it) or with security groups (to use it). This is also where you configure end-user authentication settings (the type of authentication and whether it's enforced), and web channel security, that allows you to further secure the Direct Line channel that's used for any web or custom application deployment.
4. **Entities** - Copilot Studio has many pre-built entities to help identify key information in a user utterance (for example, a city, date, or number). This menu is also where you can define your own closed-list entities or regular expression entities.
5. **Skills** - Where you register external Bot Framework skills that your Copilot Studio agent can call, or where you can configure how existing Azure Service Bot can use your Copilot Studio agent as a skill.
6. **Languages** - Where you can configure additional languages your agent can be used in and localized into.
7. **Language understanding** - Where you can configure custom language models developed and trained on Azure AI Language in Azure Conversational Language Understanding (CLU). When configured, this effectively replaces the out-of-the-box natural language understanding model (NLU) for intent detection and can also replace entity detection and extraction.

===

## Task 04: Test your agent

### Introduction

With the initial setup and configuration completed, you now need to verify that the agent responds as intended. In this task, you'll test basic interactions to ensure the agent correctly interprets and responds to common user inputs, reflecting the intended customer service experience for Contoso.

### Description

In this task, you'll use the built-in testing tool in Microsoft Copilot Studio to interact with your agent. You'll test various conversation scenarios to verify that your agent responds appropriately to user prompts.

### Success criteria

- You've successfully tested basic conversational scenarios with the agent.
- You've validated that the agent responds correctly according to defined settings.

===

## Key tasks

### 01: Test your agent

1. [] If not automatically opened, select the agent you just created.

    !IMAGE[amwg0gf4.jpg](instructions353330/amwg0gf4.jpg)

    > [!alert] For those using the optional pre-built agent:
    > 1. Select **Agents** in the left menu.
    > 2. Select **Contoso Customer Assistant**.
    >     !IMAGE [u7pa6xhw.jpg](instructions353330/u7pa6xhw.jpg)
1. [] You can always access the **Test your agent** pane by selecting **Test** in the upper-right corner of the window.

    !IMAGE [kxr7ggrb.jpg](instructions353330/kxr7ggrb.jpg)

    > The **Test your agent** pane shows that a message has already been sent to you from the agent. This message was sent from the **Conversation Start** topic, which begins automatically.
1. [] In the bottom text box of the **Test your agent** pane, enter `Hello`, then select **Enter**.

    !IMAGE [z2vj3ymd.jpg](instructions353330/z2vj3ymd.jpg)

> [!knowledge]
> You can select messages in the test pane to get redirected to the exact topic and node it was used in. You'll learn about topics and nodes shortly!
> 
> !IMAGE [729n5mfr.jpg](instructions353330/729n5mfr.jpg)

===

# Task 05: Create your first topic

### Introduction

To address specific customer inquiries and requests at Contoso, you need to create customized conversation topics. In this task, you'll define a topic tailored to handling customer queries, such as checking order status, enabling the agent to manage real-world customer service scenarios effectively.

### Description

In this task, you'll manually create a new topic within Microsoft Copilot Studio, define trigger phrases, set up **Question** and **Message** nodes, and verify the conversational flow.

### Success criteria

- You've successfully created a new conversational topic.
- You've configured trigger phrases, **Questions**, and **Message** nodes correctly.
- You've verified the topic behavior through agent testing.

===

## Key tasks

### 01: Create a new topic manually In this first task, you'll manually create a new topic.

1. [] Select **Settings** near the upper-right corner of the page.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] **Generative AI** will be selected on the left settings menu.
1. [] Under **Use generative AI orchestration for your agent's responses?**, select **No**, then select **Save** at the bottom of the page.

    !IMAGE[csqibrhu.jpg](instructions353330/csqibrhu.jpg)
1. [] Once successfully saved, select the **X** in the upper-right corner of the **Settings** page.

    !IMAGE [umzvacg5.jpg](instructions353330/umzvacg5.jpg)
1. [] Select **Topics** on the top bar.

   !IMAGE[ywtwri24.jpg](instructions353330/ywtwri24.jpg)

1. [] Select **Add a topic**, then select **From blank**.

    !IMAGE[942c4tda.jpg](instructions353330/942c4tda.jpg)

1. [] Rename your topic title by selecting **Untitled** in the upper-left corner of the window, then enter `Check Order Status`.

    !IMAGE[kqtmp893.jpg](instructions353330/kqtmp893.jpg)

1. [] Within the **Trigger** node, under **User says a phrase**, select **Edit**.

    !IMAGE[vosmicht.jpg](instructions353330/vosmicht.jpg)

1. [] Under **Add phrases**, enter the following, then select **Enter** or the **+** button for each phrase.
    - `order status`
    - `track my order`
    - `where is my package`
    - `check order status`
    - `has my order shipped`

    !IMAGE [ycn03ej5.jpg](instructions353330/ycn03ej5.jpg)
1. [] Select the **Details** button in the upper-right of the main canvas pane.

    !IMAGE [qd9alxfd.jpg](instructions353330/qd9alxfd.jpg)

    > [!note] This is where you can set a different **Display name** (what the end user will see) from the configured topic **Name** (what the maker sees).
    > The **Display name** is used in case of disambiguation (for example, when multiple topics match a user utterance, the user is prompted to choose between two or three recognized topics, with a "Did you mean..." question.
    > 
    > When generative AI orchestration is used instead of the built-in natural language understanding for topic triggering, the display name is called the Model display name and is used in addition to the Model description as part of the intent detection process.
    > 
    > The **Details** pane is also where you can configure topic input and output variables. This is useful when the topic is invoked by another topic, or when generative AI orchestration is turned on, effectively using a large language model to slot fill the necessary variables and automatically prompt the user for missing inputs.
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

    !IMAGE [541830on.jpg](instructions353330/541830on.jpg)

===

### 02: Review the topic user interface

Now that you've created your first topic, albeit without content except trigger phrases, you can explore the authoring user interface (UI) to become more familiar with it.

!IMAGE[8sz95l4f.jpg](instructions353330/8sz95l4f.jpg)

1. **Topic title** - The name of the topic you're currently editing, visible on the **Topics** page.

1. **Productivity bar** - Where you have access to tools, such as cut, copy, paste, and delete for the nodes (**Messages**, **Questions**, and so on).

1. **Copilot**, **Comments**, **Variables**, **Topic checker**, **Details**, **Analytics**, **Open code editor**, and **Reset to default** buttons - This area includes: Copilot, which helps you create and update topics using descriptions in natural language; **Comments**, where authors can collaborate and leave comments on nodes; the **Variables** menu, to see the list of topic-level and global variables, and their runtime value in the test tab; **Topic checker**, which you can run anytime from the authoring canvas to check if errors have occurred in your topic that the platform can detect (and if left unresolved would prevent you from publishing the agent); and **Details**, to access the topic properties.

1. **More** - Analytics shows topic usage metrics; Open code editor switches the user interface from a no-code/low-code experience to a pro-code view of the underlying YAML configuration of the topic that developers can edit directly. For some system topics, a Reset to default option is available to revert the topic content to its original state.

1. The **Save** button saves the topic changes.

1. The **Topic details** menu allows the agent author to update the topic Name, Display name, Description, and Status (active/inactive). When generative AI orchestration is enabled, the display name is replaced with model display name, and model description becomes available. This menu also allows the configuration of inputs and outputs. The inputs can be automatically slot filled when using generative AI as the orchestrator.

1. The **trigger switcher** button is present at the **Trigger** node of every topic. By default, new topics have the **Phrases** trigger (or are triggered by Copilot, when generative AI orchestration is enabled), but this can be switched to Message received, Event received, Activity received, Conversation update received, Invoke received, Redirect, and Inactivity.

1. **Add a new node** - Allows the agent author to add activities to a topic, such as sending a message, asking a question, and adding a condition, to build the dialog logic.

1. **Authoring canvas controls** - You can use these controls to navigate the authoring canvas, which can become large for extensive topics. The included controls are a map of the canvas, zoom, hand, selection, and reset.

===

### 03: Add content to your topic

This task doesn't cover how to add a large amount of content to your topic; rather, it provides the steps to add a single **Question** node, **Message** node, and topic redirection so that you can become familiar with the overall process of creating a topic, testing, and publishing in Microsoft Copilot Studio. A subsequent exercise has more in-depth information about the authoring capabilities in Microsoft Copilot Studio.

The next section of this task covers foundational knowledge for understanding the central components of Microsoft Copilot Studio and creating topics.

As the author of an agent, you should use the **Question** node when you're expecting a response from the user, and you want to do something based on that information. The user response is stored in a variable, and **Question** nodes can also use entities and slot filling features, concepts that are covered later in this exercise.

The **Question** node uses many functions that a **Message** node does, such as rich text, speech authoring, and rich text response types such images, videos, and Adaptive Cards.

1. [] Select the **+** button below the **Trigger** node in the canvas, then select **Ask a question** to add a new **Question** node.

   !IMAGE[j2zeqhor.jpg](instructions353330/j2zeqhor.jpg)

1. [] In the text box, enter:

    `What would you like to do with your order?`

1. [] Select the entry under **Identify**, then select **User's entire response**.

    !IMAGE [dmcb0hkl.jpg](instructions353330/dmcb0hkl.jpg)

    >[!Note] This node is asking the question after the topic is triggered about what the user wants to do. An upcoming exercise extends this task to using entities and slot filling.

1. [] Under **Save user response as**, the user response is saved as a variable named **Var1** by default.

    Select **Var1**, then for the **Variable name** enter `OrderRequest`.

    !IMAGE [wipm194z.jpg](instructions353330/wipm194z.jpg)

    >[!Knowledge] It's best practice to always properly name variables so they can be clearly identified when you reference them in your logic. It also adds clarity when doing tests and checking the variable values at runtime.
    > 
    > Customers and partners can define and follow naming conventions for their variables, for consistency and ease of maintenance.

    >[!Knowledge] Question behavior can be customized by selecting the ellipsis, **Properties**, and **Question behavior**. From here, you can define if the question can be skipped, how many times it should be re-prompted to the user, validation rules, and what should happen if the user doesn't answer as expected.
    > 
    > You can also define whether a user can jump to another topic without answering the question, and you can define the list of topics that are allowed in case of interruption. It's best practice to define retry prompts in case the user doesn't understand what's expected from them the first time. It's then appropriate to be much more explicit with the user when trying to help them properly answer a question.
    > 
    > **Fundamental knowledge: Message node**
    > - You can use the **Message** node to display a message to the user. This message can be simple based on the topic of the conversation. In direct contrast to the **Question** node, the **Message** node doesn't expect or store an answer from the user. The **Message** node also has rich text options that you can display in text, or advanced options like cards, images, videos, and Adaptive Cards.

    > [!Knowledge] To make the agent sound more natural and human, you can configure message variations, so that the agent will send one of the configured messages, avoiding strict repetition of the same message.
    > 
    > You can also use variables within **Message** nodes in the body of text displayed to the user, which is dynamic based on the data stored within the variables. This capability allows messages to be more personal, such as **Hello {System.User.FirstName}, I can get those order details for you, one moment**.
    > 
    > Variables can also store data to perform automation or calculations on them. Later exercises cover variables in more depth.
    > 
    > Lastly, you can also add Power Fx formulas to create even more dynamic content.
1. [] Select the **+** button below the **Question** node, then select **Send a message** to create a **Message** node.

    !IMAGE [qk402n2v.jpg](instructions353330/qk402n2v.jpg)
1. [] Enter a message that acknowledges the customer's question:

    `Thank you for your question!`
1. [] Select the **+** button below the **Message** node, select **Topic management**, select **Go to another topic**, then select **End of Conversation**.

    !IMAGE [wawkk3oa.jpg](instructions353330/wawkk3oa.jpg)

    >[!Note] This will redirect to a topic dedicated to ending a chat session, asking if the question has been answered, and suggesting filling out a customer satisfaction survey.

    >[!Knowledge] It's best practice to end discrete dialog paths with the **End of Conversation** topic. That way, the end-user can confirm their question was addressed. When a user confirms, a customer satisfaction (CSAT) survey is displayed. Resolution rates and CSAT scores are both displayed in the agent analytics.
1. [] In the upper-right part of the canvas, select **Save** to save the topic.

    !IMAGE [pvfulgjl.jpg](instructions353330/pvfulgjl.jpg)
1. [] In the **Test your agent** pane, select the **+** icon in the upper-right corner of the pane to start a new conversation.

    !IMAGE[4g2qz7km.jpg](instructions353330/4g2qz7km.jpg)
1. [] Enter this prompt twice to validate that the agent behaves as expected.

    `I'd like to check the status of my order please`

    !IMAGE [hp9tmjye.jpg](instructions353330/hp9tmjye.jpg)


>[!Knowledge] Trigger phrases don't need to be an exact match of all the utterances a user might say.

===

### 04: Use Copilot to create a topic

Creating topics in Microsoft Copilot Studio is more effortless than before. Now, you can create a topic in Microsoft Copilot Studio by using natural language to describe what you want the topic to do. With the **Create from description with Copilot** feature, you can automatically build a topic, reducing some manual steps that you experienced from the first task in this exercise. In this task, you'll learn how simple and quick creating a topic with Copilot can be.

1. [] Select **Topics** on the top bar.

    !IMAGE[ywtwri24.jpg](instructions353330/ywtwri24.jpg)
1. [] Select **Add a topic**, then select **Add from description with Copilot**.

    !IMAGE[iahygm7t.jpg](instructions353330/iahygm7t.jpg)
1. [] Enter the following in the new window:

    | Item | Value |
    | ---- | ----- |
    | **Name your topic** | `Support Ticket` |
    | **Create a topic to** | `Create a support ticket, including a title, severity (high / medium / low), description and an email address to send update notifications to. Define variables following this naming pattern: Topic.TicketTitle.` |
1. [] Select **Create** in the lower-right corner of the pane

    !IMAGE [dndgz6g7.jpg](instructions353330/dndgz6g7.jpg)

    >[!Note] Copilot creates your topic, including trigger phrases, **Question** nodes, entity selection, variable naming, and **Message** node confirmation.

1. [] If the **Edit with Copilot** pane is not already open, select **Copilot** at the top of the canvas.

    !IMAGE [j7xhdf8b.jpg](instructions353330/j7xhdf8b.jpg)
1. [] In the **Edit with Copilot** pane, under **What do you want to do?**, add the additional instructions below, then select **Update**.

    `Before the last message, ask a question to find out the user's preferred contact method, choosing from email, phone or SMS.`

    !IMAGE [50zag8tq.jpg](instructions353330/50zag8tq.jpg)

    >[!Note] Copilot automatically adds a **Question** node at the bottom of the canvas, which asks the customer for their contact method and stores their choice in a variable.

    !IMAGE [lomv7en4.jpg](instructions353330/lomv7en4.jpg)

    > [!alert] Skip this step if you run into the following error:
    > 
    > !IMAGE [p17qtbu1.jpg](instructions353330/p17qtbu1.jpg)

    > [!knowledge] The Copilot feature in Microsoft Copilot Studio drastically reduces authoring time, allowing you to create new topics and edit topics by using natural language.
    > 
    > Additionally, the **Edit with Copilot** panel shows what updates have been created, and it provides suggestions for what you can update in your topic.

1. [] Select **Save** in the upper-right part of the canvas to save the topic.

===

# Task 06: Publish your agent to the demo website for testing

### Introduction

To gather initial feedback from stakeholders at Contoso and validate the agent's readiness, you need to publish your newly created agent to a demonstration website. This step allows for practical testing in a simulated environment, helping ensure the agent meets customer service requirements.

### Description

In this task, you'll publish your Microsoft Copilot Studio agent to a demo website. You'll configure authentication settings, perform the publishing action, and validate that the agent is accessible and operational on the demo site.

### Success criteria

- You've successfully configured authentication settings for the demo environment.
- You've published the agent to the demo website.
- You've validated that the agent is accessible and responding correctly through the demo website.

===

## Key tasks

### 01: Change your agent authentication

For the purposes of this demo, you'll set the agent to not require authentication so that anyone with a link to the demo site can test it.

1. [] Select **Settings** near the upper-right part of the window.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] On the left settings menu, select **Security**.
1. [] Select **Authentication**.

    !IMAGE[9hriz8sx.jpg](instructions353330/9hriz8sx.jpg)
1. [] Select **No authentication**, then select **Save**.
    >[!Note] This option may be configured by default, which is why the **Save** option may not be enabled.

1. [] Select the **X** near the upper-right corner of the **Settings** page to return to your canvas.

    !IMAGE [1d72mmuf.jpg](instructions353330/1d72mmuf.jpg)

===

### 02: Publish your agent

Microsoft Copilot Studio provides a demo website so that you can invite anyone to test your agent by sending them the URL. This demo website is useful for gathering feedback to improve your content before you activate the agent for your real end-users.

1. [] Select **Channels** on the top bar of your agent.

    !IMAGE[wq0hbgbz.jpg](instructions353330/wq0hbgbz.jpg)

    > [!knowledge] After publishing your agent at least once, you can add channels to make it reachable by your customers.

1. [] Select **Publish** in the upper-right part of the window to push the latest topic updates to the demo website.

    > [!note]You'll need to complete this action before using the demo website for the first time, and after making any changes to the topics you want users to test.

    !IMAGE [eb2pkfbw.jpg](instructions353330/eb2pkfbw.jpg)

    >[!Knowledge] **Pro tips**:
    > - When you create a real agent, you'll publish whenever you want to make updated topics available in your deployed channels.
    > - The publishing process checks for errors in the topics whose Status is **On**.
    > - Publication should take only a few minutes.

1. [] Select **Publish** again on the dialog that opens. You can ignore the risk from the lack of end-user authentication.

    !IMAGE [hrz08hdi.jpg](instructions353330/hrz08hdi.jpg)

    > [!note] A green banner notification will show at the top of the screen when publishing is complete.

    > [!knowledge] Publishing to the demo website is a quick process, but publishing an agent for real-world use (for example, in Microsoft Teams) can take longer.
    > 
    > For Teams, you may need to initiate an approval workflow as an administrator before the agent is made available to users in the Teams channel. The publishing process ensures that all updates are properly validated and deployed across the environment.
    > 
    > See here for more details: [Publication fundamentals for publishing channels](https://learn.microsoft.com/en-us/microsoft-copilot-studio/publication-fundamentals-publish-channels?tabs=web)
1. [] Select the ellipsis in the upper-right corner of the agent page next to **Settings**, then select **Go to demo** website.

    !IMAGE [idixvii7.jpg](instructions353330/idixvii7.jpg)
1. [] You can interact with the agent by typing in the chat window, or by selecting a starter phrase from the options provided on the left.

    !IMAGE[z04d0gr6.jpg](instructions353330/z04d0gr6.jpg)

===

## Summary

Congratulations on completing Exercise 01! You've successfully:

- Set up the Power Platform environment and enabled Dataverse.
- Started a free Copilot Studio trial in the correct environment.
- Created - or optionally imported - a customer‑support agent.
- Explored the Copilot Studio UI and key settings.
- Published the agent to the demo website and validated basic conversations.

===

# Exercise 02: Learn basic authoring

## Scenario

After successfully setting up the basic Copilot Studio agent, Contoso now needs the agent to handle specific customer inquiries about equipment orders.

This exercise focuses on expanding the agent's capabilities by teaching it to recognize different customer requests. You'll define custom entities, implement slot-filling techniques to automatically extract information from customer messages, and configure variables to dynamically manage conversations. This refinement helps streamline Contoso's service request handling, significantly reducing manual input from service reps.

## Objectives

This exercise covers the following topics:

- Learn the fundamentals of the message and **Question** nodes.
- Discover the fundamentals of entities and slot filling.
- Learn how to use variables in Microsoft Copilot Studio.
- Explore the extensibility capability, including Power Fx and extended node properties.

## Architecture

!IMAGE [0v38i4o1.jpg](instructions353330/0v38i4o1.jpg)

## Duration

Estimated time: 60 minutes.

# Task 01: Use entities and slot filling

### Introduction

To enhance your agent's ability to handle common inquiries from Contoso's customers efficiently, you'll import content directly from Contoso's existing website. This task helps the agent leverage accurate, consistent, and already-approved customer service information, streamlining responses to frequent customer requests.

### Description

In this task, you'll use Microsoft Copilot Studio to import content from a website. Copilot Studio analyzes the webpage content and generates suggested conversational topics automatically, reducing manual content creation.

Microsoft Copilot Studio uses natural language understanding (NLU) to interpret what a user
is saying to try and match a user's utterance with an existing topic.

If a user says, "I tried to use my gift card, but it doesn't work", the agent knows to
route the user to the topic that's related to gift cards not working, even if that exact
phrase isn't listed as a trigger phrase. This concept can also be referred to as **intentrecognition**.

NLU can also help the agent identify **entities** in a user's input. An entity represents
key information you're trying to extract from a sentence. This can be a phone number, a zip
code, a city, a case ID, a person's name, and so on. Your agent can recognize the relevant
information from a user input and then save it for later use.

Two types of entities:

- **Prebuilt** - Represents the most\-used information\, such as age\, color\, number\, and
    name. Microsoft Copilot Studio can recognize these entities automatically.
- **Custom** - These are entities that you create\. While the prebuilt entities cover
    commonly used information types, you'll sometimes need to teach the agent's natural
    language understanding model some domain-specific knowledge. For instance, you might need
    to create a list of all your product types. Or you may want to configure an entity to
    recognize specific text patterns like "INC-921279" for an IT support ticket.

### Example Scenario

If the user types, "I want fifty red coffee machines" the AI can understand that:

- "**Fifty**" is the number "50," and it's also the number of products to purchase.
- "**Red**" is a color and is the color of the products to purchase.
- "**Coffee machine**" refers to the product that the person wants to purchase.

In Microsoft Copilot Studio, some subjects (such as numbers and colors) have already been
taught to the AI for the agent. The author of the agent would need to specify other
entities, such as the fact that "coffee machine" is a product.

### Success criteria

- You've successfully imported topics from the provided website.
- You've reviewed and confirmed the topics created from the imported content.

===

## Key tasks

### 01: Use entities and slot filling

1. [] Go back to your **Microsoft Copilot Studio** tab.
1. [] Select **Settings** again near the upper-right part of the window.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] On the left settings menu, select **Entities**.
1. [] Select **Add an entity** at the top, then select **New entity**.

   !IMAGE[b5l5j24h.jpg](instructions353330/b5l5j24h.jpg)
1. [] In the **Create an entity** dialog, select **Closed list**.

    !IMAGE [rgkbkerp.jpg](instructions353330/rgkbkerp.jpg)
1. [] In the **Name** field, enter `OrderAction`.
1. [] Under **List items** in the right pane, enter the following and select **Enter** or **Add** for each of the three items.
    - `Update`
    - `Check`
    - `Cancel`

    !IMAGE [3chp3mme.jpg](instructions353330/3chp3mme.jpg)

    > [!note] You can also choose to add synonyms by selecting synonyms for each option (optional for this task).
1. [] Select the **Smart matching** toggle to set it to **on**, then select **Save** in the lower-right corner of the window.

    !IMAGE [3r762pgl.jpg](instructions353330/3r762pgl.jpg)

    > [!note] This creates a new entity called **Order Action** that you can use with the **Question** node in your topic to place the **User's entire response** with the **Order Action**.
1. [] Select **Close** on the pane, then select the **X** in the upper-right corner of the **Settings** page to return to your agent.

    !IMAGE [sja295bl.jpg](instructions353330/sja295bl.jpg)
1. [] Select **Topics** on the top bar.
1. [] Select the **Check Order Status** topic you created.

    !IMAGE[qmd9be3b.jpg](instructions353330/qmd9be3b.jpg)
1. [] Within the **Question** node, select the entry under **Identify**, then search for and select the new `Order Action` entity.

    !IMAGE [6c3fe3cs.jpg](instructions353330/6c3fe3cs.jpg)
1. [] Select **Select options for user**, then select all the checkboxes to display them to the user.

    !IMAGE [hvjcfgpi.jpg](instructions353330/hvjcfgpi.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

***

You've successfully configured a custom entity for your **Question** node. By default, if the variable assigned to store the question's response already contains a value, the question is skipped and not presented.

===

# Task 02: (Optional) Test and address ambiguity issues

### Introduction

Customer conversations may sometimes be ambiguous, potentially causing confusion in the agent's responses. In this optional task, you'll test and address such ambiguity by refining the agent's ability to clarify customer inputs, improving response accuracy.

### Description

You'll test ambiguous conversation scenarios, identify where the agent struggles to interpret user intent, and adjust the agent's configuration to clarify or prompt users for more information when necessary.

### Success criteria

- You've tested ambiguous inputs.
- You've improved agent responses to clarify customer intent accurately.

===

## Key tasks

### 01: Test and address ambiguity issues

> [!alert] If you created the agent, skip this task. This is only for users who imported the pre-built solution.

You'll use the **Test** pane to see how entities and slot filling works by entering one of your trigger phrases.

1. [] In the **Test your agent** pane, select the **+** icon in the upper-right corner of the pane to start a new conversation.
1. [] Enter the following trigger phrase.

    `Order status`
1. [] If prompted, select one of the options it provides.

    !IMAGE[jkr4f5fg.jpg](instructions353330/jkr4f5fg.jpg)

    You may get a disambiguation question using the pre-built agent (for example, *"Did you mean…"*, asking to select the most relevant topic) because two or more topics have been configured with similar trigger phrases related to **orders**.

    >[!Knowledge] **Pro tip**: To avoid this ambiguity in your agent, you can:
    > - Deactivate one of the overlapping topics.
    > - Update the trigger phrases of the overlapping topics.
    > - Exclude a specific topic from the disambiguation mechanism, by going to the desired topic's Phrases properties, advanced, and unchecking **Include in multiple topic matches**.
    > - Fine tune your topic strategy by setting up catch-all parent topics that then use redirects to call the appropriate child topics, after applying your own disambiguation questions.
1. [] Go to your **Topics**.
1. [] On the line for **Lesson 3...**, toggle off **Enabled**.

    !IMAGE[sb5jzb7b.jpg](instructions353330/sb5jzb7b.jpg)
    
    > [!note] In the list of topics, a visual indicator shows what topics are disabled.

===

# Task 03: Test slot filling

### Introduction

To confirm the accuracy of information collection from customers, you'll test the slot filling capabilities of your agent. This helps ensure that the agent correctly identifies and stores critical details from customer interactions for Contoso's service requests.

### Description

You'll systematically test conversations that utilize slot filling to verify the agent accurately prompts and collects user-supplied information.

### Success criteria

- You've tested and validated slot-filling interactions.
- You've confirmed accurate collection and storage of required customer information.

===

## Key tasks

### 01: Test slot filling

1. [] In the **Test your agent** pane, select the **+** icon again to start a new conversation.
1. [] See how entities and slot filling work by entering a sentence matching one of your trigger phrases.

    `Can I check on an order?`
1. [] Select **Variables** on the top bar of the canvas.

    !IMAGE[i9g0hm6p.jpg](instructions353330/i9g0hm6p.jpg)
1. [] In the **Variables** pane, select the **Test** tab, then select **Topic** to expand.

    !IMAGE [umex618d.jpg](instructions353330/umex618d.jpg)

    > [!note] You'll see the process is working because the user has triggered this topic with the intent to "Check" an order, and the entity has been slot filled into the variable from the follow-up question after the trigger phrase.
    > 
    > As a result, the question is not asked and is skipped. This is because you used entities and slot filling to retrieve the information from the utterance the user submitted. This approach avoids you needing to ask the user a question that they've already provided information for.

===

# Task 04: Use variables

### Introduction

Contoso's customer service scenarios often require storing temporary information during interactions.

### Description

In this task, you'll configure conversation variables, enabling the agent to retain and use customer-provided details effectively throughout a conversation. You'll create and utilize conversation variables within Copilot Studio to temporarily store and reuse information provided by customers during interactions.

### Success criteria

- You've created and implemented variables within conversational topics.
- You've confirmed correct handling and storage of variable data during conversations.

===

## Key tasks

You're beginning to enhance the topic that you created in the previous section, where you used entities and slot filling to automatically detect the data from a user's sentence and store specific data in a variable. Now, you'll learn how to use the data that you obtained from the question in a variable and then display it within a message.

### 01: Learn about variable types

Variables let you save responses from your end-users to help guide the conversation (such as determining whether to provide different instructions for returns based on the purchase price of the item). And you can use them directly in the conversational response from the agent (for example, "I can help you return your {Topic.ProductName}").

By default, you can only use a variable's value in the topic where the variable is created. However, if you want the agent to reference the same value across other topics, you can choose to make it a global variable (you might know this concept from other applications). Basically, when the conversation moves to a different topic, the agent can remember and use variable values that have been filled in from previous topics in the conversation. In Microsoft Copilot Studio, you can set up variables by using Power Fx formulas and functions, outside of a **Question** node, by using the **Set a Variable Value** node.

Different types of variables in Microsoft Copilot Studio include:

- **System** - These variables are normally populated with system data\. System variables aren't user\-made and are part of the platform\. For example\, if your agent requires end\-user authentication\, system variables may include user ID\, email\, first name\, and so on\. You can access system variables in the authoring canvas from the variable selection\, under System\.

- **Topic** - These variables are user\-made from either topic Inputs\, the **Set a Variable Value** node, the **Question** node or as the output of other nodes or actions (for example, cloud flows, HTTP requests, connectors, custom prompts, and plugin actions). These variables are by default limited in scope and available only in the topic that's being created and no other topics. Two options are available to expand this scope for topic variables if they can receive values from other topics and return values to other topics. With these options set, a topic variable is no longer limited to only being used in the topic; other topics can use it. You can access topic variables in the authoring canvas from the variable selection, under **Custom**.

- **Global** - These variables are user\-made and are available from any topic\, and they're a good way to store data that multiple topics use to help the conversation\, regardless of how many topics are triggered within it\. If you embed your agent in a website or application\, you can pass context data (for example\, current page or user language\) as global variables to your agent\, if these are configured to accept external sources setting values for them\. You can access Global variables in the authoring canvas from the variable selection\, under **Custom**.

You can use variables in several places, including the **Question**, **Condition**, and **Set variable value** nodes. The variable can be a custom value that uses Power Fx, a user-entered value, a response from a question, or system variable values.

===

### 01: Review variables

Use this task to become familiar with the **Set variable value** node and to review the different types of variables. This task involves creating a new node, creating a new variable, renaming the variable, and determining other variables that you can use within Microsoft Copilot Studio at the system level. At the end of this task, you'll delete this node.

1. [] Under the **Trigger** node, select the **+** button, select **Variable management**, then select **Set a variable value**.

    !IMAGE [u8kzm7gk.jpg](instructions353330/u8kzm7gk.jpg)

    > [!note] This task is for exploring variable options, so it isn't critical that you add the variable in a specific location. You'll delete it later.
1. [] Under **Set variable**, select **Select a variable**, then select **Create new** in the flyout pane.

    !IMAGE[2secptwt.jpg](instructions353330/2secptwt.jpg)

    > [!note] Your new variable is made and is, by default, called **Var1** (or a different number if you already created a variable with this name, such as Var2 or Var3).


1. [] Select **Var1**, then for **Variable name** enter `TestDelete`.

    !IMAGE [9wz8bcx8.jpg](instructions353330/9wz8bcx8.jpg)

    >[!Knowledge] It's best practice to name your variables something descriptive based on the data that's being stored. This approach helps you in the future and helps other agent authors.
    > 
    > You can also change the scope of a variable from **Topic** or **Global**.

1. [] Select the **X** in the upper-right corner of the **Variable properties** pane to close it.

    > [!knowledge] Determine what data you can use to store in the variable. You can use other variables that you created in your authoring canvas, or you can use system variables or formulas.

1. [] Under **To value**, select the ellipsis **(...)**.

    !IMAGE[wknlgd0i.jpg](instructions353330/wknlgd0i.jpg)

    > [!note] A flyout pane appears that contains separate tabs named **Custom**, **System**, **Environment**, and **Formula** (using Power Fx, which is covered later in this lab).
1. [] Select the **System** tab.

    !IMAGE [dj4n2z5h.jpg](instructions353330/dj4n2z5h.jpg)

    > [!note] You'll be able to view all variables that Microsoft Copilot Studio uses. These variables contain data that Microsoft Copilot Studio populates, and you can also use this data in your own variables. Review these options so that you know what's available by default.
1. [] Delete the **Set variable value** node now that you reviewed the options available to you within it.

    Select the ellipsis in the upper-right corner of the node, then select **Delete**.

    !IMAGE [dg80rf7i.jpg](instructions353330/dg80rf7i.jpg)
1. [] From anywhere within the authoring canvas, you can select **Variables** at the top to review all variables within the topic, including global variables.

    !IMAGE [imt6ohhm.jpg](instructions353330/imt6ohhm.jpg)

    > [!knowledge] It's beneficial to review all variables within a topic, especially topics that are large.

===

# Task 05: Use global variables

### Introduction

Certain information needs to be accessible across multiple conversation topics for efficiency, such as customer identifiers or common details. Global variables are needed to share critical data seamlessly across Contoso's agent interactions.

### Description

In this task, you'll define global variables in Copilot Studio, allowing information to persist and remain accessible across different conversation topics and sessions.

### Success criteria

- You've defined and configured global variables.
- You've validated accessibility of global variables across multiple conversation topics.

===

## Key tasks

### 01: Use global variables

In this task, you learn how to use the data from the previous task, Check Order Status. At this point, you should have the **Question** node in your topic linked to an entity.

1. [] In the **Question** node, select the **OrderRequest** variable.

    !IMAGE [pbleajip.jpg](instructions353330/pbleajip.jpg)
1. [] In the **Variable properties** pane, under **Usage**, select **Global** so that other topics can access it.

    !IMAGE [s7hwp3n2.jpg](instructions353330/s7hwp3n2.jpg)
    > [!Note]  If a message appears indicating that the variable orderRequest already exists in the global scope, no action is required. The variable is already configured as      **Global**, and      you can proceed to the next step.
1. [] Now use the variable that you configured in the **Question** or **Trigger** phrase in the **Message** node as dynamic data.

    Replace the text in the **Message** node:

    `No problem. We can that for you. Let us take a look at that now and get your information.`

    !IMAGE [w8gl8bvg.jpg](instructions353330/w8gl8bvg.jpg)
1. [] Select and place the text cursor in the space between "**can**" and "**that**" in the message, select the **{x}** variable icon, then select the **OrderRequest** variable.

    !IMAGE [so6d0e5u.jpg](instructions353330/so6d0e5u.jpg)

    !IMAGE [yu797vj4.jpg](instructions353330/yu797vj4.jpg)

    > [!knowledge] It's common to insert a variable in place of words, making the text dynamic based on data provided by the end user.
1. [] Enter the text the following way if you know the value of your variables.

    `No problem. We can {Global.OrderRequest} that for you. Let us take a look at that now and get your information.`

    > [!note] This also fixes a spacing issue between the variable and surrounding words in the previous step.
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] If not open, select **Test** in the upper-right part of the window to test the changes you made by triggering the topic with a trigger phrase.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Enter the following:

    `Help me with an order.`
1. [] Select **Check Order Status**, and then select **Cancel**.

    !IMAGE [orhbswu7.jpg](instructions353330/orhbswu7.jpg)

    !IMAGE [4cfwkv54.jpg](instructions353330/4cfwkv54.jpg)

    > [!note] Note how the **OrderRequest** value still has its first letter capitalized. To address this grammatical issue, you can use a formula to change this to lowercase instead of directly referencing the variable value.
1. [] In the **Message** node, delete the variable value **{Global.OrderRequest}**, then select the **fx** button.
1. [] Enter the following **Lower()** Power Fx formula, then select **Insert**.

    `Lower(Global.OrderRequest)`

    !IMAGE [la5nmy10.jpg](instructions353330/la5nmy10.jpg)

    > [!note] See how the variable values can be referenced within the formula.

    >[!Knowledge] Within the **Variable management** options is the **Clear all variables** option, which clears all variable values. This option is useful if you want to begin or loop back into the same topic but take new values, especially if you set up question behavior properties where a question could be skipped if it already had a value.
1. [] Test again in a new conversation to see the changes.

    `Help me with an order.`

    !IMAGE [33s9wl0w.jpg](instructions353330/33s9wl0w.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

> [!knowledge] **Variables** are the best way to store dynamic data or data that you want to perform conditions or checks on to drive conversational behavior in a particular way, as you'll observe in the next task.

***

Congratulations on completing this task. You've now reviewed variables in Microsoft Copilot Studio.

===

# Task 06: Use variables in conditions

### Introduction

To provide tailored responses based on customer input, Contoso's agent must utilize conditions based on stored data. In this task, you'll configure conversation conditions using variables to dynamically guide the conversation according to specific scenarios.

### Description

In this task, you'll set conditions in conversational topics based on variable values, directing the conversation flow appropriately depending on user inputs or previously collected information.

### Success criteria

- You've created conditional logic based on variable values.
- You've tested and confirmed correct conversational branching based on variables.

### Learning resources

> [!knowledge] For more information on conditions, see [Authoring using conditions](https://learn.microsoft.com/microsoft-copilot-studio/authoring-using-conditions).

===

## Key tasks

### 01: Use variables in conditions

1. [] Under the **Message** node, select the **+** button, then select **Add a condition**.

    !IMAGE [uy1jy7zf.jpg](instructions353330/uy1jy7zf.jpg)

    > [!note] Two new nodes will appear. One is your **Condition** and the other is an exception for **All other conditions**.
1. [] In the **Condition** node, select **Select a variable**, then select your **OrderRequest** global variable.

    !IMAGE [3g6a6ipr.jpg](instructions353330/3g6a6ipr.jpg)
1. [] Keep the condition operator as **is equal to**.
1. [] Select the text box for **Enter or select a value**, then select **Update**.

    !IMAGE[6qtusy5p.jpg](instructions353330/6qtusy5p.jpg)
1. [] Select the **+** button between the **Message** node and the branching **Condition** nodes, then select **Add a condition** to add another branch.

    !IMAGE [fgpypqef.jpg](instructions353330/fgpypqef.jpg)
1. [] In the new **Condition** node, repeat steps 2 and 3, then set the value to **Check**.
1. [] Repeat the same steps to add a **Condition** node for **Cancel**.

    !IMAGE[95syx8z0.jpg](instructions353330/95syx8z0.jpg)
1. [] Under each **Condition** node, select the **+** button, then select **Send a message** to add a **Message** node.
1. [] Set different messages depending on the condition:

    `One moment while I update that order.`

    `Let me check on that order for you.`

    `No problem. Give me just a moment to cancel that order.`

    !IMAGE [bu6892f5.jpg](instructions353330/bu6892f5.jpg)

    >[!Knowledge] Do things faster by selecting a node and copying it using the upper-left productivity tools menu. Once copied, the node is available to be pasted, using the same tools menu or when using the **+** button to add a new node.
    > 
    > !IMAGE [w2dae79c.jpg](instructions353330/w2dae79c.jpg)
    > 
    > !IMAGE [2gz8yl2c.jpg](instructions353330/2gz8yl2c.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Explore the different trigger phrases and conditions that lead the user to view different message outcomes.

> [!knowledge] Conditions are foundational tools that help you create tailored experiences based on what the user has selected or answered in previous questions. You can nest conditions within other conditions for more complex logic.

***

Congratulations, you've now completed the basics of using conditions and using variables as parameters within them.

===

# Task 07: Use topic nodes

### Introduction

Structuring the conversation effectively is crucial for clear customer interactions.

### Description

In this task, you'll use topic nodes to clearly organize the agent's conversation logic, ensuring Contoso's customers receive structured and coherent responses.

### Success criteria

- You've created and organized topic nodes effectively.
- You've verified correct conversational flow in tests.

===

## Key tasks

### 01: Become familiar with topic type nodes

1. [] Select the **+** below the **Topic** node, then select **Topic management** to observe the options.

    !IMAGE[i0klfwxc.jpg](instructions353330/i0klfwxc.jpg)
1. [] Select an empty space in the canvas to cancel out of the menu without creating.

***

In the **Topic management** menu, you have the following:

- **Go to another topic** - This node has an extended flyout menu where you can go to another topic that you need to select.

	{: .important }	
	> **Tips**:  
	>	- It's often more manageable to create many bite-size topics rather than a few large topics. Taking this approach also helps make triggering more effective, by clearly mapping trigger phrases to the specific topics that address those areas. 
	>	- As large topics can be challenging to maintain and update, it's a good idea to break down your agent logic, when possible, especially if parts of your agent conversation logic can be shared by multiple topics. This concept is referred to as reusable topics. 
	>	- Topics don't need to all have trigger phrases, as topics can redirect to other topics and pass variable information back and forth.

- **End current topic** - Selecting this option ends the current topic. Typically, you'd use this option where the topic was called from another topic. It would be returned to where it was originally called from. You can also use this option in branching conditions. If you select this option to end an entire topic of a branch, the behavior operates similar to the **End all topics** node.

- **End all topics** - This node ends all active topics. The next message from the user is considered a new conversation and triggers the most appropriate topic based on that user message, starting a new active topic.

- **Transfer conversation** - Select this option to transfer to an agent and send a contextual message.

- **Go to step** - Allows the author of an agent to navigate to another node in the open topic. This option is useful for looping scenarios or if you want to gather more information from the user.

- **End conversation** - Sends an **endOfConversation** activity. This can be useful for a client chat widget (for example, deployed to your website), to know that the chat session is over.

***

Now that you're familiar with the basics of the topic management functions, you can practice using the **Go to another topic** node for the next task. The **Go to another topic** node is useful when you want to apply other topics from conditions based on what the user asks for in the dialog.

===

# Task 08: Use the **Go to another topic** node

### Introduction

Complex customer scenarios at Contoso often require conversations to transition seamlessly between multiple related topics.

### Description

You'll implement and test the Go to another topic node, enabling smooth transitions between separate but related conversational topics within your agent.

### Success criteria

- You've successfully configured the Go to another topic node.
- You've validated smooth and correct transitions between topics.

===

## Key tasks

In this task, you'll learn how to use the **Go to another topic** node.

### 01: Create a new topic for order cancellations

1. [] Select **Topics** on the top bar.

    !IMAGE[ywtwri24.jpg](instructions353330/ywtwri24.jpg)
1. [] Select **Add a topic** in the upper-left part of the window, then select **From blank**.

    !IMAGE[942c4tda.jpg](instructions353330/942c4tda.jpg)
1. [] Select **Untitled** in the upper-left part of the window, then change the topic name to `Order Cancellation`.

    !IMAGE[qbgtmkdw.jpg](instructions353330/qbgtmkdw.jpg)
1. [] Within the **Trigger** node, hover over the **Phrases** section, then select the **Change trigger** button that appears in the upper-right part of the node.
    
    !IMAGE[nwbh3fo3.jpg](instructions353330/nwbh3fo3.jpg)
1. [] Select **It's redirected to** from the flyout menu.

    !IMAGE[3g2re8h0.jpg](instructions353330/3g2re8h0.jpg)

    > [!note] This topic doesn't need trigger phrases.
1. [] Under the **Trigger** node, select the **+** button, then select **Send a message**.
1. [] Add a message that acknowledges the cancellation.

    `Your order has been canceled, thank you.`

    !IMAGE [yfrzvnpz.jpg](instructions353330/yfrzvnpz.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

===

### 02: Configure a node to go to another topic

1. [] Select **Topics** on the top bar.

    !IMAGE[ywtwri24.jpg](instructions353330/ywtwri24.jpg)
1. [] Select the **Check Order Status** topic.
1. [] Within the **Condition** branch for **Cancel**, below the **Message** node, select the **+** button, select **Topic management**, then select **Go to another topic**.

    !IMAGE [iuzgi0zi.jpg](instructions353330/iuzgi0zi.jpg)
1. [] Select the **Order Cancellation** topic from the list.

    !IMAGE [22grus8x.jpg](instructions353330/22grus8x.jpg)
    !IMAGE [sgx8ivm4.jpg](instructions353330/sgx8ivm4.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Test it out by entering the following prompt:

    `I'd like to cancel my order.`

    !IMAGE [jtwla3rv.jpg](instructions353330/jtwla3rv.jpg)

***

Congratulations, you're now familiar with the available actions under the **Topic management** menu. It would be useful for you to review the other options under **Topic management** before you continue; however, it's not essential for moving on to the next task.

===

### **Question** node behavior

Previously, this lab covered the basics of the **Question** node and built on this concept by using entities and slot filling. In addition to storing a user's response, the **Question** node has more behavior options that you can set up.

One option is the ability to skip asking a question if the variable that it's linked to already contains a value. You observed this process in action in a previous task where the question was skipped when the agent was asked to check an order. The question was skipped because, by using entities and slot filling, you allowed Microsoft Copilot Studio to retrieve data from the sentence that the user asked and then store the data within the variable. After the **Question** node was reached by Microsoft Copilot Studio, it already contained data, so the question didn't need to be asked again. This approach is more efficient because, when the user or customer is talking to an agent, they won't need to answer the same question multiple times.

1. [] Within the **Check Order Status** topic, select the **Question** node. Then, select the ellipsis within the upper-right corner of the **Question** node to extend the menu, as shown in the following screenshot, and then choose **Properties** from the menu.

    !IMAGE [msax6zln.jpg](instructions353330/msax6zln.jpg)
1. [] Select **Question behavior** from the **Question properties** panel that appears.

    !IMAGE [uhqe70w4.jpg](instructions353330/uhqe70w4.jpg)

    The **Question** node has several configurable options so that you're able to better identify what the user's response is to the question that you're asking. This component is important when you're developing conversational applications, because regardless of the type of AI that's behind the scenes managing the natural language responses, a user might provide unexpected or unidentifiable answers. The ability to handle the agent's behavior in those circumstances helps you provide an improved customer experience. This scenario also happens in real life when you ask a question to another person and they don't understand the question. For the best experience and conversation, it's important to rephrase or act differently than to repeat the same question that wasn't originally understood.

    The following question behavior controls are available for you to choose from in the **Question behavior property** window:
    - **Skip behavior/Skip question** - An agent author can skip the question if the variable already has a value\. The variable in the question could have a value that was set somewhere else in the topic\, in another topic\, or through slot filling and by using entities\. This behavior allows the agent author to skip the question\, or if the variable has a value\, to ask the question anyway\. Other available options include using Power Fx to create a condition\, and if that condition is true\, to skip the question\.
    - **Reprompt/How many reprompts** - You can set up the behavior to repeat the question a specific number of times\, and you can select from the dropdown menu to **not repeat**, **repeat once**, or **repeat up to two times**. Like the skip question option, you can also use Power Fx to set the condition for this behavior to occur. You can modify the **Retry prompt** option, which only occurs if you have retries selected to repeat the question. By selecting the **Retry prompt** option, you can add a different message to reword the question, and you can add message validations to make the question sound more natural and be more helpful to the customer or user.
    - **Additional entity validation/Condition** - This behavior is important if you have specific conditions to use to validate if an entity can be slot filled and if there is a dependence on the entity type\. You can also use the same prompt behavior to change the prompt\, if the conditions aren't met\, to encourage the user to provide a different input\.
    - **No valid entity found/Action if no entity found** - If no entity is found\, rather than skip the question\, you can specify the behavior\, such as leave the variable empty\, set the variable to something specific or dynamic (by using Power Fx\)\, or call the escalate system topic\.
    - **Interruptions** - You can indicate whether a customer should be able to switch to a different topic from the current topic that the **Question** node is in. This option is useful if a customer is likely to answer a question with another question and you want to continue the conversation without needing to handle all exceptions within a single **Question** node.

        !IMAGE [b5tzfnwc.jpg](instructions353330/b5tzfnwc.jpg)

Now that you're aware of the core functionality of the **Question** node and associated behavior, you can explore the rich text responses in the Message and **Question** nodes.

===

# Task 09: Use rich text capabilities in a **Message** node

### Introduction

Clear communication is vital when providing instructions or important information.

### Description

You'll use rich text formatting to improve clarity in your agent's messages, ensuring information provided to Contoso's customers is easily understood.

### Rich text options for **Message** and **Question** nodes

Microsoft Copilot Studio includes several extended capabilities for creating agents, and it provides positive conversational experiences for customers. One central feature is the rich text authoring capabilities that are available for the Message and **Question** nodes.

!IMAGE[p8r8yizw.jpg](instructions353330/p8r8yizw.jpg)

The types of rich text authoring options that are available include:

- **Image** - You can add an image, which is displayed on the card. Add the URL of the image and a title (optional).

- **Video** - You can add a video URL, which needs to be a publicly available MP4 or a YouTube video URL.

- **Basic card** - This option includes simple cards that provide adaptive cards, such as visuals; however, this option requires standard input such as the title, messages, and the ability to add buttons with basic actions.

- **Adaptive Card** - You can add Adaptive Cards, which are platform-agnostic cards that are designed to be flexible to suit the needs at the time, including requesting action, displaying information so that it's displayed with emphasis on specific information, or more. Microsoft Copilot Studio supports Adaptive Cards v.1.5 at the time when these exercises were written.

- **Quick reply** - This option allows users to select from specific options rather than needing to enter the response in text-based scenarios. Quick replies are optional, so a user can still type or speak their own response. You should use these replies to provide common suggestions or to help give the user ideas about the type of information that's being asked.
 
### Success criteria

-   Applied rich text formatting to messages.
-   Verified clear and formatted text presentation during agent interactions.

===

## Key tasks

### 01: Add rich text to Conversation Start

1. [] Select **Topics** on the top bar.
1. [] Select the **System** filter near the upper-left corner of the window, then select the **Conversation Start** topic.

    !IMAGE[pmt456bt.jpg](instructions353330/pmt456bt.jpg)
1. [] Select the **Message** node, select **Add**, then select **Image**.

    !IMAGE [asjqbyje.jpg](instructions353330/asjqbyje.jpg)
1. [] In the **Image URL** text box, enter:

    `https://learn.microsoft.com/en-us/training/achievements/build-effective-bots.svg`

    !IMAGE [6temupyj.jpg](instructions353330/6temupyj.jpg)

    > [!note] Optionally, you can also add a name for the image by using the **Title** field.
1. [] Select **Add** again in the **Message** node, then select **Quick reply**.
1. [] Enter the following under **Quick replies**:

    `Help with my order`

    !IMAGE [ea699m02.jpg](instructions353330/ea699m02.jpg)

    >[!knowledge] Quick replies are a great way to suggest available options for a user to choose from, driving a conversation to successful outcomes by proactively proposing the most common actions.
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

===

### 02: Add a regular expression entity

1. [] Select **Topics** on the top bar.
1. [] Select the **Check Order Status** topic.
1. [] Below the **Trigger** node, select the **+** button, then select **Ask a question** to add a new **Question** node.

    !IMAGE[0gw04kxe.jpg](instructions353330/0gw04kxe.jpg)
1. [] Enter the following:

    `Could you please provide your order number?`
1. [] Select the entry under **Identify**, then select **Create an Entity**.

    !IMAGE [fjsw1d6k.jpg](instructions353330/fjsw1d6k.jpg)
1. [] Select **Regular expression (Regex)**.
1. [] Enter the following for the new entity:

    | Item | Value |
    | ---- | ----- |
    | **Name** | `OrderNumber` |
    | **Pattern** | `ORD-[0-9]{6}` |

    > [!note] This pattern will automatically detect IDs like ORD-123456.
1. [] Select **Save** at the bottom of the pane.
1. [] In the same **Question** node, select **Var1**, then for **Variable name** enter `OrderNumber`.

    !IMAGE [qs4pes5n.jpg](instructions353330/qs4pes5n.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

***

Take some time to repeat the process with the following different rich response types to become familiar with the different properties before you move on to the next task.

- Video
- Basic card
- Adaptive card
- Quick reply

>[!Knowledge] For Adaptive Cards samples and authoring experiences, visit these sites:
> - [https://adaptivecards.io/samples/](https://adaptivecards.io/samples/)
> - [https://adaptivecards.io/designer/](https://adaptivecards.io/designer/)
> - [https://amdesigner.azurewebsites.net/](https://amdesigner.azurewebsites.net/)

===

# Task 10: Add message variations

### Introduction

To enhance the natural conversational experience for Contoso's customers, you'll introduce message variations. This approach ensures the agent communicates in a less repetitive, more engaging manner during multiple interactions.

### Description

You'll create message variations within Copilot Studio, allowing the agent to randomly select from multiple similar message responses to reduce redundancy.

### Success criteria

- You've created multiple variations of agent messages.
- You've verified randomized message selection during testing.

===

## Key tasks

Both Message and **Question** nodes support message variations, allowing you to add up to 15 different message options within a single node. When the agent is triggered, Microsoft Copilot Studio randomly selects one of these variations, enhancing conversational diversity. This feature helps agent authors create more natural and engaging interactions, providing users with dynamic and varied experiences over time.

### 01: Add message variations

In this task, you'll add a **Message variation** to an existing node.

1. [] Move through the **Check Order Status** canvas, and below the **Condition** branch for **Check**, select the **Message** node .
1. [] Select **Add**, then select **Message variation**.

    !IMAGE [jzaiyxau.jpg](instructions353330/jzaiyxau.jpg)
1. [] Add a message variation the agent should use:

    `Sure thing. Give me a moment to check on that.`
1. [] Now add a variation to the **Message** node under the **Update** condition path:

    `I'll get that updated right away.`
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

***

Congratulations, you've now completed the basics of using the **Message** node. Now, you can test out your message variations by selecting the **Test** option to trigger the conditions.

The **Message** node has additional advanced features not covered in the context of this exercise.

===

## Speech authoring

Within Microsoft Copilot Studio, authors of agents can use Speech Synthesis Markup Language (SSML) tags in Message and **Question** nodes to extend the behavior of speech-enabled agents. You can use Microsoft Copilot Studio for text authoring and speech authoring. By default, on voice-enabled channels, the message text that's entered in the **Message** node will be used for both voice and text display. You can override this behavior by providing different behavior for text and speech. For example, you can override when you want to provide more emphasis on certain areas of a sentence, or for an image message because you want to provide an alternative description that can be read aloud.

When using SSML, you can control how text is converted into synthesized speech to make it sound more natural. SSML tags like Audio, Break, Emphasis, and Prosody allow you to modify the way a sentence is spoken.

- **Audio** - Add pre\-recorded audio\.
- **Break** - Insert pauses or breaks between words\.
- **Emphasis** - Add levels of stress to words and phrases\.
- **Prosody** - Specify changes to pitch\, contour\, range\, rate\, and volume\.

> [!knowledge] For more information, see [Speech Synthesis Markup Language](https://learn.microsoft.com/en-us/azure/cognitive-services/speech-service/speech-synthesis-markup/).

===

# Task 11: Use code view and Power Fx

### Introduction

To meet specific interaction requirements for Contoso's customer service scenarios, advanced customization may be necessary.

### Description

You'll use the code view in Copilot Studio and employ Power Fx formulas to implement advanced conversational logic beyond default node capabilities.

### Success criteria

- You've successfully utilized code view and Power Fx formulas.
- You've confirmed advanced conversational logic behaves as intended.

===

## Key tasks

Now that you're more familiar with the authoring fundamentals in Microsoft Copilot Studio, you can explore some extended capabilities that you can use to set up and further customize the agent experience. The following sections cover two capabilities: **code view** for pro developers and **Power Fx** (for Microsoft Power Platform makers and professional developers).

Microsoft Copilot Studio has the capability to view the code behind a topic. This capability is incredibly useful for advanced authors and pro-code developers. They can view and edit the syntax directly within the web browser, and when saved, the syntax is immediately visible in the graphical authoring canvas. As a result, the process of copying and editing multiple actions becomes faster and easier.

Some specific actions are only available in the code editor view.

### 01: Access the code editor

1. [] In **Check Order Status**, select **More** (ellipsis) in the upper-right part of the canvas next to **Save**, then select **Open code editor**.

    !IMAGE [jxtyans6.jpg](instructions353330/jxtyans6.jpg)
1. [] Here you can see your dialog in YAML code view.

    !IMAGE [cxhge4se.jpg](instructions353330/cxhge4se.jpg)
1. [] Select **Close code editor** in the upper-right corner of the pane after exploring the feature.

    > [!alert] If the option is unavailable, please refresh the page to return to the canvas.

===

# Task 12: Use Power Fx across Microsoft Copilot Studio

### Introduction

Extending the Contoso agent's functionality beyond standard conversational logic requires deeper integration. To do this, you'll need to apply Power Fx expressions across Microsoft Copilot Studio and customize customer interactions for Contoso.

### Description

You'll incorporate Power Fx expressions throughout Copilot Studio, enhancing the agent's capability to handle complex scenarios and interactions comprehensively.

### Success criteria

- You've implemented Power Fx expressions effectively in various conversational topics.
- You've verified agent behavior aligns with intended advanced logic during interactions.

===

## Key tasks

Power Fx is available in Microsoft Copilot Studio. With Power Fx, you can add functions, in the same way authors currently do in canvas apps from Microsoft Power Apps or Dataverse, within the Microsoft Copilot Studio authoring canvas. You can use Power Fx in Message and **Question** nodes when you're using the Set a variable value node, and in other areas such as Conditions, Actions, Question behavior configurations, and Adaptive Cards.

This feature gives you greater control over the data that's displayed to customers and users within the conversational interface. Additionally, it allows you to perform common operations in the runtime of Microsoft Copilot Studio.

The following task goes through a basic scenario of using Power Fx within a variable and then displaying the value to the user.

### 01: Use Power Fx to modify how the date is displayed

1. [] Under the **Condition** node for **Check**, select the **+** button, select **Variable management**, then select **Set a variable value**.

    !IMAGE [mzgjfjh8.jpg](instructions353330/mzgjfjh8.jpg)
1. [] Select the entry under **Set variable**, then select **Create a new variable**.
1. [] Select the **Var1** variable, then set the **Variable name** to `OrderDeliveryDate`.
1. [] Under **To Value**, select the ellipsis **(...)**, select the **Formula** tab, and enter the following function.

    > [!alert] Using the **Copy** option in the upper-right corner of the code block and pasting with **Ctrl+V** will be quicker than using **Type**.

    ```
	Text(
		DateAdd(
			Now(),
			2,
			TimeUnit.Days
		),
		DateTimeFormat.LongDate
	)
    ```

    !IMAGE[dwz1ma70.jpg](instructions353330/dwz1ma70.jpg)

    > [!note] You can select the **expand** icon in the upper-right corner of the **Enter formula** pane to enlarge the area.

    !IMAGE [bhia7vgg.jpg](instructions353330/bhia7vgg.jpg)
1. [] Move through the **Enter formula** pane and select **Insert** at the bottom, or in the lower-right part of the expanded view.

    !IMAGE [hryylf7x.jpg](instructions353330/hryylf7x.jpg)

    > [!note] This function takes today's date and time (for example, 5/31/2035 8:00 AM), adds two days to it, and then formats it in a long date format (for example, Saturday, June 2, 2035) . This approach is important if you want to display simple date formats that are user-friendly, or if you want to store the date as a string in text format.
1. [] Add a **Message** node to the bottom of the **Check** branch, under the existing **Message** node.
1. [] Add a message using the new variables you configured:

    `Your order {Topic.OrderNumber} should be delivered by {Topic.OrderDeliveryDate}.`

    !IMAGE [mfprw6k9.jpg](instructions353330/mfprw6k9.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Trigger the topic with a relevant prompt:

    `Hi, could you check the status of my order ORD-001342?`

    !IMAGE [xbfh6039.jpg](instructions353330/xbfh6039.jpg)

===

## Summary

Congratulations, you've successfully worked through all the tasks on the central authoring features in Microsoft Copilot Studio unified authoring. In this exercise you:

- Defined and used custom entities and slot‑filling to capture user intent automatically.
- Stored customer data in topic and global variables for later use.
- Added conditions to branch conversations based on variable values.
- Practised using the Test your agent pane to trace variable values and dialog flow.

===

# Exercise 03: Build and call Power Automate cloud flows from your agent

## Scenario

To further automate responses and reduce response times, Contoso integrates their Copilot agent with existing business workflows.

In this exercise, you'll use Power Automate cloud flows to enable the agent to interact seamlessly with Contoso's backend systems. For example, when customers inquire about service appointments or equipment status, the agent automatically retrieves accurate, real-time data, improving operational efficiency and response accuracy.

## Objectives

In this exercise, you'll create a new topic, add a simple Power Automate action to retrieve information from an external service, and then display that data back to the user.

After this exercise you'll be able to:

- Understand the basics of Power Automate.
- Use Copilot Studio to request data from another data source using Power Automate and return the data in a conversational dialog with the end user.

## Architecture

!IMAGE [c39dl1kl.jpg](instructions353330/c39dl1kl.jpg)

## Duration

Estimated time: 60 minutes.

===

## Fundamental knowledge: Understanding Power Automate

Power Automate is a cloud-based service that makes it practical and simple for line-of-business users to build workflows that automate time-consuming business tasks and processes across applications and services.

Power Automate is part of a powerful and adaptable business application platform that includes Power Apps, Microsoft Dataverse, Dynamics 365, and Office 365. This platform allows our customers, our partners, and our ISV partners to create purpose-built solutions for their own companies, their industry, for functional roles, or even for specific geographies.

Line-of-business users, who understand their business needs best, can easily analyze, compose, and streamline data and processes. Professional developers can easily extend the automation, analytics, and line-of-business apps to leverage Azure services like Functions, App Services, and Logic Apps. API connectors, gateways, and Microsoft Dataverse make it possible to get more value out of services or data already in use, either in the cloud or on-premises.

Here are a few examples of what you can do with Power Automate:

- Send automatic reminders for past due tasks.
- Move business data between systems on a schedule.
- Connect to more than 1000 data sources or any publicly available API.
- You can even automate tasks on your local computer, such as computing data in Excel.

Just think about time saved once you automate repetitive manual tasks simply by recording mouse clicks, keystrokes, and copy/paste steps from your desktop! Power Automate is all about automation.

Microsoft Copilot Studio connects easily with Power Automate, being able to pass the variables from user responses and retrieve data from several different data sources, perform complex operations on that data, and return to Microsoft Copilot Studio to share that data with the user. Being able to operate on and retrieve data from almost any data source accessible via an API is one of the most valuable benefits of Copilot Studio.

Alternatively, Microsoft Copilot Studio can also directly use the same connectors, HTTP requests, or custom connectors as in Power Automate, directly from a topic or from a plugin action.

This exercise will not include an extensive introduction to Power Automate but does cover a basic scenario of how to retrieve data from an external data source and use it in the conversational experience of Copilot Studio.

To learn more specifically about Power Automate, you can review the [Microsoft Docs on Power Automate](https://learn.microsoft.com/en-us/power-automate/), and also the 'In a Day' material for Microsoft Power Apps, which includes Power Automate.

## Build a basic Power Automate cloud flow

Connecting to data provides companies with significant benefits, as it provides information and insight to users that is up-to-date and often relevant to customer or user questions.

===

# Task 01: Create a new topic

### Introduction

Contoso regularly receives customer inquiries about existing service tickets, equipment status, and maintenance schedules. To improve efficiency in handling these requests, the AI-powered agent must be equipped to gather specific details directly from customers during their interactions.

### Description

In this task, you'll create a new conversational topic in Microsoft Copilot Studio. This topic will include trigger phrases customers might use to request information, as well as questions to collect necessary details such as ticket numbers.

### Success criteria

- You've created and named a new conversational topic.
- You've defined suitable trigger phrases.
- You've added a **Question** node to collect required customer information.

===

## Key tasks

### 01: Create a new topic

1. [] Select **Topics** on the top bar.

    > [!note] To avoid confusion with the **Support Ticket** topic created in a previous task, you'll disable it here.
1. [] On the line for **Support Ticket**, select the toggle under the **Enabled** column to set it to **Off**.

    !IMAGE[sm6nsqad.jpg](instructions353330/sm6nsqad.jpg)
1. [] Select **Add a topic** in the upper-left part of the window, then select **From blank**.

    !IMAGE[942c4tda.jpg](instructions353330/942c4tda.jpg)
1. [] Select **Untitled** in the upper-left part of the window, and rename the topic to `Check Ticket Status`.
1. [] Within the **Trigger** node, under **User says a phrase**, select **Edit**.

    !IMAGE[cbno41yu.jpg](instructions353330/cbno41yu.jpg)
1. [] Under **Add phrases**, enter the following, then select **Enter** or the **+** button for each phrase.
    - `What is the status of my ticket INC0008001`
    - `Can you get me information on my ticket status`
    - `Could you check the status of my ticket`
    - `Status update on ticket INC0009005`
    - `What's happening with my ticket INC1234567`
1. [] Add a new **Question** node under the **Trigger** node, then enter:

    `Absolutely. Could you provide me with your ticket number?`
1. [] Select the entry under **Identify**, then select **Create an Entity**.

    !IMAGE [01rspymj.jpg](instructions353330/01rspymj.jpg)
1. [] Select **Regular expression (Regex)**
1. [] Enter the following for the new entity:

    | Item | Value |
    | ---- | ----- |
    | **Name** | `TicketNumber` |
    | **Pattern** | `INC[0-9]{7}` |
1. [] Select **Save** at the bottom of the pane.
1. [] Select the **Var1** variable, then for **Variable name** enter `TicketNumber`.
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

!IMAGE [5m1x28fr.jpg](instructions353330/5m1x28fr.jpg)

===

# Task 02: Create your Power Automate cloud flow

### Introduction

Contoso aims to provide customers with timely and accurate responses by automating the retrieval of service-related information. Power Automate cloud flows will facilitate this by interacting with external systems to fetch the requested data quickly.

### Description

In this task, you'll create a Power Automate cloud flow to retrieve simulated data from external sources. This flow will accept input from the Copilot Studio agent and simulate an automated process to return the required data.

### Success criteria

- Successfully created the Power Automate cloud flow.
- Configured input parameters correctly.
- Simulated a data retrieval action within the cloud flow.

===

## Key tasks

### 01: Create your Power Automate cloud flow

In this task, you'll simulate a ServiceNow connection to pull in ticket details.

> [!alert] Check with your coach to see if they want to use a real ServiceNow connection after step 6, or if you should use the simulated response.
> 
> Screenshots in subsequent tasks show the simulated ticket details.

1. [] Select the **+** button under the **Question** node, select **Add a Tool**, then select **New Agent flow**.

    !IMAGE[8k0waw5h.jpg](instructions353330/8k0waw5h.jpg)

    > [!note] This will open **Power Automate** in a new browser tab and includes the scaffolding pre and post actions for a new Power Automate cloud flow to interact with Copilot Studio.

1. [] Select the **When an agent calls the flow** node.
1. [] In the new pane, select **Add an input**, then select **Text**.

    !IMAGE [hjpqhoep.jpg](instructions353330/hjpqhoep.jpg)
1. [] Replace the name value of **Input** with `TicketNumber`.

    !IMAGE[dykraoxf.jpg](instructions353330/dykraoxf.jpg)
1. [] Select the **+** button under the **When an agent calls the flow** node.

    !IMAGE [kn4oddnw.jpg](instructions353330/kn4oddnw.jpg)
1. [] Search for `ServiceNow List Records` in the search bar, then select **List Records**.

    !IMAGE[5i8kvlvl.jpg](instructions353330/5i8kvlvl.jpg)

    > [+alert] If your coach provides a ServiceNow environment to use, expand here for details on finishing this task. If not, proceed to the next step.
    > 1. [] Input all the connection details provided by the coach.
    > 1. [] Select **Create New**.
    > 1. [] Under **Record Type**, select the dropdown menu, then search for and select `Incident`.
    > 1. [] Under **Advanced parameters**, select **Show all**.
    > 1. [] Set the **Display System References** to **Yes** to show actual values.
    > 1. [] Under **Query**, enter `numberCONTAINS`, then select the **TicketNumber** input from the dynamic content (⚡).
    >
    > Ensure there are no spaces between **numberCONTAINS** and the **TicketNumber** variable you reference.
    > Alternatively, you can also paste the following in the **Query** field:
    > 
    > `numberCONTAINS@{triggerBody()?['text']}`
    > 1. [] Under **Limit**, enter `1`.
    >
    > !IMAGE [12qw47be.jpg](instructions353330/12qw47be.jpg)
    > 1. [] Select the **Respond to Copilot** node in the cloud flow.
    > 1. [] Select **Add an output**, then select **Text**.
    > 1. [] Set the name to `SNTicketInfo`.
    > 1. [] Select the text box to the right of **SNTicketInfo** for its value field, then select the formula button (**fx**).
    >
    > !IMAGE [4r600b9w.jpg](instructions353330/4r600b9w.jpg)
    > 1. [] Enter the following formula, then select **Add**. This gets a string of the first returned record of the resulting array from the **List Records** body.
    >
    > `string(first(outputs('List_Records')?['body/result']))`
    > 
    > !IMAGE [kq39z8qn.jpg](instructions353330/kq39z8qn.jpg)
    > 1. [] Skip to step 15 in this task to publish the flow.
1. [] In the **Create connection** step, enter the following:

    | Item | Value |
    | ---- | ----- |
    | **Connection name** | `@lab.User.FirstName @lab.User.LastName ServiceNow` |
    | **Authentication Type** | Basic Authentication |
    | **Instance** | `https://dev261120.service-now.com` |
    | **Username** | `CopilotStudioServiceAccount` |
    | **Password** | `F@k3Pw29@9%92` |
1. [] Select **Create new**.

    !IMAGE[5auyysc7.jpg](instructions353330/5auyysc7.jpg)
1. [] In this scenario, you'll simulate a response that comes from this connection instead.

    Delete the **List Records** node by selecting it, then selecting the **Delete** key. Alternatively, right-click the node, then select **Delete**.

    !IMAGE[2kw768ma.jpg](instructions353330/2kw768ma.jpg)

1. [] Select the **Respond to Copilot** node in the flow.
1. [] Select **Add an output**, then select **Text**.
1. [] Set the name to `SNTicketInfo`.
1. [] Select the text box to the right of **SNTicketInfo** for its value field.

    !IMAGE [u18z7f5o.jpg](instructions353330/u18z7f5o.jpg)
1. [] For this simulated ServiceNow response, paste the following payload sample in the text box.

    > [!alert] It will be faster to use the **Copy** option on the following code block and paste it with **Ctrl+V**, rather than use **Type**.

    ```json
    {
    	"parent": "",
    	"made_sla": "true",
    	"caused_by": "",
    	"watch_list": "",
    	"upon_reject": "Cancel all future Tasks",
    	"sys_updated_on": "2018-12-12 23:18:55",
    	"child_incidents": "0",
    	"hold_reason": "",
    	"origin_table": "",
    	"task_effective_number": "INC0009005",
    	"approval_history": "",
    	"number": "INC0009005",
    	"resolved_by": "",
    	"sys_updated_by": "admin",
    	"opened_by": "System Administrator",
    	"user_input": "",
    	"sys_created_on": "2018-08-31 21:35:45",
    	"sys_domain": "global",
    	"state": "New",
    	"route_reason": "",
    	"sys_created_by": "admin",
    	"knowledge": "false",
    	"order": "",
    	"calendar_stc": "",
    	"closed_at": "",
    	"cmdb_ci": "",
    	"delivery_plan": "",
    	"contract": "",
    	"impact": "1 - High",
    	"active": "true",
    	"work_notes_list": "",
    	"business_service": "",
    	"business_impact": "",
    	"priority": "1 - Critical",
    	"sys_domain_path": "/",
    	"rfc": "",
    	"time_worked": "",
    	"expected_start": "",
    	"opened_at": "2018-08-31 21:35:21",
    	"business_duration": "",
    	"group_list": "",
    	"work_end": "",
    	"caller_id": "David Miller",
    	"reopened_time": "",
    	"resolved_at": "",
    	"approval_set": "",
    	"subcategory": "Email",
    	"work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"universal_request": "",
    	"short_description": "Email server is down.",
    	"correlation_display": "",
    	"delivery_task": "",
    	"work_start": "",
    	"assignment_group": "",
    	"additional_assignee_list": "",
    	"business_stc": "",
    	"cause": "",
    	"description": "Unable to send or receive emails.",
    	"origin_id": "",
    	"calendar_duration": "",
    	"close_notes": "",
    	"notify": "Do Not Notify",
    	"service_offering": "",
    	"sys_class_name": "Incident",
    	"closed_by": "",
    	"follow_up": "",
    	"parent_incident": "",
    	"sys_id": "ed92e8d173d023002728660c4cf6a7bc",
    	"reopened_by": "",
    	"incident_state": "New",
    	"urgency": "1 - High",
    	"problem_id": "",
    	"company": "",
    	"reassignment_count": "0",
    	"activity_due": "2018-12-13 01:18:55",
    	"assigned_to": "",
    	"severity": "3 - Low",
    	"comments": "",
    	"approval": "Not Yet Requested",
    	"sla_due": "UNKNOWN",
    	"comments_and_work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"due_date": "",
    	"sys_mod_count": "3",
    	"reopen_count": "0",
    	"sys_tags": "",
    	"escalation": "Normal",
    	"upon_approval": "Proceed to Next Task",
    	"correlation_id": "",
    	"location": "",
    	"category": "Software"
    }
    ```

    !IMAGE [2wrdhi59.jpg](instructions353330/2wrdhi59.jpg)

    >[!Note] This represents an example of what ServiceNow would typically return.

    > [!knowledge] In a real-world scenario:
    > 
    > You could select the **fx** formula button that appears for the value field.
    > 
    > !IMAGE [3p1qd5tv.jpg](instructions353330/3p1qd5tv.jpg)
    > 
    > Then you could enter a formula in the top text box, then select **Add**.
    > 
    > `string(first(outputs('List_Records')?['body/result']))`
    > 
    > !IMAGE [izp2sady.jpg](instructions353330/izp2sady.jpg)
    > 
    > This gets a string version of the first returned record of the result array from the ServiceNow **List Records** body.

1. [] Select **Publish** in the upper-right part of the page. Wait for the green success banner once published.

    !IMAGE[h8cdepa3.jpg](instructions353330/h8cdepa3.jpg)

1. [] In the dialog, select **Go back to agent**.

    !IMAGE[lidumv2k.jpg](instructions353330/lidumv2k.jpg)

===

# Task 03: Call your Power Automate cloud flow from Copilot Studio

### Introduction

To enhance Contoso's customer interactions, the agent needs to integrate seamlessly with automated processes. By connecting conversational topics to Power Automate cloud flows, the agent will dynamically fetch and provide customers with relevant information in real-time.

### Description

In this task, you'll integrate your previously created Power Automate cloud flow with the conversational topic in Microsoft Copilot Studio. You'll configure the flow invocation and pass collected customer inputs to automate the process of information retrieval.

### Success criteria

- You've linked your conversational topic to the Power Automate cloud flow.
- You've correctly configured topic variables to pass inputs to the flow.
- You've verified through testing that the integration works correctly.

===

## Key tasks

### 01: Call your Power Automate cloud flow from Copilot Studio

<!-- 1. [] Go back to your tab for Copilot Studio.
1. [] In the **Save and refresh** dialog, select **Done** to update the flow list with the one you just created. You can also manually refresh the page.

    !IMAGE [b84p7yfo.jpg](instructions353330/b84p7yfo.jpg)
1. [] If needed, select the **+** button under the **Question** node again, select **Add a tool**, then select the **Get Ticket Status (@lab.User.FirstName @lab.User.LastName)** flow.

    !IMAGE[xkf678of.jpg](instructions353330/xkf678of.jpg)

    > [!note] A new **Action** node will be added.
    > 
    > If the flow requires an input, it requests the value to be selected. The flow you created in the previous steps requires the **TicketNumber** input. Therefore, we need to add this input into the Power Automate action by selecting the variable containing the value from the user, which is **TicketNumber** from earlier in the lab.

    > [!alert] If you don't see the flow you created, **Save** the topic, refresh the page, then try again. -->

1. [] In the new **Action** node, under **Power Automate inputs**, select the ellipsis **(...)** next to **Enter or select a value**, then select the **TicketNumber** variable.

    !IMAGE[dmk2ex2j.jpg](instructions353330/dmk2ex2j.jpg)

    > [!note] This is now connected to the Power Automate flow, and outputs the result from Power Automate into the **SNTicketInfo** variable.

    >[!Knowledge] **Pro tips**:
    > - If latency is expected from your integration, go the action's properties and add a latency message , for example: 'I'm getting these details for you. Hold on...'
    > - Consider using HTTP requests and connectors directly in Microsoft Copilot Studio to avoid the added latency of invoking and running a cloud flow in Power Automate.
1. [] As ServiceNow will return the full details of the incident in a **JSON** format, you need to parse it so that Copilot Studio fully understands its content based on its schema.

    Under the **Action** node, select the **+** button, select **Variable Management**, then select **Parse value**.

    !IMAGE[uvkwqa17.jpg](instructions353330/uvkwqa17.jpg)

    > [!note] To parse the JSON you can use the Rest API Explorer in ServiceNow to get the structure of the body, or get the schema from a sample payload. For the exercise, we're providing sample ServiceNow data.
1. [] Under **Parse value**, select the ellipsis **(...)**, then select the **SNTicketInfo** variable.

    !IMAGE[cqtmqp3c.jpg](instructions353330/cqtmqp3c.jpg)
1. [] For **Data type**, select **From sample data** from the dropdown menu.
1. [] Select **Get schema from sample JSON**.

    !IMAGE [s02aculz.jpg](instructions353330/s02aculz.jpg)
1. [] Paste the schema below.

    > [!alert] Use the **Copy** option on the following code block and paste it with **Ctrl+V**, rather than use **Type**.

    ```json
    {
    	"parent": "",
    	"made_sla": "true",
    	"caused_by": "",
    	"watch_list": "",
    	"upon_reject": "Cancel all future Tasks",
    	"sys_updated_on": "2018-12-12 23:18:55",
    	"child_incidents": "0",
    	"hold_reason": "",
    	"origin_table": "",
    	"task_effective_number": "INC0009005",
    	"approval_history": "",
    	"number": "INC0009005",
    	"resolved_by": "",
    	"sys_updated_by": "admin",
    	"opened_by": "System Administrator",
    	"user_input": "",
    	"sys_created_on": "2018-08-31 21:35:45",
    	"sys_domain": "global",
    	"state": "New",
    	"route_reason": "",
    	"sys_created_by": "admin",
    	"knowledge": "false",
    	"order": "",
    	"calendar_stc": "",
    	"closed_at": "",
    	"cmdb_ci": "",
    	"delivery_plan": "",
    	"contract": "",
    	"impact": "1 - High",
    	"active": "true",
    	"work_notes_list": "",
    	"business_service": "",
    	"business_impact": "",
    	"priority": "1 - Critical",
    	"sys_domain_path": "/",
    	"rfc": "",
    	"time_worked": "",
    	"expected_start": "",
    	"opened_at": "2018-08-31 21:35:21",
    	"business_duration": "",
    	"group_list": "",
    	"work_end": "",
    	"caller_id": "David Miller",
    	"reopened_time": "",
    	"resolved_at": "",
    	"approval_set": "",
    	"subcategory": "Email",
    	"work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"universal_request": "",
    	"short_description": "Email server is down.",
    	"correlation_display": "",
    	"delivery_task": "",
    	"work_start": "",
    	"assignment_group": "",
    	"additional_assignee_list": "",
    	"business_stc": "",
    	"cause": "",
    	"description": "Unable to send or receive emails.",
    	"origin_id": "",
    	"calendar_duration": "",
    	"close_notes": "",
    	"notify": "Do Not Notify",
    	"service_offering": "",
    	"sys_class_name": "Incident",
    	"closed_by": "",
    	"follow_up": "",
    	"parent_incident": "",
    	"sys_id": "ed92e8d173d023002728660c4cf6a7bc",
    	"reopened_by": "",
    	"incident_state": "New",
    	"urgency": "1 - High",
    	"problem_id": "",
    	"company": "",
    	"reassignment_count": "0",
    	"activity_due": "2018-12-13 01:18:55",
    	"assigned_to": "",
    	"severity": "3 - Low",
    	"comments": "",
    	"approval": "Not Yet Requested",
    	"sla_due": "UNKNOWN",
    	"comments_and_work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"due_date": "",
    	"sys_mod_count": "3",
    	"reopen_count": "0",
    	"sys_tags": "",
    	"escalation": "Normal",
    	"upon_approval": "Proceed to Next Task",
    	"correlation_id": "",
    	"location": "",
    	"category": "Software"
    }
    ```
1. [] Select **Confirm**.

    !IMAGE [c9nq4vbp.jpg](instructions353330/c9nq4vbp.jpg)
1. [] Still in the **Parse value** node, under **Save as**, select **Select a variable**, then select **Create a new variable**.

    !IMAGE [6zeb9407.jpg](instructions353330/6zeb9407.jpg)
1. [] Select the new **Var1** variable, then for **Variable name** enter `SNTicketInfoParsed`.

    > [!note] The variable type will automatically be set based on its schema (**record**).
1. [] Under the **Parse value** node, add a new **Message** node, then enter the following message:

    `The status of ticket {Topic.TicketNumber} ({Topic.SNTicketInfoParsed.short_description}) is {Topic.SNTicketInfoParsed.state}.`

    !IMAGE [b77703py.jpg](instructions353330/b77703py.jpg)

    >[!Knowledge] You can bold key information either with the command bar or by surrounding the text with \*\*.
    > 
    > Copilot Studio and some channels support [Markdown](https://www.markdownguide.org/) for simple formatting.

    > [!note] You can look above at the sample JSON to see what data would be returned in what value.
1. [] Under the **Message** node, select the **+** button, select **Topic management**, select **Go to another topic**, then select **End of Conversation**.

    !IMAGE [sosvnks5.jpg](instructions353330/sosvnks5.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Test it out by entering the following prompt:

    `What is the status of my ticket INC0007001?`

    !IMAGE [3hxzkcsj.jpg](instructions353330/3hxzkcsj.jpg)

***

You've successfully created a Power Automate cloud flow, and a new topic in Copilot Studio that used the flow to provide real-time data from an external service to the user!

===

# Task 04: Display the ServiceNow ticket information in an adaptive card

### Introduction

To enhance customer interactions, Contoso needs the AI-powered agent to clearly present ticket details retrieved from external systems.

### Description

In this task, you'll configure your conversational topic to present the information retrieved from ServiceNow using an adaptive card. You'll design the card layout and integrate the data returned by your cloud flow, ensuring it displays effectively in the conversation.

### Success criteria

- You've created and configured an adaptive card within the conversational topic.
- You've integrated ServiceNow ticket data retrieved from the Power Automate cloud flow into the adaptive card.
- You've successfully tested and verified correct data display in conversations.

===

## Key tasks

### 01: Display the ServiceNow ticket information in an adaptive card

1. [] Select the message in your **Message** node, then select the delete icon in the upper-right part of the node's text box.

    !IMAGE [yvxebcmk.jpg](instructions353330/yvxebcmk.jpg)
1. [] In the **Message** node, select **Add**, then select **Adaptive card**.

    !IMAGE [4ay5kedf.jpg](instructions353330/4ay5kedf.jpg)
1. [] Select **JSON card**, then select **Formula** so that you can make the adaptive card dynamic and author it in the Power Fx language.

    !IMAGE[0y925b4k.jpg](instructions353330/0y925b4k.jpg)
1. [] Replace the text in the text box with this Power Fx formula which contains the references to the ServiceNow ticket information.

    ```json
    {
    type: "AdaptiveCard",
    version: "1.5",
    body: [
    	{
    	type: "ColumnSet",
    	columns: [
    		{
    		type: "Column",
    		width: "auto",
    		items: [
    			{
    			type: "Image",
    			url: "https://www.servicenow.com/community/s/legacyfs/online/avatars_servicenow/1f66cb9fdb3ee3c0107d5583ca961942.jpg",
    			size: "Small",
    			style: "Person"
    			}
    		]
    		},
    		{
    		type: "Column",
    		width: "stretch",
    		items: [
    			{
    			type: "TextBlock",
    			text: Topic.SNTicketInfoParsed.short_description,
    			weight: "Bolder",
    			size: "Large",
    			wrap: true,
    			color: "Attention",
    			horizontalAlignment: "Left"
    			}
    		],
    		verticalContentAlignment: "Center",
    		horizontalAlignment: "Center"
    		}
    	]
    	},
    	{
    	type: "TextBlock",
    	text: Topic.SNTicketInfoParsed.description,
    	weight: "Lighter",
    	wrap: true
    	},
    	{
    	type: "FactSet",
    	facts: [
    		{
    		title: "Number:",
    		value: Topic.SNTicketInfoParsed.number
    		},
    		{
    		title: "State:",
    		value: Topic.SNTicketInfoParsed.state
    		},
    		{
    		title: "Priority:",
    		value: Topic.SNTicketInfoParsed.priority
    		},
    		{
    		title: "Impact:",
    		value: Topic.SNTicketInfoParsed.impact
    		},
    		{
    		title: "Urgency:",
    		value: Topic.SNTicketInfoParsed.urgency
    		},
    		{
    		title: "Category:",
    		value: Topic.SNTicketInfoParsed.category
    		},
    		{
    		title: "Subcategory:",
    		value: Topic.SNTicketInfoParsed.subcategory
    		},
    		{
    		title: "Caller ID:",
    		value: Topic.SNTicketInfoParsed.caller_id
    		},
    		{
    		title: "Opened By:",
    		value: Topic.SNTicketInfoParsed.opened_by
    		},
    		{
    		title: "Opened At:",
    		value: Topic.SNTicketInfoParsed.opened_at
    		}
    	],
    	spacing: "Small"
    	},
    	{
    	type: "TextBlock",
    	text: "Comments and notes:",
    	weight: "Bolder",
    	size: "Medium",
    	wrap: true
    	},
    	{
    	type: "TextBlock",
    	text: Topic.SNTicketInfoParsed.comments_and_work_notes,
    	wrap: true,
    	size: "Small"
    	}
    ],
    actions: [
    	{
    	type: "Action.OpenUrl",
    	title: "Update Ticket",
    	url: "https://dev204932.service-now.com/nav_to.do?uri=incident.do?sys_id=" & Topic.SNTicketInfoParsed.sys_id & "%26sysparm_view=ess"
    	}
    ],
    '$schema': "http://adaptivecards.io/schemas/adaptive-card.json"
    }
    
    ```

    !IMAGE [qrzzhy7x.jpg](instructions353330/qrzzhy7x.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Test it out by entering the following prompt :

    `What's the latest on ticket INC0007001?`

    !IMAGE [xbu5dvvg.jpg](instructions353330/xbu5dvvg.jpg)

===

## Summary

Congratulations on completing Exercise 03! You've successfully:

- Created a new Power Automate cloud flow.
- Called the Power Automate cloud flow into your topic.
- Set input and output variables.
- Displayed dynamic data back to the user in Copilot Studio.

===

# Exercise 04: Make HTTP requests to connect to an API

## Scenario

Contoso's support engineers often need live information that isn't stored in internal systems - for example, share prices or third‑party service metrics. To provide customers with near‑real‑time answers, the Copilot agent must be able to call external REST APIs directly and surface the results in chat. This exercise walks through building a topic that issues an HTTP GET request, parses the JSON response, and presents the data in a user‑friendly message.

## Objectives

In this exercise, you'll create a new topic, add a simple **HTTP Request** node action to retrieve information from an external service, then display that data back to the user.

After this exercise, you'll be able to:

- Understand the basics of the **HTTP Request** node.
- Use Copilot Studio to request data from another data source using the **HTTP Request** node, then return the data in a conversational dialog with the end user.

## Architecture

!IMAGE [3qdclxr1.jpg](instructions353330/3qdclxr1.jpg)

## Duration

Estimated time: 20 minutes.

===

# Task 01: Create a new topic

### Introduction

Once external data sources are integrated, Contoso, Inc. needs to enhance their customer service agent's capabilities by enabling the agent to retrieve real-time data from external APIs.

### Description

In this task, you'll create a new topic that allows the agent to make HTTP requests to an external API to retrieve information. You'll configure the **HTTP Request** node and parse the response data.

### Success criteria

- You successfully created a new topic with trigger phrases.
- You configured the **HTTP Request** node to retrieve data from an external API.
- You parsed the response data and displayed it to the user.

===

## Key tasks

### 01: Create a new topic

1. [] Select **Topics** on the top bar.

    !IMAGE[ywtwri24.jpg](instructions353330/ywtwri24.jpg)
1. [] Select **Add a topic**, then select **From blank**.

    !IMAGE[942c4tda.jpg](instructions353330/942c4tda.jpg)
1. [] Select **Untitled** in the upper-left part of the window, then change the topic name to `Crypto Currency Price`.
1. [] Add some **Phrases** to the **Trigger** node that a user may ask:
    - `What's the current price of Bitcoin`
    - `Can you tell me the latest crypto prices`
    - `How much does Bitcoin cost now`
    - `What are the prices of digital currencies today`
    - `What's the latest on crypto prices`

    !IMAGE[ziipm0ym.jpg](instructions353330/ziipm0ym.jpg)
1. [] Add a new **Question** node, then enter the following:

    `What currency do you want to see the current price of Bitcoin in?`
1. [] Keep **Multiple choice options** as the entry for **Identify**.
1. [] Under **Options for user**, select **New option**, then enter in the following individually:
    - `USD`
    - `EUR`
    - `GBP`

    !IMAGE [3vvmwd0n.jpg](instructions353330/3vvmwd0n.jpg)
1. [] Select the **USD** entry added, then select the **Edit synonyms** icon.

    !IMAGE [oa2xmukx.jpg](instructions353330/oa2xmukx.jpg)
1. [] Under **Add synonyms**, enter `dollars`, then select **Enter** or the **+** button, then select **Done** at the bottom of the pane.

    !IMAGE [8ia58bev.jpg](instructions353330/8ia58bev.jpg)
1. [] Repeat the steps for adding synonyms to the other currencies:

    | Currency | Synonym |
    | -------- | ------- |
    | **EUR** | `euros` |
    | **GBP** | `pounds` |
1. [] Under **Save response as**, select the **Var1** variable, then for **Variable name** enter `Currency`.
1. [] Under the **Question** node, select the **+** button, select **Advanced**, then select **Send HTTP request**.

    !IMAGE [tt58pd4z.jpg](instructions353330/tt58pd4z.jpg)
1. [] In the **HTTP Request** node, under **URL**, select the ellipsis **(...)**, select the **Formula** tab, input the following Power Fx formula, then select **Insert**.

    `Lower(Concatenate("https://api.gemini.com/v2/ticker/btc",Topic.Currency))`

    !IMAGE[zuqzec8o.jpg](instructions353330/zuqzec8o.jpg)

    > [!note] This makes sure the URL passed in is lowercase, then concatenates it to include the currency that the user selected in the question about which currency to view Bitcoin in. This will make sure that the URL for USD or EUR, for example, is correct for the API.
1. [] Under **Response data type**, select the dropdown menu, then select **From sample data**.

    > [!note] You'll need to provide a sample output of the JSON payload that will be returned by the API to allow the node to parse the response.
1. [] Select **Get schema from sample JSON**.

    !IMAGE[lp1s7far.jpg](instructions353330/lp1s7far.jpg)
1. [] Paste the following sample data, then select **Confirm**.

    ```json
    {
    	"symbol": "BTCUSD",
    	"open": "67781.09",
    	"high": "68382.33",
    	"low": "67293.74",
    	"close": "67707.13",
    	"changes": [
    		"67882.6",
    		"67781.09",
    		"67805.66",
    		"67744.15",
    		"67651.01",
    		"67863.46",
    		"68053.16",
    		"68080.11",
    		"68186.09",
    		"68109.26",
    		"67914.8",
    		"68079.54",
    		"67455.47",
    		"67468.58",
    		"67712.98",
    		"67662.82",
    		"67771.15",
    		"67680.26",
    		"67799.25",
    		"67736.21",
    		"67653.87",
    		"67698.36",
    		"67832.24",
    		"67707.13"
    	],
    	"bid": "67837.17",
    	"ask": "67843.41"
    }
    ```

    !IMAGE [e9u3sc3z.jpg](instructions353330/e9u3sc3z.jpg)
1. [] Under **Save response as**, create a new variable, then update the name to `CryptoCurrentPrice`.

    !IMAGE [dkmf1c66.jpg](instructions353330/dkmf1c66.jpg)
1. [] Add a new **Message** node under your **HTTP Request** node.
1. [] Set a message leveraging the new variables to structure a response to the user about the price of Bitcoin:

    `‌The current bid price for Bitcoin in {Topic.Currency} is {Topic.CryptoCurrentPrice.bid}`

    !IMAGE [jzeyp08e.jpg](instructions353330/jzeyp08e.jpg)
20. [] Improve the formatting of the price with currency symbols and separators for the thousands.
21. [] Delete the final variable of the message you just added: "**{Topic.CryptoCurrentPrice.bid}**".

    !IMAGE [b6tde66m.jpg](instructions353330/b6tde66m.jpg)
21. [] Select the **fx** button in the **Message** node, enter the following formula, then select **Insert**.

    ```json
    Switch(
    	Text(Topic.Currency),
    		"USD",
    		Text(Value(Topic.CryptoCurrentPrice.bid),"$#,#.##"),
    		"EUR",
    		Text(Value(Topic.CryptoCurrentPrice.bid),"#,#.##€"),
    		"GBP",
    		Text(Value(Topic.CryptoCurrentPrice.bid),"£#,#.##")           
    )
    ```

    !IMAGE [feq904fa.jpg](instructions353330/feq904fa.jpg)

    !IMAGE [n70ecv5a.jpg](instructions353330/n70ecv5a.jpg)

    > [!note] This formats the price with currency symbols and separators for the thousands.
21. [] Below the **Message** node, select the **+** button, select **Topic management**, select **Go to another topic**, then select **End of Conversation**.

    !IMAGE [dv4sk6hv.jpg](instructions353330/dv4sk6hv.jpg)
21. [] Select **Save** in the upper-right part of the canvas to save the topic.
21. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
21. [] Test this with the following prompt:

    `What's the current bid price for Bitcoin in dollars?`

    !IMAGE [mgsa6p9x.jpg](instructions353330/mgsa6p9x.jpg)

***

You've successfully created an **HTTP Request** node to provide real-time data from an external service to the user!

===

## Summary

Congratulations on completing Exercise 04! You've successfully:

- Created an HTTP API call through the **HTTP Request** node in Copilot Studio.
- Structured a GET API call using Power Fx.
- Displayed dynamic data back to the user in Copilot Studio.

===

# Exercise 05: Leverage knowledge sources, AI knowledge, and custom instructions

## Scenario

As Contoso's knowledge base grows, the team wants the agent to tap into multiple authoritative sources - web pages, internal SharePoint sites, OneDrive documents and Dataverse tables - so customers always receive accurate, grounded answers. In this exercise you will configure these knowledge sources, test them, and learn how Copilot Studio uses retrieval‑augmented generation to cite each source in chat.

## Objectives

After this exercise you'll be able to:

- Make your agent instantly smart by pointing to your website and other knowledge sources.
- Navigate to the Generative AI settings.
- Navigate to the Conversational Boosting system topic.
- Set custom prompt instructions.

## Architecture

!IMAGE [kbdo6apo.jpg](instructions353330/kbdo6apo.jpg)

## Duration

Estimated time: 30 minutes.

## Knowledge sources

Knowledge in Microsoft Copilot Studio allows you to add enterprise data from Power Platform, Dynamics 365, and external systems, so your agents can provide relevant information and insights for your end users. In addition, knowledge can be incorporated with generative answers in agents. Published agents that contain knowledge use the configured knowledge sources to ground themselves.

Supported knowledge sources:

<div style="overflow-y: auto; max-height: 400px;"><table border="1" cellspacing="0" cellpadding="5">
        <thead>
            <tr>
                <th>Name</th>
                <th>Source</th>
                <th>Description</th>
                <th>Number of inputs supported in general answers</th>
                <th>Authentication</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><strong>Public Website</strong></td>
                <td>External</td>
                <td>Searches the query input on Bing, only returns results from provided websites</td>
                <td>4 public URLs (for example, microsoft.com)</td>
                <td>None</td>
            </tr>
            <tr>
                <td><strong>Documents</strong></td>
                <td>Internal</td>
                <td>Searches documents uploaded to Dataverse, returns results from the document contents</td>
                <td>Limited by Dataverse file storage allocation</td>
                <td>None</td>
            </tr>
            <tr>
                <td><strong>SharePoint</strong></td>
                <td>Internal</td>
                <td>Connects to a SharePoint URL, uses GraphSearch to return results</td>
                <td>4 URLs</td>
                <td>Copilot user's Microsoft Entra ID authentication</td>
            </tr>
            <tr>
                <td><strong>OneDrive for Business</strong></td>
                <td>Internal</td>
                <td>Connects to a OneDrive URL, uses GraphSearch to return results</td>
                <td>4 URLs</td>
                <td>Copilot user's Microsoft Entra ID authentication</td>
            </tr>
            <tr>
                <td><strong>Dataverse</strong></td>
                <td>Internal</td>
                <td>Connects to the connected Dataverse environment and uses retrieval-augmented generative technique</td>
                <td>Two Dataverse knowledge sources (and up to 15 tables per knowledge source)</td>
                <td>Copilot user's Microsoft Entra ID authentication</td>
            </tr>
            <tr>
                <td><strong>Enterprise data via graph connections</strong></td>
                <td>Internal</td>
                <td>Connects to the connected Dataverse environment and uses retrieval-augmented generative technique</td>
                <td>Two per custom agent</td>
                <td>Copilot user's Microsoft Entra ID authentication</td>
            </tr>
        </tbody>
    </table></div>

===

# Task 01: Configure the Files knowledge source

### Introduction

Contoso, Inc. needs to enhance their customer service agent by integrating various knowledge sources to provide accurate and timely information to their customers. This task demonstrates how to configure the Files knowledge source.

### Description

In this task, you'll upload a PDF file to Microsoft Copilot Studio and configure it as a knowledge source for the agent. This will enable the agent to retrieve information from the file and provide relevant answers to customer queries.

### Success criteria

- You successfully uploaded a file and configured it as a knowledge source.
- You verified that the agent can access and retrieve information from the file.
- You tested the knowledge source by asking relevant questions.

===

## Key tasks

### 01: Configure the Files knowledge source

> [!alert] If you imported the pre-built Copilot solution using the .zip file at the start of the lab, you'll need to start following along with the steps from here.

1. [] Select **Knowledge** on the top bar.

    !IMAGE[dkdkw3gr.jpg](instructions353330/dkdkw3gr.jpg)

    > [!note] You'll see the websites added as knowledge sources during creation.
    > - [https://learn.microsoft.com/en-us/microsoft-copilot-studio/](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
    > - [https://www.microsoft.com/en-us/microsoft-copilot/](https://www.microsoft.com/en-us/microsoft-copilot/)
1. [] Open a new tab, then go to `https://servicetrust.microsoft.com/DocumentPage/7adf2d9e-d7b5-4e71-bad8-713e6a183cf3`.
1. [] Select **Download**.

    !IMAGE [ugs3c1wg.jpg](instructions353330/ugs3c1wg.jpg)
1. [] Return to your Copilot Studio tab.
1. [] Select **Add knowledge** in the upper-left part of the window.

    !IMAGE [zh42u2vw.jpg](instructions353330/zh42u2vw.jpg)
1. [] Under **Upload file**, select **select to browse**.

    !IMAGE[kqb8lgmt.jpg](instructions353330/kqb8lgmt.jpg)
1. [] Go to your **Downloads** folder, select the **Azure - Compliance Offerings** PDF, then select **Open**.

    !IMAGE [ho28vweg.jpg](instructions353330/ho28vweg.jpg)
1. [] Select **Add to agent** in the lower-right part of the pane.

    !IMAGE[v9yzr435.jpg](instructions353330/v9yzr435.jpg)
    
===

# Task 02: Configure a SharePoint knowledge source

### Introduction

After configuring the Files knowledge source, you can integrate SharePoint as a knowledge source to enhance the agent's ability to provide accurate information.

### Description

In this task, you'll configure the SharePoint knowledge source to allow the agent to access and retrieve information from SharePoint sites. You'll set up the SharePoint URL and configure access permissions.

### Success criteria

- You successfully configured the SharePoint knowledge source with the correct URL and access permissions.
- You verified that the agent can access and retrieve information from the SharePoint site.
- You tested the knowledge source by asking relevant questions.

===

## Key tasks

### 01: Configure a SharePoint knowledge source

1. [] Select **Add knowledge** in the upper-left part of the window.
1. [] Select **SharePoint**.

    !IMAGE[frfqoqs6.jpg](instructions353330/frfqoqs6.jpg)
1. [] In the text box, enter the following URL, then select **Add**.

    `https://lodsprodmslearnmca.sharepoint.com/sites/Mark8ProjectTeam@lab.LabInstance.Id`

    !IMAGE[akgan184.jpg](instructions353330/akgan184.jpg)
1. [] In the **Description** field, enter `The team dedicated to the Mark 8 Project.`, then select **Add to agent** in the lower-right corner of the pane.

    !IMAGE[j7qmepwo.jpg](instructions353330/j7qmepwo.jpg)

===

# Task 03: Configure a Dataverse knowledge source

### Introduction

With the SharePoint knowledge source now configured, you can next configure a Dataverse knowledge source so that Contoso's agent can access structured data from Dataverse to deliver detailed information to customers.

### Description

In this task, you'll set up the Dataverse knowledge source to enable the agent to access and retrieve information from Dataverse tables. This involves establishing the Dataverse connection and configuring the required tables.

### Success criteria

- You successfully configured the Dataverse knowledge source with the correct connection and tables.
- You verified that the agent can access and retrieve information from the Dataverse tables.
- You tested the knowledge source by asking relevant questions.

===

## Key tasks

### 01: Configure a Dataverse knowledge source

The Dataverse knowledge source allows users to make natural language queries over structured data, stored in Dataverse tables.

1. [] Select **Add knowledge** in the upper-left part of the window.
1. [] Select **Dataverse**.

    !IMAGE[92o0chlj.jpg](instructions353330/92o0chlj.jpg)
1. [] Under **All**, select **Account**, then select **Add to agent** in the lower-right corner of the pane.

    !IMAGE[j117sqfs.jpg](instructions353330/j117sqfs.jpg)

1. [] On the table, next to **Account**, select the vertical ellipsis, then select **Edit**.

    !IMAGE[olica2im.jpg](instructions353330/olica2im.jpg)

1. [] Select the **Synonyms** tab.

    !IMAGE[t9l2k7dx.jpg](instructions353330/t9l2k7dx.jpg)

    >[!note] You'll improve the understanding of questions about specific attributes of the table.

1. [] Find the line for **Address 1**, then select **Add synonyms**.

    !IMAGE[3a7apc37.jpg](instructions353330/3a7apc37.jpg)
1. [] Enter `Address`, select **Add**, then select **Done**.

    !IMAGE [y5t3b9lk.jpg](instructions353330/y5t3b9lk.jpg)
1. [] In the **Description** field, enter `Complete address of the account`.

1. [] Select **Save** in the upper-right corner of the pane.

    !IMAGE[m45v8wcf.jpg](instructions353330/m45v8wcf.jpg)

1. [] Select the **Glossary** tab.

    !IMAGE[1lnkhzxy.jpg](instructions353330/1lnkhzxy.jpg)

1. [] Enter the following:

    | Item | Value |
    | ---- | ----- |
    | **Enter term** | `Customer` |
    | **Enter description** | `Customer is a synonym for account` |
1. [] Select **Add**.

    !IMAGE[8oafqb8g.jpg](instructions353330/8oafqb8g.jpg)

    > [!note] This improves the understanding of user questions about accounts.
1. [] Select **Save** in the upper-right corner of the pane.

1. [] **Dataverse** is an internal data source, so end users have to be signed in.

    Select **Settings** near the upper-right corner of the page.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] Select **Security** on the left settings menu.
1. [] Select **Authentication**, select **Authenticate with Microsoft**, then select **Save**.

    !IMAGE[k7mnbp8d.jpg](instructions353330/k7mnbp8d.jpg)

    >[!Note] This data source requires authentication because searches are done in the context of the connected end user. Only records the end user has read access to, at minimum, are returned and summarized.
1. [] Select **Save** on the dialog.
1. [] Once successfully saved, select the **X** in the upper-right part of the **Settings** page to return to your knowledge sources.

    !IMAGE [u264sl1d.jpg](instructions353330/u264sl1d.jpg)

===

# Task 04: Configure a website knowledge source

### Introduction

To provide additional information to Contoso's customers, you can integrate a website as a knowledge source.

### Description

In this task, you'll configure a website knowledge source to allow the agent to access and retrieve information from a specified website. You'll set up the website URL and configure access permissions.

### Success criteria

- You successfully configured the website knowledge source with the correct URL and access permissions.

===

## Key tasks

### 01: Configure a website knowledge source

1. [] Select **Knowledge** on the top bar.

    !IMAGE[dkdkw3gr.jpg](instructions353330/dkdkw3gr.jpg)

1. [] Select **Add knowledge** again in the upper-left part of the window.
1. [] Select **Public websites**.

    !IMAGE[2sjvbkkd.jpg](instructions353330/2sjvbkkd.jpg)
1. [] Enter `https://adoption.microsoft.com/en-us/`, then select **Add**.

    !IMAGE [q4554x3s.jpg](instructions353330/q4554x3s.jpg)
1. [] Select **Add to agent** in the lower-right corner of the pane.

    !IMAGE[wok4n3g9.jpg](instructions353330/wok4n3g9.jpg)

    > [!knowledge] Ensure each knowledge source has a meaningful name and explicit description of what it can return.



>[!Knowledge] **Pro tips**:
>
> - When using the default built-in natural language understanding model, knowledge sources are invoked from the **Create generative answers** node. By default, user sentences that don't trigger a topic will go to the **Conversational boosting** topic, where a **Generative answers** node is pre-configured.
> - When generative AI orchestration is enabled, the large language model will look at each knowledge source model description to know what data source to use to answer a user query.

===

# Task 05: Test website knowledge sources

### Introduction

Contoso, Inc. needs to ensure that their customer service agent can effectively utilize the configured knowledge sources to provide accurate and timely information to their customers, so you will help test the website knowledge source.

### Description

In this task, you'll test the website knowledge sources configured in Microsoft Copilot Studio to verify that the agent can retrieve information and provide relevant answers to customer queries.

### Success criteria

- You successfully tested the website knowledge sources in Microsoft Copilot Studio.
- You verified that the agent can retrieve information from the website knowledge sources and provide relevant answers.
- You confirmed the accuracy and relevance of the information provided by the agent.

===

## Key tasks

### 01: Test website knowledge sources

1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask a question that doesn't match an existing topic to trigger the **Conversational boosting** topic:

    `What is Microsoft Copilot Studio?`

    !IMAGE [j2a2cvf6.jpg](instructions353330/j2a2cvf6.jpg)

    > [!note] Notice there's a citation to ground the answer on, with a link to the source(s) that were used to generate the answer.
1. [] Ask a follow-up question:

    `How do people use it in their business environments?`

    > [!note] Although the follow-up question does not mention a specific product, the generative answer maintains context, ensuring the follow-up is interpreted in relation to the previous message.

    > [!note] You'll return to testing the other added knowledge sources later, as they'll take time to be ready for use.

===

## Custom instructions

Prompt modification allows you to expand the capabilities of generative answers and knowledge sources, by adding custom instructions. When using custom instructions, it's important to follow best practices for prompt engineering. 

Here are some tips to help you get the most out of this feature:

- **Be specific** - Custom instructions should be clear and specific, so the agent knows exactly what to do. Avoid vague or ambiguous language that could lead to confusion or incorrect responses.

- **Use examples** - Provide examples to illustrate your instructions and help the agent understand your expectations. Examples help the agent generate accurate and relevant responses.

- **Keep it simple** - Avoid overloading your custom instructions with too many details or complex logic. Keep your instructions simple and straightforward so the agent can process them effectively.

- **Give the agent an "out"** - Give the agent an alternative path for when it's unable to complete the assigned task. For example, when the user asks a question, you might include "respond with 'not found' if the answer isn't present." This alternative path helps the agent avoid generating false responses.

- **Test and refine** - It's important to test your custom instructions thoroughly to ensure they're working as intended. Adjust as needed to improve the accuracy and effectiveness of your agent's responses.

===

# Task 06: Configure custom instructions for classic orchestration

### Introduction

To customize the behavior of the Contoso customer service agent to better align with their business requirements and customer expectations, you'll configure custom instructions for classic orchestration.

### Description

In this task, you'll configure custom instructions for the customer service agent in Microsoft Copilot Studio to modify its responses and behavior based on specific requirements.

### Success criteria

- You successfully configured custom instructions for the customer service agent in Microsoft Copilot Studio.
- You verified that the agent's responses and behavior align with the specified requirements.

===

## Key tasks

### 01: Configure custom instructions for classic orchestration

When **Classic** orchestration is enabled for intent recognition, instructions need to be set at the **Create generative answers** node level, typically in the **Conversational boosting** system topic (as this node can be added anywhere).

1. [] Select **Topics** on the top bar.
1. [] Select the **System** topics filter near the upper-left corner, then select the **Conversational boosting** topic.

    !IMAGE[mfj3xxl2.jpg](instructions353330/mfj3xxl2.jpg)
1. [] On the **Create generative answers** node, select the ellipsis in the upper-right corner, then select **Properties**.

    !IMAGE [svnf5kqw.jpg](instructions353330/svnf5kqw.jpg)
1. [] In the text box below the **Content moderation level**, enter the following:

    ```
    Talk like a pirate and use pirate expressions.
    Use emojis in your responses.
    Answer in less than 50 words.
    ```

    !IMAGE[r9e3wpg8.jpg](instructions353330/r9e3wpg8.jpg)

1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Test it by asking a question that doesn't match an existing topic.

    `What is Microsoft Copilot Studio?`

    !IMAGE [1zl7iti0.jpg](instructions353330/1zl7iti0.jpg)

===

# Task 07: Configure custom instructions for Generative AI Orchestration

### Introduction

Custom instructions can be set in distinct places, depending on whether you use **Generative AI Orchestration** as the main intent recognition mechanism, or if you use the **Classic** natural language understanding approach.

When **Generative AI Orchestration** is enabled, instructions need to be set at the agent level.

Contoso, Inc. can leverage Generative AI Orchestration to enhance the capabilities of their customer service agent.

### Description

In this task, you'll configure custom instructions for Generative AI Orchestration in Microsoft Copilot Studio to modify the agent's responses and behavior based on specific requirements.

### Success criteria

- You successfully configured custom instructions for Generative AI Orchestration in Microsoft Copilot Studio.
- You verified that the agent's responses and behavior align with the specified requirements.

===

## Key tasks

### 01: Configure custom instructions for Generative AI Orchestration

Custom instructions can be set in distinct places, depending on whether you use **Generative AI Orchestration** as the main intent recognition mechanism, or if you use the **Classic** natural language understanding approach.

When **Generative AI Orchestration** is enabled, instructions need to be set at the agent level.

1. [] Select **Settings** near the upper-right corner of the page.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] Select **Generative AI** on the left settings menu.
1. [] Under **Use generative AI orchestration for your agent's responses?**, select **Yes**, then select **Save** at the bottom of the page.

    !IMAGE[io9kgz2j.jpg](instructions353330/io9kgz2j.jpg)
1. [] Once successfully saved, select the **X** in the upper-right corner of the **Settings** page.
1. [] Select **Overview** on the top bar.

    !IMAGE[40z5x2t7.jpg](instructions353330/40z5x2t7.jpg)
1. [] In the upper-right corner of the **Details** section, select **Edit**.

    !IMAGE[2bisc3yi.jpg](instructions353330/2bisc3yi.jpg)

1. [] In the upper-right corner of the **Instructions** section, select **Edit**.

    !IMAGE[vnf8l6li.jpg](instructions353330/vnf8l6li.jpg)

1. [] Replace the text in the text box with the following:

    ```
    Talk like a pirate and use pirate expressions.
    Use emojis in your responses.
    Answer in less than 50 words.
    ```

1. [] Select **Save** in the upper-right corner of the **Instructions** section.

    !IMAGE[0oeda3a5.jpg](instructions353330/0oeda3a5.jpg)

1. [] Select **Save** in the upper-right corner of the **Details** section.

    !IMAGE[pfnf82cj.jpg](instructions353330/pfnf82cj.jpg)

    > [!knowledge] Note that you can also use variables specific to the user content within the instructions.
    > 
    > !IMAGE [l1ke4bl0.jpg](instructions353330/l1ke4bl0.jpg)

===

# Task 08: Use AI general knowledge

### Introduction

In addition to knowledge sources, you can use AI general knowledge to allow your agent to find and present information in response to customer questions. General knowledge saves you from needing to manually author multiple topics, which may not address all customer questions.

This capability allows the agent to try and answer questions with its own knowledge, outside of any grounding data from your knowledge sources, like asking questions to ChatGPT.

With the built-in, default, natural language understanding model, any user utterance that does not trigger a topic goes to the **Conversational boosting** topic.

Like any other topic, the logic in the **Conversational boosting** topic can be configured to further meet your scenarios.

Contoso, Inc. can ensure that their customer service agent provides accurate and comprehensive answers to customer queries by leveraging AI general knowledge.

### Description

In this task, you'll enable and test the AI general knowledge feature in Microsoft Copilot Studio to verify that the agent can provide accurate and comprehensive answers to customer queries.

### Success criteria

- You successfully enabled the AI general knowledge feature in Microsoft Copilot Studio.
- You verified that the agent can provide accurate and comprehensive answers to customer queries using AI general knowledge.

===

## Key tasks

### 01: Use AI general knowledge

1. [] On the **Overview** page, move through the page to the **Knowledge** section, then set **Web Search** to **Enabled**.

    !IMAGE[zrs1mhmt.jpg](instructions353330/zrs1mhmt.jpg)

1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask a question that neither matches an existing or a configured knowledge source.

    `Can you list the planets from closest to farthest from the sun?`

    !IMAGE [0uli862m.jpg](instructions353330/0uli862m.jpg)

===

# Task 09: Review the **Generative answers** node

### Introduction

Contoso, Inc. now needs to ensure that their customer service agent can effectively utilize the **Generative answers** node to provide accurate and timely information to their customers.

### Description

In this task, you'll review the **Generative answers** node in Microsoft Copilot Studio to verify that the agent can retrieve information and provide relevant answers to customer queries.

### Success criteria

- You successfully reviewed the **Generative answers** node in Microsoft Copilot Studio.
- You verified that the agent can retrieve information from the **Generative answers** node and provide relevant answers.

===

## Key tasks

### 01: Review the **Generative answers** node

1. [] Select **Topics** on the top bar.
1. [] Select the **System** topics filter near the upper-left part of the window, then select the **Conversational boosting** topic.

    !IMAGE[9y46im2h.jpg](instructions353330/9y46im2h.jpg)
1. [] On the **Create generative answers** node, select the ellipsis in the upper-right corner, then select **Properties**.

    !IMAGE [svnf5kqw.jpg](instructions353330/svnf5kqw.jpg)
1. [] Under **Knowledge sources**, select the toggle on for **Search only selected sources**.

    !IMAGE [motwgeha.jpg](instructions353330/motwgeha.jpg)

    > [!note] With this selected, you can hand pick the knowledge sources that should be used when entering that specific node.
1. [] Select all knowledge sources by selecting the checkbox next to the **Name** header.

    !IMAGE [xc02vj8h.jpg](instructions353330/xc02vj8h.jpg)
1. [] Under **Classic data**, disable **Allow the AI to use its own general knowledge** by selecting the toggle.
1. [] Under **Content moderation level**, select the **Customize** checkbox.

    !IMAGE[wh3uyrwi.jpg](instructions353330/wh3uyrwi.jpg)

    > [!knowledge] The **Content moderation** setting is the level of controls you apply to avoid the agent from hallucinating (that is, coming up with a wrong answer to a question by misinterpreting or overinterpreting grounding data).
1. [] Select **Save** in the upper-right part of the canvas to save the topic.

    > [!alert] Disregard any authentication errors under **Data sources**, as they won't apply to the tests in this lab.
    > 
    > !IMAGE [x30n5q8t.jpg](instructions353330/x30n5q8t.jpg)

===

# Task 10: Test the Dataverse knowledge source

### Introduction

Now you'll help Contoso ensure that their customer service agent can effectively utilize the Dataverse knowledge source to provide accurate information.

### Description

In this task, you'll test the Dataverse knowledge source configured in Microsoft Copilot Studio to verify that the agent can retrieve structured data and provide relevant answers.

### Success criteria

- You successfully tested the Dataverse knowledge source in Microsoft Copilot Studio.
- You verified that the agent can retrieve structured data from the Dataverse knowledge source and provide relevant answers.

===

## Key tasks

### 01: Test the Dataverse knowledge source

1. [] Select **Knowledge** on the top bar.
1. [] Verify **Dataverse** shows as **Ready** under **Status** before proceeding.

    !IMAGE[22mtzlnt.jpg](instructions353330/22mtzlnt.jpg)

1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask the following about the accounts in the table:

    `Which customers are located in Redmond? List them in a table with their name and address.`

    >[!alert] If the agent does not return any data, continue to the next task, as the Dataverse sample data is currently not deploying.

1. [] Ask a follow-up:

    `Thanks. Who's the primary contact at city power and light?`

    !IMAGE [1kvlrqp6.jpg](instructions353330/1kvlrqp6.jpg)

===

# Task 11: Test the SharePoint knowledge source

### Introduction

Contoso, Inc. also needs to ensure that their customer service agent can use the SharePoint knowledge source.

### Description

In this task, you'll test the SharePoint knowledge source configured in Microsoft Copilot Studio to verify that the agent can retrieve information and provide relevant answers.

### Success criteria

- You successfully tested the SharePoint knowledge source in Microsoft Copilot Studio.
- You verified that the agent can retrieve information from the SharePoint knowledge source and provide relevant answers.

===

## Key tasks

### 01: Test the SharePoint knowledge source

1. [] Select **Knowledge** on the top bar.

    !IMAGE [r98jsagl.jpg](instructions353330/r98jsagl.jpg)

    >[!note] While the **Status** will show **Ready** for the SharePoint knowledge source, it may take more time to index all of its contents. It should not affect this test, as you'll simply verify it can pull any content.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask a question related to the SharePoint site:

    `Give me some information on what the Mark 8 Project Team is working on.`

    !IMAGE [0iyvjxd2.jpg](instructions353330/0iyvjxd2.jpg)

===

# Task 12: Test the Files knowledge source

### Introduction

Now you can help Contoso test that their customer service agent can effectively utilize the Files knowledge source.

### Description

In this task, you'll test the Files knowledge source configured in Microsoft Copilot Studio to verify that the agent can retrieve information and provide relevant answers.

### Success criteria

- You successfully tested the Files knowledge source in Microsoft Copilot Studio.
- You verified that the agent can retrieve information from the Files knowledge source and provide relevant answers.

===

## Key tasks

### 01: Test the Files knowledge source

1. [] Select **Knowledge** on the top bar.
1. [] Verify **Azure - Compliance Offerings** shows as **Ready** before proceeding.

    !IMAGE [ate8e4xi.jpg](instructions353330/ate8e4xi.jpg)

    > [!alert] This may take around 25 minutes depending on how quickly you moved through these tasks.
    > 
    > This section refreshes automatically at regular intervals, but you can also manually refresh it by selecting the refresh button in the upper-right corner.
    > 
    > !IMAGE [y6zb73ii.jpg](instructions353330/y6zb73ii.jpg)
1. [] Select the**+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask a question related to the file:

    `What are Microsoft's distinct Azure cloud environments?`

    !IMAGE [0ilkh5st.jpg](instructions353330/0ilkh5st.jpg)

    > [!note] Observe how the uploaded PDF is used as a reference in the agent's response.

***

> [!knowledge] After configuring knowledge sources, you must publish your agent to make it available in Teams:
>
> 1. Download the app package (ZIP file) from Microsoft Copilot Studio. You can find this under **Channels** by selecting the **Download app** option.
> 2. Open Microsoft Teams and go to the **Apps** section.
> 3. Select **Upload a custom app** and upload the ZIP file.
> 4. Assign the app to the appropriate Teams channel or users.

===

## Summary

Congratulations on completing Exercise 05!

You've learned how to:

- Make your agent instantly smart by pointing to your website and other knowledge sources.
- Navigate to the Generative AI settings.
- Navigate to the Conversational Boosting system topic.
- Set custom prompt instructions.

===

# Exercise 06: Use generative AI orchestration to interact with your connectors

## Scenario

Some customer requests require dynamic actions rather than static answers. Contoso intends to expose line‑of‑business operations (such as creating or updating cases) through plugin actions that the agent can invoke on demand. This exercise shows how to enable generative AI orchestration, let the agent choose the right action at runtime, and test the end‑to‑end flow.

## Objectives

After this exercise you'll be able to:

- Understand the basics of plugin actions.
- Use Copilot Studio to request data from another data source using plugin actions, then return the data in a conversational dialog with the end user.

## Architecture

!IMAGE [7aruww5k.jpg](instructions353330/7aruww5k.jpg)

## Duration

Estimated time: 20 minutes.

===

## Generative AI orchestration

By default, an agent responds to users by triggering the topic whose trigger phrases match most closely the user's query, and it fills topic inputs from the conversation context. You can configure your agent to use generative AI to choose from topics you created, and actions you added to extend the agent.

In generative mode, an agent can fill topic inputs, not only from the conversation context, but also by generating questions to prompt the user for values. To learn more about this behavior and how to manage it, see [Manage topic inputs and outputs](https://learn.microsoft.com/en-us/microsoft-copilot-studio/advanced-managing-topic-inputs-outputs).

Using generative AI to determine how your agent responds can make the conversation more natural and fluid for the users. When a user sends a message, your agent selects one or more actions or topics to prepare its response. Multiple factors determine the selection. The most important factor is the description of the topics and actions. Other factors include the name of a topic or actions, any input or output parameters, and their names and descriptions. Descriptions make it possible for your agent to be more accurate when it associates a user's intent with actions and topics.

In generative mode, an agent can select multiple actions or topics at once to handle multi-intent queries. Once actions and topics are selected, the agent generates a plan determining their execution order.

When you test an agent that uses generative mode in Copilot Studio, you can open the conversation map to follow the execution of the plan.

===

# Task 01: Create an action

### Introduction

Using the configured knowledge sources, Contoso's agent needs to perform actions based on user queries to provide a seamless customer experience. This task involves creating an action using generative AI orchestration.

When you turn on generative mode, your agent can automatically select the most appropriate action or topic to respond to a user at runtime. In classic mode, an agent can only use topics to respond to the user. However, you can still design your agent to call actions explicitly from within topics.

Actions are based on one of the following core action types:

- Prebuilt connector action
- Custom connector action
- Power Automate cloud flow
- AI Builder prompts
- Bot Framework skill

Each core action has additional information that describes its purpose, allowing the agent to use generative AI to generate questions. These questions are required to fill in the inputs needed to perform the action. Therefore, you don't need to manually author **Question** nodes to gather all inputs needed, such as the inputs on a flow. Inputs are handled for you during runtime.

Actions can generate a contextual response to a user's query, using the results of the action. Alternatively, you can explicitly author a response for the action.

### Description

In this task, you'll create an action that allows the agent to interact with external connectors and perform specific tasks. You'll configure the action and set up the necessary inputs and outputs.

### Success criteria

- You successfully created an action with the correct inputs and outputs.
- You verified that the agent can perform the action based on user queries.
- You tested the action by asking relevant questions.

===

## Key tasks

### 01: Create an action

1. [] Select **Tools** on the top bar.

    !IMAGE[ez59rmyy.jpg](instructions353330/ez59rmyy.jpg)
1. [] Select **Add a tool**.

1. [] In the search bar, enter and select `Get forecast for today` from **MSN Weather**.

    !IMAGE[irmwvvty.jpg](instructions353330/irmwvvty.jpg)

1. [] Next to **Connection**, select **Not connected**, then select **Create new connection** from the dropdown menu.

    !IMAGE[xvr59cqs.jpg](instructions353330/xvr59cqs.jpg)

1. [] In the lower-right corner of the pane, select **Create**.

1. [] In the lower-right corner of the pane, select **Add and configure**.

    !IMAGE[6gpfk21k.jpg](instructions353330/6gpfk21k.jpg)

1. [] In the **Get forecast for today** configuration, under the **Details** section, expand **Additional details**.

    !IMAGE[86f3besq.jpg](instructions353330/86f3besq.jpg)


    > [!knowledge] This uses the connector under the context of the agent author, rather than prompting the end user to connect.

1. [] Move through the page down to the **Inputs** section.

1. [] On the line for **Units**, select the dropdown menu for **Fill using**, then select **Custom value**.

    !IMAGE[etuu6r4u.jpg](instructions353330/etuu6r4u.jpg)
1. [] For its **Value**, select **Imperial** from the dropdown menu.

    !IMAGE[z8i72ieu.jpg](instructions353330/z8i72ieu.jpg)

1. [] Review the configuration, then select **Save** in the upper-right corner of the pane.

    !IMAGE[39u2nbdd.jpg](instructions353330/39u2nbdd.jpg)

===

# Task 02: Test your action

### Introduction

Once you've created an action, you'll need to test it to ensure the agent can perform actions accurately.

### Description

In this task, you'll test the created action by interacting with the agent, asking relevant questions, observing the agent's behavior, and verifying its responses.

### Success criteria

- You successfully tested the action by interacting with the agent.
- You verified that the agent performs the action accurately based on user queries.
- You observed and documented the agent's behavior.

===

## Key tasks

### 01: Test your action

1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Ask a vague question about the weather:

    `How is the weather today?`

    !IMAGE[xs5oex36.jpg](instructions353330/xs5oex36.jpg)

    > [!note] The agent will request more details for a location, and the **Activity map** will display in the main pane.
1. [] Respond with a city:

    `Dallas`

    !IMAGE[vrs2gcfd.jpg](instructions353330/vrs2gcfd.jpg)

    > [!note] The agent automatically updates the **Inputs** with the city and provides an answer.
1. [] Tell the agent you made a mistake, and ask for another location:

    `Wait, I meant the weather for London. Also, please list all information you have in bullet points.`

    !IMAGE [96lnl1mh.jpg](instructions353330/96lnl1mh.jpg)

    > [!note] Observe how the agent updates its query to the connector, and see how it also reacts to the instructions to list all information available to it.

===

## Summary

Congratulations on completing Exercise 06! You've successfully:

- Created an action in Copilot Studio.
- Displayed dynamic data back to the user.
- Leveraged conversational context to ask follow-up questions.

===

# Exercise 07: Invoke AI Builder prompts

## Scenario

Contoso wants the agent to send personalised follow‑up messages and summaries that go beyond simple data retrieval. AI Builder prompts allow makers to design custom instructions for large‑language‑model output, using variables captured earlier in the conversation. You will create and test a prompt that drafts customer‑ready communications automatically.

## Objectives

After this exercise, you'll be able to:

- Understand the basics of AI Builder prompts
- Invoke a custom prompt that leverages Copilot Studio variables.

## Architecture

!IMAGE [0m7r9ozs.jpg](instructions353330/0m7r9ozs.jpg)

## Duration

Estimated time: 25 minutes.

===

## AI Builder prompts

AI Builder prompts let you define a task or goal for a large language model (LLM) using natural language. With Prompt Builder, makers can create, test, and reuse custom prompts-complete with dynamic input variables-tailored to specific business needs.

These prompts can be shared and used across Power Automate, Power Apps, and Copilot Studio. For example, you might build a prompt to extract action items from company emails and trigger a workflow in Power Automate. Other use cases include summarizing content, classifying requests, extracting key details, translating responses, assessing sentiment, or drafting replies in the right tone.

Prompts can be integrated into flows to automate tasks or embedded in Copilot Studio agents to deliver context-aware, natural responses at runtime. By carefully designing your instructions, you can control how the model behaves, making AI Builder a powerful and flexible tool for streamlining operations, personalizing experiences, and boosting productivity.

===

# Task 01: Change to classic orchestration

### Introduction

While generative orchestration is powerful, there are scenarios - such as tightly regulated industries or highly deterministic workflows - where Contoso must disable it and fall back to the classic, topic‑only model. This task walks you through switching the agent to classic orchestration.

### Description

You will open the Generative AI settings pane, change the interaction mode from Generative to Classic, and save the configuration. Afterwards, you'll verify the change in the agent's settings and understand how this affects topic triggering and action selection.

### Success criteria

- The Generative AI setting is set to Classic and saved without errors.
- The agent no longer displays the Generative badge on the Overview page.
- Manual tests confirm that only explicit topic triggers are executed; no automatic action runs occur.

===

## Key tasks

### 01: Change to classic orchestration

1. [] Select **Settings** near the upper-right corner of the page.

    !IMAGE [3f5fs0ge.jpg](instructions353330/3f5fs0ge.jpg)
1. [] Select **Generative AI** on the left settings menu.
1. [] Under **Use generative AI orchestration for agent's responses?**, select **No**, then select **Save** at the bottom of the page.

    !IMAGE[sqklu5pn.jpg](instructions353330/sqklu5pn.jpg)
1. [] Once successfully saved, select the **X** in the upper-right corner of the **Settings** page.

===

# Task 02: Create a prompt

### Introduction

Contoso would like their agent to generate responses based on dynamic inputs, providing personalized customer service. You can support this with AI Builder prompts.

### Description

In this task, you'll create a custom prompt that leverages Copilot Studio variables to generate personalized responses. You'll configure the prompt and set up the necessary inputs and outputs.

### Success criteria

- You successfully created a custom prompt with the correct inputs and outputs.
- You verified that the agent can generate personalized responses based on dynamic inputs.
- You tested the prompt by interacting with the agent.

===

## Key tasks

### 01: Create a prompt

1. [] Select **Topics** on the top bar.
1. [] Select the **Check Ticket Status** topic.

    !IMAGE[zrjfnabs.jpg](instructions353330/zrjfnabs.jpg)

    >[!Note] Our goal is to use Generative AI to draft a letter to the user based on the issue raised in the ServiceNow ticket.

1. [] Below the **Message** node, select the **+** button, select **Add a tool**, then select **New prompt**.
    
    !IMAGE[otf9j8yd.jpg](instructions353330/otf9j8yd.jpg)
    
1. [] For the prompt name, enter `Ticket customer communication` in the top text box.

    !IMAGE[qnn7c80r.jpg](instructions353330/qnn7c80r.jpg)
1. [] In the left **Instructions** section, enter the following instructions:

    ```
    Based on the ticket details, write a personalized apologetic message to the person impacted. You can summarize the issue to show you understand it. Show empathy and suggest ways to mitigate the situation based on the ticket details. Have a positive attitude and use emojis when applicable. Don't include hashtags. Text should be a single paragraph. Do not use a signature. 
    
    ## Ticket Details 
    ```
1. [] Select **Enter** to add a new line below the added instructions.
1. [] Enter `/` to bring up the menu for adding new input or knowledge, then select **Text** from the dropdown menu.

    !IMAGE [ldsbosto.jpg](instructions353330/ldsbosto.jpg)
1. [] In the dialog, enter `Ticket Details` for the **Name**.
1. [] Under **Sample data**, enter the previously used **ServiceNow Sample JSON Payload**.

    > [!alert] Use the **Copy** option on the following code block and paste it with **Ctrl+V**, rather than use **Type**.

    ```json
    {
    	"parent": "",
    	"made_sla": "true",
    	"caused_by": "",
    	"watch_list": "",
    	"upon_reject": "Cancel all future Tasks",
    	"sys_updated_on": "2018-12-12 23:18:55",
    	"child_incidents": "0",
    	"hold_reason": "",
    	"origin_table": "",
    	"task_effective_number": "INC0009005",
    	"approval_history": "",
    	"number": "INC0009005",
    	"resolved_by": "",
    	"sys_updated_by": "admin",
    	"opened_by": "System Administrator",
    	"user_input": "",
    	"sys_created_on": "2018-08-31 21:35:45",
    	"sys_domain": "global",
    	"state": "New",
    	"route_reason": "",
    	"sys_created_by": "admin",
    	"knowledge": "false",
    	"order": "",
    	"calendar_stc": "",
    	"closed_at": "",
    	"cmdb_ci": "",
    	"delivery_plan": "",
    	"contract": "",
    	"impact": "1 - High",
    	"active": "true",
    	"work_notes_list": "",
    	"business_service": "",
    	"business_impact": "",
    	"priority": "1 - Critical",
    	"sys_domain_path": "/",
    	"rfc": "",
    	"time_worked": "",
    	"expected_start": "",
    	"opened_at": "2018-08-31 21:35:21",
    	"business_duration": "",
    	"group_list": "",
    	"work_end": "",
    	"caller_id": "David Miller",
    	"reopened_time": "",
    	"resolved_at": "",
    	"approval_set": "",
    	"subcategory": "Email",
    	"work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"universal_request": "",
    	"short_description": "Email server is down.",
    	"correlation_display": "",
    	"delivery_task": "",
    	"work_start": "",
    	"assignment_group": "",
    	"additional_assignee_list": "",
    	"business_stc": "",
    	"cause": "",
    	"description": "Unable to send or receive emails.",
    	"origin_id": "",
    	"calendar_duration": "",
    	"close_notes": "",
    	"notify": "Do Not Notify",
    	"service_offering": "",
    	"sys_class_name": "Incident",
    	"closed_by": "",
    	"follow_up": "",
    	"parent_incident": "",
    	"sys_id": "ed92e8d173d023002728660c4cf6a7bc",
    	"reopened_by": "",
    	"incident_state": "New",
    	"urgency": "1 - High",
    	"problem_id": "",
    	"company": "",
    	"reassignment_count": "0",
    	"activity_due": "2018-12-13 01:18:55",
    	"assigned_to": "",
    	"severity": "3 - Low",
    	"comments": "",
    	"approval": "Not Yet Requested",
    	"sla_due": "UNKNOWN",
    	"comments_and_work_notes": "2018-12-12 23:18:42 - System Administrator (Work notes)\nupdated the priority to high based on the criticality of the Incident.\n\n",
    	"due_date": "",
    	"sys_mod_count": "3",
    	"reopen_count": "0",
    	"sys_tags": "",
    	"escalation": "Normal",
    	"upon_approval": "Proceed to Next Task",
    	"correlation_id": "",
    	"location": "",
    	"category": "Software"
    }
    ```
1. [] Select **Close** in the lower-right corner of the dialog.

    !IMAGE [97fr1xfp.jpg](instructions353330/97fr1xfp.jpg)
    !IMAGE[983txzer.jpg](instructions353330/983txzer.jpg)
1. [] Select the **Model** dropdown at the top of the **Instructions** section, then select **Standard GPT-4.1**.

    !IMAGE[ldfnydat.jpg](instructions353330/ldfnydat.jpg)
1. [] Select **Save** in the lower-right corner of the prompt pane.

    !IMAGE[7afy9jkv.jpg](instructions353330/7afy9jkv.jpg)

===

### 02: Configure the **Prompt** and **Message** nodes

1. [] In the new **Prompt** node, under **Inputs**, select the ellipsis **(...)**, then select the **SNTicketInfo** variable.

    !IMAGE[1jp4h3hx.jpg](instructions353330/1jp4h3hx.jpg)
1. [] Under **Outputs**, select **Select a variable**, then select **Create a new variable**.

    !IMAGE [2o04d5ap.jpg](instructions353330/2o04d5ap.jpg)
1. [] Select the **Var1** variable under **Outputs**, then set **Variable name** to `PersonalizedMessage`.

    !IMAGE[bkb6o39v.jpg](instructions353330/bkb6o39v.jpg)
1. [] Under the **Prompt** node, add a **Message** node.
1. [] In the **Message** node, select the **{x}** (insert variable) icon, then select the **PersonalizedMessage.text** variable.

    !IMAGE [gqm9bump.jpg](instructions353330/gqm9bump.jpg)
1. [] Select **Save** in the upper-right part of the canvas to save the topic.
1. [] Select the **+** icon in the upper-right corner of the **Test your agent** pane to start a new conversation.
1. [] Test the agent by entering the following prompt:

    `Hi, could I get an update on ticket INC0007001?`

    !IMAGE [uozaavge.jpg](instructions353330/uozaavge.jpg)

===

## Summary

Congratulations on completing Exercise 07! You've successfully:

- Created a custom prompt from Copilot Studio.
- Passed it inputs and used its output as a generated answer for the end user.

===

# Conclusion

**Congratulations!** You've successfully completed this lab!
