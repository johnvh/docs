page_title: Deploying a Rails app with your own database
page_author: 
page_description: Deploying a Rails app with your own database
page_keywords: 

## Deploying a Rails app with your own database

Out of the box, Ninefold enables you to implement a database server with PostgreSQL installed. Want to bring your own database? Read on! The following is our recommendation on how to implement BYOD.

Before you deploy, we recommend you read the entire article so you deploy with all of the current settings. There is a quiz at the end of the article!

#### Infrastructure
If your want your DB hosted on Ninefold and its not PostgreSQL, Please ensure you deploy this as a bare virtual server before deploying your app ensuring you tick the 'Enable NinefoldNet' box to ensure it is provisioned on the same private network as your app.

#### Gemfile

Include the relevant database gem in your Gemfile. Be sure to bundle install!

Example for this article will be with MySQL:

	# Use mysql as the database for Active Record

	gem 'mysql2'

#### Database.yml configuration

If you have a database.yml file, change it to database.yml.sample. In an effort to keep your passwords out of your repo (no fun if they get out there!), alter the file to the following format for the Rails environment being used on your Ninefold app.

For a ‘production’ environment:

	production:

		adapter: mysql2

 		database: your_db_name

 		host: #{DATABASE_URL} or ENV[DATABASE_URL]

Your file can include encoding, if you like.

#### Deploying an app with BYOD

In the deployment wizard, just uncheck the __I would like a database built for my app__ box in Step 3 of 4.

#### Environmental variables

In Portal, we have the Environment variables section (under the Configuration tab) or in Step 4 of 4, we will ask for your variables. You will want to include the following configured line for your database:

 	DATABASE_URL=mysql://username:password/location:port/your_db_name

in the __Environment Variable__ window.

#### Before migration triggers

Also in Step 4 of 4, add a __before migrations trigger__ (under Additional deployment commands):

 	mv config/database.yml.sample config/database.yml

_Quiz: just kidding but we’re glad you read to the bottom!_
