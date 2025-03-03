# BlogFlow - Blogging Backend Application

**BlogFlow** is a modern, scalable, and feature-rich blog application backend built with **TypeScript**, **NestJS**, **GraphQL**, and **Prisma**. It uses **PostgreSQL** for efficient data storage and retrieval, providing a seamless experience for managing blog posts, user authentication, comments, tags, and likes. Whether you're building a personal blog or a content management system, BlogFlow is designed to make development easier and more enjoyable.

## Features

- **TypeScript:** Strongly-typed codebase for better maintainability and developer experience.
- **NestJS:** A progressive Node.js framework for building efficient and scalable server-side applications.
- **GraphQL:** Flexible and powerful API for querying and mutating data.
- **Prisma:** Next-generation ORM for database management with type safety and auto-generated queries.
- **PostgreSQL:** Relational database for storing blog posts, user data, and more.
- **JWT Authentication:** Secure user authentication using JSON Web Tokens (JWT).
- **Docker Support:** Easy containerization for development and deployment.

## Technologies Used

- **NestJS:** Framework for building scalable server-side applications.
- **TypeScript:** Adds static typing to JavaScript for enhanced code quality.
- **GraphQL:** Query language for APIs with a flexible and efficient data-fetching mechanism.
- **Prisma:** ORM for database management and type-safe queries.
- **PostgreSQL:** Relational database for data storage.
- **JWT:** JSON Web Tokens for secure authentication.

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v16 or higher)
- npm or yarn
- Docker (optional, for running PostgreSQL in a container)
- PostgreSQL (if not using Docker)

### Installation
1. **Clone the Repository:**
```
  git clone https://github.com/your-username/BlogFlow.git
  cd BlogFlow
```

2. **Install Dependencies:**
```
  npm install
```

3. **Set Up Environment Variables:**

Create a `.env` file in the root directory and add the following:
```
PORT=3000
DATABASE_URL="postgresql://postgres:mypassword@localhost:5432/blog_app"
JWT_SECRET=
JWT_EXPIRES_IN=24h
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_CALLBACK_URL=
```
5. **Run Prisma Migrations:**
```
  npx prisma migrate dev --name init
```

5. **Start the Server:**
```
  npm run start / nest start
```

6. **Access the Application:**

The GraphQL Playground will be available at `http://localhost:3000/graphql`.

## GraphQL API

Explore the APIs using the following endpoints:

### Queries

#### Fetch All Posts -
  ```
  query {
    posts(skip: 0, take: 10) {
      id
      title
      content
      author { name email }
      tags { name }
      comments { content author { name } }
      likes { user { name } }
    }
  }
  ```

#### Fetch a Single Post by ID -
  ```
  query {
    getPostById(id: 1) {
      id
      title
      content
      author { name }
      tags { name }
      comments { content author { name } }
    }
  }
  ```

#### Fetch All Users -
  ```
  query {
    users {
      id
      name
      email
      posts {
        title
      }
    }
  }
  ```

### Mutations
#### Register a User -
  ```
  mutation {
    createUser(createUserInput: {
      name: "John Doe",
      email: "john@example.com",
      password: "password123",
      bio: "A passionate blogger.",
      avatar: "https://example.com/avatar.jpg"
    }) {
      id
      name
      email
      bio
      avatar
    }
  }
  ```

#### Create a Post -
  ```
  mutation {
    createPost(createPostInput: {
      title: "My First Post",
      content: "This is the content of my first post.",
      tags: ["blog", "tutorial"]
    }) {
      id
      title
      content
      author { name }
    }
  }
  ```

#### Add a Comment to a Post -
  ```
  mutation {
    createComment(createCommentInput: {
      content: "This is a great post!",
      postId: 1
    }) {
      id
      content
      author {
        id
        name
      }
      post {
        id
        title
      }
      createdAt
    }
  }
  ```

#### Like a Post -
  ```
  mutation {
    likePost(postId: 1)
  }
  ```

## Authentication

BlogFlow uses **JWT (JSON Web Tokens)** for secure authentication. After registering or logging in, users receive a JWT token that must be included in the `Authorization` header for protected GraphQL operations.

**Example:**
```
  Authorization: Bearer <your_jwt_token>
```
