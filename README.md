# WDB Backend Technical Project Sp '23 - Unicorn Adoption

## Preface

Thanks for applying to Web Development at Berkeley & for taking the time to work on this technical project. Projects are due Monday, January 30th by 11:59 PM.

This project is designed for **you** to gauge whether you want to apply to the **bootcamp** or **industry** branch. Completing all checkpoints for the branch you are applying to is highly preferred, but don't worry if you aren't able to finish everything! As an estimate, you shouldn't need to spend any longer than ~3-4 hours on this project -- we don't want this to be a huge burden on you.

## Clarifications

This section will be updated with clarifications as they come up!

## Submission Instructions

Welcome to WDB's backend project for development branch applicants — Spring 2023 👋

Make sure you read this ENTIRE DOCUMENT, especially these instructions, carefully before you start. If you have any questions please reach out to [our email](webatberkeley@gmail.com).

To submit your project, please place your submission into a GitHub repo that is set to private. You
will be submitting your code on [Gradescope](https://www.gradescope.com/). If you do not have a
Gradescope account, please create one and if you are unable to create one, please email us
immediately. The Gradescope course code is `8NBBGP`. You will see two different assignments:
`Frontend Project` and `Backend Project`. _Please only submit to Backend Technical Project._ You can ignore Frontend Technical Project.

The technical project will be due by Monday, 1/30 at midnight. We will be unable to respond to clarification emails sent in after then, so if you have any questions about the project, please let us know before then (we will be hosting technical project office hours in our club recruitment Discord, which you can join [here](https://linktr.ee/webdevatberkeley)).

Also, this page may potentially keep changing if we get some frequently asked questions, so keep this repository bookmarked and check back on it every now and then! If there are major changes however, we'll make sure to email you about those.

## Introduction

> Introducing the magical world of unicorn adoptions! We're My Little Unicorn, a unicorn adoption agency. Our platform allows you to bring a touch of whimsy and wonder into your life by adopting your very own unicorn. These mystical creatures come in all shapes and sizes and each one is as unique as a fingerprint. Whether you're looking for a playful companion or a majestic addition to your herd, we have the perfect unicorn for you. Adopting a unicorn is easy, simply browse our gallery, choose your favorite and we'll take care of the rest. So why wait? Bring a touch of magic into your life today and adopt a unicorn!

My Little Unicorn is looking to bring their adoption system to the web and is seeking to build a backend service with the following features:

1. Register a unicorn for adoption
2. Get the list of all unicorns and their attributes
3. Ride a unicorn for a certain duration
4. Get the user who's ridden a particular unicorn for the longest time
5. Complete the adoption of a unicorn according to the use who rode it the most
6. Get the list of unicorns adopted by a certain user (**INDUSTRY ONLY**)

In particular, they want you to build an API capable of handling all of the functionality mentioned above.

_**NOTE: THERE ARE SEPARATE TASKS FOR BOOTCAMP VS. INDUSTRY**_. If you are applying to the bootcamp branch but you think you can complete the industry tasks, feel free to give them a shot! This will help us identify which branch might be the best fit for you as well.

# API Specification

The client has listed a comprehensive set of rules/business logic for the event (_make sure you read through this carefully_).

## Register Unicorn

Unicorns can be signed up for adoption at any point. When unicorns are added, attributes like their name, fur color, horn length, whether or not they're a baby unicorn, and the owner of the unicorn are all provided and should be tracked by your API service.

Example request:

```
POST /unicorns
```

Request body:

```json
{
  "name": "Big Drip J",
  "fur": "white",
  "hornLength": 8,
  "isBaby": true,
  "owner": null
}
```

## Get All Unicorns

Return a list of all unicorns currently registered (any order is fine).

Example request:

```
GET /unicorns
```

Example response:

```json
{
  "unicorns": [
    {
      "name": "Big Drip J",
      "fur": "white",
      "hornLength": 8,
      "isBaby": true,
      "owner": "Jiro"
    },
    {
      "name": "Sapphire",
      "fur": "blue",
      "hornLength": 12,
      "isBaby": false,
      "owner": "Saketh"
    },
    {
      "name": "Brother",
      "fur": "yellow",
      "hornLength": 99
      "isBaby": false
      "owner": "Nico"
    }
  ]
}
```

**Industry Checkpoint**: Add additional functionality to this API route allowing you to include a query parameter that filters the unicorns by their fur color property.

Example request:

```
GET /unicorns?fur=white
```

Example response:

```json
{
  "unicorns": [
    {
      "name": "Big Drip J",
      "fur": "white",
      "hornLength": 8,
      "isBaby": true,
      "owner": "Jiro"
    }
  ]
}
```

## Ride Unicorn

A user can ride a unicorn that's up for adoption to see whether they're a good match for each other. When they ride a unicorn, the duration they ride for should tracked.

**INDUSTRY ONLY**: Users should only be able to ride a unicorn which has not been adopted yet, i.e. only when its owner is `null`. Also, a user should only be able to ride the same unicorn twice; if they try to ride a unicorn a third time, the API should return an error.

Example request:

```
POST /ride
```

Request body:

```json
{
  "user": "Anish",
  "unicorn": "Puff",
  "duration": 10
}
```

## Get Longest Rider

This route should return the name of the user who has ridden a unicorn with a particular name for the longest **total** duration.

- Break ties by choosing the user who has the name that comes first in alphabetical order.
- If there is no user who has ridden the unicorn, then the API should return an error.

Example request:

```
GET /longest-rider/Puff
```

Example response:

```json
{
  "user": "Emir"
}
```

## Adopt Unicorn (**INDUSTRY ONLY**)

This route should receive the name of a unicorn and complete an adoption by changing its owner to the user who has ridden it for the longest duration.

- Break ties the same way as the previous `GET /longest-rider` route.
- If there is no user who has ridden the unicorn, then the API should return an error.

Example request:

```
POST /adopt
```

Request body:

```json
{
  "unicorn": "Big Drip J"
}
```

## Get Adopted Unicorns (**INDUSTRY ONLY**)

This route should return a list of unicorns that have been adopted by a certain user, along with the total duration they rode each unicorn for.

Example request:

```
GET /adopted-unicorns/Jiro
```

Example response:

```json
{
  "unicorns": [
    {
      "name": "Big Drip J",
      "duration": 10
    },
    {
      "name": "Sapphire",
      "duration": 20
    }
  ]
}
```

# More Examples

In case it helps, here's a couple of example scenarios of how the API might be used:

1. Register a few unicorns:

```
Request: POST /unicorns
```

Request body:

```json
{
  "name": "Big Drip J",
  "fur": "white",
  "hornLength": 8,
  "isBaby": true,
  "owner": null
}
```

---

```
Request: POST /unicorns
```

Request body:

```json
{
  "name": "Sapphire",
  "fur": "blue",
  "hornLength": 12,
  "isBaby": false,
  "owner": null
}
```

---

```
Request: POST /unicorns
```

Request body:

```json
{
  "name": "Brother",
  "fur": "yellow",
  "hornLength": 99,
  "isBaby": false,
  "owner": null
}
```

---

```
Request: POST /unicorns
```

Request body:

```json
{
  "name": "Puff",
  "fur": "pink",
  "hornLength": 5,
  "isBaby": true,
  "owner": "Andy"
}
```

2. A user checks the list of all unicorns:

```
Request: GET /unicorns
```

Response:

```json
{
  "unicorns": [
    {
      "name": "Big Drip J",
      "fur": "white",
      "hornLength": 8,
      "isBaby": true,
      "owner": null
    },
    {
      "name": "Sapphire",
      "fur": "blue",
      "hornLength": 12,
      "isBaby": false,
      "owner": null
    },
    {
      "name": "Brother",
      "fur": "yellow",
      "hornLength": 99,
      "isBaby": false,
      "owner": null
    },
    {
      "name": "Puff",
      "fur": "pink",
      "hornLength": 5,
      "isBaby": true,
      "owner": "Andy"
    }
  ]
}
```

(**INDUSTRY ONLY**) A user checks the list of all blue unicorns:

```
Request: GET /unicorns?fur=blue
```

Response:

```json
{
  "unicorns": [
    {
      "name": "Sapphire",
      "fur": "blue",
      "hornLength": 12,
      "isBaby": false,
      "owner": null
    }
  ]
}
```

3. Users ride some unicorns:

```
Request: POST /ride
```

```json
{
  "user": "Natalia",
  "unicorn": "Sapphire",
  "duration": 5
}
```

---

```
Request: POST /ride
```

```json
{
  "user": "Nico",
  "unicorn": "Sapphire",
  "duration": 5
}
```

---

```
Request: POST /ride
```

```json
{
  "user": "Jiro",
  "unicorn": "Big Drip J",
  "duration": 15
}
```

---

```
Request: POST /ride
```

```json
{
  "user": "Anish",
  "unicorn": "Big Drip J",
  "duration": 20
}
```

---

```
Request: POST /ride
```

```json
{
  "user": "Jiro",
  "unicorn": "Big Drip J",
  "duration": 15
}
```

---

**(INDUSTRY ONLY)** If you complete the industry checkpoint, the following request should fail since Jiro has already ridden Big Drip J twice:

```
Request: POST /ride
```

```json
{
  "user": "Jiro",
  "name": "Big Drip J",
  "duration": 1
}
```

---

**(INDUSTRY ONLY)** This request should also fail if you complete the industry checkpoint, since Puff already has an owner:

```
Request: POST /ride
```

```json
{
  "user": "Natalia",
  "name": "Puff",
  "duration": 20
}
```

4. Find who's ridden some unicorns for the longest total time:

```
Request: GET /longest-rider/Big Drip J
```

Response:

```json
{
  "user": "Jiro"
}
```

Natalia and Nico both rode Sapphire for 5 minutes, but Natalia's name comes first in alphabetical order, so she should be returned:

```
Request: GET /longest-rider/Sapphire
```

Response:

```json
{
  "name": "Natalia"
}
```

Nobody rode Brother, so the API should return an error for this request:

```
Request: GET /longest-rider?name=Brother
```

5. **(INDUSTRY ONLY)** Some unicorns are adopted:

```
Request: POST /adopt
```

```json
{
  "name": "Big Drip J"
}
```

---

```
Request: POST /adopt
```

```json
{
  "name": "Sapphire"
}
```

This request should fail since nobody rode Brother:

---

```
Request: POST /adopt
```

```json
{
  "name": "Brother"
}
```

6. Check the updated list of unicorns, including their new owners (the updated owners is necessary for **INDUSTRY ONLY**):

```
Request: GET /unicorns
```

Response:

```json
{
  "unicorns": [
    {
      "name": "Big Drip J",
      "fur": "white",
      "hornLength": 8,
      "isBaby": true,
      "owner": "Jiro"
    },
    {
      "name": "Sapphire",
      "fur": "blue",
      "hornLength": 12,
      "isBaby": false,
      "owner": "Natalia"
    },
    {
      "name": "Brother",
      "fur": "yellow",
      "hornLength": 99,
      "isBaby": false,
      "owner": null
    },
    {
      "name": "Puff",
      "fur": "pink",
      "hornLength": 5,
      "isBaby": true,
      "owner": "Andy"
    }
  ]
}
```

7. (**INDUSTRY ONLY**) Get the list of Natalia's unicorns, and how long she's ridden each of them:

```
Request: GET /adopted-unicorns/Natalia
```

Response:

```json
{
  "unicorns": [
    {
      "name": "Sapphire",
      "duration": 5
    }
  ]
}
```

## Some closing thoughts

Some of these routes are naturally harder than others. If you aren't able to finish all of the routes for the project, **don't worry**! It's supposed to be challenging, and we don't expect everyone to finish it. We have created separate checkpoints for the bootcamp vs. industry, so you don't necessarily need to complete the full project in order to move on in this round :)

Note: we highly recommend using MongoDB as your database for this project, although if you don't have experience with it, any NoSQL database is also a great alternative. If none of those work however, you are still welcome to use other databases.

It is also encouraged to use JavaScript/TypeScript with Node.js for your backend, but it is completely fine if you would rather use a different stack.

## Design Doc

In addition to building out this API, you will need to write up a short design doc (designdoc.md). We don't intend for this to take very much time, but we want to hear some of the choices you made and why. To be specific, here are some points you might want to talk about:

- Why did you choose to organize your data schemas/models in a particular way?
- Feel free to talk a bit about the "harder" routes that you worked on and how you approached them — harder is completely subjective, so feel free to get creative here!
- How did you decide on certain response codes?

This should be at most a page, so feel free to be brief!

## Assumptions

There are many details that are left intentionally vague. Though you are very much welcome to
email us to ask for clarifications, we will most likely tell you to use your best judgement.
Because of this, feel free to create a `assumptions.md`, where you can type out and
voice any assumptions you made throughout this project - we really want to hear about your rationale behind every design decision.
