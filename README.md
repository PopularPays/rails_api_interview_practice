# Rails API Interview Practice Project
The objective of this practice project is to build an API only Rails application. This application should run locally and consist of several API endpoints and Rails models.

## Models

There are several models: **creators**, **gigs**, and **gig payments**

### Creators

_Attributes_: `first_name` and `last_name`

_Relationships_: A `creator` has many `gigs`

### Gigs

_Attributes_: `brand_name` and `state`

_Relationships_: A `gig` has one `gig payment`

The `brand_name` for a `gig` can be any arbitrary string. The initial value of `state` is `applied`. The other possible states for a `gig` are `accepted`, `completed` and `paid`

When the `state` is set to `completed` a `gig payment` should automatically be created for this `gig`.

### Gig Payments

_Attributes_: `state`

The initial value of `state` is `pending`. The other possible value is `complete`. When the `state` is set to `complete` the state of the related `gig` should be set to `paid`.

## API Endpoints

### Creators resource

**POST** `/creators` - saves a `creator` record to the database. It should provide values for the `first_name` and `last_name` attributes in the request body.

---

**GET** `/creators` - returns a list of creators. It accepts `sort`, `sort_direction`, `limit` and `offset` query params. 

The `sort` param determines which attribute of `creator` to sort by. The `sort_direction` param should accept either `asc` (ascending) or `desc` (descending)

The `limit` param defines the max number of records returned.

The `offset` param defines how many records to skip in the results sets. E.G. if `limit` was 5 and `offset` was 5 this would return records 6 through 10.

---

**GET** `/creators/<id>` - returns a single creator with the given ID

### Gigs resource

**POST** `/gigs` - saves a `gig` record to the database. It should provide value for the `brand_name` attribute in the request body.

---

**GET** `/gigs` - returns a list of gigs. The request has the option to specify a brand name or creator. In this case the endpoint should only return gigs with the given brand name or creator.

---

**GET** `/gigs/<id>` - returns a given gig. The request has the option to specify a relationship to include with the response. E.G. If the `gig payment` relationship is specified it returns the `gig` **and** its `gig payment`

---

**PUT** `/gigs/<id>` - updates the attributes for a given gig based on the ID. 

## CRON

A CRON job should run every 2 minutes. This job changes the state of any `pending` `gig payments` to `completed`. You can use the [whenever](https://github.com/javan/whenever) gem to [schedule rake tasks](https://dev.to/risafj/cron-jobs-in-rails-a-simple-guide-to-actually-using-the-whenever-gem-now-with-tasks-2omi) to accomplish this behavior.

## Serialization

All endpoints should return data using the [JSON API format](https://jsonapi.org/). You can use the [active model serializers gem](https://github.com/rails-api/active_model_serializers) to automatically serialize data using this format. This gem can also be used to include relationships of records in the response.

## Changing state

There should be some mechanism for changing the state for `gigs` and `gig payments`. You can optionally use the [AASM gem](https://github.com/aasm/aasm).

## Testing

Add whatever test coverage you deem necessary. Please use the [rspec](https://github.com/rspec/rspec-rails) testing framework. 
