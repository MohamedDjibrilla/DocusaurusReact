# DocusaurusReact

Introduction:
Welcome to this tutorial, I am going to present how to set up a docusaurus website in general and then build a new website for a tutorial on React and React Native for beginners. In the first phase, we will be discussion the installation process, the file structure, the implementation of features like page creation, sidebar, versioning, building and deployment of a basic website. In the second phase, I am going to follow the instructions of the tutorial to set up an open source project from A-Z.  Let us get started.

What is Docusaurus?
It is a tool designed to make it easy for teams to publish documentation websites without having to worry about the infrastructure and design details. ... Docusaurus also provides core website and documentation features out-of-the-box including blog support, internationalization, search, and versioning.
To build docusaurus projects we need the following:

1-	Node version >=  10.15.1 

To install node js visit this link:  https://nodejs.org/en/download/

2-	Docusaurus version 2.0

To install all the dependencies needed for this project:
1-	Open your command line  


2-	Navigate to the desired folder location for your project


3-	Tape the following command 

npx @docusaurus/init@next init my-website classic



4-	Run your  localhosted docusaurus template

To preview your changes as you edit the files, you can run a local development server that will serve your website and it will reflect the latest changes.
Cd my-website
Npm  start

Docusaurus structure

After creation of the template, you should use a code editor to open the folder. There are a lot of code editor out there. It all depends on which you are more familiar. However, for the purpose of this tutorial, we are going to use VS CODE. More information on how to install it can be found here: https://code.visualstudio.com/download

Open the docusaurus folder you will see the following file structure:


my-website
├── blog
│   ├── 2019-05-28-hola.md
│   ├── 2019-05-29-hello-world.md
│   └── 2020-05-30-welcome.md
├── docs
│   ├── doc1.md
│   ├── doc2.md
│   ├── doc3.md
│   └── mdx.md
├── src
│   ├── css
│   │   └── custom.css
│   └── pages
│       ├── styles.module.css
│       └── index.js
├── static
│   └── img
├── docusaurus.config.js
├── package.json
├── README.md
├── sidebars.js
└── yarn.lock

•	/blog/ - Contains the blog Markdown files. You can delete the directory if you do not want/need a blog. More details can be found in the blog guide.
•	/docs/ - Contains the Markdown files for the docs. Customize the order of the docs sidebar in sidebars.js. More details can be found in the docs guide.
•	/src/ - Non-documentation files like pages or custom React components. You don't have to strictly put your non-documentation files in here but putting them under a centralized directory makes it easier to specify in case you need to do some sort of linting/processing
o	/src/pages - Any files within this directory will be converted into a website page. 
•	/static/ - Static directory. Any contents inside here will be copied into the root of the final build directory.
•	/docusaurus.config.js - A config file containing the site configuration. This is the equivalent of siteConfig.js in Docusaurus 1.
•	/package.json - A Docusaurus website is a React app. You can install and use any npm packages you like in them.
•	/sidebar.js - Used by the documentation to specify the order of documents in the sidebar. (I can add a  link since it is an advance tutorial)
Basic building blocks of a docusaurus website
How to create pages

To create a page in Docusaurus, one can use React or Markdown (more on markdown at https://www.markdownguide.org/). For the purpose of this example, we are going to use React.

 /src/pages/helloReact.js

import React from 'react';
import Layout from '@theme/Layout';

function Hello() {
  return (
    <Layout title="Hello">
      <div
        style={{
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
          height: '50vh',
          fontSize: '20px',
        }}>
        <p>
          Edit <code>pages/hello.js</code> and save to reload.
        </p>
      </div>
    </Layout>
  );
}

export default Hello;


How to add sidebar

For a better readability, one  will need add a sidebar to your project, by configuring the contents of the sidebar, and the order of its documents, in the website/sidebars.json file. Until you add your document to website/sidebars.json, they will only be accessible via a direct URL. The pages will not show up in any sidebar.
Within sidebars.json, add the id you used in the document header to the existing sidebar/category. In the below case, docs is the name of the sidebar and Getting Started is a category within the sidebar.

{
  "docs": {
    "Getting Started": [
      "getting-started"
    ],
    ...
  },
  ...
}




How to add versioning

You can use the version script to create a new documentation version based on the latest content in the docs directory. That specific set of documentation will then be preserved and accessible even as the documentation in the docs directory changes moving forward. Versioning is best suited for websites with high-traffic and rapid changes to documentation between versions

Directory structure#
website
├── sidebars.json        # sidebar for master (next) version
├── docs                 # docs directory for master (next) version
│   ├── foo
│   │   └── bar.md       # https://mysite.com/docs/next/foo/bar
│   └── hello.md         # https://mysite.com/docs/next/hello
├── versions.json        # file to indicate what versions are available
├── versioned_docs
│   ├── version-1.1.0
│   │   ├── foo
│   │   │   └── bar.md   # https://mysite.com/docs/foo/bar
│   │   └── hello.md
│   └── version-1.0.0
│       ├── foo
│       │   └── bar.md   # https://mysite.com/docs/1.0.0/foo/bar
│       └── hello.md
├── versioned_sidebars
│   ├── version-1.1.0-sidebars.json
│   └── version-1.0.0-sidebars.json
├── docusaurus.config.js
└── package.json

Routing#
If you are familiar with other static site generators like Jekyll and Next, this routing approach will feel familiar to you. Any JavaScript file you create under /src/pages/ directory will be automatically converted to a website page, following the /src/pages/ directory hierarchy. For example:
•	/src/pages/index.js → <baseUrl>
•	/src/pages/foo.js → <baseUrl>/foo
•	/src/pages/foo/test.js → <baseUrl>/foo/test
•	/src/pages/foo/index.js → <baseUrl>/foo/
In this component-based development era, it is encouraged to co-locate your styling, markup and behavior together into components. Each page is a component, and if you need to customize your page design with your own styles, we recommend co-locating your styles with the page component in its own directory. For example, to create a "Support" page, you could do one of the following:
•	Add a /src/pages/support.js file
•	Create a /src/pages/support/ directory and a /src/pages/support/index.js file.
The latter is preferred as it has the benefits of letting you put files related to the page within that directory. For example, a CSS module file (styles.module.css) with styles meant to only be used on the "Support" page. Note: this is merely a recommended directory structure and you will still need to manually import the CSS module file within your component module (support/index.js). By default, any Markdown or Javascript file starting with _ will be ignored, and no routes will be created for that file (see the exclude option).

Build#
Docusaurus is a modern static website generator so we need to build the website into a directory of static contents and put it on a web server so that it can be viewed. To build the website:
Npm run build


Summary:
We have gone through a lot during this first phase. Let us now build our own open source documentation website.
Docusaurus at a glance
React and React Native
Components
Properties
States
Suggested work

