# Sections

Sections is an efficient serverless app relying on modern technologies to increase page render speed and facilitate the work of frontend developers. This package provide a VueJS Component to use right off the bat to interface with Sections' server

In order to benefit from this service you should register for free on the following [link](https://sections.geeks.solutions/register)

# Vue Sections

Is a vue.js 2 wrapper for sections.

# Get started

Make sure to have your projectID, then install the library on your project

```npm
npm install vue-sections@1.0.1
```

Configure the library with your ProjectID

```
import Sections from 'vue-sections'

...

Vue.use(Sections, {projectId: "60352afc1ad7f0006327a38"})
```

Then add the sections component on the page(s) of your choice

```
   <template>
        <div id="app">
            <Sections
            :admin="admin"
            :pageName="page_name"
            :variations="[]"
            />
        </div>
    </template>

    <script>
        export default {
            name: "App",
            data() {
                return {
                    admin: false,
                    pageName: "home"
                };
            },
            created() {
                this.admin = this.$cookies.get("sections-auth-token") ? "true" : false;
            },
        };

    </script>
```

Here we load props from data on the page, the admin prop is used to indicate if the edit interface for the page should display or not. Sections uses a cookie named `sections-auth-token` to store a user token to secure communications for page editing actions, if the cookie is found it assumes the edit button should show.

To get the UserToken and have it stored in the above cookie, simply set sections on a page of your website, then head to your Sections project page (where you have your projectID) and set the login redirect url properly, then hit connect sections to my app. This library will receive and process the request to generate the UserToken and store it in the cookie for further use. for more information check the [docs](https://sections.geeks.solutions/docs/frontend/index.html)

If you now want to move on and start providing local and static sections for your website editor, or customize the display of dynamic or configurable ones, read below.

# How it works

Sections server comes with a Wysiwyg and any public sections out of the box.
The Wysiwg can be added to any page and will display of the box thanks to internal components, yet if you wish to override anything (the view, the icon or the form) you can do so be redeclaring any (or all) component(s) in your project.

You can also define your own local and static section types and you have the ability to control the way any section will display on your website.

You do this by creating custom VueJS components and placing them in the right configurations folder.

The configurations folder follows the following structure:

```
src
|_ configs
    |_ views
       |_ {your-component}_{section-type}.vue
    |_ type-icons
       |_ {your-component}.vue
    |_ forms
       |_ {your-component}.vue
```

Out of the box, this library will point to `@/sections_config` in case you want to override this path you can do so with the `VUE_APP_SECTIONS_CONF` env. variable.

- `views` folder will contain the design of your component that will be displayed on the page to your visitors (and during preview)
- `type-icons` folder will contain the icons that will illustrate your section in the add a new section box for content editors.
- `forms` is the folder where you create the form that will help you fill the data while adding or editing `your-component` to your page. This is only for static section types, local and dynamic ones persist no data and configurable ones have their data entry form automatically built by the library as this comes from the third party developer providing this section.

In case you are trying to use a section that you haven't properly declared on your project, a warning will display in the console indicating where sections is epxecting the component to be located according to your configuration.

---

## For Contributors

If you wish to contribute to this project, head to this [wiki](https://github.com/Geeks-Solutions/vue-sections/wiki) and follow the instructions there.