# FeelY

**A space to reflect, understand yourself, and become your own creation.**

FeelY explores how AI-supported conversation can help people make sense of their experiences and recognize connections across their lives.

At its center are conversations and **My Map**: a personal, evolving collection of the observations, values, relationships, and experiences you choose to save. Individual reflections can become part of a larger picture, while you decide which suggested connections feel meaningful.

Reflection is valuable in its own right. Practices and next steps are optional.

## Project status

**Development of this project concluded with v4.**

This repository preserves the final implementation and earlier development snapshots. The default branch, **`v4-project-closed`**, contains the closing version.

The code and documentation remain available for reference. Project closure does not imply that every planned feature was completed or that the application is production-ready.

## The experience

- **Conversations:** explore experiences and questions with an AI companion.
- **Topics and connections:** review suggestions that connect conversations to recurring themes.
- **My Map:** collect and revisit the people, experiences, values, and observations that matter to you.
- **Your choice of what to save:** review and edit suggested map entries before accepting them.

FeelY was developed as a tool for personal reflection. It is not a substitute for psychotherapy, medical care, or emergency support.

## Versions

The repository preserves four versions as separate branches.

| Version | Place in the project |
|---|---|
| [v1](https://github.com/sina3lla/FeelY-master/tree/v1) | Earlier snapshot with the original static website, Python backend, conversations, My Map, and journal functionality. |
| [v2](https://github.com/sina3lla/FeelY-master/tree/v2) | A subsequent snapshot of the original application, retaining the static website and journal. |
| [v3](https://github.com/sina3lla/FeelY-master/tree/v3) | A later snapshot with PostgreSQL support and expanded backend and deployment documentation. |
| [v4 — project closed](https://github.com/sina3lla/FeelY-master/tree/v4-project-closed) | Final snapshot with React as the consumer frontend, updated chat storage and database migrations, and deployment tooling. Journal functionality was retired. |

The former `working` branch was retired when v4 became the default. Its previous state remains preserved in `v3`.

The earlier snapshots do not share a common Git ancestor with v4. They are preserved versions, rather than feature branches intended to be merged into the final implementation.

## Technical overview

The final version combines:

- **React and TypeScript** for the application interface.
- **Python and FastAPI** for accounts, conversations, and application services.
- **SQLite or PostgreSQL** for persistent storage.
- Configurable AI providers: **OpenAI, Anthropic, Ollama**, or mock responses for development.
- Native and Docker deployment options.

When an external AI provider is configured, relevant conversation content is transmitted to that provider to generate responses. Data handling depends on the deployment configuration.

## Explore the implementation

- [Frontend guide](frontend-react/README.md)
- [Code guide](docs/CODE_GUIDE.md)
- [My Map and self-authorship architecture](docs/SELF_AUTHORSHIP.md)
- [Native setup](docs/DEPLOYMENT_NATIVE.md)
- [Local Docker setup](docs/DEPLOYMENT_LOCAL.md)
- [Deployment documentation](docs/DEPLOYMENT_PRODUCTION.md)

Technical guides describe the implementation at the time of closure. Earlier branches retain documentation for their respective versions.
