# Static resources(css/images/js and grunting)

---

We have a defined way of working with CSS, images, grunting in **Postnl** module.


## How to work with CSS

We have different files in the repository for example **Postnl-Component.css**, **Postnl-General.css**, **Postnl-Forms.css** where all the CSS which are used in the project resides. </br>

**Postnl-Component.css** : Any CSS changes related to base components should go in this file</br>

**Postnl-General.css**   : Any CSS changes related to styling, page styling or any general CSS should go in this file</br>

**Postnl-forms.css**     : Any CSS changes related to forms should go in this file</br>

**Postnl-Variables.css** : All the hardcoded values that we are using in css, will be migrated to variables in this file.

For example: Button colouring using Variable css

Old way of using harcoded CSS for colour:
```
.postnl-loader .loading-spinner div {
  border-color: #e45656;
  border-top-color: transparent;
}
```

New way using Variables
```
// Define all the harcoded values in Postnl-Variable.css file in a variable which can be resued everywhere where ever the same color is needed.
.postnl-loader .loading-spinner div {
  border-color: var(--postnl-loader-loading-spinner-border-color);
  border-top-color: transparent;
}
```

---

```
// Some examples from general.css file
.postnl-m-top_custom {
    margin-top: 1.25rem;
}

.postnl-p-around_custom {
    padding: 1.25rem;
}

.postnl-m-top_x-small {
    margin-top: 0.5rem;
}

.postnl-m-vertical_small {
    margin-top: 0.75rem;
    margin-bottom: 0.75rem;
}


// Some examples from Component.css file
--For Agenda Component
.postnl-agenda-box-shadow {
    box-shadow: inset 0px -3px 0px 0px var(--postnl-primary-orange);
}

-- for datagrid related css
.postnl-datagrid .postnl-datagrid_expand-inner .postnl-datagrid_PO_loc {
    font-size: 16px;
    font-weight: 300;
    line-height: 1.5;
    letter-spacing: normal;
    color: var(--postnl-grey-dark);
    margin-bottom: 1rem;
}

```

**Important:**  Always try to reuse the existing CSS first instead of creating a new. In the file General.css many CSS are already defined for example different variations of margin, padding, aligning (also for mobile) which can be reused.


## How to Grunt

####  1. Install npm on you machine

####  2. Install Salesforce cli

####  3. Run the commands in the below sequence
```
-npm install

-npm install -g grunt-cli

//After adding/changing the CSS or after adding any image, you can run the grunt command

-grunt

After grunting, save the PNL_Assets.resource file in the static resource to reflect the changes
```

**Important** Always navigate to the below path before grunting
build >> business_portal >> pnl  (if working for pnl module)


## How to work with Images

####  1. Add the image to the specific folder. Follow the below path.

Path to Image folder: <br>
build >> business_portal >> pnl >> src >> assets >> images >> your specific folder >> your specific image




#### 2. After adding the image, Run grunt.

Navigate to the pnl directory in the terminal and run the command: grunt.

After grunting, save the PNL_Assets.resource file in the static resource to reflect the changes


**Important:** Always create a separate folder for images if working with any new module. Do not place the images in any random folder.
For example, images related to shipment module should go in existing shipment folder




---

[Home](/wiki/Home.md) - [Frontend](/wiki/frontend/frontend.md) - Static resources(css/images/js and grunting)