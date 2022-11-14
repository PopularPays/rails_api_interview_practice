# City Slicker - Full Stack Interview Practice Project

Create a Rails application and complete the various parts below.

At Popular Pays & Lightricks, we use Rails project with Rspec (for testing) and Postgresql database. This command:
`rails new app-name -T -d postgresql` && `rails generate rspec:install` is a command to help you quickly instantiate a new app and get rolling.  Please reach out with questions on the exercise - clarifications are never counted against your submission.

----------------------

Part 1 - Modeling

We all call somewhere home. We're proud of where we live and we want to share with the world all the things that make our home special to us. We have an API that allows us to showcase things about a `Place` when you query against it. 

A `Place` has personal information about its geolocation - `latitude` and `longitude` attributes - as well a `name` and `description` that are both support free text. A `Place` also has a `rating` instance method which is an aggregate average of all `Rating` objects that have that relationship.

A `Rating` has a float attribute that stores the `value` and a relationship to a particular place. The presence of these attributes and relationships between models should be mandatory and validated.

Instructions: Build your modeling based on the information above. This should include DB tables and Rails models with methods.

-----------------------

Part 2 - API Exposure

A `Place` needs to be discoverable by searching. We need to expose the data before we can build the UI.

We want to be able to fuzzy search a `Place` against it's `name` and `description` attributes.  

> We also want to be able to search a `Place` against proximity - or distance. For this, we would use a geolocation mapping library and compare distance from the current location of the user. This is not in scope for the exercise (it's a decent amount of work), but if you finish everything else in the exercise and want to tackle it, go for it!

The endpoint should sort by the most popular - meaning the first object in the collection should have the highest aggregate `rating`.

Instructions: 
1.) Build an collection (ie. index) endpoint that supports fuzzy search by name - making sure to ensure santization/normalization of the search for capitalization differences and trailing and prefixing whitespace search queries.

2.) Ensure the response implements pagination parameter support (roll your own for the enpoint or insert a gem library) as well as the sort requirements listed above.

3.) Ensure the endpoint returns JSON with all attributes needed for the UI.

4.) Make sure the endpoint is well tested for all branching logic and handlers.

5.) Keep in mind errors you might want to rescue.

6.) Further considerations of rate limiting and error handling.

------------------------

Part 3 - UI/UX

We want to connect the API to a UI that a web browser user can enjoy and search against. For this exercise you can use any framework you choose to create a Search UI that displays the results.  This means, Vue.js, React.js, Ember.js (this is what we use at Pop Pays), Rails MVC, etc.

Instructions:
1.) Build a UI that allows you to search based on the requirements of the API.

2.) We can have a search bar as a header and a table view as the main content part of the page that returns the table cells of information about the `Place` including `name`, `description` and `rating`.

3.) Style the UI as you want. We're not expecting you to be a design pro, but since this is a full stack exercise we are interested in how you layout the UI and your ability to create basic styles.

------------------------


Part 4 - Scaling & Data Integrity

This is new web app and idea so we don't expect much traffic in the beginning, but we're hoping to scale it and make sure it can handle the throughput and load growth.

Imagine the amount of records on the `places` table is large - At least 1 million records.  The index enpoint for `Place` resource returns a paginated collection but the majority of load on the DB is happening in the search query (see Part 2).

If you had to design a scalable search on this endpoint, how would you go about doing so? This is a critical thinking question that we want you to include as part of the exercise, but do not expect you to implement. Think about issues of scalability and how you would solve them as well as design of the search feature. How would you create a system to handle that quantity of records to query assuming it's only going to grow larger and larger (maybe exponentially)? This could include a plan to implement monitoring, solutions at the DB layer, as well as controller layer.

What are some problems you might have to solve, or even better pre-emptively in terms of data integrity. For example, the attribute on a `Place` object could easily result in duplicate records if not properly validated and sanitized before persisting.

ie. Place 1 has name `Chicago`, Place 2 has name `chicago`, Place 3 has name `CHICAGO`. Tell us / show us the best way to solve this and other considerations we may want to take into account.

To submit your proposal for this part, simply create a markdown file at the top level of your Rails project titled `Part 4 - Scaling & Integrity`


-----------------------

Part 5 - Testing

We test a lot at Popular Pays and Lightricks.  Not only does it give us security in the features we ship but also piece of mind. Write tests to include coverage of all controller branching, success and error request/response cycle, and unit testing for all model layer logic.

We use Rspec, Capybara, FactoryBot, and shoulda-matchers as utilities and framework for testing. Those are not strictly mandatory but allow to have coverage from the acceptance level down to the unit level.

Make you have a `seeds.rb` to fill the DB.  This will allow us to fire up the app locally and fill the development database with records to manually QA your app build but also could help you have seeded records in the DB for your tests.


-----------------------

Part 6 - Delivery

To submit your exercise, you have two options:

1.) Please archive the project folder in a ZIP and email it to `justin@lightricks.com` with the subject `Interview Practice Submission - <your name>`.

2.) Please create a public repo and pass the link to `justin@lightricks.com` to be cloned and reviewed.
