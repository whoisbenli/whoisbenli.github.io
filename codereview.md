Implementation Guidelines
=========================

Or, what to look out for when writing, submitting, and reviewing code.

To be a code review nazi, hit every point!

### Correctness

The code should be correct! This is the #1 most important point.

### Description

The first line should be short describing what the commit does, _not_ what the feature or bug is about. E.g.

Note that the first line is commonly used by tools, commands, etc, as a brief title in their user interface.

Mention the JIRA # if relevant, without any punctuation, e.g.

    JIRA-112534 BeaconManager now uses HttpClient

Additional details in later lines are encouraged, but not required.

### Atomicity

The patchset should be a single, logical change that does one thing. Commits relating to different features, or different bug fixes, should be separate.

This makes it easier to review, since the change is smaller and easier to reason about. It also makes re-ordering, excluding, reverting commits, etc a whole lot easier if there problem with one bugfix/feature and the code changes are not intermingled with changes for another bugfix or feature.

Commits that do not introduce behavior changes - what I like to call no-op commits, should be separate. This way, if a no-op commit changes behavior/staging results, we immediately know something is wrong.

### Test Coverage

Tests let you prove to your manager and your peers that your code works, and helps detect bugs when the tests get run as part of continuous integration and deployment.

Tests may also be expensive (in terms of time and computing resources), as with the case with tests that require a whole browser to be launched. Try to have a unit test if possible, and only resort to more expensive test cases when you have no choice.

Here is just a sample of the types of tests you should have:

- every component/pure function should be covered, e.g have a test class
- test that instances are in the right state for methods that mutate state
- test behavior/io is done right for relevant methods
- test for valid output for expected inputs
- test normal operation and unexpected input/error conditions
- always handle io errors
- test edge cases
- pay attention to code that is easily wrong - e.g. parsing code - have extra tests
- consult with QA to come up with test cases

### API Compatibility

Check for API breakage/non-backwards compatible changes. This is VERY IMPORTANT!!

### Design

The change should be a part of some larger design, approved by the manager in charge of the project. This is a section that deserves its own document.
(See Design guidelines and API Guidelines - TBA)

### Documentation and Comments

*Internal Standard Library APIs and Public APIs MUST be documented.*

Use the standard notation for the document generator for that platform.

Each logical module - e.g. class, should have a brief description of what service it provides, what it does, and perhaps point to a larger document that describes how it fits in the big picture.

Methods and properties should have short blurbs, and describe any mutations to the instance state, or if it does any I/O.

Include comments for anything that may not be immediately obvious to the reader of the code, for example:

- Where the logic is complex
- A technique or feature of a language is used, where the average developer may not be familiar with
- A non-obvious design decision was made
- TODOs to fix in the future
- Any reasons for non-idiomatic code

Remember to update the documentation/comments, or even remove them should the code change require it!

### Style

Follow coding style guidelines for the platform. (We have a style guide for ActionScript 3 and JavaScript)

### Samples

Samples/examples should be updated where relevant

### Security

Does the change have security implications?
