# uploader

The project is managed as a monorepo with the following structure:
```
.
├── backend
│   ├── ...
├── frontend
│   ├── ...
├── package.json
└── README.md
```

## Requirements

Make sure you have [Yarn](https://classic.yarnpkg.com/en/docs/install#debian-stable), [Node.js](https://nodejs.org/en) and either [Docker Desktop](https://docs.docker.com/get-docker) (which includes Docker Compose as part of the installation) or both [Docker Engine](https://docs.docker.com/engine/) and [Docker Compose](https://docs.docker.com/compose/) installed and working on your system. Allowing Docker to be managed as a non-root user may also be necessary depending on how you installed it. See [here](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

## How to run

### Backend

Inside the `/backend` folder, create a `.env` file with the following development environment variables:

```
NODE_ENV=development
PORT=80

POSTGRES_DB=bonusx_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
DATABASE_URL=postgresql://postgres:password@database.local:5432/bonusx_db

S3_ENDPOINT=http://storage.local:9000
S3_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
S3_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
S3_BUCKET_NAME=bonusx-bucket
S3_REGION=us-east-1

JWT_SECRET=2ab0ab2e8dab76751456a765e5455dd6
JWT_EXPIRES_IN=7d
```

Run the required infrastructure services (PostgreSQL database, S3-compatible storage and backend service) with:

```bash
cd backend && docker-compose up -d
```

**NOTE:** The ports exposed in `docker-compose.yml` are intended for local testing purposes only and should not be used in production environments. They allow access to an S3-like GUI at `localhost:9000/ui` and to the PostgreSQL database.

### Frontend

Inside the `/frontend` folder, create a `.env` file with the following development environment variables:

```
PUBLIC_API_BASE_URL=http://localhost:3000/api
```

Run the client with:

```bash
cd frontend && yarn start:dev
```

Your application is not ready at `localhost:3001`.