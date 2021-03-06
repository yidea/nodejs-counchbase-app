README
===============

Nodejs + Couchbase + Angular sample app

## Install

`
//start your couchbase server.app beforehand 
npm install
node app.js
//http://localhost:3000
`

## REST API DOCUMENTATION
#### GET /api/airport/findAll?search=<_search string_> [**RETURNS: {"airportname":"<_airport name_>"} for typeahead airports passed in the query string in the parameter "search"**] 	
--Used for Typeahead   
--Queries for Airport by Name, FAA code or ICAO code.

#### GET /api/flightPath/findAll?from=<_from airport_>&to=<_to airport_>&leave=<_leave date_>&ret=<_return date_> [**RETURNS: {"sourceairport":"<_faa code_>","destinationairport":"<_faa code_>","name":"<_airline name_>","equipment":"<_list of planes airline uses for this route_>"} of available flight routes**]
--Populates the available flights panel on successful query.  
--Queries for available flight route by FAA codes, and joins against airline information to provide airline name.  

#### POST /api/user/login _request body_ {"user":<_user_>,"password":<_encrypted password_>} [**RETURNS:{encrypted JSON Web Token}**]
--Creates a new user.   
--Returns an Encrypted JSON Web Token used by the Application

#### GET /api/user/login?user=<_user_>&password=<_encrypted password_>[**RETURNS:{<_success or failure_>:<_error or encrypted JSON Web Token_>}**]
--Logs in a user   
--Returns success and JSON Web Token OR failure and error message

#### POST /api/user/flights _request body_ {"token":<_JSON Web Token_>,"flights":<_group of flights to book_>} [**RETURNS:{"added":<_number of flights booked in this request_>}**]
--Checks if user is logged in from the JSON Web Token and then if token is correct it will book the list of flights passed in.   
--Returns number of flights added if successful, or error.  

#### POST /api/user/flights?token=<_JSON Web Token_> [**RETURNS:{list of flights previously booked specific to user}**]
--Checks if the user is logged in from the JSON Web Token  and then if token is correct it will return a list of previously booked flights.   
--Returns JSON Array of Documents of previously booked flights, or error.  

