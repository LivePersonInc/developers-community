## LivePerson Developer Center

**As of August 2018, please open all Pull Requests DIRECTLY TO THE MASTER BRANCH ON THE PUBLIC VERSION OF THIS REPOSITORY. THERE IS NO MORE NEED FOR THE INTERNAL REPOSITORY**

**This site is maintained by the Product Communications and Experience team. Please contact lmart@liveperson.com for issues, questions, and the such**.

This repository generates LivePerson's Developer Center, which can be found at https://developers.liveperson.com. The site is generated using [Jekyll](https://jekyllrb.com/). If you find an issue with the documentation, site structure, meta or anything else, please open an issue and we'll respond as soon as possible.


**Table of Contents**

* :satellite:[Updating the Documentation](https://github.com/LivePersonInc/developers-community#updating-the-documentation)

* :hammer:[Building the Site Locally](https://github.com/LivePersonInc/developers-community#building-the-site-locally)

* :clipboard:[Template](https://github.com/LivePersonInc/developers-community#template)

* :scroll:[Licensing](https://github.com/LivePersonInc/developers-community#licensing)

### Updating the Documentation

All pages on the site correspond to a Markdown file (.md) which can be found inside `pages/Documents`. 
To update a file, please branch off of the `master` branch, edit the file in question and create a Pull Request **back to the master branch**. 
There's no need for the old Development branch, so please don't create pull requests to it.

### Commiting Changes to Developer Center
Before making any commits, please make sure to read the Updating/Creating Headers section. 
There is now a github precommit hook that makes sure you follow the rules on markdown file creation. 
This hook will run on every commit and deny commits if they fail the test. 
The errors will be outputed to `./_scripts/docOutputError.log`. 
If you are adding new content, please make sure you are updating the content in documentsupdated.yaml file. 
Our tests will use the documents updated yaml file as the source of truth. So make sure your header naming structure matches the documentsupdated.yaml.

File name rules:
1. All markdown files must match the pagename that is provided in the headers
2. Spaces in pagename must be replaced with a '-'
3. All words are lowercased
4. All special characters excluding periods and dashes need to be removed from the filename
5. Periods are replaced with dashes.

Folder name rules:
1. They must be TitleCase
2. All files in the folder, must include a reference in its header to its folder name. This will be in either the documentname, categoryname, or subfoldername ( depending on the location of the folder)
3. All special characters excluding periods, dashes, and & need to be removed from Foldername
4. Periods are replaced with dashes.

E.G pagename : `Customizing the Conversational Cloud!` should be filename `customizing-the-conversational-cloud.md`
E.G documentname:  `Add Agent Widgets` should be a folder with name  `AddAgentWidgets`

* Category name will always be the top most folder in the sidebar

### How to understand the documentsupdated yaml file
  Example Normal Layout:
  
    - categoryname: Agent Experience
      image: agent-experience-new
      documents:
      - documentname: Add Agent Widgets
        pages:
        - pagename: Add Your Own Widgets to the Agent Workspace
      - documentname: Agent Workspace Widget SDK
        pages:
          - pagename: Overview
          - pagename: Limitations
          - pagename: Methods
          - pagename: Public Model Structure
          - pagename: Public Properties
          - pagename: Best Practices and Troubleshooting
          - pagename: Release Notes
      - documentname: Chat Agent API
        basedomain: https://{domain}/api/account/{accountId}/agentSession
        pages:
        - pagename: Overview 
        
The Top layer 0 in this structure is the category name Agent Experience. Its folder name is`AgentExperience`.
Add Agent Widgets is a folder in layer 1 with path `AgentExperience/AddAgentWidgets`
The Add Agent Widgets folder only contains one page in it. `AgentExperience/AddAgentWidgets/add-your-own-widgets-to-the-agent-workspace.md`
the permalink for the file must include all parent folders excluding the layer 0 categoryname. For above example the permalink is:
`add-agent-widgets-add-your-own-widgets-to-the-agent-workspace.html`

If you look at the next document name `Agent Workspace Widget SDK` it is still on level 1 with path `AgentExperience/AgentWorkspaceWidgetSDK/`
The files in the folder are all listed below pages until you get to last pagename.
IE documentname Chat Agent API is not a folder located inside `Agent Workspace Widget SDK`

Example Subfolder Layout:

    - categoryname: Conversational AI
      image: agent-experience
      documents:
      - documentname: Conversational AI
        pages:
          - pagename: Overview
      - documentname: Conversation Builder
        pages:
          - pagename: Tutorials & Guides
            subpages:
              - subpagename: Getting Started
              - subpagename: Using Meta Intents with Conversation Builder
              - subpagename: Implementing a Web View Integration
              - subpagename: Using LivePerson Functions with a Bot
  
  1. pagename `Tutorial & guides` because it has subpages is actually a folder not a file
  2. in the markdown file for `Using Meta Intents with Conversation Builder` its pagename must match the subpagename.
  3. the file must include `Tutorial & Guides` as a `subfoldername` header since it is at level 2 
  4. the file must include `Conversation Builder` as a `documentname` in the header. 
  4. the permalink must be `conversation-builder-tutorials-guides-using-meta-intents-with-conversation-builder.html`
  5. notice how the `&` in the subfoldername is replaced with a dash in the permalink.
  
Example Documentname is pagename:

    - categoryname: Getting Started
      image: getting-started
      documents:
      - documentname: Getting Started with your Free Trial Account
      - documentname: Do More with the Conversational Cloud
      - documentname: Customizing the Conversational Cloud
      - documentname: Starting with your Concierge Bot
      - documentname: API Guidelines
        pages:
        - pagename: Accessing LivePerson APIs
        - pagename: Create API keys
        - pagename: Domain API
        - pagename: Data APIs
        - pagename: API Data Metrics
        - pagename: Engagement Attributes
        - pagename: Analytics Builder Data Metrics
        - pagename: Retry Policy Recommendations
        
1. Documentname name is `Getting Started with your Free Trial Account` is not a folder name becauase it does not contain a pages key below it
2. Since this above file only contains one parent, there should not be a document name in the file `getting-started-with-your-free-trial-account.md`
3. The pagename for `getting-started-with-your-free-trial-account.md` must match the documentname in the yaml file  `Getting Started with your Free Trial Account`

#### Environments
To updated production and staging enviornments, create a pull request for master or Staging. When pull request is merged a automated release cycle will start and publish those changes in around five minutes.

* Production (built from the `master` branch): [https://developers.liveperson.com/](https://developers.liveperson.com/)

* Staging (built from the `Staging` branch): [https://developers.liveperson.com.staging-vdt2zeq-jlynhjefjcpgg.us.platform.sh/](https://developers.liveperson.com.staging-vdt2zeq-jlynhjefjcpgg.us.platform.sh/)


#### Updating/Creating Headers

Jekyll uses a [front-matter](https://jekyllrb.com/docs/frontmatter/) to arrange and define the various documents in the site. This is the text which appears in between the "---" at the top of each document. It's technically a YAML snippet, so all [YAML formatting](http://www.yamllint.com/) and rules apply to it. Our headers are usually comprised of the following key/value pairs:

* `pagename`: This is the name of the page that will appear at the top of the document.

* `keywords`: This replaces the keywords found in the `<meta>` tag of the page. Leave it unpopulated.

* `documentname`: This key accepts either `Documents` or `Solutions`. This designates which part of the site the document is under.

* `categoryname`: This is the category to which the document's API belongs (for example, the "Create Users" method belongs to the Users API which is under Contact Center Management).

* `documentname`: This is the API to which the document belongs.

* `subfoldername`: This is a sub-folder to which the document belongs, if there is one.

* `permalink`: this key defines the link at which the document can be found. The format of this value **MUST BE** as follows. Any other value format will cause the sidebar to malfunction:

  * If the page has a `subfoldername` value: documentname - subfoldername - pagename. For example: `mobile-app-messaging-sdk-for-android-advanced-features-audio-messages.html`

  * If the page does not have a `subfoldername` value: documentname - pagename. For example: users-api-overview.html

* `indicator`: this key sets the Chat or Messaging indicator (or both) on a document. It accepts `chat`, `messaging` or `both` as its value.

**Any other parameters which are not documented here which you might find in the front-matter are deprecated and are only present for backwards compatibility purposes. These should not be used**.


#### Adding New Documents to the Sidebar

Once you've created a new document, you'll need to have it manually added. We chose a manual process for the sidebar for a few reasons. First, it reduces the fragility of the sidebar (the extra, manual step gives us another layer of QA). Secondly, it increases the flexibility of the sidebar (we write code once and then maintain a YAML file, making it easier to add options). Lastly, it decreases site build times (since the `forloops` needed to dynamically build a sidebar in a site of our size and complexity are time and resource consuming).

The sidebar's YAML file can be found in the `_data` folder. It's called `documentsupdated.yaml`. You **must** make sure the name of the file and the pagename in the sidebar correspond; the link the sidebar sends to is auto-generated and **must** match the `permalink` in the file's header (see above). Please make sure the markdown file created contains its pagename, documentname, categoryname, and permalink in its header. The markdown file might need more information depending on where it will need to be in the sidebar. 

The max width for an image in this repo is 800px.

### Building the Site Locally

If you have not already done so, make sure your computer has Ruby installed. Here's a helpful guide on how best do that on [Mac](http://railsapps.github.io/installrubyonrails-mac.html) (you can stop once Ruby is installed, you don't need Rails) and on [any other system](https://www.ruby-lang.org/en/documentation/installation/).

Once you have installed Ruby, clone this repository to your machine. Once done, navigate to it using Terminal or your preferred command line interface. Follow the steps below to run the site from your machine. **If you're on Windows, don't forget to run your CLI as an admin**.

**First time install**
1. Run `npm install`
2. Run `npm run serve`
3. Navigate to http://localhost:4000/ (or the port you chose) and you'll see the site.

**OSX Installation**

1. We recommend installing a standalone Ruby Installation and RVM
2. See this for an example: [Stack Overflow](https://stackoverflow.com/questions/39381360/how-do-i-install-ruby-gems-on-mac)

**Serving the site after the first install**

You have two options to run the site locally after the first install:

* **Using gulp.js**. [Gulp](https://gulpjs.com/) is a toolkit for automating painful or time-consuming tasks. By simply typing in `gulp` in your command line, it takes care of all the build commands needed to serve the site. It also watches the root directory and will automatically refresh your browser once any changes were built. Gulp and its dependencies are installed locally in the project, so there's no further installation needed from your end.

* **Using Jekyll's standard commands**. All you need to run in consequent builds of the site is `bundle exec jekyll serve`. You can add the suffix `--incremental` to enable incremental building of the site. This saves build times since the regeneration feature is enabled by default (the site rebuilds every time you hit "save"). When `--incremental` is used, Jekyll won't rebuild the entire site on every save, only the affected sections. If you'd like the project to automatically open in a new tab, you can add the `-o` flag to the end of the above command.

**Note**: changes that alter site navigation or other changes that change the site as a whole might not show up when using `--incremental`. If that occurs, simply "kill" the build and run `bundle exec jekyll serve` without the suffix. **This is also true for gulp: you will need to kill your gulp instance and then run the direct Jekyll command**.

### Template

See the `_template` folder above for a complete template of a simple REST API. Other templates will follow in the future. However, if you have a unique API to document or need further assistance, please reach out to Product Communications *before* starting to write your document so that we can advise on its structure.

### Testing the site for errors

If you would like to test the validity of this site, you can run one of the following commands:

```rake test_internal_links```

This will output a list of all the broken internal links

```rake test_external_links```

This will output a list of all the broken external links

```rake test_all```

This will output a list of all broken external links, scripts, images, and html accessibility standards

### Licensing

All usage of the contents, documentation or code found in this repository is subject to the [LivePerson API Terms of Use](https://www.liveperson.com/policies/apitou). Please use the link above to read them carefully before utilizing the site.
