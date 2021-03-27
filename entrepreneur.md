# Entrepreneur

## Summary

Way back when, in 1998, a couple Stanford students built a search engine called Backrub \(thankfully, the name didn't stick\) in a garage in California. Roughly five years later, a soon-to-be-college-dropout created a social networking website of sorts called FaceMash in his dorm room. Today, you know these companies as Google and Facebook, and collectively they're worth north of $2 trillion by market capitalization.

DoorDash, Instacart, Robinhood, Lyft, Instagram, Snapchat, Coinbase, the list goes on and on. All of these companies are valued at $1 billion or more, and none of them existed a mere ten years ago. These applications have become so engrained in society and in our lives, it's hard to imagine that they all started as nothing more than an idea \(and a whole hell of a lot of hard work!\).

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

* Stories. A story is a self-contained description of a single feature \(as outlined in the SRS\), including which member of the team will be working on it and an estimate \(in hours\) of how long it'll take the complete.
* Sprints. A sprint it a collection of stories that will be completed \(and, for our purposes, deployed to QA\) together. Sprints should probably be about a week long to keep the product moving, which means some sprints might have more stories than others depending on their overall complexity.
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

## Development

Coming soon!

## Deployment

Coming soon!

## Testing

Coming soon!

