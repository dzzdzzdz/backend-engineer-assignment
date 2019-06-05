# Primephonic Backend coding challenge
Thanks for your interest in Primephonic and for taking the time to do our backend coding challenge. We hope you enjoy developing it as much as we did :)

## Background
An important part of our business is keeping track of what our customers stream, so we can pay back royalties towards the labels and artists. Our payout model is different than other streaming services though, in that we pay royalties based on total number of seconds streamed, instead of how many times a track has been streamed.

For this, the client apps (Android, iOS & Web) monitor the tracks being streamed and periodically send usage reports to our backend, which collects and processes these events.

## Summary
Your task is to develop a system which is able to generate a financial report based on streaming usage of users. As an output, this report should indicate how much money should be distributed to each label. For this, you will need to gather data from 3 different data sources:

1. [streaming.csv](https://github.com/Primephonic/backend-engineer-assignment/blob/master/streaming.csv): local file containing information of which tracks have been streamed by which users, and the duration of each stream.
2. [users.csv](https://github.com/Primephonic/backend-engineer-assignment/blob/master/users.csv): local file containing user profile information such as their active subscription plan and which platform they subscribed with (Apps stores or via web).
3. [Music Streaming API](https://backend-assignment.s3.eu-central-1.amazonaws.com/tracks.json): remote JSON file which provides additional metadata per each track, such as the track name and the label it belongs to.

## Business rules
To work out how much money needs to be sent to each label, we first need to determine what our overall revenue is. As each user has an active subscription, we simply add up all of their subscription fees, taking the following into account that:
1. Users that subscribed via the app stores (`origin = app_store`) only contribute `70%` towards our revenue (So, if a user paid €7.99, we only consider €5.59 as their contribution towards our overall revenue).
2. Users that subscribed via the web app (`origin = web`) only contribute `90%` towards our revenue.

Now we need to analyse the streaming data itself to determine how many seconds in total have been streamed, and then split it per label. With these 2 data points, we can now extrapolate the percentage each label needs to receive, based on how many seconds have been streamed per label.

## Sample calculation

**Total Revenue**: `€10.000`<br/> 
**Total Seconds Streamed**: `20.000`

| Label   |      Seconds Streamed      |  Percentage Streamed |  Revenue Split |
|----------|:-------------:|------:|------:|
| Label 1 |  10.000 | 50% | €5.000 |
| Label 2 |    6.000   |   30% | €3.000 |
| Label 3 | 4.000 |    20% | €2.000 |

## Tasks
The assignment must:
1. Consolidate all 3 different data sources into a single source of truth (can be stored in-memory). Each entry in this storage must have the following structure:</br>
`{ date, user_id, product_type, fee, origin, region, track_id, track_name, track_labelm seconds }`

2. Generate the financial output based on the business rules

3. Expose this data via a RESTful API (`GET /report`)

## Evaluation criteria
The assignment will be evaluated based on the following points:

1. Code organization
<br/>Is the code well organized, easy to follow and well-structured? Think responsibilities, separation of concerns.

2. Performance
<br/>Although the dataset is small in size, the proposed solution should be able to scale to handle input files significantly larger in size

3. Compliance
<br/>Does the application satisfy the described use cases?

4. Simplicity
<br/>Don't over-engineer it. If you feel like you're taking shortcuts you're not comfortable with, go with the simple solution and later explain how you would do it differently in a real production app in the `README.md`.

## Technologies
Any of the following are allowed: `Typescript`, `JavaScript`, `Node.js`

## Submission Guidelines
- Submit your project in a single `zip` file to your Primephonic contact
- Include a `README.md` with instructions on how to run it, together with any additional information you consider appropriate (assumptions, design decisions made, etc.)
- Include *only* source code and assets (no libraries, modules, etc.)
