# Entrepreneur

## Summary

Way back when, in 1998, a couple Stanford students built a search engine called Backrub \(thankfully, the name didn't stick\) in a garage in California. Roughly five years later, a soon-to-be-college-dropout created a social networking website of sorts called FaceMash in his dorm room. Today, you know these companies as Google and Facebook, and collectively they're worth north of $2 trillion by market capitalization.

DoorDash, Instacart, Robinhood, Lyft, Instagram, Snapchat, Coinbase, the list goes on and on. All of these companies are valued at $1 billion or more, and none of them existed a mere ten years ago. These applications have become so engrained in society and in our lives, it's hard to imagine that they all started as nothing more than an idea \(and a whole hell of a lot of hard work!\).

## Technology Stack

If you hated Java ever since you laid eyes on it, then this is your chance to spread your wings. We're going to dive into the world of [MeteorJS](https://www.meteor.com/) and [ReactJS](https://reactjs.org/). The only caveat is that you'll need to use a [PostgreSQL](https://www.postgresql.org/) database. Normally, you'd use a NoSQL database like [MongoDB](https://www.mongodb.com/cloud/atlas/lp/try2?utm_source=google&utm_campaign=gs_americas_united_states_search_core_brand_atlas_desktop&utm_term=mongodb&utm_medium=cpc_paid_search&utm_ad=e&utm_ad_campaign_id=12212624338&gclid=Cj0KCQjw9YWDBhDyARIsADt6sGa4BEbU1CphTpdMJ45aekj1oGX3rUhbakX9F-_C3pHhBfnFUBwVQFwaAuSOEALw_wcB). We're going to use [Heroku](https://www.heroku.com/) to host our applications, and alas, PostgreSQL is the only database you can use without a credit card.

With that being said, our technology stack is going to look something like this.

* React \(a JavaScript framework for creating user interfaces\)
* Meteor \(another JavaScript framework for creating full-stack applications\)
* PostgreSQL \(an open source database\)

I recommend you dive into some [MeteorJS tutorials](https://www.meteor.com/developers/tutorials) before you get into development. You can get a jumpstart on the [SRS](https://ucvts.gitbook.io/software-development/entrepreneur#software-requirements-specification-srs), [SDP](https://ucvts.gitbook.io/software-development/entrepreneur#software-development-plan-sdp), and [STP](https://ucvts.gitbook.io/software-development/entrepreneur#software-testing-plan-stp) documents, since none of these require you to write any code.

## Formalizing the Creative Process

Have you had your billion dollar idea yet? Time to put it in writing!

### Software Requirements Specification \(SRS\)

A software requirements specification document is the basis of your entire product. It provides the framework that all parties involved in the creation and deployment of the application will follow.

Typically, an SRS document includes the following components.

* A purpose. A brief description of the product. What are the objectives, goals, and benefits of creating and using this product?
* An overview. An outline of uses and their needs. Who is going to be using your product, why they'll need to use it, and how they'll be using it?
* A list of requirements. A list of features and functionalities. What must your product be capable of doing?

Remember, the entire team—product managers, developers, and testers—will be relying on the accuracy and detail of this document. Poorly documented requirements are inevitably translated into poorly implemented features. A well-written SRS uses text, images, charts, and figures to clearly and effectively communicate, so give your billion dollar idea the attention and care it deserves.

### Software Development Plan \(SDP\)

A software development plan keeps your engineering team focused and on track. It breaks a project down into manageable phases, and provides timelines for completing these phases.

Typically, an SDP document includes the following components.

* Stories. A story is a self-contained description of a single feature \(as outlined in the SRS\), including which member of the team will be working on it and an estimate \(in hours\) of how long it'll take the complete. There needs to be a story for every feature or piece of functionality that will exist in your application.
* Sprints. A sprint is a collection of stories that will be completed \(and, for our purposes, deployed to QA\) together. Sprints should probably be about a week long to keep the product moving, which means some sprints might have more stories than others depending on their overall complexity.
* Unit tests. A unit test is an isolated test that verifies the functionality of a single feature \(often, this takes the form of method-by-method testing\). At this stage, it isn't necessary that you know every method you're going to write and how you'll test them; however, you should have a plan for testing that your feature meets its stated requirements.

After development, your code is going to the quality assurance team. Their job is find a way to break your code. So, unless you want to be embarrassed when they do so quickly and easily, you should probably thoroughly unit test your work!

### Software Testing Plan \(STP\)

A software testing plan guides your QA team in their quest to validate that each of the requirements outlined in the SRS was satisfied. These tend to be extremely detailed, but can save you hours of headaches later fixing bugs that you inadvertently shipped to production.

Typically, an STP document includes one or more test cases for each story completed during development \(remember, a story represents a feature outlined in the SRS\). A test case should contain a list of steps to complete, along with the expected outcome for each step.

Imagine a simple login feature, where users type in an email and a password before logging in.

| Step | Outcome |
| :--- | :--- |
| Enter a valid and existing email address. | The email address field is populated with plaintext. |
| Enter a valid and matching password. | The password field is populated with masked text. |
| Press the Login button. | The user is logged into the application and the dashboard successfully loads. |

To emphasize the level of detail required for a well-written test plan, let's think of related test cases we might need for something as simple as logging into an application.

* Email addresses can be valid \(i.e., legal\), but not existing \(i.e., they haven't been registered yet\).
* Email addressees can be invalid \(i.e., not legal\).
* Passwords can be valid \(i.e., meets all length and complexity requirements\), but not matching \(i.e., it doesn't match the provided email address\).
* Passwords can be invalid \(i.e., doesn't meet length or complexity requirements\).
* Users may use the Enter key instead of pressing the Login button with the mouse.
* The expected outcome will be understandably different for failed logins.

Going through these permutations, you can start to see how the number of test cases we'll need quickly adds up. Testing is how development teams ship quality code. Get it? Quality assurance.

## Division of Labor

This project is unique in that you'll have a partner, but not really... Allow me to explain.

Every aspect of this project—from drafting the [SRS](https://ucvts.gitbook.io/software-development/entrepreneur#software-requirements-specification-srs), [SDP](https://ucvts.gitbook.io/software-development/entrepreneur#software-development-plan-sdp), and [STP](https://ucvts.gitbook.io/software-development/entrepreneur#software-testing-plan-stp) documents, developing, testing, and deploying application code—must be completed independently.

That being said, you'll be creating the STP and Test Cycle documents **for your partners application**. To clarify, you'll be using your parts SRS and SDP to create an STP for their product. And when it's time to execute the test cases in the STP, you'll be executing those tests \(and documenting the results\) against your partners code.

You'll need to find a way to work together on development, builds, testing cycles, and bug fixes. If I ship buggy code, the responsibility for that failure rests equally on the shoulders of the development and QA teams.

I will need to know who your partner will be when you submit your SRS document. There are 13 students in the course, so there will be only a single group of three. No exceptions.

## Development

Your development work should be completed in stages, as specified in the Sprints section of our SDP document. Implementation needs to follow the specified sprints. This makes the lives the developers and testers a whole lot more manageable.

Let's envision a sample sprint that contains five stories. This particular sprint is to handle the registration of new users, as well as the logging in and out of existing ones.

1. Unregistered users should be able to create an account.
2. Registered users should be able to login to the application.
3. Registered users should be able to logout of the application.
4. Registered users should be able to recover a forgotten password.
5. Registered users should be able to delete their account.

Of course, these are just titles for these stories. The actual stories themselves would contain far more detail pertaining to business logic, design, and expected behavior. From the development perspective, you should have one or more commits for each of these stories. When all five stories are complete \(i.e., the code is committed and unit testing has passed\), then you're ready for a build!

## Deployment

You'll deploy your code each time you complete a sprint. This allows QA to work with a stable version of the application at that point in time, while development can continue on with the next sprint without having to wait for the test cycle to complete.

Each time you deploy your code \(i.e., a build\), we'll submit a changelog to QA documenting what stories were including in this latest build. The final build \(i.e., the one that is deemed complete and bug-free\) is what we'll ultimately ship as our finished product.

We'll be deploying our code to Heroku, which is a cloud-based platform that will host our application. This gives you the ability to provide your partner \(i.e., your QA\) team with a public URL where they can execute their tests cases against your code. There are a number of [tutorials to help you get started](https://devcenter.heroku.com/start).

## Testing

Much like development, testing should be completed in cycles. Typically, you'll run through one cycle per build, during which you'll focus on attacking newly released features, as well as verifying that existing features are still functioning correctly.

You'll use the changelog provided by the developer to identify the stories that were including in the latest build. As a tester, your job is to execute each test case application to items on the changelog, as well as to retest existing functionality. The latter half of that is called regression testing.

When you're finished, you'll submit the testing cycle document to the developer and to me. The developer needs it to address deficiencies in their code, and I need it to grade your progress. If something isn't working as expected, you should log a new issue on your partners GitHub repository detailing the bug.

## Deliverables

1. Submit your SRS Document.
2. Submit your SDP Document.
3. Submit your STP Document.
4. Submit your Changelogs \(one per build\)
5. Submit your Test Cycle Documents \(one per build\).
6. Submit your repository URL.
7. Submit your application URL.

## Deadlines

Because this is a longterm, complex project, the deadlines aren't as simple as a date and time by which everything needs to be completed. Here's the initial outline we'll be following.

1. SRS Documents are due on Canvas by 11:59pm on Wednesday, April 7, 2021.
2. SDP Documents are due on Canvas by 11:59pm on Friday, April 9, 2021.
3. STP Documents are due on Canvas by 11:59pm on Monday, April 12, 2021.

Changelogs and Test Cycle Documents are something of a running tally. You'll need one of each for every build, and for our purposes, you'll need to build at least once per week. Changelogs and Test Cycle Documents are due on the following schedule.

* Changelogs are due on Canvas by 11:59pm every Sunday, starting April 18, 2021.
* Test Cycle Documents are due on Canvas by 11:50pm every Sunday, starting April 25, 2021.

Remember, every change requires a build. This includes planned feature releases, as well as necessary bug fixes. You are working as a team, and you'll be graded as a team. Even though separate people are responsible for these submissions, you'll both be held accountable.

And lastly, the final submissions.

1. Repository URLs are due on Canvas by 11:59pm on Sunday, June 4, 2021.
2. Application URLS are due on Canvas by 11:59pm on Sunday, June 4, 2021.

We'll spend the week of June 7 presenting completed projects to the class.

