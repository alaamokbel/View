

 
# Contoso Real Estate App

## Table of Contents

1. [Introduction](#introduction)
2. [Functionalities](#functionalities)
3. [Architecture and Data Model](#architecture-and-data-model)
4. [User Interface (UI) Development](#user-interface-ui-development)
5. [Workflow and Processes](#workflow-and-processes)
6. [Status Tracking and Business Rules](#status-tracking-and-business-rules)
7. [Challenges and Solutions](#challenges-and-solutions)
8. [Potential Improvements](#potential-improvements)
9. [Conclusion](#conclusion)

## Introduction

The **Contoso Real Estate App** is a model-driven application built using Microsoft Power Apps and Dataverse. This application was developed based on the guided project in Microsoft Learning Path Create and manage model-driven apps with power Apps and Dataverse, with additional features added to enhance the application.  
The app streamlines the management of commercial and residential real estate properties and client interactions of a fictional company named Contoso Real Estate, which keeps track of property listings. This app demonstrates how businesses can effectively use low-code platforms to create efficient and scalable solutions based on their needs.

## Functionalities

The Contoso Real Estate App provides the following functionalities:

- **Property Listings Management**: Add, edit, and view details of real estate properties.
- **Showings Management**: Schedule, track, and record information about property showings.
- **Client Interaction**: Maintain customer data and associate showings with clients.
- **Navigation and Grouping**: Logical organization of clients and properties for seamless navigation.
- **Data Visualization**: Interactive dashboard charts for enhanced insights.

## Architecture and Data Model

### Tables

The app utilizes Dataverse to manage its data including the following tables:

1. **Real Estate Properties**: 
   - Columns: Property Name (Text), Asking Price (Number), Street (Text), City (Text), Bedrooms (Lookup), Bathrooms (Lookup), Sold (Yes/No).
   - Relationships: Related to Showings table.

2. **Showings**: 
   - Columns: Name (Text), Showing Date (Date), Shown to (Lookup to Contact), Shown by (Lookup to User), Property Shown (Lookup to Real Estate Property), Comments (Text), Level of Interest (Lookup).

3. **Contacts**: Pre-existing table for customer information.

4. **Account**: Pre-existing table for account information.

### Relationships

- **One-to-Many**:

    - Real Estate Properties to Showings: Each property can have multiple showings.
    - Accounts to Contacts: Each account can have multiple associated contacts.

- **Lookup Relationships**:

    - Showings to Real Estate Properties: Links each showing to a specific property.
    - Showings to Contacts: Links each showing to a client.
    - Showings to Users: Links the "Shown by" field to a specific user (agent).

These relationships ensure data integrity and enable seamless navigation between related records, providing an integrated view of property and client interactions.

## User Interface (UI) Development

The UI is developed using the model-driven app designer, ensuring consistency and responsiveness.

- **Real Estate Properties Form** (Renamed to **Property Information**): Contain sections such as *Address Information* that includes Street and City fields and *Showings*, sub-grid displaying related showings with the Active Showings view.
[Real Estate Properties Form](https://drive.google.com/file/d/1d4vkvER4QY6ejpjvucIP6pASTY83ausb/view?usp=drive_link)

- **Showings Form** (Renamed to Showing details): Included fields like Property Shown, Showing Date, Shown to, Shown by, Level of Interest, Comments.
[Showings Form](https://drive.google.com/file/d/1PTrQnyaxq6cpFarqRyUL-3ghpUSiigY0/view?usp=drive_link)

-  **Accounts Form**: Contain sections such as *Account Information* that includes Name, Phone and City fields, *Address* and *Contacts*.
[Accounts Form](https://drive.google.com/file/d/1204N2xu38Bz9k9W5NwDYLNM4WwD80pr2/view?usp=drive_link)

- **Contacts Form**: Included fields for personal information Name, Job title, Email, Phones and Address.
[Contacts Form](https://drive.google.com/file/d/1IiK7fPF5hl5YSAAYCMAP505mTWy9HhcI/view?usp=drive_link)

- **Active Real Estate Properties View:** 
  Added columns: Property Name, Asking Price, City, Bedrooms, Bathrooms, Sold.
[Real Estate Properties View](https://drive.google.com/file/d/1_nDJ5-nSjksfRX98CxXUHo_oIy8ELuRf/view?usp=drive_link)

- **Active Showings View:** 
  Added columns: Name, Property Shown, Showing Date, Shown to, Level of Interest.
[Showings View](https://drive.google.com/file/d/1BSDUaL9dv42KGlwIOBoOAQntUd_E6AHm/view?usp=drive_link)

- **Active Accounts View:** 
  Added columns: Account Name, Main Phone, Address, Primary Contact, Email.
[Accounts View](https://drive.google.com/file/d/1_muEzQZsd1zCoIcr5Uzhait7Nf_rz3ok/view?usp=drive_link)

- **Active Contacts View:** 
  Added columns: Full Name, Email, Company Name and Business Phone.
[Contacts View](https://drive.google.com/file/d/1_muEzQZsd1zCoIcr5Uzhait7Nf_rz3ok/view?usp=drive_link)


The UI includes a dashboard with the following visualizations:

- **New Accounts by Month**: A column chart displaying new accounts created each month.

- **Asking Price by City**: A column chart showing the average asking price per city.

- **Property Name by Sold Status**: A column chart showing properties grouped by whether they are sold or not.

- **Level of Interest in a Property**: A column chart displaying the level of interest for each property.

- **Property Showings Over Time**: A line chart at the bottom showing the number of property showings by date.

[Dashboard](https://drive.google.com/file/d/1eX7gkm85Z97OfAmA4tU1uUy6osMPABfr/view?usp=drive_link))

#### Navigation

The navigation pane provides access to three main sections:

- **Clients Group**: Includes Contacts and Accounts table.
- **Properties Group**: Includes Real Estate Properties and Showings table.
- **Dashboard Section**: Includes an interactive dashboard with visualizations.

[Navigation](https://drive.google.com/file/d/1KBaYEDdt-HWV-kKJeiN-SSNhpsSPvRJG/view?usp=drive_link)


## Workflow and Processes

1. **Adding a contact:

   - Navigate to Contact.
   - Create a new contact filling out the corresponding fields like Name and personal information.

2. **Create an account:**

   - Navigate to accounts.
   - Create a new account and input the account information.

3. **Adding a New Real Estate Property**:

   - Navigate to Real Estate Properties.
   - Create a new property record with details like Property Name, Asking Price, Street, City, Bedrooms, and Bathrooms.

4. **Scheduling a Showing**:

   - Open a property record.
   - Use the Showings sub-grid to create a new showing record.
   - Link it to a client, assign a showing agent, and record the date and comments.

5. **Tracking Client Interest**:

   - Use the *Level of Interest* field to categorize client feedback after showings.

6. **Tracking Sales:

   - Use the *Sold* field to track properties sold by the Company.
   
## Status Tracking and Business Rules

1.  **Validation**:
    - Business rule that ensures that some of the fields cannot be empty (eg. Account Name in the Accounts form, Contact Last Name in the Contact form, Property Name in the Real Estate Properties form and Name and Owner in the Showing form.
[Error empty account name](https://drive.google.com/file/d/1v0kHOofmnaVcC7Ab7HoVTy0cgvBChvRm/view?usp=drive_link)
[Error empty contact last name](https://drive.google.com/file/d/1puo-dn3uJkdwpKNtjZeULDov0DRK9nk4/view?usp=drive_link)
[Error empty property name](https://drive.google.com/file/d/1oPgxwDGH42oej7pUsmcQOFD-NbmNwXbb/view?usp=drive_link)

2. **Automation**:
    - Default Level of Interest set to "None" if left blank.
 
3. **Sub-Grid for Related Records**:
    - Showings linked to properties display only relevant records in the Property Information form.

## Challenges and Solutions

### Challenges

1. **Handling Lookup Relationships Efficiently**: 
- *Solution*: Utilized Dataverse’s lookup fields to establish relationships between tables, ensuring seamless data integration.

2. **User-Friendly Navigation**: Ensuring good performance of the app while keeping it easy to understand.
 - *Solution:* Organized navigation into logical groups (Clients, Properties and Dashboard) for intuitive access.


## Potential Improvements

1. **Email Notifications**:
    - Use Power Automate to notify agents and clients about upcoming showings.

2. **Mobile Optimization**:
    - Enhance app usability on mobile devices for agents in the field.

3. **Advanced Filtering**:
    - Enable users to filter views by specific criteria, such as city or client interest level.
 
## Conclusion

The Contoso Real Estate App is a practical solution tailored to the real estate industry that provides a robust and user-friendly solution for managing property listings and showings.  The app streamlines operations, enhances data visibility, and empowers Contoso Real Estate to manage its processes effectively. It showcases the power of Microsoft Power Apps and Dataverse in delivering efficient and customizable business applications. While the app is functional, there are opportunities for further enhancements to meet evolving business needs.

---

### Appendix

- [Microsoft Power Apps Training Reference](https://learn.microsoft.com/en-us/training/paths/create-manage-model-driven-apps/))


