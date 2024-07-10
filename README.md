# Crowdfunding Platform

Welcome to the Crowdfunding Platform! This project is built with Go using the Gin framework, GORM for ORM, and Midtrans as the payment gateway.

## Features

- **User Authentication**: Secure user authentication with JWT.
- **Campaign Management**: Create, read, update, and delete campaigns.
- **Campaign Images**: Upload and manage campaign images.
- **Transaction Management**: Handle donations and transactions.
- **Payment Integration**: Payment processing with Midtrans.

## Tech Stack

- **Go**: The primary programming language.
- **Gin**: A fast and lightweight web framework for Go.
- **GORM**: An ORM library for Go.
- **Midtrans**: A payment gateway for handling transactions.

## Getting Started

### Prerequisites

- Go 1.14+ installed
- MySQL installed and running
- Midtrans account

### Installation

1. **Clone the repository**
    ```bash
    git clone https://github.com/yourusername/crowdfunding-platform.git
    cd crowdfunding-platform
    ```

2. **Install dependencies**
    ```bash
    go mod tidy
    ```

3. **Set up environment variables**

    Create a `.env` file in the root directory and add the following:
    ```env
    DB_USER=your_db_user
    DB_PASSWORD=your_db_password
    DB_NAME=your_db_name
    DB_HOST=localhost
    MIDTRANS_SERVER_KEY=your_midtrans_server_key
    ```

4. **Run database migrations**

    Make sure you have a running MySQL instance and the database specified in the `.env` file exists.
    ```bash
    go run main.go migrate
    ```

5. **Start the server**
    ```bash
    go run main.go
    ```

### API Endpoints

#### User Authentication

- **Register**: `POST /api/v1/register`
- **Login**: `POST /api/v1/login`

#### Campaign Management

- **Create Campaign**: `POST /api/v1/campaigns`
- **Get Campaigns**: `GET /api/v1/campaigns`
- **Get Campaign by ID**: `GET /api/v1/campaigns/:id`
- **Update Campaign**: `PUT /api/v1/campaigns/:id`
- **Delete Campaign**: `DELETE /api/v1/campaigns/:id`
- **Upload Campaign Image**: `POST /api/v1/campaigns/:id/images`

#### Transaction Management

- **Create Transaction**: `POST /api/v1/transactions`
- **Get Transactions**: `GET /api/v1/transactions`
- **Get Transaction by ID**: `GET /api/v1/transactions/:id`

#### Payment Integration

- **Create Payment**: `POST /api/v1/payments`
- **Get Payment Status**: `GET /api/v1/payments/:id`

## Database Schema

Here is the database schema for reference:

### Users

| Column           | Type         | Description            |
|------------------|--------------|------------------------|
| id               | int(11)      | Primary key            |
| name             | varchar(255) | User's name            |
| occupation       | varchar(255) | User's occupation      |
| email            | varchar(255) | User's email           |
| password_hash    | varchar(255) | Hashed password        |
| avatar_file_name | varchar(255) | Avatar file name       |
| role             | varchar(255) | User role              |
| token            | varchar(255) | JWT token              |
| created_at       | datetime     | Creation timestamp     |
| updated_at       | datetime     | Update timestamp       |

### Campaigns

| Column            | Type         | Description                 |
|-------------------|--------------|-----------------------------|
| id                | int(11)      | Primary key                 |
| user_id           | int(11)      | Foreign key referencing users(id) |
| name              | varchar(255) | Campaign name               |
| short_description | varchar(255) | Short description           |
| description       | text         | Detailed description        |
| perks             | text         | Campaign perks              |
| backer_count      | int(11)      | Number of backers           |
| goal_amount       | int(11)      | Goal amount                 |
| current_amount    | int(11)      | Current amount raised       |
| slug              | varchar(255) | URL-friendly name           |
| created_at        | datetime     | Creation timestamp          |
| updated_at        | datetime     | Update timestamp            |

### Campaign Images

| Column       | Type         | Description                 |
|--------------|--------------|-----------------------------|
| id           | int(11)      | Primary key                 |
| campaign_id  | int(11)      | Foreign key referencing campaigns(id) |
| file_name    | varchar(255) | Image file name             |
| is_primary   | tinyint(4)   | Primary image flag          |
| created_at   | datetime     | Creation timestamp          |
| updated_at   | datetime     | Update timestamp            |

### Transactions

| Column       | Type         | Description                 |
|--------------|--------------|-----------------------------|
| id           | int(11)      | Primary key                 |
| campaign_id  | int(11)      | Foreign key referencing campaigns(id) |
| user_id      | int(11)      | Foreign key referencing users(id) |
| amount       | int(11)      | Transaction amount          |
| status       | varchar(255) | Transaction status          |
| code         | varchar(255) | Transaction code            |
| created_at   | datetime     | Creation timestamp          |
| updated_at   | datetime     | Update timestamp            |

## Contributing

1. Fork the repository.
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- [Gin](https://gin-gonic.com/)
- [GORM](https://gorm.io/)
- [Midtrans](https://midtrans.com/)
