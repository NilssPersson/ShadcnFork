# Contributing

Thanks for your interest in contributing to ui.shadcn.com. We're happy to have you here.

Please take a moment to review this document before submitting your first pull request. We also strongly recommend that you check for open issues and pull requests to see if someone else is working on something similar.

If you need any help, feel free to reach out to [@shadcn](https://twitter.com/shadcn).

## About this repository

This repository is a monorepo.

- We use [pnpm](https://pnpm.io) and [`workspaces`](https://pnpm.io/workspaces) for development.
- We use [Turborepo](https://turbo.build/repo) as our build system.
- We use [changesets](https://github.com/changesets/changesets) for managing releases.

## Structure

This repository is structured as follows:

```
apps
└── www
    ├── app
    ├── components
    ├── content
    └── registry
        ├── default
        │   ├── example
        │   └── ui
        └── new-york
            ├── example
            └── ui
packages
└── cli
```

| Path                  | Description                              |
| --------------------- | ---------------------------------------- |
| `apps/www/app`        | The Next.js application for the website. |
| `apps/www/components` | The React components for the website.    |
| `apps/www/content`    | The content for the website.             |
| `apps/www/registry`   | The registry for the components.         |
| `packages/cli`        | The `shadcn-ui` package.                 |

## Development

### Fork this repo

You can fork this repo by clicking the fork button in the top right corner of this page.

### Clone on your local machine

```bash
git clone https://github.com/your-username/ui.git
```

### Navigate to project directory

```bash
cd ui
```

### Create a new Branch

```bash
git checkout -b my-new-branch
```

### Without Docker
This section is for those who want to run the project without Docker. If you want to use Docker, please skip to the [Using Docker](#using-docker) section.

### Install dependencies

```bash
pnpm install
```

### Run a workspace

You can use the `pnpm --filter=[WORKSPACE]` command to start the development process for a workspace.

#### Examples

1. To run the `ui.shadcn.com` website:

```bash
pnpm --filter=www dev
```

2. To run the `shadcn-ui` package:

```bash
pnpm --filter=shadcn-ui dev
```

### Using Docker

We have implemented containerization using [Docker](https://www.docker.com/get-started) to streamline the development environment. This ensures consistency across different environments and makes it easier to get started if you're already familiar with Docker. However, it requires an understanding of [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/), **so please make sure you're comfortable with these tools before proceeding**. Using Docker is optional, and you can run the project without it (see the previous section) - although we recommend using Docker for a consistent development environment.

#### Prerequisites

Make sure you have the following installed on your system:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

#### Building and Running the Development Environment with Docker

1. **Build the Docker image:**

First, you need to build the Docker image. You can do this by running the following command:

```bash
  docker-compose build
```

2. **Start the development environment:**

Once the image has been built, you can start the development environment for the workspace you want to work on. 

**To start the `ui.shadcn.com` website in the `www` workspace:**
  
```bash	
docker-compose up web
```
Now, you can access the website at [http://localhost:3333](http://localhost:3333) in your browser.

**To start the `shadcn-ui` package in the `cli` workspace:**
```bash	
  docker-compose up cli
```

**To run the tests:**
```bash
docker-compose up test
```

**You can also run all the environments at once:**
```bash
docker-compose up
```

3. **Stop the development environment:**

To stop the development environment, you can run the following command:

```bash
docker-compose down
```

4. **Rebuilding the Docker image:**

If you make changes to the Dockerfile or any other configuration files, you will need to rebuild the Docker image. You can do this by running the following command:

```bash
docker-compose build
```

5. **Running commands inside the Docker container:**

You can run commands inside the Docker container by using the `docker-compose exec` command. For example, to run the tests inside the Docker container, you can use the following command:

```bash
docker-compose exec web pnpm test
```

This will run the tests inside the Docker container of the `www` workspace for the `ui.shadcn.com` website. In this case, the `web` service container is used to run the tests. You can replace `web` with `cli` or any other service name to run commands inside the container of that service.

## Documentation

The documentation for this project is located in the `www` workspace. You can run the documentation locally by running the following command:

```bash
pnpm --filter=www dev
```

Documentation is written using [MDX](https://mdxjs.com). You can find the documentation files in the `apps/www/content/docs` directory.

## Components

We use a registry system for developing components. You can find the source code for the components under `apps/www/registry`. The components are organized by styles.

```bash
apps
└── www
    └── registry
        ├── default
        │   ├── example
        │   └── ui
        └── new-york
            ├── example
            └── ui
```

When adding or modifying components, please ensure that:

1. You make the changes for every style.
2. You update the documentation.
3. You run `pnpm build:registry` to update the registry.

## Commit Convention

Before you create a Pull Request, please check whether your commits comply with
the commit conventions used in this repository.

When you create a commit we kindly ask you to follow the convention
`category(scope or module): message` in your commit message while using one of
the following categories:

- `feat / feature`: all changes that introduce completely new code or new
  features
- `fix`: changes that fix a bug (ideally you will additionally reference an
  issue if present)
- `refactor`: any code related change that is not a fix nor a feature
- `docs`: changing existing or creating new documentation (i.e. README, docs for
  usage of a lib or cli usage)
- `build`: all changes regarding the build of the software, changes to
  dependencies or the addition of new dependencies
- `test`: all changes regarding tests (adding new tests or changing existing
  ones)
- `ci`: all changes regarding the configuration of continuous integration (i.e.
  github actions, ci system)
- `chore`: all changes to the repository that do not fit into any of the above
  categories

  e.g. `feat(components): add new prop to the avatar component`

If you are interested in the detailed specification you can visit
https://www.conventionalcommits.org/ or check out the
[Angular Commit Message Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines).

## Requests for new components

If you have a request for a new component, please open a discussion on GitHub. We'll be happy to help you out.

## CLI

The `shadcn-ui` package is a CLI for adding components to your project. You can find the documentation for the CLI [here](https://ui.shadcn.com/docs/cli).

Any changes to the CLI should be made in the `packages/cli` directory. If you can, it would be great if you could add tests for your changes.

## Testing

Tests are written using [Vitest](https://vitest.dev). You can run all the tests from the root of the repository.

```bash
pnpm test
```

Please ensure that the tests are passing when submitting a pull request. If you're adding new features, please include tests.
