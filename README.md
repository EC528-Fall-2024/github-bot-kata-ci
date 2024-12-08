## [MAIN DASHBOARD REPOSITORY](https://github.com/kata-containers/kata-containers.github.io)

- (Instructions below and in this repo)

## [DEPLOYED DASHBOARD](https://kata-containers.github.io/)

## Collaborators

| Names             | Roles   | Emails                       | GitHub Handles |
| :---------------- | ------- | ---------------------------- | -------------- |
| Aurelien Bombo    | Mentor  | aurelien.bombo@microsoft.com | sprt           |
| Archana Choudhary | Mentor  | archana1@microsoft.com       | arc9693        |
| Saul Paredes      | Mentor  | saulparedes@microsoft.com    | Redent0r       |
| Anna Finn         | Student | afinn12@bu.edu               | afinn12        |
| James Knee        | Student | jknee@bu.edu                 | JamesKnee      |
| Chris Krenz       | Student | ckrenz@bu.edu                | chris-krenz    |
| Alicja Mahr       | Student | alicja@bu.edu                | a1icja         |
| Xiteng Yao        | Student | xtyao@bu.edu                 | xtyao66        |

## Other Relevant Repositories

- [Original Dashboard Repo](https://github.com/kata-containers/kata-containers.github.io)
- [Forked Dashboard Repo](https://github.com/a1icja/kata-dashboard-next) (work mostly done here, PR into original)
- [Old Forked Dashboard Repo](https://github.com/afinn12/portersrc.github.io) (before switch to React/Next.js, stale)

## Sprint Demo Videos

1. [Sprint 1 Video](https://drive.google.com/file/d/1We9vtgX5poMUT0BkioDxLE8eoD2TF5NO/view?usp=sharing)
2. [Sprint 2 Video](https://drive.google.com/file/d/15YUULSI2Xe6KHCUbwtsGrMwh4HszdG7H/view?usp=sharing)
3. [Sprint 3 Video](https://drive.google.com/file/d/1qCYdzWGJTecCp1liND09Lp17qN61Xw_1/view?usp=sharing)
4. [Sprint 4 Video](https://drive.google.com/file/d/1ygEmctDjnu6iLNQIfxE3_Ri0lu93uumF/view?usp=sharing)
5. [Sprint 5 Video](https://drive.google.com/file/d/1O4HhWOrTOynqY4QIdDS_sEb1kgp2TRFY/view?usp=sharing)

## Sprint Demo Slides

1. [Sprint 1 Slides](https://docs.google.com/presentation/d/1YY3hOz72ddWBu9trWHyxlHmOa4Xpm7kRqmj7HP0JlaQ/edit#slide=id.g304af07303f_6_6)
2. [Sprint 2 Slides](https://docs.google.com/presentation/d/11SlJg44mNMW-6hoD_dekvK64vk646ftpcA0L6TzLGWY/edit?usp=sharing)
3. [Sprint 3 Slides](https://docs.google.com/presentation/d/1zIPiGBRkyaaVgajAXlqNz-Tdb6NFuN7FT9XffjaEJI0/edit?usp=sharing)
4. [Sprint 4 Slides](https://docs.google.com/presentation/d/1JWvncefIY-mVV4SW9QUd362THwFW1hYgPA8rdsd-TDk/edit?usp=sharing)
5. [Sprint 5 Slides](https://docs.google.com/presentation/d/1YRQFQA7O5_xs-XQSTuFy182kfTP2yZVaZxzPwVXXWp0/edit?usp=sharing)

## Final Presentation

* [Presentation](https://drive.google.com/file/d/1NMbA7HrLLp7KjLt1C25P3nxwJhRIfru7/view)
* [Slides](https://docs.google.com/presentation/d/1fArOblI6RxerWxFWaAetssDYMQYcX-Zrg8bEyxsIdtU/edit?usp=sharing)


## 1.   Vision and Goals Of The Project:

Kata Containers is an open-source community working to build a secure container runtime with lightweight virtual machines that feel and perform like containers but provide stronger workload isolation using hardware virtualization technology as a second layer of defense.

As Kata Containers support many different systems, architectures, hypervisors, and other underlying technologies, CI (continuous integration) along with a stable and automated test environment are paramount to the project's success. As such, the community is continuously investigating ways to strengthen our testing pipelines and make our processes more efficient.

To that end, the primary goals of this project were to:

1. Implement improvements to the recently developed [Kata CI Dashboard](https://kata-containers.github.io/) to visualize CI runs, improve the clarity of the dashboard feedback, and better assess the health of the testing infrastructure
2. Develop a plan for—and a cost estimate of—implementing a CI GitHub Bot for Kata Containers that would help Kata Container developers automate a variety of tasks and run commands via GitHub comments
3. And, if time permits, implement the GitHub Bot along with a variety of commands that facilitate CI development and transparency

**Note**: Since the original project proposal, the Kata CI Dashboard was released and became a focal point of the community's efforts to improve Kata Container CI/CD.  The dashboard offered a timely and valuable opportunity to deliver impactful CI/CD functionality to the developer community.  As such, we initially prioritized dashboard development over the original objective of GitHub Bot development.  That said, we did invest a bit more time into the GitHub Bot toward the end of the semester, after it was clear the Dashboard feastures were all on track.

A high level overview of the project can be found in the following diagram:

![1729668351257](image/README/ProjectArchitecture.png)

This essentially shows the 4 key components of the system:

* GitHub where PR checks and Nightly (or other) CI tests are initiated
* CI Dashboard where test statuses and related data can be viewed
* Test Environments where the Kubernetes clusters and Kata containers run
* Prow—a Kubernetes-based CI/CD pipeline—that facilitates communication between GitHub and the test environments (Prow enables features like allowing developers to rerun specific tests by adding comments to PRs)

These features are discussed further below.

## 2. Users/Personas Of The Project:

The typical user will be a developer of Kata Containers who is utilizing GitHub-based CI/CD.  More specifically, there are non-maintainers/regular developers and then maintainers/reviewers. Non-maintainers have fewer permissions and any time they update or push code their work needs to be checked before it is run through the testing pipeline.  This is in contrast to maintainers who could be seen more as admins of the system. They ensure code quality as well as review merge requests and pull requests.

Both of these user groups require a UI and tools to easily view and assess the results of their CI tests, though their use cases may differ somewhat.  Maintainers may find it especially useful to have Dashboard features that monitor the health and status of all tests at merge time.  Other (non-maintainer) developers, who are not directly responsible for approving pull requests or performing merges, may find more utility in commands that can be run prospectively to assess code quality, etc.  Maintainers will be more interested in running all available tests (at least the required tests) to ensure code compatitilbity and stability, whereas non-maintainer developers may prefer to zoom in on specific tests that relate to the particular features they are implementing. Regardless, all tools—both GitHub commands and Dashboard features—will be available to and useful for any Kata Containers developer.

Critical to this project was be the team's ability to communicate and coordinate with the broader Kata Containers developer community in order to identify and properly define the features that would be most useful to the community.  This process of brainstorming and operationalizing can be helpful for the community's future development, even for features we were not able to implement ourselves.  To this end, the student team presented to two developer communities, beyond their core group of mentors:

* [Cloud Native Computing Foundation](https://www.cncf.io/about/who-we-are/) confidential containers (CoCo) )meeting on October 9, 2024
* OpenInfra Foundation's Project Teams Gathering ([PTG](https://openinfra.dev/ptg/)) meeting on October 21, 2024

For example, at the first meeting, the team presented two options for the CI Dashboard architecture: sticking with the original jQuery implementation or upgrading to Next.js/React.  These options are discussed further in the next section.  During the CoCo meeting, the community approved the team's transition to Next.js/React, which is the architecture the team implemented.

## 3.   Scope and Features Of The Project:

The Dashboard repo is currently located [here](https://github.com/kata-containers/kata-containers.github.io), though the student team started implementing these features in two separate repos:

* [Repo](https://github.com/afinn12/portersrc.github.io) with upgrades to the original jQuery (and HTML/CSS) architecture
* [Repo](https://github.com/a1icja/kata-dashboard-next) with the Next.js/React implementation of the dashboard (deployed Dashboard is accessible [here](https://a1icja.github.io/kata-dashboard-next/))

These versions were initially created so the students could explore both implementations—jQuery and Next.js/React—identify the pros/cons of each, and present the two options to the community.  jQuery is a fast, lightweight JS library (simplifies DOM/event manipulations); Next.js is a React-based framework for server-rendered, static, or hybrid web apps; and React is a JS library for UIs with reusable components & declarative style.  Each implementation has its own advantages and disadvantages, but Next.js/React were ultimately chosen, largely to increase development velocity and avoid reinventing the wheel (through the use of pre-defined React components).

Currently, the Dashboard runs on a static GitHub Pages page and displays data on both: 1) a battery of tests run Nightly and 2) checks that are run on certain PRs.  The GitHub Bot--implemented via Prow, which is discussed further below--is not currently implemented but is being planned.

Here are the features we currently have implemented or plan to implement.

***Dashboard:***

- [X] Switch to React/Next.js
- [X] Implement a way to filter using the URL
- [X] Implement a way to only take into account required tests
  - [X] Added filter/sort for required tag
- [X] Implement a feature to collapse and expand data regarding each test
- [X] Implement new views/indexing (currently nightly results indexed by test name):
  - [X] PR results indexed by test name
  - [X] Test results indexed by PR run
  - [X] Single PR view
- [X] Authenticate fetch scripts to raise rate limits
- [X] Fetch data on changes to fetch scripts (if new data is required)
- [X] Add Maintainers list (group to contact about test)
  - [X] Design backend/create groupings
  - [X] Allow community to update these mappings
- [X] Indicate if test was rerun
  - [X] Add number of reruns in dropdown menu
    - [X] Add individual results of reruns in dropdown menu
  - [X] Add info to table column
- [X] Add ok-to-test-tdx label
- [X] Default sort by worst performing job/check
- [X] Create CoCo dashboard using iFrame to easily replicate for other communities

## Screenshots of Dashboard:

![image](https://github.com/user-attachments/assets/89037c60-f4b0-4a74-ab0b-fcc73f2c5955)
![image](https://github.com/user-attachments/assets/6f9d5f60-e105-468b-be4b-42660f77cab3)
![image](https://github.com/user-attachments/assets/cb43fa37-750e-468e-a752-d7b3fba7f8b9)
![image](https://github.com/user-attachments/assets/6b5c9680-51b5-4eea-baec-47892e7c8cfb)

## Notes

- Clicking on the Maintainer's Github/slack opens links to the person's account
- CLicking on the run/check number or rerun attempt result opens the job/check in Github
- URL search and display (Nightly/PR/Single) is appended to the URL

***CI Bot Automation/Commands:***

- [X] Early draft proposal for Prow implementation
- [X] Get rough cost estimate for AKS deployment
- [X] Finalize proposal for Prow implementation
- [X] Develop documentation to help the community deploy Prow
- [ ] Fully implement and test Prow

## 4. Solution Concept

In terms of the Dashboard, we built on the existing [Kata Containers CI Dashboard](https://kata-containers.github.io/) to add the desired changes/functionality, and we leveraged a testing PR labeling system that allows users to:

* Group tests into specific categories
* Display required tests while hiding less important tests
* Set which tests to be run for which PRs

At a high level, fetch scripts are executed to pull data on nightly runs and PR checks, the results of which are then displayed in the Dashboard.

In terms of the CI Automation and GitHub Bot, we followed our mentors' suggestion to use [Prow](https://docs.prow.k8s.io/docs/getting-started-deploy/)—a Kubernetes based CI/CD system.  However, this is deployed in a Kubernetes cluster and so requires hosting with a cloud provider.  Since this comes with a non-negligible cost, one of our first goals was to assess this cost and flesh out the implementation details.  Our primary goal was to use Azure Kubernetes Service (AKS), as Microsoft is already sponsoring the Kata project.  However, we did simultaneously pursue development on Google Kubernetes Engine (GKE) for a few reasons:

- $300 worth of free credits offered by Google
- This allowed multiple developers to work in parallel
- Obstacles identified in GKE informed the implementation in AKS

Prow allows users to trigger jobs from various types of events and report their status to many  different services. Critically, Prow also provides GitHub automation in the form of policy enforcement, chat-ops via /foo style commands, and automatic PR merging.  These features made Prow a good fit for the project.

Additional information on Prow and steps on how to implement it can be found [here](https://docs.google.com/document/d/17UyHFISMm3XhTnqK5VWlg2GftkLSPbJdtMezvP_CWqc/edit?tab=t.0#heading=h.qgcjy19595ny).

Here is a high level overview of the steps

1. Set Up Kubernetes Cluster on Azure

   * Deployed on both AKS and GKE for testing
2. Deploy Prow Components

   * Deployed the following pods:
     * crier (reports job statuses to GitHub)
     * deck (displays pipeline results and logs)
     * ghproxy (caches and throttles requests to the GitHub API to optimize usage and avoid rate limits)
     * hook (receives GitHub webhook and triggers jobs)
     * horologium (scheduels periodic jobs)
     * prow-controller-manager (manages job execution in build cluster)
     * sinker (cleans up old jobs and pods)
     * statusreconciler (ensures job statuses in Prow and GitHub remain consistent by reconciling discrepancies)
     * tide (automates PR merges on test results)
   * Still need to configure storage properly on AKS (MinIO presented significant challenge in AKS)
3. Configure GitHub Integration

   * Created a Github app and linked it to Prow’s hook
4. Implement CI/CD Pipelines

   * In progress
   * At least in GKE: tests can be run in Prow but not yet initiated from GitHub
5. Set Up a Database for CI/CD Results

   * In progress
   * A database will be needed to store the CI/CD results
   * Potentially use Azure Cosmos DB or table DB
6. Show the Pipeline results on our webpage

   * In progress
   * Use Deck to display results through a UI
   * For advanced filtering or historical views, connect the web interface to the CI/CD results database
   * Implement role-based access for secure viewing

See the images below for an overview of the architectures for both Kata Contains and Prow.

#### Kata Containers Overview

![Architecture diagram](https://katacontainers.io/static/589e3d905652847b22c395fe6bbbace7/8fef6/katacontainers_architecture_diagram.jpg)

This diagram shows a basic Kata Containers architecture.  Unlike traditional containers, Kata Containers run inside lightweight VMs.

Inside each VM, an agent runs, managing container processes inside the VM. The agent receives gRPC calls from the Kata Shim to perform actions like starting or stopping containers.

Here is a summary of each component:

* Kubernetes: Manages the lifecycle of containers using the OCI (Open Container Initiative).
* Kata Shim V2: Acts as a proxy between the Kubernetes container runtime and the virtual machine running the container. OCI commands/specs are passed from Kubernetes to the Kata Shim, which translates them into gRPC calls (or Google Remote Procedure Calls–a modern, high-performance, open-source framework for inter-process communication (IPC) between applications.)
* Hypervisor: Kata Containers rely on a hypervisor (we used QEMU) to manage the lightweight VMs, ensuring strong isolation and superior security compared to a traditional container.
* VSOCK: Enables fast and secure communication between the Kata Shim and the VM, bypassing traditional networking overhead and efficient gRPC communication between the Kubernetes runtime (outside) and the agent inside the VM.

In summary:

* Kubernetes sends container commands.
* Kata Shim V2 translates those commands into gRPC calls for the VM.
* The agent inside the VM runs container workloads within lightweight VMs for enhanced security.
* VSOCK provides efficient communication between the Kata Shim and the VM.

#### Prow Overview

![1726854857223](image/README/ProwArchitecture.png)

This diagram illustrates how Prow integrates GitHub, Kubernetes, and various plugins to automate continuous integration (CI) tasks like testing, retesting, reporting, and merging PRs.

An example Prow flow would be:

1. PR Created: A contributor opens a PR in the Kata Containers GitHub repo.
2. Prow Triggers Tests: Prow automatically triggers CI jobs defined for Kata Containers (e.g., tests that run Kata Containers on different configurations).
3. Bot Feedback: The Prow GitHub bot comments on the PR with test results. Developers can use bot commands (e.g., /retest) to interact with it.
4. Merge After Approval: Once tests pass and approvals are obtained (e.g., via /approve), Prow can merge the PR automatically.

The different pieces of the diagram can be understood as follows:

* GitHub Interaction:
  * Webhooks trigger actions when pull requests (PRs) are opened, commented on, or updated.
  * GitHub commands like /retest or /meow (which are handled by Prow plugins) can be used in PR comments to trigger certain CI/CD workflows.
* Prow Components:
  * Webhook Handler: Receives webhooks from GitHub and forwards them to Prow for further actions.
  * Tide: Handles retesting and automatic merging of PRs if all conditions are met.
  * Crier: Reports status and results (e.g., pass/fail) back to GitHub.
  * Horologium: Manages scheduled jobs, creating new ones at specific intervals.
  * Sinker: Cleans up old jobs and resources, such as Pods, after they are no longer needed.
* Job Management:
  * Prowjobs: A key concept in Prow. These are Kubernetes CRDs (Custom Resource Definitions) that define and track the CI/CD jobs.
  * Build Cluster: Where the actual job execution (e.g., running tests in Pods) happens.
  * Pods: The jobs are run as Pods inside the Kubernetes cluster.
* Deck: The dashboard for visualizing job status and results.

Regarding the cost estimate, after experimenting, we came up with the following:
 - 1 cluster with 1 node of low-tier processor is enough
 - 100 GB blob storage should be enough
 - Estimated cost of around $100

We will provide further details on this in our final report to the Kata community.


## 5. Acceptance criteria

These features are elaborated on in greater detail in **Section 3** above.  This section provides a brief summary of the features.

#### Minimum Viable Product:

* CI Dashboard:
  * New filtering, sorting, and search options
  * PR data
  * Additional info, such as maintainer info
* CI Automation
  * (This goal was abandoned given its overlap with Prow) Implementation of additional PR labels that control CI tests
  * (Instead, this became the focus) Experiment with Prow and come up with a rough cost estimate
  * A detailed plan for how our team—or the community—can implement a GitHub Bot and associated CI/CD commands

#### Original Stretch Goals:

* Dashboard
  * Implement graphs
  * Implement a tree view
* CI Automation and GitHub Bot
  * Implement a basic backend to manage data fetching
  * Implement Prow
  * Implement commands to set labels via GitHub comments

We were able to complete our MVP goals, though did not complete all stretch goals.  

Progress on Prow was slowed due to outdated documentation, concerns about cost, and depioritization by the mentors. However, the team was able to experiment with Prow and will present these results to the community.

Progress on these specific Dashboard features was slowed by lengthy processes for merging to the Dashboard repo. However, the team was able to pursue other objectives not listed here, such as a CoCo Dashboard (using an iFrame to the Kata Dashboard)


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

The installation and running of the CI Dashboards are discussed further in those repos:

* Current Kata Dashboard [repo](https://github.com/kata-containers/kata-containers.github.io)
* Next.js/React Dashboard [repo](https://github.com/a1icja/kata-dashboard-next) that ultimately replaced the jQuery version

## Dashboard Instructions

This repository contains the **Kata Containers Test Dashboard**, a web application that visualizes data for the nightly tests run by the Kata Containers repository. Built using **Next.js** and styled with **TailwindCSS**, this dashboard provides a simple and efficient interface to monitor test results, leveraging modern frontend technologies to ensure responsive and scalable performance.

### Features

- Fetches nightly CI test data using custom scripts.
- Displays weather-like icons to reflect test statuses (e.g., sunny for success, stormy for failures).
- Utilizes **Next.js** for server-side rendering and optimized builds.
- **TailwindCSS** for responsive, utility-first styling.
- Integration of **PrimeReact** components for UI elements.

---

### Project Structure in Dashboard Repo

```bash
.
├── next.config.js              # Next.js configuration
├── package.json                # Project dependencies and scripts
├── package-lock.json           # Dependency lock file
├── pages
│   ├── _app.js                 # Application wrapper for global setup
│   └── index.js                # Main dashboard page
├── postcss.config.js           # PostCSS configuration for TailwindCSS
├── public
│   ├── cloudy.svg              # Weather icons for test statuses
│   ├── favicon.ico
│   ├── partially-sunny.svg
│   ├── rainy.svg
│   ├── stormy.svg
│   └── sunny.svg
├── README.md                   # Project documentation (this file)
├── scripts
│   └── fetch-ci-nightly-data.js # Script to fetch nightly test data
├── styles
│   └── globals.css             # Global CSS imports
└── tailwind.config.js          # TailwindCSS configuration
```

#### Key Files

- **`pages/index.js`**: The main entry point of the dashboard, displaying test results and their statuses.
- **`scripts/fetch-ci-nightly-data.js`**: Custom script to retrieve CI data for the dashboard.
- **`styles/globals.css`**: Custom global styles, mainly extending the TailwindCSS base.
- **`public/`**: Contains static assets like icons representing different test statuses.

---

### Setup Instructions

Follow these steps to set up the development environment for the Kata Containers Test Dashboard:

#### Prerequisites

- [**Node.js**](https://nodejs.org/en/download) (version 18.x or later recommended)
- **npm** (comes with Node.js)

#### Installation

1. **Clone the dashboard repository**:

   ```bash
   git clone https://github.com/kata-containers/kata-containers.github.io.git
   cd kata-containers.github.io
   ```
2. **Install dependencies**:
   Run the following command to install both the project dependencies and development dependencies.

   ```bash
   npm install
   ```

#### Development

3. **Run the development server**:
   Start the Next.js development server with hot-reloading enabled.

   To run the script to fetch the data, a .env file must be created with an access token. This is required to authenticate our calls and increase the rate limit. To get the token, click [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)

   Create the .env file:

   ```bash
    NODE_ENV=development
    TOKEN=<GITHUB_PAT_OR_OTHER_VALID_TOKEN>
   ```

   Create the folder /localData. Then, run:

   ```bash
   node scripts/fetch-ci-nightly-data.js > localData/job_stats.json
   npm run dev    # On Windows, run `npm run win-dev` instead.
   ```

   The app will be available at [http://localhost:3000](http://localhost:3000).

#### Production

4. **Build for production**:
   To create an optimized production build, run:

   ```bash
   npm run build
   ```
5. **Start the production server**:
   After building, you can start the server:

   ```bash
   npm start
   ```

#### Notes

In deploy.yml:

```bash
env:
   NEXT_PUBLIC_BASE_PATH: ${{ vars.NEXT_PUBLIC_BASE_PATH }}
```

If the variable is undefined, it will use "" for the basePath and assume the site is being served at root.
This makes it easier for people to fork the repo and deploy with GitHub pages such that they can have a preview for their PR.

## License

[CC0 1.0 Universal](https://github.com/EC528-Fall-2024/github-bot-kata-ci/blob/main/LICENSE)
