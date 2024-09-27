+++
title = 'Building a Go Api for Handling User Coin Balances'
date = 2024-09-26T11:14:39+02:00
draft = true
tags = ["Go", "Development", "WebDevelopment", "API"]
+++

In this post, I'll walk through a recent project where I built a **RESTful API in Go** that manages user authentication and handles  requests for checking user coin balances.
The project showcases how to create an API with Go's powerful capabilities, using the `chi` router, middleware for authrization, and handling mock database interactions.

## Project Overview

This API enables users to retrieve their coin balances after passing through authorization checks. It stimulates interaction with a mock database that stores login details and coin balances for different users.

### Key Features:

- **User Authentication**: Validates requests using a token passed in the headers.
- **Get Coin Balance**: Allows authorized users to request their current coin balance.
- **Mock Database Integration**: Uses an in-memory mock database to simulate real-world database calls.
- **Error Handling**: Responds with appropriate HTTP status codes and messages for errors.

## Code Breakdown

1. **Main API Structure**

The `main.go` file initialize the API, sets up the router using `chi`, and starts the server on `localhost:8000`.

```go
var r *chi.Mux = chi.NewRouter()
handlers.Handler(r)

err := http.ListenAndServer("localhost:8000", r)
if err != nil {
	log.Error(err)
}
```

This file also provides a welcome message in the terminal when the server starts.

2. **Router Setup**

In `handlers.go`, the `chi` router is used to manage routes and assign middleware. The `/account/coins` endpoint is protected by an authorization middleware, ensuring only authorized users can access it.

3. **Authrization Middleware**

The `Authorization` middleware checks if a request contains valid credentials before allowing access to the resource.

```go
var token = r.Header.Get("Authorization")
loginDetails = (*database).GetUserLoginDetails(username)

if loginDetails == nil || (token != (*loginDetails).AuthToken) {
	api.RequestErrorHandler(w, UnAuthorizedError)
	return
}
```

The middleware retrieves the user's token from the request header and checks if it matches the one in the mock database. If the credentials are missing or invalid, an error response is returned, and the request is denied.

4. **Get Coin Balance Handler**

The `GetCoinBalance` handler fetches the user's coin balance from the database once the authorization is successul.

```go
tokenDetails = (*database).GetUserCoins(params.Username)
if tokenDetails == nil {
	api.InternalErrorHandler(w)
	return
}
```

The handler decodes the request parameters, interacts with the mock database, and returns the coin balance in a JSON response. If any error occurs, suck as the user not being found, an internal server error is returned.

5. **Mock Database**

In `mockdb.go`, a mock database is implemented to simulate real-world database calls.
The database stores predefined user login tokens and coin balances.

```go
var mockLoginDetails = map[string]LoginDetails{
	"alex": {AuthToken: "123ABC", username: "alex"},
	"jason": {AuthToken: "456DEF", username: "jason"},
}

var mockCoinDetails = map[string]CoinDetails{
	"alex": {Coins: 100, username: "alex"},
	"jason": {Coins: 200, username: "jason"}
}
```

The `mockDB` struct simulates delay (`time.sleep()`) to mimic real database latency. It also returns nil if a user is not found, which is handled gracefully by the API.

## How to Run the Project

### Prerequisites:

- Go installed on your machine.

### Steps:

1. Clone the project:

```sh
git clone https://github.com/kaliban2056/go-API
```

2. Navigate to the project directory:

```sh
cd go-API
```

3. Run the API:

```sh
go run main.go
```

4. The API will be running on `localhost:8000`.

### Testing the API

Use postman or `curl` to send requests.

**Example Request (Authorized)**:

```sh
curl -H "Authorization: 123ABC" "http://localhost:8000/account/coins?username=alex"
```

Expected response:

```json
{
    "Code": 200,
    "Balance": 100
}
```

**Unauthorized Request**:

If you send a request without a valid token:

```sh
curl -H "Authorization: invalidToken" "http://localhost:8000/account/coins?username=alex"
```

Expected Response:

```json
{
    "Code": 400,
    "Message": "Invalid username or token."
}
```

## Learning Points

1. **Modular API Design**:

This project demonstrates the importance of modularizing your API logic. By separating route handling, middleware, and database logic into distinct files, the code becomes more maintainable and scalable.

2. **Middleware for Security**:

Using middleware for authorization is a powerful way to enforce security on routes. It ensures that every request is authenticated before sensitive data, suck as user balances.

3. **Mock Database for Testing**:

In this project, the mock database simulates real-world database interaction without the need for setting up an actual database. It's a great way to prototype and test your API before moving to production.

4. **Gracedul Error Handling**:

Error handling is critical in any API. In this project, it's implemented custom error responses that provide mainingful feedback to the API users, suck as `400 Bad Request` or `500 Internal Server Error`.

## Final Thoughts

This project showcases how to build a lightweight, secure, scalable API using Go.
By leveraginf Go's concurrency and modlar design patterns, this API is highly efficient and can be easily extended to include more functionality, suck as user management, transaction history, or even interaction with real databases.
