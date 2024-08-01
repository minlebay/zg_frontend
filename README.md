--- 

# ZG_frontend Project

This is a simple Vue.js project created for fun and learning purposes. 
Zg_frontend is the frontend part of the ZmeyGorynych project. 
It is a simple application that displays messages from a SQL and NoSQL database.
The project demonstrates basic usage of Vue components, API integration, and styling.

## Project Structure

```
src/
├── App.vue
├── main.ts
├── assets/
│   ├── base.css
│   ├── main.css
│   └── logo.svg
├── api-client/
│   ├── .gitignore
│   ├── .npmignore
│   ├── .openapi-generator-ignore
│   ├── .openapi-generator/
│   │   ├── FILES
│   │   └── VERSION
│   ├── api.ts
│   ├── base.ts
│   ├── common.ts
│   ├── configuration.ts
│   └── git_push.sh
└── components/
    ├── CustomDropdown.vue
    ├── NoSqlMessageDetail.vue
    ├── SqlMessageDetail.vue
    ├── MessageListSql.vue
    ├── MessageListNoSql.vue
    └── icons/
        ├── IconCommunity.vue
        ├── IconDocumentation.vue
        ├── IconEcosystem.vue
        ├── IconSupport.vue
        └── IconTooling.vue
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (version 12.x or later)
- [Vue CLI](https://cli.vuejs.org/guide/installation.html)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/minlebay/zg_frontend.git
cd zg_frontend
```

2. Install dependencies:

```bash
npm install
```

### Running the Application

To start the development server, run:

```bash
npm run serve
```

The application will be available at `http://localhost:8080`.

### Building for Production

To build the project for production, run:

```bash
npm run build
```

The production-ready files will be generated in the `dist` directory.

## Project Overview

### Components

- **CustomDropdown.vue**: A customizable dropdown component.
- **NoSqlMessageDetail.vue**: Displays details of NoSQL messages.
- **SqlMessageDetail.vue**: Displays details of SQL messages.
- **MessageListSql.vue**: Lists SQL messages.
- **MessageListNoSql.vue**: Lists NoSQL messages.
- **Icon Components**: A set of icon components for documentation, support, ecosystem, community, and tooling.

### Assets

- **base.css**: Base styles for the application.
- **main.css**: Main styles for the application.
- **logo.svg**: Application logo.

### API Client

The `api-client` directory contains the API client configuration and scripts generated using OpenAPI.

- **api.ts**: Contains API methods.
- **base.ts**: Base API configuration.
- **common.ts**: Common utilities for API client.
- **configuration.ts**: API client configuration.
- **git_push.sh**: Script to push generated API client to a remote repository.

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Vue.js Documentation: [Vue.js](https://vuejs.org/)
- OpenAPI Generator: [OpenAPI Generator](https://openapi-generator.tech/)

--- 