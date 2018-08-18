---
title: "Mince Pie Challenge: Adding and Listing Mince Pies with Amazon DynamoDB"
link: https://tech.mybuilder.com/mince-pie-challenge-adding-and-listing-mince-pies-with-amazon-dynamodb/
meta: "Mince Pie Challenge: Adding and Listing Mince Pies with Amazon DynamoDB"
---

In the [previous post](https://tech.mybuilder.com/mince-pie-challenge-adding-the-bootstrap-endpoint-and-serverless-offline/) we began to implement the API endpoints, starting off with creating the bootstrap response.
We did this in a manor that catered for both online and offline development access.
In this post we will incorporate the ability to add and list mince pies, persisting the state within [Amazon DynamoDB](https://aws.amazon.com/dynamodb/).
Following this, we will enrich our offline development process by setting up a [Amazon DynamoDB Local](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html) instance using Docker.
<!--more-->
