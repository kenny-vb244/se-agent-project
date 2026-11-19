# Full Spec: <App name>

**Team:** Kendall, Kendall, Buraporn, Maimuna  **Date:** 11/19/26  **Committer:** ______

> How to use this file: copy it to `docs/FULL_SPEC.md` in your fork. Fill every section. There is **no length limit** here (the Run Brief has one).
> Put a name next to each section: that person owns it and can explain it without the AI.
> If you do not know something, write `TODO:` or add it to Open questions. A marked gap scores better than an invented answer.
> In every section, finish with one line: **AI contribution:** what an AI suggested, and what you changed or rejected (write "none" if none).
> Delete these quote lines when you are done.

**Roles:** Product Owner ______ | Process lead ______ | Architect ______ | Quality lead ______ | Prompt engineer ______

---

## 0. The idea (Chapter 1)
- The single main problem, and for whom (one sentence): Clothing Tracker helps individuals organize clothing items they are interested in purchasing by saving product links, organizing items into categories, and comparing prices across different sellers.
  
- Who is harmed if this app fails, is wrong, or leaks data?
Users may lose saved clothing items or receive inaccurate pricing and availability information.
Users may make purchasing decisions based on outdated or incorrect information.
Users could have their privacy compromised if personal information is collected or stored unnecessarily.
  
- Anything the app must never do (privacy, safety, legal):
Store personally identifiable information.
Collect payment information or process purchases.
Claim that prices or stock availability are current when they cannot be verified.
Access websites in ways that violate their terms of service or applicable laws.
Store passwords insecurely or imply that the login feature provides production-level account security.

## 1. Process and plan (Chapters 2 and 3)  Owner: ______
- Process model we chose (plan-driven, incremental, or agile) and **why it fits this app** (2 sentences): Incremental, allows the team to build and test the three main pages and their functionality separately before combining them. It also allows the team to prioritize essential features, such as saving clothing items and organizing them, before attempting optional features like price comparisons and stock alerts.
  
- Practices we actually use: stand-up / sprints / board / retrospective / code review / tests on every change
- **Definition of Done** (checklist, 4 or more items):
  - [ ] feature works in a desktop and mobile browser
  - [ ] relevant unit tests pass
  - [ ] feature does not violate privacy or technical constraints 
  - [ ] code has been reviewed and merged
- Sprint plan (what is working at the end of each sprint):

| Sprint | Working software at the end | se-agent run? |
|---|---|---|
| 1 |Basic application structure, login page, explore page, and myclothes page navigation |Yes|
| 2 |Users can save clothing items, store product links, and organize saved items into folders or categories using local storage|Yes|
| 3 |Price comparison display, accessibility improvements, error handling, and final testing |Yes|

- Biggest schedule risk and what we will do about it:
Accessing live pricing and stock information from external shopping websites may be difficult because of website restrictions, changing page structures, and the absence of a backend. We will prioritize manually entered or saved product information and implement live price retrieval only if a reliable and legally permitted method is available.

- AI contribution:
AI suggested an incremental process and a three-sprint development plan. The team should adjust the sprint assignments to match its actual schedule and progress.

## 2. Requirements (Chapter 4)  Owner (Product Owner): ______
**Stakeholders and what each wants:**

| Stakeholder | Wants |
|Clothing Tracker Uses|Save clothing items and organize potential purchases|
|Development Team|Build a functional application within the project constraints|
|External clothing retailers|Have their product links and publicly available product information represented accurately|
|Project evaluator/instructor|See that the application satisfies its documented requirements and acceptance criteria
**User stories** (as a ___, I want ___, so that ___), each with acceptance criteria:
1. As a user, I want to access a login page so that I can enter the application and manage my clothing wishlist.
  1a. Acceptance criteria: The login page accepts the locally defined login credentials and provides access to the application. No personal information is collected or transmitted.
2. As a user, I want to save clothing items and their product links so that I can keep track of items I may purchase.
  2a. Acceptance criteria: Saving an item adds its name, link, and available product details to MyClothes.
