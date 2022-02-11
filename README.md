# **Goals**

To provide guidelines for choosing technologies and making effective tradeoffs, maximize collective frontend knowledge within the company. To standardise developer experience across different projects to improve the speed and efficiency of new feature development as well as maintenance.

## 1. Choosing the technology/framework

When choosing a framework we need to consider:

  

-   How well do the tools provided by the framework solve business case needs?
    
-   Are there any large companies, or projects currently using it and planning to use it in the future?
    
-   Long term stability and sustainability of the community.
    

-   For example React is supported by facebook, Vue has no big sponsors
    

-   Adoption rate within the broader industry, learning resource amount (documentation, github community size, amount of media resources)
    
-   Amount of currently active projects in company based on that framework (currently React/Next)
    
-   Amount of developers who are familiar with the framework within the company in case the project would need support
    
-   Ecosystem size for libraries supporting the framework


    -   F.e Global state managers

## 2. Choosing the build set for framework

  

-   Consider using SPA if:
    

    -   Don’t need public indexed pages for web crawler

    -   Project examples: Saas tools, internal admin systems

    -   Technology examples: Create React App CLI
    

-   Consider using SSR if:
    

    -   If you need public indexed pages for web crawler

    -   If client has ability to pay for node.js server infrastructure

    -   Project examples: Marketplaces, Ecommerce shops

    -   Technology examples: Next.js SSR mode
    

-   Consider using SSG if:
    

    -   If you need public indexed pages for web crawler

    -   If you don’t have dynamic pages or content

    -   Project examples: Blogs, Product landing pages

    -   Technology examples: Next.js SSG mode / Gatsby
    

  

-   Long term maintenance
    

    -   Custom Webpack/Parcel/Gulp/Grunt build will need internal team maintenance down the road when sub dependencies update (like typescript, babel, etc)

    -   Using frameworks like Next.js will solve most of the breaking changes by the updates in the dependencies. Meaning that you’ll only need to update Next.js version and you will have a broad community catching all the bugs and issues in Github issues page


  
  

## 3. Code standards and linting

All new projects should have linting and formatting setup, so developers could just load the project, open their IDE and format the code exactly the same way between projects.

  

We also advise to use Prettier but exact setup might differ to be compatible with your project needs.

  

Eslint rules:

[https://gitlab.nfq.lt/nfq/fe-linting/-/blob/master/.eslintrc.json](https://gitlab.nfq.lt/nfq/fe-linting/-/blob/master/.eslintrc.json)

Stylelint rules:

[https://gitlab.nfq.lt/nfq/fe-linting/-/blob/master/.stylelintrc.json](https://gitlab.nfq.lt/nfq/fe-linting/-/blob/master/.stylelintrc.json)

  

## 4. Ecosystem and libraries  
It’s important to use battle tested libraries for things like utilities, translations etc. We have a list of libraries that we’ve used in many projects throughout the years.

  

Principles by which we determine if a library is “battle tested”:

-   Github star amount
    
-   Amount and quantity of documentation
    
-   Adoption rate
    
-   Active open source community
    
-   Preferably choose packages and libraries that are recommended and supported by the core framework you’re using. If the core framework has the functionality you need inbuilt don’t go for third party libraries in case you don’t have to
    

    -   Example: Internationalized Routing for next.js [https://nextjs.org/docs/advanced-features/i18n-routing](https://nextjs.org/docs/advanced-features/i18n-routing) (before you had to use 3rd party libraries to archive this type of routing)
    

  
  

Tech stack list link:
https://github.com/nfq-frontend/tech-stack-list

## 5. Folder structure / architecture

Should translate business requirements into code architecture. Since the project will be maintained by many different developers over time, a newcomer should be able to tell what the app does just by looking at the file tree.

-   The structure has to be clear
    
-   Reflects business requirements
    

-   Just by looking at the folder names and filenames a new developer should be able to say what this application does
    

-   Naming has to be consistent across business requirements (design sketches), FE codebase and BE codebase (API response/payload property names) too
    

-   To ensure clarity across the team and save time for needless communication/searching
    
-   Example: a functionality that returns a list of users should not be called members in BE, users in FE and business refers to them as people in the design specs.
    

  

## 6. Styling solution

CSS needs to be scalable and easy to maintain.

Common problems that we want to avoid writing CSS:

-   Name collision
    
-   Specificity issues
    
-   Performance issues
    
-   DRY (do not repeat yourself)
    
-   Inconsistent styling parameters across components like spacing, border-radius, colours, font-sizes, layouts, etc
    
-   Poorly optimized mobile css (f.e. hard to change without breaking desktop version)
    

  

To optimize CSS performance and avoid issues like specificity there are a few approaches that could be chosen:

####   Utility based (tailwind)

  -   When components don’t have to be isolated

  -   When you don’t have a big amount of snow flake (unique) components

  -   Advantages:


      -   Clear and consistent naming

      -   “Tree Shaking”

      -   Single source of truth for variables in config (e.g. spacing)


  -   Disadvantages:


      -   Lack of flexibility for components that require complex styling

      -   Might be hard to read for some developers


####   Isolation based (CSS modules, styled-components)
  
  -   To have a collection of reusable components independent from any other library (e.g. tailwind)

  -   Advantages:


      -   Flexibility to implement custom styling that can not be archived by using utilities

      -   Good for creating component libraries



  -   Disadvantages:


      -   Hard to maintain consistent proportions and spacing throughout components without having a central config

      -   File bundle size grows with more components because of the need of rewriting the same styles


####   Naming pattern based (BEM, OOCSS)

  -   Works well when you don’t have ability to adjust the FE build to add libraries like Tailwind or CSS modules

  -   Advantages:


      -   Avoids CSS conflicts by having unique contextual class names

      -   Better than pure CSS without any scalable solution


  -   Disadvantages:


      -   Hard to enforce a chosen naming convention, also there’s a log of disagreeing within the same convention

      -   Hard to read for developers who are not familiar with the convention (might be excessively long)


## 7. Global state

Things to consider when choosing a state manager library:

-   Do you actually need a global state?
    

-   If yes, examine the application needs:
    

Does the project require a complex client side state?

-   Use a state manager like Redux, Mobx, etc
    

Is it a typical CRUD application?

-   Use a server state manager like React Query, Apollo client and handle client state with React Context API
    

-   Before installing a global state library refer to step 4 Principles by which we determine if a library is “battle tested”
    

  

## 8. Tests

Key functionalities of the project should be covered with tests. The code itself should be written in a way that’s easy to test.


  

-   E2E tests are good for:
    

    -   Simulating your application in different screen sizes

    -   Going through the business critical user flow

    -   See your application from the end user eyes as opposed to just testing the code

    -   Creating integration tests to make sure there no untested scenarios left by unit tests

    -   Technology examples: Cypress, Testcafe
    

-   Unit tests are good for:
    

    -   Good for testing algorithms, complex utilities

    -   When used with TDD can help to write code easier in certain scenarios

    -   Technology examples: Jest, Enzyme, React testing library


  
  

