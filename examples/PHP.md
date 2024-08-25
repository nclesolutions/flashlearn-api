# PHP PDO Example for Profile API

**Last Updated:** *8/25/2024*

## Introduction

This guide provides a step-by-step example of how to interact with the Profile API using PHP and PDO. The example demonstrates how to authenticate, fetch user profile details, and handle the response in a PHP application.

## Requirements

- PHP 7.0 or higher
- PDO enabled for database interaction
- cURL enabled for API requests

## Setup

Before you begin, ensure that your PHP environment is set up with the necessary extensions (PDO, cURL).

### 1. Database Connection Setup

Create a database connection using PDO. This example assumes you're using MySQL, but PDO can be configured for any database supported by PHP.

```php
<?php

// Database connection parameters
$host = '127.0.0.1';
$db = 'flashlearn';
$user = 'root';
$pass = '';
$charset = 'utf8mb4';

// Set up the DSN (Data Source Name)
$dsn = "mysql:host=$host;dbname=$db;charset=$charset";

// Set up options for PDO
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    // Create a new PDO instance
    $pdo = new PDO($dsn, $user, $pass, $options);
} catch (\PDOException $e) {
    // Handle connection errors
    throw new \PDOException($e->getMessage(), (int)$e->getCode());
}
```

### 2. Making a Request to the Profile API

Use cURL to send an authenticated GET request to the Profile API. Replace `your_access_token_here` with your actual API token.

```php
<?php

// API endpoint and token
$apiUrl = 'https://yourdomain.com/api/profile';
$accessToken = 'your_access_token_here';

// Initialize cURL
$ch = curl_init();

// Set cURL options
curl_setopt($ch, CURLOPT_URL, $apiUrl);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $accessToken,
    'Accept: application/json',
]);

// Execute the request and get the response
$response = curl_exec($ch);

// Check for errors
if (curl_errno($ch)) {
    echo 'Error:' . curl_error($ch);
}

// Close cURL resource
curl_close($ch);

// Decode the JSON response
$profileData = json_decode($response, true);

// Output the profile data
echo "Name: " . $profileData['account']['name'] . PHP_EOL;
echo "Email: " . $profileData['account']['email'] . PHP_EOL;
echo "Biography: " . $profileData['biography'] . PHP_EOL;

if ($profileData['schoolInfo']) {
    echo "School Name: " . $profileData['schoolInfo']['school_name'] . PHP_EOL;
    echo "School Address: " . $profileData['schoolInfo']['address'] . PHP_EOL;
} else {
    echo "No school information available." . PHP_EOL;
}
```

### 3. Handling the Response

After decoding the JSON response, you can handle the data as needed. For instance, you can store or update the profile information in your database using PDO.

```php
<?php

// Check if profile data exists
if ($profileData) {
    // Example: Insert or update profile information in the database
    $stmt = $pdo->prepare('REPLACE INTO user_profiles (id, name, email, biography) VALUES (:id, :name, :email, :biography)');
    $stmt->execute([
        'id' => $profileData['account']['id'],
        'name' => $profileData['account']['name'],
        'email' => $profileData['account']['email'],
        'biography' => $profileData['biography'],
    ]);
    
    echo "Profile data saved successfully.";
} else {
    echo "Failed to retrieve profile data.";
}
```

### 4. Error Handling

It's essential to handle errors effectively in both the API request and database operations:

- **cURL Errors:** Use `curl_errno()` and `curl_error()` to capture any issues during the HTTP request.
- **PDO Exceptions:** Handle PDO exceptions using try-catch blocks to ensure that database connection and operations are secure.

### 5. Full Example Code

Here’s how everything ties together:

```php
<?php

// Database connection setup
$host = '127.0.0.1';
$db = 'flashlearn';
$user = 'root';
$pass = '';
$charset = 'utf8mb4';
$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
} catch (\PDOException $e) {
    throw new \PDOException($e->getMessage(), (int)$e->getCode());
}

// API request setup
$apiUrl = 'https://yourdomain.com/api/profile';
$accessToken = 'your_access_token_here';
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, $apiUrl);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer ' . $accessToken,
    'Accept: application/json',
]);

$response = curl_exec($ch);

if (curl_errno($ch)) {
    echo 'Error:' . curl_error($ch);
    exit;
}

curl_close($ch);

$profileData = json_decode($response, true);

if ($profileData) {
    $stmt = $pdo->prepare('REPLACE INTO user_profiles (id, name, email, biography) VALUES (:id, :name, :email, :biography)');
    $stmt->execute([
        'id' => $profileData['account']['id'],
        'name' => $profileData['account']['name'],
        'email' => $profileData['account']['email'],
        'biography' => $profileData['biography'],
    ]);
    
    echo "Profile data saved successfully.";
} else {
    echo "Failed to retrieve profile data.";
}
```