3.  As a user, I want to organize saved clothing items into folders or categories so that I can find them easily
   3a. Acceptance criteria: Users can assign items to categories or folders and view items grouped accordingly.
4. As a user, I want to compare clothing prices from different sellers so that I can identify the available purchasing options.
  4a. Acceptance criteria: The application displays available seller names, product links, and prices for the same or comparable clothing item.
5. As a user, I want the application to support accessibility features so that I can navigate and understand the application more easily.
   5a. Users can increase text size, access text-to-speech functionality, and identify navigation and actions through icons and images with appropriate labels.


**Requirements table**

| ID | Type (F = functional, NF = non-functional) | Requirement (one testable sentence) | Priority (Must/Should) | Acceptance test (input -> expected result) |
|---|---|---|---|---|
| R1 | F |The application shall provide a login page that allows a user to access the locally stored clothing wishlist without collecting personally identifiable information.| Must |Enter valid locally configured credentials → application opens. Enter invalid credentials → access is denied.|
| R2 | F |The application shall allow users to save clothing items with a name and product URL, along with optional product details.| Must |Enter a clothing name and valid URL and select Save → item appears in MyClothes.|
| R3 | F |The application shall allow users to organize saved clothing items into user-defined folders or clothing categories.| Must |	Save three items into two categories → MyClothes displays the items under their assigned categories.|
| R4 | NF (performance) |The application shall load its locally stored clothing list within 2 seconds for a collection of up to 500 items on a supported device.| Should |Load 500 stored items → list renders within 2 seconds under the agreed test environment.|
| R5 | NF (usability) |	The application shall provide adjustable text size, text-to-speech controls, and accessible labels for interactive icons.| Must |Increase text size, activate text-to-speech, and navigate controls using keyboard and screen-reader labels.|
| R6 | NF (security or privacy) |The application shall store wishlist data only in browser local storage and shall not transmit personally identifiable information.| Must |Inspect browser storage and network requests → wishlist remains local and no personally identifiable information is transmitted.|
| R7 | NF (cost) |The application shall not require paid AI services, and any optional AI feature must cost less than $0.01 per use. | Must | Review external service integrations and cost estimates → no required paid AI calls; optional AI calls cost less than $0.01 each.|

**Out of scope** (so nobody builds it by accident):
- Password encryption and production-level account security.
- Synchronizing wishlist data across multiple devices.
- Personalized clothing recommendations.
- Processing payments or completing purchases.
- Building a backend or cloud database.
- Developing a native mobile application.

**Requirements we removed as unnecessary, and why:**
- Personalized clothing recommendations: Removed because recommendations are explicitly outside the project scope and are not necessary for the core wishlist functionality.
- Password encryption: Removed because the application has no backend and does not support production-level account management.
- Device synchronization: Removed because all data is stored locally in the user's browser.

**Open questions** (better listed than guessed):
- Will users create their own login credentials, or will the application use predefined local credentials?
- Should folders be customizable, or should the application provide predefined clothing categories?
- How will prices be retrieved from external retailers?
- Which retailers will be supported for price comparisons?
- How frequently should prices and stock availability be updated?
- Will users manually enter product prices when automatic retrieval is unavailable?
- Should the application support multiple sellers for one saved clothing item?
- How will locally stored data be handled if the user clears browser storage?

**Check:** could two people read each requirement and build different things? Are there words like *fast*, *easy*, *secure*? Replace each with something observable.
Requirements should be testable and avoid vague terms. Performance is defined by a time and collection size. Privacy is verified through storage and network inspection. Price comparison depends on available retailer information.
- AI contribution: AI helped draft the user stories, functional and non-functional requirements, acceptance tests, and out-of-scope list. The team should verify that all requirements reflect the intended application.

## 3. Models (Chapter 5)  Owner (Architect): ______

The Clothing Tracker system consists of three HTML pages and locally stored application data.

**Context model** (what is inside the system, what is outside, what crosses the boundary):
Inside the system:
- Login page: Provides access to the application.
- Explore page: Allows users to view and save clothing items.
- MyClothes page: Displays saved items and organizes them into folders or categories.
- Local storage: Stores saved clothing information and user preferences.
- Application logic: Handles saving, editing, deleting, organizing, and displaying items.



