# WDB Backend Technical Project Fa '23 - Husband Calling 🗣️

## Preface

Thanks for applying to Web Development at Berkeley & for taking the time to work on this technical project. Projects are due **FILL IN THE DATE/TIME HERE**

This project is designed for **you** to gauge whether you want to apply to the **bootcamp** or **industry** branch. Completing all checkpoints for the branch you are applying to is highly preferred, but don't worry if you aren't able to finish everything! As an estimate, you shouldn't need to spend any longer than ~3-4 hours on this project -- we don't want this to be a huge burden on you.

## Clarifications

This section will be updated with clarifications as they come up!

## Submission Instructions

Welcome to WDB's backend project for development branch applicants — Fall 2023 👋

Make sure you read this ENTIRE DOCUMENT, especially these instructions, carefully before you start. If you have any questions please reach out to [our email](webatberkeley@gmail.com).

To submit your project, please place your submission into a GitHub repo that is set to private. You
will be submitting your code on [Gradescope](https://www.gradescope.com/). If you do not have a
Gradescope account, please create one and if you are unable to create one, please email us
immediately. The Gradescope course code is **FILL IN A GRADESCOPE CODE HERE**. You will see two different assignments:
`Frontend Project` and `Backend Project`. _Please only submit to Backend Technical Project._ You can ignore Frontend Technical Project.

The technical project will be due by **FILL IN THE TIME HERE** at midnight. We will be unable to respond to clarification emails sent in after then, so if you have any questions about the project, please let us know before then.

Also, this page may potentially keep changing if we get some frequently asked questions, so keep this repository bookmarked and check back on it every now and then! If there are major changes however, we'll make sure to email you about those.

## Introduction

> The annual Husband Calling contest at the Iowa State Fair is an entertaining event that has seen more than 500 contestants and over 2000 spectators from around the country gather to share little moments of affection. Contestants take turns on stage in speaking to their partner, competing to be the dearest and most loving of all. It is a great way of strengthening relationships and fostering a community of love.

The Iowa State Fair is looking to bring their registration and contest-management system to the web and is seeking to build a backend service with the following features:

1. Register a contestant/husband pair
2. Get a list of all contestants
3. Perform a "husband call" and score it
4. Get the highest-score shout across all contestants **(INDUSTRY ONLY)**
5. Buy a power-up item **(INDUSTRY ONLY)**

In particular, they want you to build an API capable of handling all of the functionality mentioned above.

_**NOTE: THERE ARE SEPARATE TASKS FOR BOOTCAMP VS. INDUSTRY**_. If you are applying to the bootcamp branch but you think you can complete the industry tasks, feel free to give them a shot! This will help us identify which branch might be the best fit for you as well.

# API Specification

The client has listed a comprehensive set of rules/business logic for the event (_make sure you read through this carefully_).

## Register Contestant/Husband

Register a contestant and associate them with their husband. Every contestant also has a "vocalRange" field (which represents how many meters their voice will go). Lastly, the husband has a "location" which represents their distance (in meters) from the contestant zone.

You can assume that all contestants and husbands have a unique name.

Example request:

```
POST /contestants
```

Request body:

```json
{
  "contestantName": "Alice",
  "husbandName": "Bob",
  "vocalRange": 100,
  "location": 500
}
```

The response can look like anything. You should raise an error if a field is missing, with a descriptive error message.

## Get All Contestants

Return a list of all contestants and the husband they are paired with.

**Industry Checkpoint**: Add additional functionality to this API route allowing you to include a query parameter `sortByName=true` that determines if you should return by sorted order of contestantName. (ex: GET /contestants?sortedByName=true)

Example request:

```
GET /contestants
```

Example response:

```json
{
  "pairs": [
    {
      "contestantName": "Alice",
      "husbandName": "Bob"
    },
    {
      "contestantName": "Cady",
      "husbandName": "Desmond"
    }
  ]
}
```

## Perform Husband Call and Score it

Of course, no husband calling is complete without, well, a husband call!

We determine the score of a husband call based on the husband's location and the contestant's vocalRange. If the vocalRange is exactly equal to the location, the score is equal to the location. If the vocal range is greater, the score is the absolute difference between the location and the vocalRange. In both these cases, return the score.

If the vocalRange is less, we should raise an error with a descriptive message.

Example request:

```
GET /husbandCall
```

Example response:

```json
{
  "score": 100
}
```

## Get Highest Score Shout (INDUSTRY ONLY)

This route should return the score of the best shout across all contestants, as well as the contestant. You can either assume no ties or break ties randomly, just make sure it is clear which option you go for.

Example request:

```
GET /bestShout
```

Example response:

```json
{
  "contestantName": "Alice",
  "score": 100
}
```

## Buy a Power-up Item **(INDUSTRY ONLY)**

Some contestants have said they want to be able to use the best and latest tech to improve their scores! Implement an API route that lets contestants purchase an item and add it to their inventory. The response should be a list of all the items in the user's inventory.

- Each item has a "boost", which increases the vocalRange by that amount.
- Items cannot be removed from the inventory.
- All items in the inventory get used when a husbandCall is made.

Note that completing this section will also involve modifying your existing husbandCall route!

Example request (note the route has the contestantName in it!):

```
POST /buyItem/Alice
```

Request body:

```json
{
  "item": "megaphone",
  "boost": 150
}
```

Example response:

```json
{
  "inventory": ["megaphone", "mysterious drugs"]
}
```

## Some closing thoughts

Some of these routes are naturally harder than others. If you aren't able to finish all of the routes for the project, **don't worry**! It's supposed to be challenging, and we don't expect everyone to finish it. We have created separate checkpoints for the bootcamp vs. industry, so you don't necessarily need to complete the full project in order to move on in this round :)

Note: we highly recommend using MongoDB as your database for this project, although if you don't have experience with it, any NoSQL database is also a great alternative. If none of those work however, you are still welcome to use other databases.

It is also encouraged to use JavaScript/TypeScript with Node.js for your backend, but it's completely fine if you would rather use a different stack.

Finally, we recommend using [Postman](https://www.postman.com/) or a similar tool to test your API.

## Design Doc

In addition to building out this API, you will need to write up a short design doc (designdoc.md). We don't intend for this to take very much time, but we want to hear some of the choices you made and why. To be specific, here are some points you might want to talk about:

- Why did you choose to organize your data schemas/models in a particular way?
- Feel free to talk a bit about the "harder" routes that you worked on and how you approached them — harder is completely subjective, so feel free to get creative here!
- How did you decide on certain response codes or errors?

This should be at most a page, so feel free to be brief!

## Assumptions

There are many details that are left intentionally vague. Though you are very much welcome to
email us to ask for clarifications, we will most likely tell you to use your best judgement.
Because of this, feel free to create a `assumptions.md`, where you can type out and
voice any assumptions you made throughout this project - we really want to hear about your rationale behind every design decision.
