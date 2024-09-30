## Collaborators

| Names             | Roles   | Emails                       | GitHub Handles |
| :---------------- | ------- | ---------------------------- | -------------- |
| Aurelien Bombo    | Mentor  | aurelien.bombo@microsoft.com | sprt           |
| Archana Choudhary | Mentor  | archana1@microsoft.com       | arc9693        |
| Saul Paredes      | Mentor  | saulparedes@microsoft.com    | Redent0r       |
| Anna Finn         | Student | afinn12@bu.edu               | afinn12        |
| James Knee        | Student | jamesaknee@gmail.com         | JamesKnee      |
| Chris Krenz       | Student | ckrenz@bu.edu                | chris-krenz    |
| Alicja Mahr       | Student | alicja@bu.edu                | a1icja         |
| Xiteng Yao        | Student | xtyao@bu.edu                 | xtyao66        |

## Sprint Demo Videos

1. [Sprint 1 Video](https://drive.google.com/file/d/1We9vtgX5poMUT0BkioDxLE8eoD2TF5NO/view?usp=sharing)
2. Due by Wednesday, October 9th/October 16th
3. Due by Wednesday, October 23rd/October 30th
4. Due by Wednesday, November 6th/November 13th
5. Due by Wednesday, November 20th/Monday, November 25th

## Sprint Demo Slides

1. [Sprint 1 Slides](https://docs.google.com/presentation/d/1YY3hOz72ddWBu9trWHyxlHmOa4Xpm7kRqmj7HP0JlaQ/edit#slide=id.g304af07303f_6_6)
2. Due by Wednesday, October 9th/October 16th
3. Due by Wednesday, October 23rd/October 30th
4. Due by Wednesday, November 6th/November 13th
5. Due by Wednesday, November 20th/Monday, November 25th

## Final Presentation

1. Due by Monday, December 9th/Wednesday, December 11th

## 1.   Vision and Goals Of The Project:

***The vision section describes the final desired state of the project once the project is complete. It also specifies the key goals of the project. This section provides a context for decision-making. A shared vision among all team members can help ensuring that the solution meets the intended goals. A solid vision clarifies perspective and facilitates decision-making.***

***The vision statement should be specific enough that you can look at a proposed solution and say either "yes, this meets the vision and goals", or "no, it does not".***

Kata Containers is an open-source community working to build a secure container runtime with lightweight virtual machines that feel and perform like containers but provide stronger workload isolation using hardware virtualization technology as a second layer of defense.

As Kata Containers support many different systems, architectures, hypervisors, and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the project's success. As such, the community is continuously investigating ways to strengthen our testing pipelines and make our processes more efficient.

To that end, the goal of this project will be to:

1. Implement improvements to the recently developed [Kata CI Dashboard](https://kata-containers.github.io/) to visualize CI runs, improve the clarity of the dashboard feedback, and better assess the health of the testing infrastructure
2. Develop a plan for—and a cost estimate of—implementing a CI GitHub Bot for Kata Containers that would help Kata Container developers automate a variety of tasks and run commands via GitHub comments
3. And, if time permits, implement the GitHub Bot along with a variety of commands that facilitate CI development and transparency

**Note**: Since the original project proposal, the Kata CI Dashboard was released recently and has become a focal point of the community's efforts to improve Kata Container CI/CD.  The dashboard offers a timely and valuable opportunity to deliver impactful CI/CD functionality to the developer community.  As such, we will prioritize dashboard development over the original objective of GitHub Bot development, though the latter remains an important long-term goal.

## 2. Users/Personas Of The Project:

***This section describes the principal user roles of the project together with the key characteristics of these roles. This information will inform the design and the user scenarios. A complete set of roles helps in ensuring that high-level requirements can be identified in the product backlog.***

***Again, the description should be specific enough that you can determine whether user A, performing action B, is a member of the set of users the project is designed for.***

The typical user will be a developer of Kata Containers who is utilizing GitHub-based CI/CD.  More specifically, there are non-maintainers/regular developers and then maintainers/reviewers. Non-maintainers have fewer permissions and any time they update or push code their work needs to be checked before it is run through the testing pipeline.  This is in contrast to maintainers who could be seen more as admins of the system. They ensure code quality as well as review merge requests and pull requests.

Both of these user groups require a UI and tools to easily view and assess the results of their CI tests, though their use cases may differ somewhat.  Maintainers may find it especially useful to have Dashboard features that monitor the health and status of all tests at merge time.  Other (non-maintainer) developers, who are not direclty responsible for approving pull requests or performing merges, may find more utility in commands that can be run prospectively to assess code quality, etc.  Maintainers will be more interested in running all available tests (at least the required tests) to ensure code compatitilbity and stability, whereas non-maintainer developers may prefer to zoom in on specific tests that relate to the particular features they are implementing.

Regardless, all tools—both GitHub commands and Dashboard features—will be available to and useful for any Kata Containers developer.

## 3.   Scope and Features Of The Project:

***The Scope places a boundary around the solution by detailing the range of features and functions of the project. This section helps to clarify the solution scope and can explicitly state what will not be delivered as well.***

***It should be specific enough that you can determine that e.g. feature A is in-scope, while feature B is out-of-scope.***

As Kata Containers support many different systems, architectures, hypervisors, and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the success of the project.  Critical to this project will be the team's ability to communicate and coordinate with the broader Kata Contaiers developer community in order to identify and properly define the features that will be most useful to the community.  This process of brainstorming and detailed specification/operationalization can be helpful for the community's future development, even for features we are not able to implement ourselves.

From our preliminary discussions, our currently planned features include:

***Dashboard:***

- Implement a tree view
- Implement a way to filter specific tests
- Implement a way to only take into account required tests
- Indicate how many required/non-required tests were passed
- Implement a feature to collapse and expand data regarding each test
- Implement new views/indexing (currently nightly results indexed by test name):
  - New: PR results indexed by test name
  - New: Test results indexed by nightly run
  - New: Test results indexed by PR run
- Implement graphs (stretch goal)

***CI Bot Automation/Commands:***

- Automatically add the ok-to-test label to PRs from maintainers
- Automatically remove the ok-to-test label after every push to increase security (for non-maintainers)
- Implement labels that trigger specific subsets of tests (e.g. ok-to-test-perf)
- Create proposal for how to implement a GitHub bot (likely with Prow; will require hosting)
- Implement commands to set such labels via GitHub comments (stretch goal)

**Note**: This list of features will undoubtedly grow as we continue to interact with the entire community.  We will update these lists with additional features/goals as they become clear.

## 4. Solution Concept

***This section provides a high-level outline of the solution.***

***Global Architectural Structure Of the Project: T******his section provides a high-level architecture or a conceptual diagram showing the scope of the solution. If wireframes or visuals have already been done, this section could also be used to show how the intended solution will look. This section also provides a walkthrough explanation of the architectural structure.***

***Design Implications and Discussion: This section discusses the implications and reasons of the design decisions made during the global architecture design.***

In terms of the Dashboard, we plan to leverage the existing [Kata Contianers CI Dashboard](https://kata-containers.github.io/) to add the desired changes/functionality. In terms of implementation, we will create a testing PR labeling system. This would allow users to:

* Group tests into specific categories
* Display required tests while hiding less important tests
* Set which tests to be run for which PRs

In general, we will reference the CI pipeline that was just run for a given job and then add the corresponding results to the Dashboard. When doing this we will give the entries different properties and labels that allow us to develop different ways of viewing the information. The labels, including the ones mentioned above, would have to be implemented in the CI pipeline automation.

In terms of the CI Automation and GitHub Bot, we plan to use [Prow](https://docs.prow.k8s.io/docs/getting-started-deploy/)—a Kubernetes based CI/CD system.  However, this is deployed in a Kubernetes cluster and so will require hosting with a cloud provider.  Since this comes with a non-negligible cost, one of our first goals will be to assess this cost and flesh out the implementation details.  Our current plan is to use Azure Kubernetes Service, as Microsoft is already sponsoring the Kata project.

Prow allows users to trigger jobs from various types of events and report their status to many  different services. Critically, Prow also provides GitHub automation in the form of policy enforcement, chat-ops via /foo style commands, and automatic PR merging.  These features make Prow a perfect fit for the current project.

See the images below for an overview of the architectures for both Kata Contains and Prow.

![Architecture diagram](https://katacontainers.io/static/589e3d905652847b22c395fe6bbbace7/8fef6/katacontainers_architecture_diagram.jpg)

![1726854857223](image/README/ProwArchitecture.png)

## 5. Acceptance criteria

***This section discusses the minimum acceptance criteria at the end of the project and stretch goals.***

These features are elaborated on in greater detail in **Section 3** above.  This section provides a brief summary of the features.

#### Minimum Viable Product:

* CI Dashboard:
  * New tree view
  * New filtering options
  * New indexing/sorting options
* CI Automation
  * Ability to automatically add/remove test labels to PRs
  * Have labels that trigger a subset of tests to be run
* A detailed plan for how our team—or the community—can implement a GitHub Bot and associated CI/CD commands

#### Stretch Goals:

* Dashboard
  * Implement graphs
* CI Automation and GitHub Bot
  * Implement commands to set labels via GitHub comments

**Note**: As we communicate further with the community, we will undoubtedly add to these feature lists— both for the MVP and the Stretch goals.

## 6.  Release Planning:

***Release planning section describes how the project will deliver incremental sets of features and functions in a series of releases to completion. Identification of user stories associated with iterations that will ease/guide sprint planning sessions is encouraged. Higher level details for the first iteration is expected.***

We plan on 5 major releases, corresponding to the 5 planned sprints throughout the semester:

1. Project setup, implementation of and experimentation with Kata Containers, skeletons of planned Dashboard features, and basic research on a potential Bot implementation
2. Substantive improvements to existing CI Dashboard (visualizations and health checks) and research into a GitHub Bot implementation
3. Creation of placeholder GitHub Bot and further improvements to the Dashboard
4. Implement labels for the PRs and, if time permits, implementation of GitHub Bot commands
5. Finalize and test features

**Note**: Once our sprint schedule is known, we will update this section with specific sprint/release dates.

## Resources

* Kata board: [https://github.com/orgs/kata-containers/projects/49/views/1](https://github.com/orgs/kata-containers/projects/49/views/1)
* Dashboard code: [https://github.com/kata-containers/kata-containers.github.io](https://github.com/kata-containers/kata-containers.github.io)
* Kubernetes and containers: [https://kubernetes.io/](https://kubernetes.io/)
* Kata containers: [https://katacontainers.io/learn/](https://katacontainers.io/learn/)
* Kata repo:  [https://github.com/kata-containers/kata-containers](https://github.com/kata-containers/kata-containers)
* Installation guide: [https://github.com/kata-containers/kata-containers/tree/main/docs/install](https://github.com/kata-containers/kata-containers/tree/main/docs/install)
* Community info (incl. weekly meeting and Slack channels): [https://github.com/kata-containers/community](https://github.com/kata-containers/community)
* Architecture: [https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture](https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture)
* Architecture 3.0: [https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture_3.0](https://github.com/kata-containers/kata-containers/tree/main/docs/design/architecture_3.0)
* Contributing guide: [https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md](https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md)
* Patch format: [https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md#patch-format](https://github.com/kata-containers/community/blob/main/CONTRIBUTING.md#patch-format)
* CI guide: [https://github.com/kata-containers/kata-containers/blob/main/ci/README.md](https://github.com/kata-containers/kata-containers/blob/main/ci/README.md)
* Prow: [https://docs.prow.k8s.io/docs/getting-started-deploy/](https://docs.prow.k8s.io/docs/getting-started-deploy/)

---

## About

This is a project for BU EC528: Cloud Computing Fundamentals that is intended to implement a GitHub bot for the Kata Containers CI to automate various tasks, as well as implement improvements to the existing [Kata Containers CI Dashboard](https://kata-containers.github.io/).

## Installation

Kata Containers: [https://github.com/kata-containers/kata-containers/pull/10335](https://github.com/kata-containers/kata-containers/pull/10335)

#### Dependencies

## Usage

#### Examples

## License

[CC0 1.0 Universal](https://github.com/EC528-Fall-2024/github-bot-kata-ci/blob/main/LICENSE)