Outside the system:
- Clothing retailer websites.
- Browser and device operating system.
- External text-to-speech functionality provided by supported browser features.



What crosses the boundary:
- Product URLs and publicly accessible product information.
- Price and stock information, when retrieval is supported.
- User interactions, such as saving items and changing categories.
- No personally identifiable information should be transmitted.

**Use cases or a sequence model for the most important story:**
Main use case: Saving a clothing item to MyClothes.
1. User opens the application and accesses the Explore page.
2. User enters or selects a clothing item.
3. User provides the product name and URL.
4. User selects the Save Item option.
5. Application validates the required information.
6. Application stores the item in browser local storage.
7. Application updates MyClothes to display the saved item.
8. User can assign the item to an existing or new category.
Expected result: The item appears in MyClothes and remains available after refreshing the browser.

**Class or data model** (main entities and how they relate):
| Entity | Attributes | Relationship |
| UserSession	| sessionStatus, loginStatus | Controls access to the application. |
| ClothingItem	| itemID, name, URL, brand, size, color, categoryID	| Belongs to a clothing category.|
| Category	| categoryID, categoryName |	Contains multiple clothing items.|
| Seller |	sellerID, sellerName, sellerURL |	Can offer multiple clothing items.|
| PriceRecord	| itemID, sellerID, price, stockStatus, lastUpdated	| Stores available pricing and stock information for an item from a seller.|

Relationships:
- One Category can contain many ClothingItems.
- One ClothingItem can have multiple PriceRecords.
- One Seller can have multiple PriceRecords.
- UserSession controls access but does not require a persistent personal identity.

**State model** (only if the app has modes; otherwise write "no modes"):
The application has the following login states:
- Logged Out: User is viewing the login page.
- Logged In: User has successfully accessed the application.
- Session Ended: User has logged out or the browser session has ended.

A clothing item may also have the following saved states:
- Not Saved: Item has not been added to MyClothes.
- Saved: Item is stored in local storage.
- Organized: Item has been assigned to a category.
- Removed: Item has been deleted from the wishlist.

**Consistency check:** a requirement that appears in no model, or a model element no requirement needs, and how we resolved it:
R1 is represented by UserSession and the login state model.
R2 is represented by ClothingItem and the saving use case.
R3 is represented by Category and its relationship with ClothingItem.
R5 is represented by the application interface and accessibility controls.
R6 is represented by local storage and the system boundary.
R7 is represented by the restriction on paid external services.
R4 is represented by the performance requirement for displaying stored items.

- AI contribution: AI suggested the entities, relationships, and use-case sequence. The team should validate the model against the actual features implemented.

## 4. Architecture (Chapter 6)  Owner (Architect): ______
- Pattern we chose (layered, MVC, client-server, pipe-and-filter, other): The application will separate the user interface, application logic, and data storage into distinct layers. The three HTML pages will handle user interaction, JavaScript modules will handle application functionality, and browser local storage will maintain the saved clothing information.
- Which non-functional requirements drove it (name the R-numbers):
R4: Performance through efficient local data retrieval.
R5: Usability through accessible and consistent interfaces.
R6: Privacy through local data storage.
R7: Cost through avoiding required paid services and backend infrastructure.

- Alternatives we rejected, and why:
Client-server architecture: Rejected because the project does not allow a backend.
Cloud database architecture: Rejected because user data must remain locally stored.
Monolithic architecture: Rejected because combining all application functionality into one file would make testing and maintenance more difficult.

- **If the app uses an AI model:** where it is used; what happens when it is slow, wrong, or down (the non-AI fallback); the cost per use:
The core application will not require an AI model.
No AI-based clothing recommendations will be implemented.
If optional AI functionality is considered later, it must cost less than $0.01 per use.
If an optional AI service is unavailable or produces incorrect results, the application will continue functioning without that feature.
TODO: Determine whether any optional AI service is necessary.

**Decisions log**

