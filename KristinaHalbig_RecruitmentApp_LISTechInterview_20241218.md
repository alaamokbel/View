# 📌 SynapticSci Technical Exercise: Creating a Model-Driven App With Dataverse and PowerApps

## Table of Contents

01 - [Introduction](#introduction)<br>
02 - [Functionalities](#functionalities)<br>
03 - [Architecture and Data Model](#architecture-and-data-model)<br>
04 - [User Interface Development](#user-interface-development)<br>
05 - [Workflow and Processes](#workflow-and-processes)<br>
06 - [Status Tracking and Business Rules](#status-tracking-and-business-rules)<br>
07 - [Challenges and Solutions](#challenges-and-solutions)<br>
08 - [Potential Improvements](#potential-improvements)<br>
09 - [Conclusion](#conclusion)

## Introduction

For this exercise, I developed a model-driven app to track hiring roles, applications, and interview processes for open positions at Kepler Labs, a fictitious laboratory. I chose to follow a tutorial by Lisa Crosbie titled [Model Driven Power Apps Full Course for Beginners](https://www.youtube.com/watch?v=HrILchHvMUA&t=7750s) and modified the data to be more relevant for laboratory environments.

While I completed Microsoft's training on creating and managing model-driven apps, I find it beneficial to use multiple resources when learning new skills. Microsoft's training provided a solid foundation, but Lisa Crosbie's video offered insights into features like business process flows and Power Apps grid control.

## Functionalities

The model-driven app provides seamless tracking for open roles, associated applications, and their current stages in the interview process. The built-in business process flow ensures all necessary information is completed and helps users monitor the timeline of each application. Conditional logic adds a step for reference checks when needed.

The Power Apps grid control enables users to drill down into each role, view the number of applications, and quickly identify successful interview outcomes with color-coded indicators. The same color-coding system highlights the statuses of open and filled roles.

Quick Create Forms for Applications and Contacts streamline the creation of new records, making data entry faster.

The Welcome Page offers an at-a-glance view of open roles, which can be clicked to access detailed information. Additionally, a shortcut button allows users to navigate directly to a list of all active applications.

## Architecture and Data Model

The model-driven app is housed in a solution called **Lab Solution**.  The following objects are required for the model-driven app.

### Solution: Lab Solution
|Display Name|Type|Purpose|
|---|---|---|
|**Application**|*Table*|Contains relevant data, such as application number, candidate name, and interview outcome
|**Contact**|*Table*|Standard table that stores candidate data, including name and email
|**Department**|*Choice*|List of departments within the lab
|**Managers**|*Table*|Stores data about managers, including names and email addresses
|**Outcomes**|*Choice*|Options for 'Successful' or 'Unsuccessful,' required for completing the application form
|**Recruitment App**|*Model-Driven App*|The model-driven application used for recruitment tracking
|**Recruitment Process**|*Business Process Flow*|Conditional business process flow that adds reference check fields if required.
|**Recruitment Process**|*Table*|Table that is required to accompany the business process flow of the same name
|**Role**|*Table*|Contains data about lab roles, including name, department, and reporting manager
|**Welcome Page**|*Page*|Page that appears when app starts with links to open applications and specific roles


The following data dictionaries outline the tables the model-driven app uses.  Four main tables are used: **Application**, **Contact**, **Managers**, and **Role**.

### **Table: Application**

|Column Name|Type|Data|
|---|---|---|
|**Application Number**|*Auto Number*|Automatically assigned number for each application
|**Role**|*Text*|Lab role title
|**Candidate**|*Text*|Name of candidate applying for the role
|**Interview Start Time**|*Date and Time*|Scheduled date and time of interview
|**Interview Outcome**|*Choice*|Indicates whether the interview was 'Successful' or 'Unsuccessful'
|**Offer Made?**|*Choice*|Indicates if an offer was made, with options for 'Yes' or 'No.'

### **Table: Contact (Standard Table)**

|Column Name|Type|Data|
|---|---|---|
|**Full Name**|*Text*|Name of person
|**Email**|*Email*|Email of person
|**Business Phone**|*Phone Number*|Business phone number of person

### **Table: Managers**

|Column Name|Type|Data|
|---|---|---|
|**Manager Name**|*Text*|Name of manager
|**Email**|*Email*|Email of manager
|**Department**|*Choice*|Department to which the manager belongs

### **Table: Role**

|Column Name|Type|Data|
|---|---|---|
|**Name**|*Text*|Name of role
|**Created On**|*Date and Time*|Date and time the role was created
|**Department**|*Choice*|Department to which the role belongs
|**Reports To**|*Text*|Manager who oversees the department
|**Role Status**|*Choice*|Indicates if the role is 'Open' or 'Filled'

### Relationships

#### The following diagrams showcase the relationships between tables that the model-driven app uses.

[![Many Candidates to One Application Number](https://i.postimg.cc/0jWsmyPR/apptocandidate.png)](https://postimg.cc/0KwF1xzc)
<p align="center"><em>Many to one relationship between Applications and Contacts table - one application can have many candidates</em></p>
<br>

[![Many Applications to One Role](https://i.postimg.cc/Hx6mJJvS/roletoapp.png)](https://postimg.cc/S2Y33Kh8)
<p align="center"><em>Many to one relationship between Role and Applications table - one role can have many applications</em></p>
<br>

[![Many Roles to One Manager](https://i.postimg.cc/0N33hp31/managertorole-drawio-4.png)](https://postimg.cc/xkvtzbn6)
<p align="center"><em>Many to one relationship between Manager and Role table - one manager can oversee many roles</em></p>

## User Interface Development

### Welcome Page
The user is greeted with a welcome page upon opening the model-driven application.  From here, they have the choice of clicking on the arrow to the right of the open role to see both details about the role and the application submitted for the role. They can also click on the 'Applications' button to view all open applications.

[![Welcome Page](https://i.postimg.cc/k4fWBsn5/welcome.jpg)](https://postimg.cc/sQGMLpGF)

### Roles View
The Roles view displays all active roles, showing their department, manager, and color-coded status of open or filled. Clicking the arrow beside a role name reveals a dropdown with associated applications, including candidate names, interview start times, and a color-coded indicator for interview outcomes.

[![Roles View](https://i.postimg.cc/PJ6FzY17/rolesview.jpg)](https://postimg.cc/4H95XKLv)

### Individual Role View

**NOTE: This view is accessed either by clicking on a role link in the Roles view OR clicking on the arrow next to a role on the Welcome Page.**<br>
The individual role view displays detailed information about a specific role, including its department and status (open or filled). It also lists associated applications for the role, showing details like the application number and candidate name.

[![Individual Role View](https://i.postimg.cc/FRNPMDZq/individualroleview.jpg)](https://postimg.cc/QBYk5gvk)

### Applications View
**NOTE: This view is accessed either by clicking on Application in the navigation pane on the left OR clicking on Applications button on the Welcome Page.**<br>
This view shows all of the active applications across all roles.  Details include the application number, interview outcome, and if an offer was made to the candidate.

[![applicationsview.jpg](https://i.postimg.cc/prx3jXf6/applicationsview.jpg)](https://postimg.cc/XGH2SWDf)

### Individual Application View
This view is accessed by clicking on an application number. It features two tabs:

* **General Tab:** Displays application details, candidate information, and a timeline of recorded activities related to the application.
* **Interview Tab:** Provides interview details and includes a comments section.

A business process flow is integrated into this view to guide users through entering application-related data, with an option to add a reference check entry if required.

[![General Tab](https://i.postimg.cc/y69mmFy3/individualapplication.jpg)](https://postimg.cc/Z0bvZvgJ)
[![Interview Tab](https://i.postimg.cc/zBFFTWry/individualapplication2.jpg)](https://postimg.cc/ftkdNVks)

### Contacts View
This view displays a list of contacts from the out-of-the-box Contacts Table in Power Apps. The Candidate column references this table to retrieve candidate details.

[![Contacts View](https://i.postimg.cc/FsHKrvzF/contactsview.jpg)](https://postimg.cc/xqBQ5WLB)

### Quick Create Forms
Both the Application and Contact tables make use of Quick Create forms so that the user can easily create new records with minimal navigation.  The Quick Create forms can be accessed by clicking on the plus symbol on the upper right.

[![quickcreateforms.png](https://i.postimg.cc/RVCqSYZr/quickcreateforms.png)](https://postimg.cc/14TyMJFM)<br>
[![quickcreateapplication.jpg](https://i.postimg.cc/DwfppCxM/quickcreateapplication.jpg)](https://postimg.cc/2VJxVxRQ)<br>
[![quickcreatecontact.jpg](https://i.postimg.cc/d1QYKbJD/quickcreatecontact.jpg)](https://postimg.cc/t1cf3mZH)

## Workflow and Processes

The flowchart below illustrates the basic workflow of the recruitment app. A business process flow includes a conditional step to perform a reference check when required. New applications can be created through the Applications view or via a Quick Create Form. Additionally, new contacts, managers, and roles can be added to the database as needed.

[![flowchart.png](https://i.postimg.cc/Lsf9RJnX/flowchart.png)](https://postimg.cc/GBLwxhPw)



# Status Tracking and Business Rules

Status tracking for role status, interview outcomes, and offers is available in the Roles view. Each role references the Applications table, allowing users to view all associated applications by clicking the arrow next to the role. Role statuses and interview outcomes are color-coded for quick identification.

For an example of status tracking in the recruiting app, refer to the [Roles View](#roles-view) sub-section in this document, which includes a screenshot.

The screenshot below illustrates the business process flow for determining whether an application requires a reference check. If a reference check is needed, the app prompts the user to complete fields for the reference check date and outcome.

[![Business Process Flow for Reference](https://i.postimg.cc/zB3s5Xwm/referenceflow.jpg)](https://postimg.cc/phbGJv1k)



# Challenges and Solutions

One of the biggest challenges I faced when building the recruitment app was the unexpected behavior of the Applications table after adding it to the app. The views and forms didn’t match the ones I had created, and the business process flow for the reference check was missing. After some investigation, I realized I had accidentally added a pre-built Dataverse table named "Applications" instead of my custom table.  The one I created started with 'cra00'. I identified the mistake by noticing the name in the 'Name' column differed, with my name prefixed with 'cra00.' Once I removed the pre-built table and added my custom one, the issue was resolved.

[![dupeapp.jpg](https://i.postimg.cc/0QfzgnCX/dupeapp.jpg)](https://postimg.cc/r0DVxS35)

Another general issue I experienced was deleting tables and apps.  For practice, I created this app from scratch twice.  Model-driven apps create relationships and dependencies that must be disconnected before deletion. I spent significant time understanding these dependencies, including those from automatically created tables. The most challenging part was removing the Power Apps grid control, as its dependency was not immediately apparent to me.

## Potential Improvements

The application could benefit from adding automatic triggers. For example, a new column in the Applications table titled "Accepted Offer?" could automatically change a role’s status from "Open" to "Filled" when set to "Yes." Additional triggers could include sending automated emails to relevant parties when a new application is submitted or when an offer is made. Further automation might deactivate applications that did not result in a successful hire.

Dashboard visualizations would also improve the app by tracking hiring metrics. Useful metrics could include the number of applicants per role and the average time for the interview process. This data could help the laboratory refine job roles to attract more applicants and streamline hiring by identifying bottlenecks in the process.

## Conclusion

Using guidance from tutorials, I developed a basic Model-Driven Power App designed to track and fill roles at a fictitious laboratory. The app enables users to create and monitor applications, incorporates a business process flow for references, and features color-coded statuses for easy navigation, along with a welcome page for quick access to key views.

This was my first experience building a model-driven app, and through this project, I gained skills in creating custom tables, views, and forms, as well as managing dependencies and relationships between tables. I also developed troubleshooting experience, particularly in understanding the distinction between Power Apps' pre-built tables and custom tables.

This exercise demonstrates my ability to quickly learn and apply new technologies to optimize laboratory operations. My experience in technical documentation and attention to detail is evident in this project, and I see significant potential for these skills to enhance lab processes such as inventory tracking and sample management. I am excited about the opportunity to bring my laboratory experience and technical adaptability to SynapticSci’s team, helping laboratories work smarter and faster with their data.