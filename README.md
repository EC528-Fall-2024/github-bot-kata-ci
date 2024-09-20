## Project Description Template

***The purpose of this Project Description is to present the ideas proposed and decisions made during the preliminary envisioning and inception phase of the project. The goal is to analyze an initial concept proposal at a strategic level of detail and attain/compose an agreement between the project team members and the project customer (mentors and instructors) on the desired solution and overall project direction.***

***This template proposal contains a number of sections, which you can edit/modify/add/delete/organize as you like.  Some key sections we’d like to have in the proposal are:***

- ***Vision: An executive summary of the vision, goals, users, and general scope of the intended project.***
- ***Solution Concept: the approach the project team will take to meet the business needs. This section also provides an overview of the architectural and technical designs made for implementing the project.***
- ***Scope: the boundary of the solution defined by itemizing the intended features and functions in detail, determining what is out of scope, a release strategy and possibly the criteria by which the solution will be accepted by users and operations.***

***Project Proposal can be used during the follow-up analysis and design meetings to give context to efforts of more detailed technical specifications and plans. It provides a clear direction for the project team; outlines project goals, priorities, and constraints; and sets expectations.***

---

## 1.   Vision and Goals Of The Project:

***The vision section describes the final desired state of the project once the project is complete. It also specifies the key goals of the project. This section provides a context for decision-making. A shared vision among all team members can help ensuring that the solution meets the intended goals. A solid vision clarifies perspective and facilitates decision-making.***

***The vision statement should be specific enough that you can look at a proposed solution and say either "yes, this meets the vision and goals", or "no, it does not".***

Kata Containers is an open source community working to build a secure container runtime with lightweight virtual machines that feel and perform like containers, but provide stronger workload isolation using hardware virtualization technology as a second layer of defense.

The goal of this project will be to implment a Continuous Integration GitHub Bot for Kata Containers that will help users automate a variety of tasks and run commands via GitHub comments.  We plan to do this using Prow--the Kubernetes CICD system.

We plan to:

- Enhance test management dashboard 
  - Implement tree view
  - Implement filtering capabilities to allow users to target specific test criteria (e.g., required vs. optional tests)
  - Implement feature to collapse and expand data regarding each test
  - Implement different way to index tests:
    - Test name
    - Nightly run
    - PR run
- Implement a CI bot to help us automate things and run commands via Github comments
  - Automatically label PRs with okay-to-test
    - Remove okay-to-test label after every push for security
      - Speficially for non-maintainers
    - Add okay-to-test to PRs from maintainers
  Implement methods to trigger specific subgroups of tests 


If time permits:
  - Implement graphs to the dashboard
  - Proposal on Host Prow including expense estimates and implementation requirements
  - Implement commands to add label via GitHub comments

## 2. Users/Personas Of The Project:

***This section describes the principal user roles of the project together with the key characteristics of these roles. This information will inform the design and the user scenarios. A complete set of roles helps in ensuring that high-level requirements can be identified in the product backlog.***

***Again, the description should be specific enough that you can determine whether user A, performing action B, is a member of the set of users the project is designed for.***

The typical user will be a developer of Kata Containers utilizing GitHub-based CI/CD. More specially there is maintainers and non-maintainers. Non-maintainers have less permissions and any time they update or push code their work needs to be check over before it is run through the testing pipeline. Compared to maintainers who could be seen more as admin of the system. They ensure code quality, review merge requests, as well as pull requests. None the less both user groups require a user interface to easily view the results of their tests.

---

## 3.   Scope and Features Of The Project:

***The Scope places a boundary around the solution by detailing the range of features and functions of the project. This section helps to clarify the solution scope and can explicitly state what will not be delivered as well.***

***It should be specific enough that you can determine that e.g. feature A is in-scope, while feature B is out-of-scope.***

As Kata Containers support many different systems, architectures, hypervisors and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the success of the project.

Our planned features include:

***Dashboard:***
- Implement tree view
- Implement way to filter specific tests
- Implement way to only take into account required tests
- Implement collapse/expand all
- Implement new views:
- Currently: Nightly results indexed by test name
  - New: PR results indexed by test name
  - New: Test results indexed by nightly run
  - New: Test results indexed by PR run

***CI Automation:***
- Automatically add the ok-to-test label to PRs from maintainers
- Automatically remove the ok-to-test label after every push to increase security (for non-maintainers)
- Implement labels that trigger specific subsets of tests (e.g. ok-to-test-perf)

## 4. Solution Concept

***This section provides a high-level outline of the solution.***

***Global Architectural Structure Of the Project:***

***This section provides a high-level architecture or a conceptual diagram showing the scope of the solution. If wireframes or visuals have already been done, this section could also be used to show how the intended solution will look. This section also provides a walkthrough explanation of the architectural structure.***

***Design Implications and Discussion:***

***This section discusses the implications and reasons of the design decisions made during the global architecture design.***

Prow will require deployment to a Kubernetes Cluster, which will need to be hosted, for which we plan to use Microsoft's Azure Kubernetes Service.

## 5. Acceptance criteria

***This section discusses the minimum acceptance criteria at the end of the project and stretch goals.***

Minimum Acceptance Criteria:

CI Dashboard:
- Implement tree view
- Implement way to filter specific tests
- Implement way to only take into account required tests
- Implement collapse/expand all
- Implement new views:
  - PR results indexed by test name
  - Test results indexed by nightly run
  - Test results indexed by PR run
  
CI automation:
- Automatically add the ok-to-test label to PRs from maintainers
- Automatically remove the ok-to-test label after every push to increase security (for non-maintainers)
- Implement labels that trigger specific subsets of tests (e.g. ok-to-test-perf)

Stretch Goals:

CI Dashboard:
- Implement graphs 

CI Automation:
- Implement commands to set such labels via Github comments

## 6.  Release Planning:

***Release planning section describes how the project will deliver incremental sets of features and functions in a series of releases to completion. Identification of user stories associated with iterations that will ease/guide sprint planning sessions is encouraged. Higher level details for the first iteration is expected.***

We plan on 5 major releases, corresponding to the 5 planned sprints throughout the semester:

1. Project setup, creation of placeholder GitHub Bot, and skeletons of planned features
2. Improvements to existing CI Dashboard: visualizations and health checks
3. Basic GitHub bot commands
4. Implement labels for the PRs
5. Finalize and test features