| # | Decision | Alternatives | Reason (tie to an R-number) | Consequence |
|---|---|---|---|---|
| D1 |	Use browser local storage. | Cloud database or server database. | R6: Keeps wishlist information on the user's device.| Data is limited to the browser and device where it was saved |
| D2 | 	Separate application logic from HTML display code. | Combine all JavaScript and HTML into one file. | R4 and R5: Supports maintainability and testing. | Additional JavaScript modules will be required. |
| D3 | Use three separate HTML pages. | Single-page application or native mobile application. | R5: Provides the requested three-page structure. | Navigation must work across Login, Explore, and MyClothes. |

- AI contribution: AI suggested a layered architecture and helped identify architectural alternatives. The team selected local storage and separate application logic to meet the original constraints.

## 5. Design and implementation (Chapter 7)  Owner: ______
- Modules, and the owner of each:

| Module | Owner | Responsibility |
|---|---|---|
| Login.html | TODO | Displays the login interface and validates locally configured credentials. |
Explore.html	| TODO	| Displays available clothing items and provides item-saving functionality. |
MyClothes.html |	TODO	| Displays saved items and allows users to organize them. |
storage.js	| TODO |	Handles reading, writing, updating, and deleting local storage data.|
clothing.js	| TODO |	Handles clothing item creation, validation, and organization. |
pricing.js	| TODO	| Handles seller information, price comparison, and price update logic when data is available. |
accessibility.js	| TODO |	Handles text resizing, text-to-speech controls, and accessibility features.
navigation.js	| TODO | Handles movement between the three application pages.|

- Where the logic lives **apart from the display** (so it can be unit-tested):
Application logic will be placed in separate JavaScript files rather than directly inside HTML elements.

- Design patterns we will use, and where (or "none yet"):
Separation of concerns: Separates page display, application logic, and data storage.
Module pattern: Organizes JavaScript functionality into reusable modules.
TODO: Additional patterns will be determined during implementation.

- Code or libraries we will reuse, with their licenses:
HTML5, CSS3, and JavaScript: Standard web technologies.
Browser Local Storage API: Built-in browser functionality.
Web Speech API: Browser-supported text-to-speech functionality, subject to browser compatibility.
TODO: Identify any external libraries and verify their licenses before use

- Branching and review rule (for example: pull request, one approval, tests green):
Use Git for version control.
Create separate branches for individual features.
Submit changes through pull requests.
Require at least one teammate to review changes before merging.
Run applicable tests before merging.
Keep the main branch functional.

- Technical debt we are knowingly accepting:
Local storage does not support automatic synchronization across devices.
Local login functionality does not provide production-level account security.
External retailer pricing may not update automatically.
Some accessibility features may vary depending on browser support.
The application will depend on browser storage availability and capacity.

- AI contribution: AI suggested a modular JavaScript structure and separation of concerns. The team should assign module ownership and confirm any external libraries before implementation.

## 6. Testing (Chapter 8)  Owner (Quality lead): ______
**Requirement-to-test map** (every Must-do needs at least one):

| Requirement | Test (file::name) | Type (unit / component / system / user) | How we will check it can fail |
|---|---|---|---|
| R1 | login.test.js::validLogin | Unit / component | Enter incorrect credentials and confirm access is denied. |
| R2 | 	clothing.test.js::saveItem | Unit / component | Attempt to save an item with a missing name or invalid URL. |
| R3 | 	clothing.test.js::assignCategory | Unit / component | Assign an item to a nonexistent category and confirm validation prevents it.|
| R4	| performance.test.js::load500Items |	System | Load a larger dataset and measure whether the 2-second limit is exceeded. |
| R5	| accessibility.test.js::accessibilityControls | Component / user |	Disable or remove an accessibility control and confirm the test fails. |
| R6 |	storage.test.js::localOnlyStorage |	System |	Inspect network requests and verify no wishlist data or personal information is transmitted. |
| R7 |	cost.test.js::externalServiceCost	| Unit / review |	Introduce a simulated paid service cost above $0.01 and confirm the check fails. |

