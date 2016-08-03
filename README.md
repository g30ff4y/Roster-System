# Roster-System
A system for making advanced profiles and display in the UMT Ponderosa Template in the Cascade CMS. The Roster System has been an adaptation of a similar profile directory system developed by UM's Central IT Web Team, which was inherited by SFD on a collaborative site in 2013. I have since been maintaining and modifying the system to better serve SFD sites in the College of Humanities and Sciences. The following was originally documented with Bitbucket markdown intended for internal use and is provided here for reference.

Updated 6/2/2016 @g30ff4y 

[TOC]

##Overview
The Roster is a system designed to display people associated with an office, lab or other special project who are not on the UM campus and not in the Employee Database. This system is a good choice when there are many people associated with a project that need bios and contact information. The Roster will create an accordion-based page for the list of folks associated with the project and keep individual profiles in a separate folder for easier maintenance. 

****Please note that the Roster system requires quite a bit of setup and should only be used in special cases.****

###Examples
* [American Indian Gateway](http://www.cas.umt.edu/aig/directory/faculty.php)
* [Global Public Health External Advisory Committee](http://hs.umt.edu/_staging/gph/people/external-advisory.php)

##Implementation

****Please note that the Roster system requires quite a bit of setup and should only be used in special cases.****

###Initial Setup

####Configuration Set

1. On the site you are implementing the Roster System, browse to the Administration menu and select Configuration Sets (![cascade-configuration-set.png](https://bitbucket.org/repo/G9KG4E/images/1025319023-cascade-configuration-set.png)).
2. Copy the Page Configuration Set using the flyout menu to the right of the file name, before clicking submit, rename the new Configuration Set to Roster.
3. Edit the Roster Configuration Set.
4. In the Format section of the DEFAULT region, choose a new Format by clicking on the existing Format.
5. Browse to SFD - New Templates > scripts > Page Scripts > roster-info-page and confirm the selection.
6. Submit changes to the Roster Configuration Set.

####Content Type

1. Select Content Types (![cascade-content-type.png](https://bitbucket.org/repo/G9KG4E/images/155501841-cascade-content-type.png)) from the Administration Menu or Left Navigation.
2. Copy the Page Content Type using the flyout menu to the right of the file name, before clicking submit, rename the new Content Type to Roster.
3. Edit the Roster Content Type.
4. Configuration Set: Connect the Roster Configuration Set you just made.
5. Metadata Set: Leave the Global:Default Metadata Set alone.
6. Data Definition: Browse to SFD - New Templates > Data Definitions > Page Page Definitions > roster-info-page and confirm the selection.
7. Submit changes to the Roster Content Type.

####Roster Index Folder

1. Browse to the folder on the site that will utilize the Roster System.
2. Under the New menu in the blue bar, select **Folder**.
3. Rename the folder to **roster** in the **System Name** line. 
4. Delete the default page that is automatically generated when you made the folder.

####Accordion Index Page

1. Browse to the starter block: SFD - New Templates > Blocks > blankSiteBlocks > Roster Index
2. Select **Copy** from the fly-out menu to the right of the file name.
    1. Rename the block in the **System Name** line.
    2. Select a new **Parent Folder** in the site you are working on.
    3. Click **Submit**. You will be automatically be taken to your new site.
3. Go to the page you need the Roster on.
    1. Click the **Edit** tab.
    2. Click **Outputs** in the blue bar below the Edit Tab.
    3. Select where you want the profiles to appear on the page; either above or below the main page content. This will most likely be in either **DEFAULT-AFTER** or **DEFAULT-BEFORE** System Regions:
        1. **BLOCK:** Search for the Roster Index block you just copied.
        2. **FORMAT:** Search, then Browse to SFD - New Templates > scripts > Page Scripts > roster-accordions
4. Index Setup
     1. Browse to the Roster Index block you just copied and connected.
     2. Click the **Edit** tab. For most scenarios the following two settings are the only ones that will need to be adjusted.
          1. **Index Folder:** select the folder you just created.
          2. **Depth of Index:** Default is 2, meaning the index folder is two folders from the Base Folder. Adjust this based on the number of folders away from the Base Folder.

####Roster Profile Basepage

1. Browse to _cms > basepages
2. Under the New menu in the blue bar, select **Page**.
3. Rename the page to **roster-profile** in the **System Name** line.
4. Click **System** in the dark blue bar.
     1. Change Content Type to **Roster**. Click the existing Content Type and browse to the current site and select the Roster Content Type you created earlier.
5. Click **Outputs** in the dark blue bar.
     1. Change DEFAULT Format to Roster Info Page. Click the existing Format and browse to SFD - New Templates > scripts > Page Scripts > roster-info-page
6. Click **Submit**.

####Asset Factory

1. Browse to the Administration menu and select Asset Factories (![cascade-asset-factory.png](https://bitbucket.org/repo/G9KG4E/images/2313503241-cascade-asset-factory.png))
2. Click **New Asset Factory**.
3. Click the **Page** radio button.
4. **Name:** Roster.
5. **Base Asset:** Search and browse to the Roster page in the basepages folder.
6. **Placement Folder:** Search and browse to the the Roster folder you created earlier.
7. Assign the Asset to applicable groups including sfd_it and the site group (This may need to be performed by the SFD Manager if you cannot see the applicable group.
8. Click **Submit**.

###Adding Profiles

1. Under the New menu in the blue bar, select **Roster**.
2. Change the System Name to the last name of the person you are entering data for. This should be all lowercase, separate words if necessary with '-'.
3. **Display Name and Title:** Person's name.
4. Each profile will have these fields to enter:
     1. **Name:** Person's name, first and last.
     2. **College or School:** College or School Affiliation, could also be department name, etc. Text rendered in bold and above their title(s).
     3. **Title(s):** This is a person's Tile or their Department which is formatted in a list below the College or School field. You have the option to add multiple titles. Use the standard Cascade Plus and Minus signs to add/delete Title fields. Titles can be reordered with the black up and down arrows next to the add/delete options.
     4. **Office:** Office Location and/or room number.
     5. **Phone:** Person's phone number. Will be rendered as a link for phone size devices.
     6. **Email:** The person's email address.
     7. **Image:** Add an image to the button. Search for the image (must already be uploaded to the site)
     8. **Biography:** Use this area to add additional information. Use the WYSIWYG editor to format information.

##Customizing

Due to the nature of the system using dedicated scripts, customization is limited for Rosters. Styling is possible for the Accordions. Use developer tools like Firebug to target elements.

###Anatomy of a Roster

####Accordion Index

The Accordion Index utilizes the jQuery Accordion Widget to display collapsible content panels for presenting information in a limited amount of space. For more technical information about the accordion structure visit the [jQuery Accordion UI Guide](https://jqueryui.com/accordion/).

```
#!html

<div class="profile_accordion">  <!-- accordion wrapper -->    
     <div class="info_click">  <!-- accordion panel -->
          <div class="row-fluid"> <!-- row -->
               <div class="col-xs-4 roster-name"> <!-- column for name -->
                    <h2>name</h2> <!-- name formatted as heading level 2 -->
               </div>
               <div class="col-sm-6 col-xs-4 roster-contact"> <!-- column for contact information -->
                    <ul class="roster-affiliations"> <!-- list for affiliations and titles -->
                         <li class="roster-school"><b>school</b></li>
                         <li class="roster-title">title</li>
                    </ul>
                    <span class="hidden-xs hidden-sm roster-phone">Phone: phone<br /></span> <!-- phone number displayed as text on desktop devices -->
                    <span class="hidden-md hidden-lg roster-phone">Phone: <a href="tel://phone">phone</a><br /></span> <!-- phone number displayed as text link on mobile devices -->
                    <span class="roster-email"><a href="mailto:email">email</a></span><br /> <!-- email link -->
                    <span class="roster-office">Office: room</span><br /> <!-- office -->
               </div>
               <div class="pull-right col-sm-2 col-xs-4 roster-photo"> <!-- column for photo -->
                    <img class="pull-right" src="photo" alt="name" />
               </div>
          </div>
     </div>          
     <div id="info"> <!-- accordion collapsible content -->
            <span class="roster-bio">WYSIWYG content</span> <!-- WYSIWYG content wrapped in a span, but will contain it's own individual markup applicable to each person's formatting if necessary. -->
     </div>           
</div>

```

