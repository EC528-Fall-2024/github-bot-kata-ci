## Collaborators

| Names          | Roles   | Emails                       | GitHub Handles |
| :------------- | ------- | ---------------------------- | -------------- |
| Aurelien Bombo | Mentor  | aurelien.bombo@microsoft.com | sprt           |
| Anna Finn      | Student | afinn12@bu.edu               | afinn12        |
| James Knee     | Student | jamesaknee@gmail.com         | JamesKnee      |
| Chris Krenz    | Student | ckrenz@bu.edu                | chris-krenz    |
| Alicja Mahr    | Student | alicja@bu.edu                | a1icja         |
| Xiteng Yao     | Student | xtyao@bu.edu                 | xtyao66        |

## Sprint Demo Videos

1. Due by Wednesday, September 25th/October 2nd
2. Due by Wednesday, October 9th/October 16th
3. Due by Wednesday, October 23rd/October 30th
4. Due by Wednesday, November 6th/November 13th
6. Due by Wednesday, November 20th/Monday, November 25th

## Sprint Demo Slides

1. Due by Wednesday, September 25th/October 2nd
2. Due by Wednesday, October 9th/October 16th
3. Due by Wednesday, October 23rd/October 30th
4. Due by Wednesday, November 6th/November 13th
5. Due by Wednesday, November 20th/Monday, November 25th

## Project Description Template

## 1.   Vision and Goals Of The Project:

***The vision section describes the final desired state of the project once the project is complete. It also specifies the key goals of the project. This section provides a context for decision-making. A shared vision among all team members can help ensuring that the solution meets the intended goals. A solid vision clarifies perspective and facilitates decision-making.***

***The vision statement should be specific enough that you can look at a proposed solution and say either "yes, this meets the vision and goals", or "no, it does not".***

Kata Containers is an open-source community working to build a secure container runtime with lightweight virtual machines that feel and perform like containers but provide stronger workload isolation using hardware virtualization technology as a second layer of defense.

As Kata Containers support many different systems, architectures, hypervisors, and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the project's success. As such, the community is continuously investigating ways to strengthen our testing pipelines and make our processes more efficient.

To that end, the goal of this project will be to:

1. Implement improvements to the recently developed [Kata CI Dashboard](https://portersrc.github.io/) to visualize CI runs, improve the clarity of the dashboard feedback, and better assess the health of the testing infrastructure
2. Develop a plan for—and a cost estimate of—implementing a CI GitHub Bot for Kata Containers that would help Kata Container developers automate a variety of tasks and run commands via GitHub comments
3. And, if time permits, implement the GitHub Bot along with a variety of commands that facilitate CI development and transparency

Note: Since the original project proposal, the Kata CI Dashboard was released recently and has become a focal point of the community's efforts to improve Kata Container CI/CD.  The dashboard offers a timely and valuable opportunity to deliver impactful CI/CD functionality to the developer community.  As such, we will prioritize dashboard development over the original objective of GitHub Bot development, though the latter remains an important long-term goal.

More specifically, we plan to...
- Enhance the test management dashboard 
  - Implement tree view
  - Implement filtering capabilities to allow users to target specific test criteria (e.g., required vs. optional tests)
  - Implement a feature to collapse and expand data regarding each test
  - Indicate how many required/non-required tests were passed
  - Implement different ways to index tests:
    - Test name
    - Nightly run
    - PR run
- Implement a CI bot to help us automate things and run commands via Github comments
  - Automatically label PRs with okay-to-test
    - Remove the 'okay-to-test' label after every push for security
      - Specifically for non-maintainers
    - Add okay-to-test to PRs from maintainers
  Implement methods to trigger specific subgroups of tests 

If time permits:
  - Implement graphs to the dashboard
  - Proposal on Host Prow including expense estimates and implementation requirements
  - Implement commands to add labels via GitHub comments


## 2. Users/Personas Of The Project:

***This section describes the principal user roles of the project together with the key characteristics of these roles. This information will inform the design and the user scenarios. A complete set of roles helps in ensuring that high-level requirements can be identified in the product backlog.***

***Again, the description should be specific enough that you can determine whether user A, performing action B, is a member of the set of users the project is designed for.***

The typical user will be a developer of Kata Containers who is utilizing GitHub-based CI/CD.  More specifically, there are maintainers and non-maintainers. Non-maintainers have fewer permissions and any time they update or push code their work needs to be checked before it is run through the testing pipeline. Compared to maintainers who could be seen more as admin of the system. They ensure code quality as well as review merge requests and pull requests. Nonetheless, both user groups require a user interface to easily view the results of their tests.

Here we briefly describe a couple of hypothetical users and describe the utility of this project to each of their workflows.


#### Doug the Dashboard User

Doug is a developer for Kata Containers.  Doug's primary development CI/CD workflow is centered on the Kata Containers CI Dashboard.  


#### Ben the Bot User

Ben is also a Kata Containers developer, but their CI/CD workflow is instead focused on using a GitHub Bot and running commands to monitor the progress and health of development.


## 3.   Scope and Features Of The Project:

***The Scope places a boundary around the solution by detailing the range of features and functions of the project. This section helps to clarify the solution scope and can explicitly state what will not be delivered as well.***

***It should be specific enough that you can determine that e.g. feature A is in-scope, while feature B is out-of-scope.***

As Kata Containers support many different systems, architectures, hypervisors, and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the success of the project.

Our planned features include:

***Dashboard:***
- Implement tree view
- Implement a way to filter specific tests
- Implement a way to only take into account required tests
- Indicate how many tests were passed
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

In terms of the Dashboard, we believe we could leverage the current dashboard and implement the desired changes directly. In terms of implementation, we plan to create a testing label system. This would allow users to group tests into specific categories. Additionally, the required tests would be displayed while less important tests are not. We could leverage these same labels for other aspects of the dashboard, such as filtering. All other aspects of the dashboard will be implemented as they see fit. In general, we will reference the Ci pipeline that was just run for a given job and then add the corresponding results to the dashboard. When doing this we will give the entries different properties and labels that allow us to develop different ways of viewing the information. The labels including the ones mentioned above would have to be implemented in the CI pipeline automation.

![Architecture diagram](https://katacontainers.io/static/589e3d905652847b22c395fe6bbbace7/8fef6/katacontainers_architecture_diagram.jpg)

## 5. Acceptance criteria

***This section discusses the minimum acceptance criteria at the end of the project and stretch goals.***

#### Minimum Viable Product:

* Basic CI Dashboard improvements, minimally including:
  * A tree view
  * A way to filter to specific tests
  * A way to only consider the *required* tests
  * Ability to collapse and expand all
  * New views for:
    * PR results indexed by test name
    * Test results indexed by nightly run
    * Test results indexed by PR run
  * Graph overviews
  * A variety of Dashboard features identified by the team and broader community throughout the course of the project.
* A detailed plan for how our team—or the community—can implement a GitHub Bot and associated CI/CD commands

#### Stretch Goals:

* A GitHub Bot that allows for CI automation
* Associated commands to:
  * Automatically add the ok-to-test label to PRs from maintainers
  * Automatically remove the ok-to-test label after every push to increase security (for non-maintainers)
  * Implement labels that trigger specific subsets of tests (e.g. ok-to-test-perf)
  * A variety of additional commands identified by the team and broader community throughout the course of the project.

**Note**: We will update these lists with additional features/goals as they become clear through discussions with the community.

## 6.  Release Planning:

***Release planning section describes how the project will deliver incremental sets of features and functions in a series of releases to completion. Identification of user stories associated with iterations that will ease/guide sprint planning sessions is encouraged. Higher level details for the first iteration is expected.***

We plan on 5 major releases, corresponding to the 5 planned sprints throughout the semester:

1. Project setup, implementation of and experimentation with Kata Containers, skeletons of planned Dashboard features, and basic research on a potential Bot implementation
2. Substantive improvements to existing CI Dashboard (visualizations and health checks) and research into a GitHub Bot implementation
3. Creation of placeholder GitHub Bot and further improvements to the Dashboard
4. Implement labels for the PRs and, if time permits, implementation of GitHub Bot commands
5. Finalize and test features

Note: Once our sprint schedule is known, we will update this section with specific sprint/release dates.

## Resources

* Kubernetes and containers: [https://kubernetes.io/](https://kubernetes.io/)
* Kata containers: [https://katacontainers.io/learn/](https://katacontainers.io/learn/)
* Kata repo:  [https://github.com/kata-containers/kata-containers](https://github.com/kata-containers/kata-containers)
* Installation guide: [https://github.com/kata-containers/kata-containers/tree/main/docs/install](https://github.com/kata-containers/kata-containers/tree/main/docs/install)
* Community info (incl. weekly meeting and Slack channels): [https://github.com/kata-containers/community](https://github.com/kata-containers/community)
* Architecture: [https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture](https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture)
* Architecture 3.0: [https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture_3.0](https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture_3.0)
* Contributing guide: [https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md](https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md)
* CI guide: [https://github.com/kata-containers/kata-containers/blob/main/ci/README.md](https://github.com/kata-containers/kata-containers/blob/main/ci/README.md)
* Prow: [https://docs.prow.k8s.io/docs/getting-started-deploy/](https://docs.prow.k8s.io/docs/getting-started-deploy/)
* Porters: [https://portersrc.github.io/](https://portersrc.github.io/)

---

## About

## Installation

#### Dependencies

## Usage

#### Examples

## License

[CC0 1.0 Universal](https://github.com/EC528-Fall-2024/github-bot-kata-ci/blob/main/LICENSE)