**The three most important tests, in plain language** (input -> expected result):
1. Saving an item: User enters a clothing name and product URL and selects Save → the item appears in MyClothes and remains there after refreshing the page.
2. Organizing clothing: User saves multiple clothing items and assigns them to different categories → MyClothes displays each item under the correct category.
3. Comparing prices: User enters or retrieves prices for the same clothing item from multiple sellers → the application displays the seller names, prices, and corresponding product links.

- Edge cases we will try to break each Must-do with (zero, negative, empty, huge, missing):

R1 Login:
- Empty username or password.
- Incorrect credentials.
- Missing login information.
- Repeated login attempts.
- Refreshing the browser after login.



R2 Saving items:
- Empty item name.
- Missing product URL.
- Invalid URL.
- Duplicate items.
- Very long item names.
- Special characters in item information.



R3 Organization:
- Empty category name.
- Duplicate category names.
- Deleting a category containing items.
- Moving items between categories.
- Saving an item without assigning a category.



R5 Accessibility:
- Increasing text size multiple times.
- Unsupported text-to-speech browser functionality.
- Missing image descriptions.
- Keyboard-only navigation.



R6 Privacy:
- Inspect browser storage.
- Inspect network requests.
- Clear local storage.
- Refresh the application.
- Attempt to access stored data from a different browser.

  
- User testing: who (outside the team), and what we want to learn:
Ask participants to:
- Log into the application.
- Find and save a clothing item.
- Organize the item into a category.
- Locate the item in MyClothes.
- Use the accessibility controls.
We want to determine whether users can complete these tasks without assistance and whether the interface is understandable.

- What we are deliberately **not** testing, and why:
Password encryption and production-level authentication because they are outside the project scope.
Cross-device synchronization because the application uses local storage.
AI recommendation accuracy because recommendations are out of scope.
Live price accuracy across every retailer because website access and data availability cannot be guaranteed.
Payment processing because purchasing functionality is not included.

- Test command: `TODO: Determine test framework and command (for example, npm test or uv run pytest).`
- AI contribution: AI suggested unit, component, and system tests and identified edge cases. The team should implement and verify each test against the final code.

## 7. Evolution (Chapter 9)  Owner: ______
- The most likely future change: Adding automatic price and stock availability updates from supported clothing retailers. This would allow users to receive notifications when an item goes on sale or becomes available in their selected size.


- Impact analysis: modules, models, requirements and tests that would change, and about how long:
This change would affect:
- pricing.js: Add functionality to retrieve and update product prices.
- storage.js: Store price history, seller information, and last-update timestamps.
- MyClothes.html: Display updated prices and stock availability.
- Explore.html: Display product information from supported retailers.
- Data model: Add or expand the PriceRecord entity.
- Requirements: Add requirements for automatic updates, stock notifications, and sale notifications.
- Tests: Add tests for price changes, unavailable products, failed requests, and outdated information.
Estimated development time: TODO: Approximately 1–2 additional sprints, depending on retailer access and technical requirements.

- What design choice today would make that change easier:
Keeping price retrieval and comparison logic in a separate pricing.js module will make it easier to add new retailers and update pricing functionality without changing the entire application. Keeping seller and price information separate from the main ClothingItem entity will also allow multiple sellers to be associated with one item.

- AI contribution: AI suggested separating price-related functionality from clothing management so future price tracking can be added without redesigning the application.

## 8. Decisions we are least sure about
(Prepare to be asked about these.)
Login functionality: Since the application does not have a backend and cannot store personally identifiable information, we need to determine whether login will use predefined local credentials or simply act as a demonstration access screen. Neither option should be presented as secure authentication.

Automatic price retrieval: We are unsure whether clothing retailers allow their prices to be retrieved directly through browser JavaScript. Some websites restrict automated access or prevent cross-origin requests.

Price comparison: We need to decide whether users will manually enter prices from multiple sellers or whether the application will retrieve prices automatically.

Stock availability: Retailers may display stock differently and may require users to select a particular size or color before availability can be determined.

Data persistence: Local storage will preserve information in the same browser, but users may lose their saved clothing items if they clear browser data.

Accessibility: Text-to-speech functionality depends on browser and device support, so the application needs a fallback if the feature is unavailable.

Folder organization: We need to decide whether users can create custom folders, use predefined clothing categories, or both.

Price update frequency: We need to determine how frequently price information should be checked without creating unnecessary requests or violating retailer restrictions.

## 9. Run plan and cost (se-agent)  Owner (Prompt engineer): ______
- Prompts in `prompts/` we will use, in order:
- Proposed order:
1. design.md – Define the application structure, user interface, and main functionality.
2. build.md – Implement the three HTML pages and supporting JavaScript functionality.
3. verify.md – Review the application against the project requirements and identify errors.

- Model (use `gpt-6-luna` for iteration; ask before using a stronger one):
- Planned runs (default: one per sprint):

| Run | Sprint | Prompts | Model | Estimated cost (`uv run python cost_estimate.py docs/RUN_BRIEF.md`) |
|---|---|---|---|---|
| 1 | 1 | design.md, build.md, verify.md | gpt-6-luna | Run cost_estimate.py|
| 2 |	2	| build.md, verify.md	| gpt-6-luna |	TODO: Run cost_estimate.py
| 3	| 3	| build.md, verify.md	| gpt-6-luna	| TODO: Run cost_estimate.py

- Before we request a run, we confirmed: `uv run pytest` passes / Run Brief is 4,000 characters or fewer / each prompt follows the 8-section template

Before we request a run, we confirmed:
- [ ] uv run pytest passes.
- [ ] Run Brief is 4,000 characters or fewer.
- [ ] Each prompt follows the eight-section template.
- [ ] The application requirements and constraints are documented.
- [ ] Estimated AI usage costs have been reviewed.

## 10. Run Brief
The Run Brief is a **separate file**: `docs/RUN_BRIEF.md`. It is what se-agent reads, and it must be **4,000 characters or fewer** (about 700 words). The agents do not read this Full Spec, so anything a model must know has to be in the Run Brief, in words.

The existing Clothing Tracker project brief already provides a foundation for this file. It should be revised to make requirements more specific and remove conflicting or unnecessary instructions.

Characters in our Run Brief: TODO: Run the following command after updating the file.
python -c "print(len(open('docs/RUN_BRIEF.md', encoding='utf-8').read()))"

**Keep:** the main problem and user; numbered Must-dos (each testable); technology and data constraints; any cost limit on AI features; the out-of-scope list; 3 to 5 acceptance checks.
**Cut:** process reasoning, stakeholder analysis, long rationale, diagrams (describe the one relationship that matters in a sentence).
**Translate:** non-functional requirements become constraints with numbers; the architecture becomes one sentence; the test plan becomes quality expectations and acceptance criteria.

What we cut to fit, and why it was safe to cut:
- Detailed stakeholder analysis: Not necessary for implementation because the primary user and problem are already identified.
- Sprint planning: The agents only need to understand what to build, not how the team manages development.
- Detailed diagrams and models: These are documented in the Full Spec and can be summarized in a few sentences.
- Testing explanations: The Run Brief includes quality expectations and acceptance criteria rather than the complete test plan.
- Detailed architectural reasoning: The Run Brief describes the architecture and technical constraints without including every alternative considered.
- Future development ideas: Optional future features are either listed as Should-do or excluded to keep the implementation focused.

Check the length:
```
python -c "print(len(open('docs/RUN_BRIEF.md', encoding='utf-8').read()))"
```

- Characters in our Run Brief: ______
- What we cut to fit, and why it was safe to cut:

## 11. Presentation notes (six beats; every member speaks)
| Beat | Who | One sentence we will say |
|---|---|---|
| 1. Problem, user, Must-dos (Ch 4) | | |
| 2. Process choice and Definition of Done (Ch 2, 3) | | |
| 3. Context model and one more model (Ch 5) | | |
| 4. One architecture decision: chosen, rejected, which requirement forced it (Ch 6) | | |
| 5. Three most important tests, and how we know they can fail (Ch 8) | | |
| 6. Likely change, Run Brief, cost plan (Ch 9, 4) | | |
